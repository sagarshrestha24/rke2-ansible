# Scanning and Resolving minio operatr sidecar Docker Image Vulnerabilities using Trivy


## Step1: Trivy Scan 

Run the following command to perform a vulnerability scan on the ArgoCD Docker image:
```
trivy image quay.io/minio/operator-sidecar:v6.0.2

```
### Vulnerability Scan Report

This document provides a summary of the vulnerabilities identified during a Trivy scan of the specified binaries.

---

### Scanned Binaries

- minio-operator-sidecar (gobinary)


---

## Scan Summary

### `csi-provisioner`
**Total Vulnerabilities**: 6  
- **UNKNOWN**: 0  
- **LOW**: 1  
- **MEDIUM**: 2
- **HIGH**: 2  
- **CRITICAL**: 1  
---

## Recommendations

### For `csi-provisioner`
- **Update** `golang.org/x/net` to version **0.33.0** or later to resolve CVE-2024-45338.
- **Update** `golang.org/x/crypto` to version **0.31.0** or later to resolve CVE-2024-45337.
- **Update** `go version` to version *1.23**

---



## Step2: Clone kong minio operator Official GitHub Repository

Clone the minio operator repository and switch to the specified version:
```
git clone https://github.com/minio/operator.git 
cd operator/
git checkout v6.0.4
cd sidecar
```

## Step3: Update the go.mod file
```
go get golang.org/x/net@v0.33.0
go mode tidy
```
## Step4: Change the version of go in go.mod file from 1.22.5 to 1.23

```
vim go.mod
```
## Step5: Make the binary file of minio operator sidecar

```
make binary
ls minio-operator-sidecar
```

## Step 6: Build and Push the Dockerfile

```
make docker
docker tag docker.io/minio/operator-sidecar:v6.0.4 savannah.ornl.gov/kdi/coreii-data-lake/minio/operator-sidecar:v6.0.4
docker push savannah.ornl.gov/kdi/coreii-data-lake/minio/operator-sidecar:v6.0.4
```

## Step 5: Check the Trivy Scan with Latest Images

Perform a Trivy scan on the updated Docker image:
```
trivy image savannah.ornl.gov/kdi/coreii-data-lake/minio/operator-sidecar:v6.0.4
```
