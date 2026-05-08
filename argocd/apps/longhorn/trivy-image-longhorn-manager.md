# Scanning and Resolving longhorn manager Docker Image Vulnerabilities using Trivy


## Step1: Trivy Scan 

Run the following command to perform a vulnerability scan on the ArgoCD Docker image:
```
trivy image longhornio/longhorn-manager:v1.7.2

```
### Vulnerability Scan Report

This document provides a summary of the vulnerabilities identified during a Trivy scan of the specified binaries.

---

### Scanned Binaries

- `longhorn-manager` (gobinary)


---

## Scan Summary

### `csi-provisioner`
**Total Vulnerabilities**: 2  
- **UNKNOWN**: 0  
- **LOW**: 0  
- **MEDIUM**: 0
- **HIGH**: 1  
- **CRITICAL**: 0  


| Library               | Vulnerability    | Severity  | Status | Installed Version | Fixed Version | Title                                                                                  |
|------------------------|------------------|-----------|--------|-------------------|---------------|----------------------------------------------------------------------------------------|
| `golang.org/x/net`    | CVE-2024-45338   | HIGH      |   fixed     | v0.32.0           | 0.33.0        | Non-linear parsing of case-insensitive content in `golang.org/x/net/html`.             |


---

## Recommendations

### For `longhorn-manager`
- **Update** `golang.org/x/net` to version **0.33.0** or later to resolve CVE-2024-45338.

---



## Step2: Clone longhorn-maanager Official GitHub Repository

Clone the longhorn manager and switch to the specified version:
```
git clone https://github.com/longhorn/longhorn-manager.git
cd longhorn-manager/
git checkout v1.7.2
```

## Step3: Update the go.mod file
```
go get golang.org/x/net@v0.33.0
go mode tidy
go mod vendor
make 
```


## Step 4: Build and Push the Dockerfile

```
docker tag docker.io/longhornio/longhorn-manager:fd2ef9c5e-dirty savannah.ornl.gov/kdi/coreii-data-lake/longhorn-manager:v1.7.x-head
docker push savannah.ornl.gov/kdi/coreii-data-lake/longhorn-manager:v1.7.x-head
```

## Step 5: Check the Trivy Scan with Latest Images

Perform a Trivy scan on the updated Docker image:
```
trivy image savannah.ornl.gov/kdi/coreii-data-lake/longhorn-manager:v1.7.x-head
```
