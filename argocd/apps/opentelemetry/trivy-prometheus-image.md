# Scanning and Resolving prometheus Docker Image Vulnerabilities using Trivy


## Step1: Trivy Scan 

Run the following command to perform a vulnerability scan on the ArgoCD Docker image:
```
trivy image quay.io/prometheus/prometheus:v3.0.1

```
### Vulnerability Scan Report

This document provides a summary of the vulnerabilities identified during a Trivy scan of the specified binaries.

---

### Scanned Binaries

- `bin/prometheus` (gobinary)
- `bin/promtool` (gobinary)


---

## Scan Summary

### `csi-provisioner`
**Total Vulnerabilities**: 4  
- **UNKNOWN**: 0  
- **LOW**: 0  
- **MEDIUM**: 0
- **HIGH**: 2  
- **CRITICAL**: 2  


## Recommendations

### For `bin/promtool`
- **Update** `golang.org/x/crypto` to version **0.31.0** or later to resolve CVE-2024-45337.
- **Update** `golang.org/x/net` to version **0.33.0** or later to resolve CVE-2024-45338.

---



## Step2: Clone prometheus Official GitHub Repository

Clone the ArgoCD repository and switch to the specified version:
```
git clone https://github.com/prometheus/prometheus.git
cd prometheus
git checkout v3.0.1
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
docker tag docker.io/prom/prometheus-linux-s390x:HEAD savannah.ornl.gov/kdi/coreii-data-lake/prometheus/prometheus:main
docker push savannah.ornl.gov/kdi/coreii-data-lake/prometheus/prometheus:main
```

## Step 5: Check the Trivy Scan with Latest Images

Perform a Trivy scan on the updated Docker image:
```
trivy image savannah.ornl.gov/kdi/coreii-data-lake/prometheus/prometheus:main
```
