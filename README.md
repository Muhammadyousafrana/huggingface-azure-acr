# huggingface-azure-acr

[![Build & Deploy to Azure Container App from ACR](https://github.com/Muhammadyousafrana/huggingface-azure-acr/actions/workflows/main.yml/badge.svg)](https://github.com/Muhammadyousafrana/huggingface-azure-acr/actions/workflows/main.yml)

## Overview

This project demonstrates an end-to-end MLOps pipeline using GitHub Actions for CI/CD to build and deploy a FastAPI application that leverages Hugging Face’s GPT-2 model for sentence completion. The deployment target is Azure Container Apps, with Docker images managed via Azure Container Registry (ACR).

- **Tech Stack**: Python, FastAPI, Hugging Face Transformers (GPT-2), Docker, Azure Container Registry, Azure Container Apps, GitHub Actions (CI/CD)
- **Use case**: Sentence completion using GPT-2 via a production-ready, scalable REST API

---

## Features

- Automated CI/CD pipeline with GitHub Actions
- Dockerized FastAPI service for serving Hugging Face GPT-2
- Seamless deployment to Azure Container Apps from ACR
- Secure Azure authentication using repository secrets
- MLOps best practices for model deployment

---

## Prerequisites

- Azure subscription with permissions to create resources
- Docker (for local builds/tests)
- Python 3.8+
- Azure CLI

---

## Setup & Deployment

### 1. Clone the repository

```sh
git clone https://github.com/Muhammadyousafrana/huggingface-azure-acr.git
cd huggingface-azure-acr
```

### 2. Azure Credentials

To deploy via GitHub Actions, create `AZURE_CREDENTIALS`:

1. Open Azure Cloud Shell and run:
    ```sh
    az login
    ```
2. Create a service principal:
    ```sh
    az ad sp create-for-rbac \
      --name gha-deploy \
      --role contributor \
      --scopes /subscriptions/<subscription ID> \
      --sdk-auth
    ```
   - Replace `<subscription ID>` with your Azure Subscription ID.
   - Copy the JSON output.

3. In your GitHub repo, go to **Settings > Secrets and variables > Actions**, add a new secret named `AZURE_CREDENTIALS`, and paste the JSON output.

---

### 3. Build & Deploy

- On each push to `main`, GitHub Actions will:
  - Build the Docker image with FastAPI and GPT-2
  - Push to Azure Container Registry
  - Deploy to Azure Container Apps

You can monitor the deployment status via the GitHub Actions tab.

---

### 4. Logs

After deployment, view logs using Azure CLI:

```sh
az containerapp logs show \
  --name <container-app-name> \
  --resource-group <resource-group-name>
```

---

## Usage

The deployed FastAPI service exposes a REST API for sentence completion using GPT-2.

**Example request:**

```sh
curl -X POST "https://<your-app-url>/complete" -H "Content-Type: application/json" -d '{"prompt": "Once upon a time"}'
```

**Response:**
```json
{
  "completion": "Once upon a time, there was a..."
}
```

---

## Contributing

Contributions are welcome! Please open issues or submit pull requests for improvements.

---

## License

[MIT License](LICENSE)

---

## Contact

For questions, open an issue or contact the repo owner.

---
