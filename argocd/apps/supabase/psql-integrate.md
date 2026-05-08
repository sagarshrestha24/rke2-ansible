# Supabase with External postgres cluster

This directory contains the configurations and steps required to run Supabase with external postgres db inside a Kubernetes cluster.

## Pre-requisite
1. Supabase running with supabase postgres cluster default.

## Deploy bitnami postgres Cluster
Add Helm repo
`helm repo add bitnami https://charts.bitnami.com/bitnami`

Install helmchart

`helm install postgresql-db bitnami/postgresql -n supabase --version 16.3.2`

Install with custom values.yaml
Create values.yaml and apply. 

`helm install my-postgresql bitnami/postgresql -f values.yaml -n supabase --version 16.3.2`

## Copy all schema. script file from supabase database

`kubectl cp supabase-supabase-db-788:/docker-entrypoint-initdb.d/ . -n supabase`

## Connect dedicated postgres cluster (Bitnami)

`kubectl get pod -n supabase`

```
PostgreSQL can be accessed via port 5432 on the following DNS names from within your cluster:

    postgresql-db.supabase.svc.cluster.local - Read/Write connection

To get the password for "postgres" run:

    export POSTGRES_PASSWORD=$(kubectl get secret --namespace supabase postgresql-db -o jsonpath="{.data.postgres-password}" | base64 -d)

To connect to your database run the following command:

    kubectl run my-postgresql-client --rm --tty -i --restart='Never' --namespace supabase --image docker.io/bitnami/postgresql:17.2.0-debian-12-r3 --env="PGPASSWORD=$POSTGRES_PASSWORD" \
      --command -- psql --host postgresql-db -U postgres -d postgres -p 5432

    > NOTE: If you access the container using bash, make sure that you execute "/opt/bitnami/scripts/postgresql/entrypoint.sh /bin/bash" in order to avoid the error "psql: local user with ID 1001} does not exist"

To connect to your database from outside the cluster execute the following commands:

    kubectl port-forward --namespace supabase svc/postgresql-db 5432:5432 &
    PGPASSWORD="$POSTGRES_PASSWORD" psql --host 127.0.0.1 -U postgres -d postgres -p 5432

```
## Configure postgres cluster with schema and migration

### Connect database

`kubectl port-forward --namespace supabase svc/postgresql-db 5432:5432`

### Create script Ready

Open aother terminal and switch directory to file where scripts and schema copied from supabase-db pod.

schema-migration.sh

```                                                                                                                                                                           
#!/bin/bash

# Variables
DB_USER="postgres"        # Replace with your DB username
DB_PASS="fhfhf"      # Replace with your DB password
DB_NAME="postgres"        # Replace with your database name
DB_HOST="localhost"       # Replace if using a remote host

SQL_DIRS=("./migrations" "./init-scripts") # Directories containing SQL files

# Loop through each directory
for SQL_DIR in "${SQL_DIRS[@]}"; do
    if [ ! -d "$SQL_DIR" ]; then
        echo "Directory $SQL_DIR does not exist. Skipping..."
        continue
    fi

    # Loop through all SQL files in the directory
    for sql_file in "$SQL_DIR"/*.sql; do
        if [ -f "$sql_file" ]; then
            echo "Running $sql_file ..."
            PGPASSWORD="$DB_PASS" psql -U "$DB_USER" -h "$DB_HOST" -d "$DB_NAME" -f "$sql_file"

            # Check for errors
            if [ $? -ne 0 ]; then
                echo "Error executing $sql_file. Stopping script."
                exit 1
            fi
        fi
    done
done

echo "All SQL scripts executed successfully!"
```

migrate.sh

