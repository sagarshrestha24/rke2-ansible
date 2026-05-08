# Dependencies Documentation

This document outlines the dependencies required for the server setup, including pre-installation, installation steps, and post-installation configurations.

---

## Pre-Installation Dependencies

# Air-Gap Install

RKE2 can be installed in an air-gapped environment with two different methods. You can either deploy via the rke2-airgap-images tarball release artifact, or by using a private registry.

All files mentioned in the steps can be obtained from the assets of the desired released rke2 version [here](https://github.com/rancher/rke2/releases).

If running on an SELinux enforcing air-gapped node, you must first install the necessary SELinux policy RPM before performing these steps. See our [RPM Documentation](https://docs.rke2.io/install/methods/#rpm) to determine what you need.

# Tarball Method
This ansible playbook will detect if the `rke2-images.linux-amd64.tar.zst` and `rke2.linux-amd64.tar.gz` files are in the tarball_install/ directory. If the files are in the directory then the install process will skip both the yum install and the need to download the tarball.

## Images Install
If either the `rke2-images.linux-amd64.tar.zst` or `rke2-images.linux-amd64.tar.gz` files are found in the tarbarll_install/ directory then this playbook will use the images inside the tarball and not docker.io or a private registry.

## Tarball Install
If the `rke2.linux-amd64.tar.gz` file is found in the tarball_install/ directory then this playbook will install RKE2 using that version. This will use the default docker.io registry unless the images tarball is present or unless the `system-default-registry` variable is set.


# Yum Package install
Before installing the server components, ensure the following binaries are installed via the `yum` package manager:

- **NGINX**  
  A web server and reverse proxy server.

- **iscsi-initiator-utils**  
  Utilities for connecting to iSCSI storage devices.

- **kubectl**  
  A command-line tool to interact with Kubernetes clusters.

- **Helm**  
  A package manager for Kubernetes.


---

## Installation Steps


1. Install the required binaries using the following commands:

    ```bash
    yum install -y nginx iscsi-initiator-utils

    # Install kubectl
    curl -LO "https://dl.k8s.io/release/$(curl -L -s https://dl.k8s.io/release/stable.txt)/bin/linux/amd64/kubectl"
    install -o root -g root -m 0755 kubectl /usr/local/bin/kubectl

    # Install Helm
    curl -fsSL https://raw.githubusercontent.com/helm/helm/main/scripts/get-helm-3 | bash
    ```
---

# Post-Installation Dependencies and Configurations

## Workflow for Downloading and Pushing Images to GitLab Container Registry

**Prerequisites**

 1. Ensure you have access to the GitLab Container Registry.
 2. Authenticate using GitLab credentials:

```bash
docker login registry.gitlab.com
```
 3. Define your GitLab repository URL (e.g., registry.gitlab.com/<group>/<project>).

### Steps for Each Image

  1. Pull the Image: Use the docker pull command to fetch the image from its source registry.

  2. Tag the Image: Retag the image to the GitLab Container Registry path.

  3. Push the Image: Use docker push to upload the image to the GitLab Container Registry.

  4.  Verify Push: After pushing, verify the image is available in the GitLab Container Registry.

## List of Images that it should download from and push it their respective registry

### **ArgoCD**

### Images:

- `quay.io/argoproj/argocd:v2.13.1`
- `ghcr.io/dexidp/dex:v2.41.1`


### **Longhorn**

A distributed block storage system for Kubernetes.

### Images:
- `longhornio/longhorn-engine:v1.7.2`
- `longhornio/longhorn-manager:v1.7.2`
- `longhornio/longhorn-ui:v1.7.2`
- `longhornio/longhorn-instance-manager:v1.7.2`
- `longhornio/longhorn-share-manager:v1.7.2`
- `longhornio/backing-image-manager:v1.7.2`
- `longhornio/support-bundle-kit:v0.0.45`

---

### **Longhorn CSI**

### Images:
- `longhornio/csi-attacher:v4.7.0`
- `longhornio/csi-provisioner:v4.0.1-20241007`
- `longhornio/csi-node-driver-registrar:v2.12.0`
- `longhornio/csi-resizer:v1.12.0`
- `longhornio/csi-snapshotter:v7.0.2-20241007`
- `longhornio/livenessprobe:v2.14.0`

---

### **MetalLB**

A load balancer for Kubernetes.

### Images:
- `quay.io/metallb/controller`
- `quay.io/metallb/speaker`
- `quay.io/frrouting/frr`

---

### **MinIO**

A high-performance object storage system.

### Images:
- `quay.io/minio/operator:v6.0.4`
- `quay.io/minio/minio:RELEASE.2024-10-02T17-50-41Z`

---

### **Postgres**

A database management system.

### Controller Images:
- `registry.developers.crunchydata.com/crunchydata/postgres-operator:ubi8-5.6.1-0`

### Related Images:
- `registry.developers.crunchydata.com/crunchydata/crunchy-postgres:ubi8-16.4-0`
- `registry.developers.crunchydata.com/crunchydata/crunchy-postgres:ubi8-15.8-0`
- `registry.developers.crunchydata.com/crunchydata/crunchy-pgadmin4:ubi8-4.30-29`
- `registry.developers.crunchydata.com/crunchydata/crunchy-pgbackrest:ubi8-2.52.1-1`

---

### **Supabase**

An open-source backend-as-a-service.

### Images:
- `supabase/postgres:latest`
- `supabase/studio:latest`
- `supabase/gotrue:latest`
- `postgrest/postgrest:latest`
- `supabase/realtime:latest`
- `supabase/postgres-meta:latest`
- `supabase/storage-api:latest`
- `kong:latest`

---

### **Kong**

A cloud-native API gateway.

### Images:
- `kong:3.7`

---

### **Kong Ingress Controller**

Manages ingress resources in Kubernetes.

### Images:
- `kong/kubernetes-ingress-controller:3.3`

---

### **OpenTelemetry**

### Images:
- `quay.io/prometheus/alertmanager:v0.27.0`
- `ghcr.io/open-telemetry/demo:1.12.0-frontend`
- `ghcr.io/open-telemetry/demo:1.12.0-frontendproxy`
- `docker.io/grafana/grafana:11.2.2`
- `jaegertracing/all-in-one:1.53.0`
- `registry.k8s.io/kube-state-metrics/kube-state-metrics:v2.13.0`
- `otel/opentelemetry-collector-contrib:0.110.0`
- `ghcr.io/open-telemetry/opentelemetry-operator/opentelemetry-operator:0.110.0`
- `quay.io/brancz/kube-rbac-proxy:v0.18.1`
- `quay.io/prometheus/node-exporter:v1.8.2`
- `quay.io/prometheus/pushgateway:v1.9.0`
- `quay.io/prometheus-operator/prometheus-config-reloader:v0.76.0`
- `quay.io/prometheus/prometheus:v2.54.1`
- `valkey/valkey:7.2-alpine`

---

## **Usage**

1. Pull the images using the specified tags.
2. Retag them for your GitLab Container Registry:
   ```bash
   docker tag <source-image> registry.gitlab.com/<group>/<project>/<image-name>
   ```
3. Push the images to your GitLab Container Registry:

   ```bash
   docker push registry.gitlab.com/<group>/<project>/<image-name>
   ```
4. Verify that the images are available in the registry.
   

