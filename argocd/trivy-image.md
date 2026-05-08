# Scanning and Resolving ArgoCD Docker Image Vulnerabilities using Trivy


## Step1: Trivy Scan 

Run the following command to perform a vulnerability scan on the ArgoCD Docker image:
```
trivy image quay.io/argoproj/argocd:v2.13.1
```
### Vulnerability Scan Report

This document provides a summary of the vulnerabilities identified during a Trivy scan of the specified binaries.

---

### Scanned Binaries

- `/usr/local/bin/helm` (gobinary)
- `/usr/local/bin/kustomize` (gobinary)

---

### Scan Summary

### `/usr/local/bin/helm`
**Total Vulnerabilities**: 2  
- **UNKNOWN**: 0  
- **LOW**: 0  
- **MEDIUM**: 0  
- **HIGH**: 1  
- **CRITICAL**: 1  

| Library               | Vulnerability    | Severity  | Status | Installed Version | Fixed Version | Title                                                                                  |
|------------------------|------------------|-----------|--------|-------------------|---------------|----------------------------------------------------------------------------------------|
| `golang.org/x/crypto` | CVE-2024-45337   | CRITICAL  | fixed  | v0.27.0           | 0.31.0        | Misuse of `ServerConfig.PublicKeyCallback` may cause authorization bypass in `crypto`. |
|                        |                  |           |        |                   |               | [More Info](https://avd.aquasec.com/nvd/cve-2024-45337)                                |
| `golang.org/x/net`    | CVE-2024-45338   | HIGH      |        | v0.26.0           | 0.33.0        | Non-linear parsing of case-insensitive content in `golang.org/x/net/html`.             |
|                        |                  |           |        |                   |               | [More Info](https://avd.aquasec.com/nvd/cve-2024-45338)                                |

---

### `/usr/local/bin/kustomize`
**Total Vulnerabilities**: 3  
- **UNKNOWN**: 0  
- **LOW**: 0  
- **MEDIUM**: 2  
- **HIGH**: 1  
- **CRITICAL**: 0  

| Library | Vulnerability    | Severity  | Status | Installed Version | Fixed Version  | Title                                                                                  |
|---------|------------------|-----------|--------|-------------------|----------------|----------------------------------------------------------------------------------------|
| `stdlib`| CVE-2024-34156   | HIGH      | fixed  | v1.21.12          | 1.22.7, 1.23.1 | Calling `Decoder.Decode` on a message with deeply nested structures.                  |
|         |                  |           |        |                   |                | [More Info](https://avd.aquasec.com/nvd/cve-2024-34156)                                |
| `stdlib`| CVE-2024-34155   | MEDIUM    |        |                   |                | Calling Parse functions containing deeply nested literals.                             |
|         |                  |           |        |                   |                | [More Info](https://avd.aquasec.com/nvd/cve-2024-34155)                                |
| `stdlib`| CVE-2024-34158   | MEDIUM    |        |                   |                | Calling Parse on a `// +build` build tag line with deeply nested literals.             |
|         |                  |           |        |                   |                | [More Info](https://avd.aquasec.com/nvd/cve-2024-34158)                                |

---

## Recommendations

### For `/usr/local/bin/helm`
- **Update** `golang.org/x/crypto` to version **0.31.0** or later to resolve CVE-2024-45337.
- **Update** `golang.org/x/net` to version **0.33.0** or later to resolve CVE-2024-45338.

### For `/usr/local/bin/kustomize`
- **Update** the `stdlib` to version **1.22.7** or **1.23.1** to resolve CVE-2024-34156.
- Monitor updates for fixes to CVE-2024-34155 and CVE-2024-34158.

---



## Step2: Clone ArgoCD Official GitHub Repository

Clone the ArgoCD repository and switch to the specified version:
```
git clone https://github.com/argoproj/argo-cd.git
git checkout v2.14.0-rc2
cd argo-cd
```

## Step3: Update the Binaries for Kustomize and Helm

### 1. Check the Current Binary Versions

Inspect the current binary versions by running:

```
cat hack/tool-versions.sh
```

### 2. Update Binary Versions

Modify the file to update the versions of helm and kustomize as shown below:

```
helm3_version=3.16.4
kubectl_version=1.17.8
kubectx_version=0.6.3
kustomize5_version=5.5.0
protoc_version=27.2
```

### 3. Update Checksums

Run the following scripts to update the checksums for the updated versions:
```
./add-kustomize-checksums.sh 5.5.0
./add-helm-checksums.sh 3.16.4
```

## Step 4: Build and Push the Dockerfile

Build and push the updated Docker image:
```
docker build -t docker-registry/argocd:v2.14.0
docker push docker-registry/argocd:v2.14.0
```

## Step 5: Check the Trivy Scan with Latest Images

Perform a Trivy scan on the updated Docker image:
```
trivy image docker-registry/argocd:v2.14.0
```