```
#!/bin/sh
set -eu

#######################################
# Used by both ami and docker builds to initialise database schema.
# Env vars:
#   POSTGRES_DB        defaults to postgres
#   POSTGRES_HOST      defaults to localhost
#   POSTGRES_PORT      defaults to 5432
#   POSTGRES_PASSWORD  defaults to ""
#   USE_DBMATE         defaults to ""
# Exit code:
#   0 if migration succeeds, non-zero on error.
#######################################

export PGDATABASE="postgres"
export PGHOST="localhost"
export PGPORT="5432"
export PGPASSWORD="fdbdbbdb"

# if args are supplied, simply forward to dbmate
connect="$PGPASSWORD@$PGHOST:$PGPORT/$PGDATABASE?sslmode=disable"
if [ "$#" -ne 0 ]; then
    export DATABASE_URL="${DATABASE_URL:-postgres://supabase_admin:$connect}"
    exec dbmate "$@"
    exit 0
fi

db=$( cd -- "$( dirname -- "$0" )" > /dev/null 2>&1 && pwd )
if [ -z "${USE_DBMATE:-}" ]; then
    # run init scripts as postgres user
    for sql in "$db"/init-scripts/*.sql; do
        echo "$0: running $sql"
        psql -v ON_ERROR_STOP=1 --no-password --no-psqlrc -U postgres -f "$sql"
    done
    psql -v ON_ERROR_STOP=1 --no-password --no-psqlrc -U postgres -c "ALTER USER supabase_admin WITH PASSWORD '$PGPASSWORD'"
    # run migrations as super user - postgres user demoted in post-setup
    for sql in "$db"/migrations/*.sql; do
        echo "$0: running $sql"
        psql -v ON_ERROR_STOP=1 --no-password --no-psqlrc -U supabase_admin -f "$sql"
    done
else
    # run init scripts as postgres user
    DBMATE_MIGRATIONS_DIR="$db/init-scripts" DATABASE_URL="postgres://postgres:$connect" dbmate --no-dump-schema migrate
    psql -v ON_ERROR_STOP=1 --no-password --no-psqlrc -U postgres -c "ALTER USER supabase_admin WITH PASSWORD '$PGPASSWORD'"
    # run migrations as super user - postgres user demoted in post-setup
    DBMATE_MIGRATIONS_DIR="$db/migrations" DATABASE_URL="postgres://supabase_admin:$connect" dbmate --no-dump-schema migrate
fi

# run any post migration script to update role passwords
postinit="/etc/postgresql.schema.sql"
if [ -e "$postinit" ]; then
    echo "$0: running $postinit"
    psql -v ON_ERROR_STOP=1 --no-password --no-psqlrc -U supabase_admin -f "$postinit"
fi

# once done with everything, reset stats from init
psql -v ON_ERROR_STOP=1 --no-password --no-psqlrc -U supabase_admin -c 'SELECT extensions.pg_stat_statements_reset(); SELECT pg_stat_reset();' || true

```
### Run the script

```
chmod +x schema-migration.sh.sh
chmod +x migrate.sh
```

```
bash migrate.sh
bash new-migration.sh
```

### Create role for 

supabase_admin            
supabase_auth_admin        
supabase_storage_admin 

First connect to the database with postgres user

psql -h localhost -p 5432 -U postgres -d postgres -W

Enter password

Run the query

```
ALTER ROLE supabase_auth_admin WITH LOGIN;
ALTER ROLE supabase_auth_admin WITH PASSWORD 'pgpass';
ALTER ROLE supabase_auth_admin WITH SUPERUSER;
ALTER ROLE supabase_auth_admin WITH LOGIN PASSWORD 'pgpass' SUPERUSER;

ALTER ROLE supabase_admin WITH LOGIN;
ALTER ROLE supabase_admin WITH PASSWORD 'pgpass';
ALTER ROLE supabase_admin WITH SUPERUSER;
ALTER ROLE supabase_admin WITH LOGIN PASSWORD 'pgpass' SUPERUSER;

ALTER ROLE supabase_storage_admin  WITH LOGIN;
ALTER ROLE supabase_storage_admin  WITH PASSWORD 'pgpass';
ALTER ROLE supabase_storage_admin  WITH SUPERUSER;
ALTER ROLE supabase_storage_admin  WITH LOGIN PASSWORD 'pgpass' SUPERUSER;
```
Check Access

`/du`

## Configure supabase auth, reatime, storage and analytics with deployed external postgrtes cluster

Edit values-dev.yaml and configure env with external database host and password.

