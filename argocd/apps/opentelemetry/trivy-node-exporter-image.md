# Scanning and Resolving prometheus node exporter Docker Image Vulnerabilities using Trivy


## Step1: Trivy Scan 

Run the following command to perform a vulnerability scan on the ArgoCD Docker image:
```
trivy image quay.io/prometheus/node-exporter:master

```
### Vulnerability Scan Report

This document provides a summary of the vulnerabilities identified during a Trivy scan of the specified binaries.

---

### Scanned Binaries

- `bin/node_exporter` (gobinary)



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

### For `bin/node_exporter`
- **Update** `golang.org/x/net` to version **0.33.0** or later to resolve CVE-2024-45338.

---



## Step2: Clone prometheus node exporter Official GitHub Repository

Clone the ArgoCD repository and switch to the specified version:
```
git clone https://github.com/prometheus/node_exporter.git
cd node_exporter
```

## Step3: Update the go.mod file
```
go get golang.org/x/net@v0.33.0
go mode tidy
make build
```


## Step 4: Build and Push the Dockerfile

```
make docker
docker build -t savannah.ornl.gov/kdi/coreii-data-lake/prometheus/node-exporter:master .
docker push savannah.ornl.gov/kdi/coreii-data-lake/prometheus/node-exporter:master
```

## Step 5: Check the Trivy Scan with Latest Images

Perform a Trivy scan on the updated Docker image:
```
trivy image savannah.ornl.gov/kdi/coreii-data-lake/prometheus/node-exporter:master
```
