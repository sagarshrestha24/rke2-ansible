# Scanning and Resolving longhorn support bundle kit Docker Image Vulnerabilities using Trivy


## Step1: Trivy Scan 

Run the following command to perform a vulnerability scan on the ArgoCD Docker image:
```
trivy image longhornio/support-bundle-kit:v0.0.48
```
### Vulnerability Scan Report

This document provides a summary of the vulnerabilities identified during a Trivy scan of the specified binaries.

---

### Scanned Binaries

- `usr/bin/yq` (gobinary)


---

## Scan Summary

### `manager`
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

### For `usr/bin/yq`
- **Update** `golang.org/x/net` to version **0.33.0** or later to resolve CVE-2024-45338.

---



## Step2: Clone kong ingress controoler Official GitHub Repository

Clone the ArgoCD repository and switch to the specified version:
```
git clone https://github.com/mikefarah/yq.git
cd yq
```



## Step3: Update the go.mod file
```
go get golang.org/x/net@v0.33.0
go mode tidy
CGO_ENABLED=0 go build -ldflags "-s -w" .
```


## Step 4: Build and Push the Dockerfile

Build and push the updated Docker image:

Create Dockerfile-yq file 
```
FROM longhornio/support-bundle-kit:v0.0.48
user root 

COPY yq /usr/bin/
```

```
docker build -t savannah.ornl.gov/kdi/coreii-data-lake/support-bundle-kit:v0.0.48-12_19_24
docker push savannah.ornl.gov/kdi/coreii-data-lake/support-bundle-kit:v0.0.48-12_19_24
```

## Step 5: Check the Trivy Scan with Latest Images

Perform a Trivy scan on the updated Docker image:
```
trivy image savannah.ornl.gov/kdi/coreii-data-lake/support-bundle-kit:v0.0.48-12_19_24
```
