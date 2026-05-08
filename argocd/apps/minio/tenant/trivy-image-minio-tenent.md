# Scanning and Resolving minio Docker Image Vulnerabilities using Trivy


## Step1: Trivy Scan 

Run the following command to perform a vulnerability scan on the minio Docker image:
```
trivy image quay.io/minio/minio:RELEASE.2024-10-02T17-50-41Z

```
### Vulnerability Scan Report

This document provides a summary of the vulnerabilities identified during a Trivy scan of the specified binaries.

---

### Scanned Binaries

- `minio` (gobinary)


---

## Scan Summary

### `csi-provisioner`
**Total Vulnerabilities**: 2  
- **UNKNOWN**: 0  
- **LOW**: 0  
- **MEDIUM**: 0
- **HIGH**: 1  
- **CRITICAL**: 1  


---

## Recommendations

### For `csi-provisioner`
- **Update** `golang.org/x/net` to version **0.33.0** or later to resolve CVE-2024-45338.
- **Update** `golang.org/x/crypto` to version **0.31.0** or later to resolve CVE-2024-45338.

---

## Step2: Clone minio Official GitHub Repository

Clone the mc repository and switch to the specified version:
```
git clone https://github.com/minio/minio.git
cd minio
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
docker tag quay.io/minio/minio:RELEASE.2024-12-18T13-15-44Z-3-g330dca9a3 savannah.ornl.gov/kdi/coreii-data-lake/minio/minio:v6.0.4
docker push savannah.ornl.gov/kdi/coreii-data-lake/minio/minio:v6.0.4
```

## Step5: Clone mc Official GitHub Repository

Clone the mc repository and switch to the specified version:
```
git clone  https://github.com/minio/mc.git
cd mc
```

## Step6: Update the go.mod file
```
go get golang.org/x/net@v0.33.0
go mode tidy
make build
```
## Step7: Update the Dockerfile

```
FROM savannah.ornl.gov/kdi/coreii-data-lake/minio/minio:v6.0.4-12_19-24 
COPY mc  /usr/bin/mc

```


## Step 8: Build and Push the Dockerfile

```
docker build -t savannah.ornl.gov/kdi/coreii-data-lake/minio/minio:v6.0.4-12_19-24 -f Dockerfile .
docker push savannah.ornl.gov/kdi/coreii-data-lake/minio/minio:v6.0.4-12_19-24
```

## Step 9: Check the Trivy Scan with Latest Images

Perform a Trivy scan on the updated Docker image:
```
trivy image savannah.ornl.gov/kdi/coreii-data-lake/minio/minio:v6.0.4-12_19-24
```
