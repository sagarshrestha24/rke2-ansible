# Install pgadmin in Kubernetes Cluster

pgAdmin4 is the leading Open Source management tool for Postgres, the world’s most advanced Open Source database. pgAdmin4 is designed to meet the needs of both novice and experienced Postgres users alike, providing a powerful graphical interface that simplifies the creation, maintenance and use of database objects.

## Pre-requisite

Before deploying the pgadmin, ensure the following are running

1. Kubernetes cluster.
2. Postgres cluster 
3. helm 
4. Argocd installed for installation using argocd.

## Install pgadmin using helm chart

### Step 1: Add the Helm Chart Repository

```
helm repo add runix https://helm.runix.net
```

### Step 3: Customize values.yaml
We can customize the installation by providing a values.yaml file.

Create values.yaml
```
ingress:
  enabled: true
  ingressClassName: nginx
  hosts:
  - host: pgadmin4.coreii.labenv.ai
    paths:
      - path: /
        pathType: ImplementationSpecific
  tls: []

env:
  
  email: pgadmin@coreii.com  #can be email and password for pgadmin dashboard
  password: pgadmin@123
```
### Install the Helm chart with the custom values.yaml

```
helm install pgadmin4 runix/pgadmin4 -n pgo -f values.yaml
```

Check the pod state and ingress

```
kubectl get pod -n pgo
kubectl get ing -n pgo
```

Now, we just need to run port forwarding for the pgAdmin service name or access through ingress 

## Install pgadmin using Argodcd

### Step 1: Add the Helm Chart Repository

```
helm repo add runix https://helm.runix.net
```

### Step 2: Pull helm charts

```
helm pull runix/pgadmin4
```
untar tar file

```
tar -xvf <pgadminfile>.tar
```
Copy all the chart file to the repo directory where we have to sync

Clone the repository
```
cp -r pgadmin4 <repo directory>
```
For inl-infra repo.

```
cp -r pgadmin4 inl-infra/argocd/apps/
```
### Step 3: Customize values.yaml
We can customize the installation by providing custom value to the values.yaml file.

Edit values.yaml
```
ingress:
  enabled: true
  ingressClassName: nginx
  hosts:
  - host: pgadmin4.coreii.labenv.ai
    paths:
      - path: /
        pathType: ImplementationSpecific
  tls: []

env:
  
  email: pgadmin@coreii.com  #can be email and password for pgadmin dashboard
  password: pgadmin@123
```
### Step 3: Create application manifest 

For inl-infra repo

Create manifest in inl-infra/argocd/crs

pgadmin.yaml
```
apiVersion: argoproj.io/v1alpha1
kind: Application
metadata:
  name: pgadmin4
  namespace: argocd
spec:
  destination:
    name: ''
    namespace: pgo
    server: 'https://kubernetes.default.svc'
  source:
    path: argocd/apps/pgadmin4
    repoURL: 'https://github.com/01cloud/inl-infra.git'
    targetRevision: HEAD
  sources: []
  project: default
  syncPolicy:
    automated:
      prune: true
      selfHeal: true
    syncOptions:
      - CreateNamespace=true
      - ServerSideApply=true

```
Apply application manifest in argocd namespace

```
kubectl apply -f pgadmin.yaml -n argocd
```

Check pod Status and application status in argocd.

## Configuration of pgadmin 

### Configure pgadmin host name 

#### linux
Map host name in etc/hosts

```
sudo vi /etc/hosts
```

Add this ip and ingress host

`ingress ip   pgadmin4.coreii.labenv.ai`

#### Windows

Open powershell using adminitrator mode

```
notepad system32/etc/drivers/hosts
```

Add this ip and ingress host

`ingress ip  pgadmin4.coreii.labenv.ai`

### Acess pgadmin Dashboard in browser

#### Using ingress hostname

http://pgadmin4.coreii.labenv.ai

Log in to pgAdmin using the configured username and password.

#### Using Port Forwarding

```
kubectl port-forward svc/pgadmin4 8080:80 -n pgo
http://localhost:8080
```

Log in to pgAdmin using the configured username and password

### Add postgres cluster (server)
After that, you only need to add a connection to Postgres by clicking Add New Server.


- Name: Any name (e.g., PostgreSQL)
- Host: The hostname or service name of your PostgreSQL instance.
- Port: 5432 (default PostgreSQL port).
- Username and Password: Your PostgreSQL credentials.

In our scenario we have deployed postgres cluster using pgo operator in same pgo namespace

 ```
Kubectl get secret -n pgo

kubectl get secret hippo-pguser-coreii -n pgo -oyaml
```

Decode password, host, username and password for access in pgadmin

### Add existing pgo cluster i.e. crunchy data postgres cluster

Add a connection to Postgres by clicking Add New Server in pgadmin Dashboard

1. First provide server name
2. Provide hostame i.e. hippo-primary.pgo.svc
3. Provide database name i.e. Decode from secret
4. Provide username i.e. Decode from secret
5. Provide password i.e. Decode from secret

We can manage Postgres using the pgAdmin interface or SQL queries. Viewing databases, schemas, and tables and writing SQL queries has become very convenient.
