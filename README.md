# Fully automated iperf3 testing between Azure regions

## Requirements
- Create a storage account.
- Create a SAS token for that storage account.
- Create a container in the storage account called 'iperf'

Pass in parameters `storageAccountName` and `SAS-token` either via a parameters file, or at runtime. Recommended approach is parameters file.

Example parameters file, called `vm-deploy.parameters.json`
```json
{
    "$schema": "https://schema.management.azure.com/schemas/2019-04-01/deploymentParameters.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "SAS-token":{
            "value": "?sv=2019-12-12&ss=bfqt&srt=sco&sp=rwdlacuptfx&se=2020-10-29T08:07:43Z&st=2020-10-28T00:07:43Z&spr=https&sig=XXX%3D"
        }
    }
}
```

## How to deploy
```bash
az group create -l westus2 -n networktest
az deployment group create --template-file vm-deploy.json --parameters @vm-deploy.parameters.json -g networktest
```