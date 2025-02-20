# Configuration Repository

This repository manages **client and environment-specific configurations** for deployments.

## 🏗️ **Directory Structure**
```
├── .github/workflows/ # CI/CD pipeline configurations 
│ ├── deploy.yaml ├── C1/ # Client-specific configuration 
│ ├── PROD/ # Environment-specific configuration 
│ │ ├── values.yaml 
│ ├── TEST/ 
│ ├── UAT/ 
├── C2/ # Another client-specific configuration 
│ ├── PROD/ 
│ ├── TEST/ 
│ ├── UAT/ 
├── deployments/ # Common deployment templates 
│ ├── common-deployment.yaml 
├── README.md
```

## 📌 **Client & Environment Configurations**
Each client (`C1`, `C2`, etc.) has its own directory, and **each environment** (`PROD`, `TEST`, `UAT`) has a `values.yaml` file with configuration details.

### **Example: `C1/PROD/values.yaml`**
```yaml
clientName: "c1"
env: "prod"

modules:
  - name: "API-dotnet"
    image: "umang/api-dotnet:v1"
    port: 8080
    env:
      LG_LEVEL: "info"

  - name: "db"
    image: "umang/db:v1"
    port: 8082
```
## Deployment Process

- The deployment pipeline uses GitHub Actions (deploy.yaml) to apply configurations.

- Deploying to Kubernetes [This will be mentioned in pipeline to deploy]
```
kubectl apply -f deployments/common-deployment.yaml \
  --values=C1/PROD/values.yaml
```

# Managing Secrets Securely

Instead of storing database credentials in plain text, use Kubernetes Secrets or environment variables managed by a secret management tool like:

- AWS Secrets Manager
- HashiCorp Vault
- Kubernetes Secrets

  - can create it using pipeline only or can store it AWS secreate manager / vault and retrieve it while pipeline is running