```
secret:
  jwt:
    anonKey: eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.ewogICJyb2xlIjogImFub24iLAogICJpc3MiOiAic3VwYWJhc2UiLAogICJpYXQiOiAxNzI4OTI5NzAwLAogICJleHAiOiAxODg2Njk2MTAwCn0.0xHGoz8AJx05etWjxXMzA96k7m8W_jBfAOaQ2936VH4
    serviceKey: eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.ewogICJyb2xlIjogInNlcnZpY2Vfcm9sZSIsCiAgImlzcyI6ICJzdXBhYmFzZSIsCiAgImlhdCI6IDE3Mjg5Mjk3MDAsCiAgImV4cCI6IDE4ODY2OTYxMDAKfQ.9OmlKCQMzbkGHX9znqUYC8VEK8bDCEivzwnCnnGilig
    secret: gX8jgYU4Yr3lWMevAl/D+Ak9fksNlsQsPLIXuzy7zmk=
  smtp:
    username: "test@gmail.com"
    password: "test1234"
  dashboard:
    username: supabase
    password: supabase
  db:
    username: postgres
    password: pgpass
    database: postgres
  analytics:
    apiKey: gX8jgYU4Yr3lWMevAl/D+Ak9fksNlsQsPLIXuzy7zmk=

db:
  enabled: false
  image:
    tag: 15.1.0.147
  livenessProbe:
    exec:
      command:
        - pg_isready
        - -U
        - postgres
    initialDelaySeconds: 3
  persistence:
    enabled: true
    storageClassName: longhorn

studio:
  image:
    tag: 20240326-5e5586d
  environment:
    STUDIO_DEFAULT_ORGANIZATION: "My Organization"
    STUDIO_DEFAULT_PROJECT: "My Project"
    SUPABASE_PUBLIC_URL: http://supabase.coreii.labenv.ai/
    NEXT_PUBLIC_ENABLE_LOGS: "true"
  livenessProbe:
    httpGet:
      path: /api/profile
      port: 3000
    initialDelaySeconds: 3

auth:
  image:
    tag: v2.143.0
  environment:
    # Override the database hostname if using external database
    DB_HOST: postgresql-db.supabase.svc.cluster.local
    DB_USER: supabase_auth_admin
    DB_PORT: 5432
    DB_PASSWORD: pgpass
    DB_DRIVER: postgres
    DB_SSL: disable  # disable, allow, prefer, require, verify-ca, verify-full
    API_EXTERNAL_URL: http://supabase.coreii.labenv.ai
    GOTRUE_API_HOST: "0.0.0.0"
    GOTRUE_API_PORT: "9999"
    GOTRUE_SITE_URL: http://supabase.coreii.labenv.ai
    GOTRUE_URI_ALLOW_LIST: "*"
    GOTRUE_DISABLE_SIGNUP: "false"
    GOTRUE_JWT_DEFAULT_GROUP_NAME: authenticated
    GOTRUE_JWT_ADMIN_ROLES: service_role
    GOTRUE_JWT_AUD: authenticated
    GOTRUE_JWT_EXP: "3600"
    GOTRUE_EXTERNAL_EMAIL_ENABLED: "true"
    GOTRUE_MAILER_AUTOCONFIRM: "true"
    GOTRUE_MAILER_SECURE_EMAIL_CHANGE_ENABLED: true
    GOTRUE_SMTP_MAX_FREQUENCY: 1s
    GOTRUE_SMTP_ADMIN_EMAIL: "test@gmail.com"
    GOTRUE_SMTP_HOST: "smtp.gmail.com"
    GOTRUE_SMTP_PORT: "587"
    GOTRUE_SMTP_SENDER_NAME: "test@gmail.com"
    GOTRUE_EXTERNAL_PHONE_ENABLED: "false"
    GOTRUE_SMS_AUTOCONFIRM: "false"
    GOTRUE_MAILER_URLPATHS_INVITE: "/auth/v1/verify"
    GOTRUE_MAILER_URLPATHS_CONFIRMATION: "/auth/v1/verify"
    GOTRUE_MAILER_URLPATHS_RECOVERY: "/auth/v1/verify"
    GOTRUE_MAILER_URLPATHS_EMAIL_CHANGE: "/auth/v1/verify"

rest:
  image:
    tag: v12.0.1

realtime:
  environment:
    # Override the database hostname if using external database
    DB_HOST: postgresql-db.supabase.svc.cluster.local
    DB_USER: supabase_admin
    DB_PORT: 5432
    DB_DRIVER: postgres
    DB_SSL: disable
  image:
    tag: v2.27.5
  livenessProbe:
    httpGet:
      path: /
      port: 4000
    initialDelaySeconds: 3

meta:
  image:
    tag: v0.80.0

storage:
  environment:
    # Override the database hostname if using external database
    DB_HOST: postgresql-db.supabase.svc.cluster.local
    DB_USER: supabase_storage_admin
    DB_PORT: 5432
    DB_DRIVER: postgres
    DB_SSL: disable
  image:
    tag: v0.46.4
  livenessProbe:
    httpGet:
      path: /status
      port: 5000
    initialDelaySeconds: 3
  persistence:
    enabled: false
    storageClassName: longhorn

imgproxy:
  image:
    tag: v3.8.0
  environment:
    IMGPROXY_ENABLE_WEBP_DETECTION: "true"
  livenessProbe:
    exec:
      command:
        - imgproxy
        - health
    initialDelaySeconds: 3
  persistence:
    enabled: false
    storageClassName: longhorn

kong:
  image:
    repository: kong
    tag: 2.8.1
  environment:
    KONG_DECLARATIVE_CONFIG: /usr/local/kong/kong.yml
    KONG_LOG_LEVEL: info
  ingress:
    enabled: true
    className: "nginx"
    annotations:
      nginx.ingress.kubernetes.io/rewrite-target: /
    tls: []
    hosts:
      - host: supabase.coreii.labenv.ai
        paths:
          - path: /
            pathType: Prefix
  service:
    type: NodePort
    nodePort: 32689


analytics:
  environment:
    DB_HOST: postgresql-db.supabase.svc.cluster.local
    DB_USERNAME: supabase_admin
    DB_PORT: 5432
    DB_DRIVER: postgres
    DB_SCHEMA: _analytics
  image:
    tag: 1.4.0
  livenessProbe:
    httpGet:
      path: /health
      port: 4000
    initialDelaySeconds: 3

vector:
  image:
    tag: 0.34.0-alpine
  livenessProbe:
    httpGet:
      path: /health
      port: 9001
    initialDelaySeconds: 3
  ## Vector requires logs from the control plane to function.
  ## This is normally stored in /var/log/pods
  ## Modify these values according to your environment.
  volumeMounts:
    - name: pod-logs
      mountPath: /var/log/pods
  volumes:
    - name: pod-logs
      hostPath:
        path: /var/log/pods

functions:
  image:
    tag: v1.41.2

```









