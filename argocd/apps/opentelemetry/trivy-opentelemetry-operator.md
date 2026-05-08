# Scanning and Resolving opentelemetry-operator Docker Image Vulnerabilities using Trivy


## Step1: Trivy Scan 

Run the following command to perform a vulnerability scan on the ArgoCD Docker image:

```
trivy image  ghcr.io/open-telemetry/opentelemetry-operator/opentelemetry-operator:v0.116.0
```

### Vulnerability Scan Report

This document provides a summary of the vulnerabilities identified during a Trivy scan of the specified binaries.

---

### Scanned Binaries

- `bin/node_exporter` (gobinary)



---

## Scan Summary

### `opentelemetry-operator`
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



## Step2: Clone opentelemetry-operator Official GitHub Repository

Clone the opentelemetry-operator
```
git clone https://github.com/open-telemetry/opentelemetry-operator.git
```

## Step3: Update the go.mod file
```
go get golang.org/x/net@v0.33.0
go mode tidy
make container
```


## Step 4: Check image

image already pull with new tag
```
docker images
```

## Step 5: Check the Trivy Scan with Latest Images

Perform a Trivy scan on the updated Docker image:
```
trivy image savannah.ornl.gov/kdi/coreii-data-lake/opentelemetry-operator:0.116.0-1
```
