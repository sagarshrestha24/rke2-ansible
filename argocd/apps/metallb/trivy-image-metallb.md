# Scanning and Resolving metallb Docker Image Vulnerabilities using Trivy


## Step1: Trivy Scan 

Run the following command to perform a vulnerability scan on the ArgoCD Docker image:
```
trivy image quay.io/metallb/controller
trivy image quay.io/metallb/speaker

```
### Vulnerability Scan Report

This document provides a summary of the vulnerabilities identified during a Trivy scan of the specified binaries.

---

### Scanned Binaries

- `controller` (gobinary)
- `speaker` (gobinary)


---

## Scan Summary

### `speaker`
**Total Vulnerabilities**: 1  
- **UNKNOWN**: 0  
- **LOW**: 0  
- **MEDIUM**: 0
- **HIGH**: 1  
- **CRITICAL**: 0  


| Library               | Vulnerability    | Severity  | Status | Installed Version | Fixed Version | Title                                                                                  |
|------------------------|------------------|-----------|--------|-------------------|---------------|----------------------------------------------------------------------------------------|
| `golang.org/x/net`    | CVE-2024-45338   | HIGH      |   fixed     | v0.30.0           | 0.33.0        | Non-linear parsing of case-insensitive content in `golang.org/x/net/html`.             |

### `controller`
**Total Vulnerabilities**: 1  
- **UNKNOWN**: 0  
- **LOW**: 0  
- **MEDIUM**: 0
- **HIGH**: 1  
- **CRITICAL**: 0  


| Library               | Vulnerability    | Severity  | Status | Installed Version | Fixed Version | Title                                                                                  |
|------------------------|------------------|-----------|--------|-------------------|---------------|----------------------------------------------------------------------------------------|
| `golang.org/x/net`    | CVE-2024-45338   | HIGH      |   fixed     | v0.30.0           | 0.33.0        | Non-linear parsing of case-insensitive content in `golang.org/x/net/html`.             |


---

## Recommendations

### For `controller`
- **Update** `golang.org/x/net` to version **0.33.0** or later to resolve CVE-2024-45338.

### For `speaker`
- **Update** `golang.org/x/net` to version **0.33.0** or later to resolve CVE-2024-45338.

---



## Step2: Clone metallb Official GitHub Repository

Clone the metallb repository and switch to the specified version:
```
git clone https://github.com/metallb/metallb.git
cd metallb
```

## Step3: Update the go.mod file
```
go get golang.org/x/net@v0.33.0
go mode tidy
make all
```


## Step 4: Build and Push the Dockerfile

```
docker  build --build-arg GIT_BRANCH=v0.14.9   --label org.opencontainers.image.created=2024-12-17T14:50:29.605Z  --platform linux/amd64 --tag savannah.ornl.gov/kdi/coreii-data-lake/metallb/controller:v0.14.9 -f controller/Dockerfile .
docker  build --build-arg GIT_BRANCH=v0.14.9   --label org.opencontainers.image.created=2024-12-17T14:50:29.605Z  --platform linux/amd64 --tag savannah.ornl.gov/kdi/coreii-data-lake/metallb/speaker:v0.14.9 -f speaker/Dockerfile .
docker push savannah.ornl.gov/kdi/coreii-data-lake/metallb/speaker:v0.14.9
docker push savannah.ornl.gov/kdi/coreii-data-lake/metallb/controller:v0.14.9
```

## Step 5: Check the Trivy Scan with Latest Images

Perform a Trivy scan on the updated Docker image:
```
trivy image savannah.ornl.gov/kdi/coreii-data-lake/metallb/speaker:v0.14.9
trivy image savannah.ornl.gov/kdi/coreii-data-lake/metallb/controller:v0.14.9
```
