# Scanning and Resolving Kong Ingress Controller Docker Image Vulnerabilities using Trivy


## Step1: Trivy Scan 

Run the following command to perform a vulnerability scan on the kong Ingress  Docker image:
```
trivy image kong/kubernetes-ingress-controller:2.12
```
### Vulnerability Scan Report

This document provides a summary of the vulnerabilities identified during a Trivy scan of the specified binaries.

---

### Scanned Binaries

- `manager` (gobinary)


---

## Scan Summary

### `manager`
**Total Vulnerabilities**: 2  
- **UNKNOWN**: 0  
- **LOW**: 0  
- **MEDIUM**: 1  
- **HIGH**: 1  
- **CRITICAL**: 0  


| Library               | Vulnerability    | Severity  | Status | Installed Version | Fixed Version | Title                                                                                  |
|------------------------|------------------|-----------|--------|-------------------|---------------|----------------------------------------------------------------------------------------|
| `golang.org/x/net`    | CVE-2024-45338   | HIGH      |   fixed     | v0.23.0           | 0.33.0        | Non-linear parsing of case-insensitive content in `golang.org/x/net/html`.             |


---

## Recommendations

### For `manager`
- **Update** `golang.org/x/net` to version **0.33.0** or later to resolve CVE-2024-45338.

---



## Step2: Clone kong ingress controoler Official GitHub Repository

Clone the kong ingress repository and switch to the specified version:
```
git clone https://github.com/Kong/kubernetes-ingress-controller.git
cd kubernetes-ingress-controller
git checkout v2.12.7

```

## Step3: Update the go.mod file
```
go  get golang.org/x/net@v0.33.0
go mod tidy
```


## Step 4: Build and Push the Dockerfile

Build and push the updated Docker image:
```
make container
docker tag docker-registry/kong-ingress-controller:v2.12.7 savannah.ornl.gov/kdi/coreii-data-lake/kong/kubernetes-ingress-controller:v2.12.7-12_19_24
docker push savannah.ornl.gov/kdi/coreii-data-lake/kong/kubernetes-ingress-controller:v2.12.7-12_19_24
```

## Step 5: Check the Trivy Scan with Latest Images

Perform a Trivy scan on the updated Docker image:
```
trivy image savannah.ornl.gov/kdi/coreii-data-lake/kong/kubernetes-ingress-controller:v2.12.7-12_19_24
```












