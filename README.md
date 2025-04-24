[![Build & Deploy to Azure Container App from ACR](https://github.com/Muhammadyousafrana/huggingface-azure-acr/actions/workflows/main.yml/badge.svg)](https://github.com/Muhammadyousafrana/huggingface-azure-acr/actions/workflows/main.yml)
# huggingface-azure-acr

### To create `AZURE_CREDENTIALS` go to azure portal and open cloud shell and run the following commands:
1. 
```sh
az login
```
2.
```sh
az ad sp create-for-rbac \
  --name gha-deploy \
  --role contributor \
  --scopes /subscriptions/<subscription ID> \
  --sdk-auth
```
