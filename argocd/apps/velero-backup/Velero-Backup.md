# Velero Namespace Backup Instructions

This guide outlines the steps to back up a specific Kubernetes namespace using Velero, with the backup stored in MinIO.

## Steps to Back Up a Specific Namespace

### 1. Create a Velero Backup Manifest  
Create a Velero manifest for the namespace you want to back up. Below is a sample manifest for backing up the `minio` namespace:

```yaml
apiVersion: velero.io/v1
kind: Backup
metadata:
  name: minio-backup
spec:
  includedNamespaces:
    - minio
  excludedNamespaces:
    - kube-system
  includedResources:
    - pods
    - services
  excludedResources:
    - events
  labelSelector:
    matchLabels:
      app: minio
  storageLocation: velero
  snapshotVolumes: true
  ttl: 72h

```

### 2. Verify Backup in MinIO Dashboard

Once the backup process is initiated, navigate to the MinIO dashboard to confirm the backup's presence. The backup will be stored under the `backups` directory, in a subfolder named after the backup's name (e.g., `minio-backup`).

For example, a backup named minio-backup will appear in the path:
`backups/minio-backup`.

### Note: 
The same process can be repeated for other namespaces by modifying the `includedNamespaces`, `labelSelector`, and `metadata.name` fields in the manifest to match the desired namespace and application.
