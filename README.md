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
it will output something like this:

```sh
{
  "clientId": "...",
  "clientSecret": "...",
  "subscriptionId": "...",
  "tenantId": "...",
  "activeDirectoryEndpointUrl": "...",
  "resourceManagerEndpointUrl": "...",
  "clientCertificate": null
}
```

3. copy this json output and go to repository setting and in the secret section create a secrect for `Action` with the name `AZURE_CREDENTIALS` and put the json output and save it
