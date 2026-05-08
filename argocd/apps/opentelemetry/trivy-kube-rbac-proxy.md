# Scanning and Resolving kube rbac proxy Docker Image Vulnerabilities using Trivy


## Step1: Trivy Scan 

Run the following command to perform a vulnerability scan on the  Docker image:
```
trivy image quay.io/brancz/kube-rbac-proxy:master-2024-12-13-af1a90b6

```
### Vulnerability Scan Report

This document provides a summary of the vulnerabilities identified during a Trivy scan of the specified binaries.

---

### Scanned Binaries

- `usr/local/bin/kube-rbac-proxy` (gobinary)



---

## Scan Summary

### `csi-provisioner`
**Total Vulnerabilities**: 0
- **UNKNOWN**: 0  
- **LOW**: 0  
- **MEDIUM**: 0
- **HIGH**: 1  
- **CRITICAL**: 0 


## Recommendations

### For `usr/local/bin/kube-rbac-proxy`
- **Update** `golang.org/x/net` to version **0.33.0** or later to resolve CVE-2024-45338.

---



## Step2: Clone prometheus node exporter Official GitHub Repository

Clone the ArgoCD repository and switch to the specified version:
```
git clone https://github.com/brancz/kube-rbac-proxy.git
cd kube-rbac-proxy
```

## Step3: Update the go.mod file
```
go get golang.org/x/net@v0.33.0
make container
```


## Step 4: Build and Push the Dockerfile

```
docker tag quay.io/brancz/kube-rbac-proxy:v0.18.2-af1a90b6-amd64 savannah.ornl.gov/kdi/coreii-data-lake/brancz/kube-rbac-proxy:v0.18.2
docker push savannah.ornl.gov/kdi/coreii-data-lake/brancz/kube-rbac-proxy:v0.18.2
```

## Step 5: Check the Trivy Scan with Latest Images

Perform a Trivy scan on the updated Docker image:
```
trivy image savannah.ornl.gov/kdi/coreii-data-lake/brancz/kube-rbac-proxy:v0.18.2
```
