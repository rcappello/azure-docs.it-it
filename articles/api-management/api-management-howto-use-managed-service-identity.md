---
title: Usare l'identità del servizio gestito di Azure in Gestione API di Azure | Microsoft Docs
description: Informazioni su come usare l'identità del servizio gestito di Azure in Gestione API
services: api-management
documentationcenter: ''
author: miaojiang
manager: anneta
editor: ''
ms.service: api-management
ms.workload: integration
ms.topic: article
ms.date: 10/18/2017
ms.author: apimpm
ms.openlocfilehash: 98aa70935a3efbbe2edb07aade85fa3ea17ce786
ms.sourcegitcommit: e2adef58c03b0a780173df2d988907b5cb809c82
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 04/28/2018
ms.locfileid: "32150431"
---
# <a name="use-azure-managed-service-identity-in-azure-api-management"></a>Usare l'identità del servizio gestito di Azure in Gestione API di Azure

Questo articolo descrive come creare un'identità del servizio gestito per un'istanza del servizio Gestione API e come accedere ad altre risorse. Un'identità del servizio gestito generata da Azure Active Directory (Azure AD) consente all'istanza di Gestione API di accedere con facilità e sicurezza ad altre risorse protette da Azure AD, ad esempio Azure Key Vault. L'identità del servizio gestito viene gestita da Azure e non è necessario eseguire il provisioning o ruotare il segreto. Per altre informazioni sull'identità del servizio gestito di Azure, vedere [Identità del servizio gestito per le risorse di Azure](../active-directory/msi-overview.md).

## <a name="create-a-managed-service-identity-for-an-api-management-instance"></a>Creare un'identità del servizio gestita per un'istanza di Gestione API

### <a name="using-the-azure-portal"></a>Uso del portale di Azure

Per impostare un'identità del servizio gestita nel portale, è prima necessario creare un'istanza di Gestione API come di consueto e quindi abilitare la funzionalità.

1. Creare un'istanza di Gestione API nel portale come di consueto. Accedervi nel portale.
2. Selezionare **Managed service identity** (Identità servizio gestito).
3. Impostare Registra con Azure Active Directory su ON. Fare clic su Save.

![Abilitare l'identità del servizio gestita](./media/api-management-msi/enable-msi.png)

### <a name="using-the-azure-resource-manager-template"></a>Uso del modello di Azure Resource Manager

È possibile creare un'istanza di Gestione API con un'identità includendo la proprietà seguente nella definizione della risorsa: 

```json
"identity" : {
    "type" : "SystemAssigned"
}
```

Questa proprietà indica ad Azure di creare e gestire l'identità per l'istanza di Gestione API. 

Ad esempio, un modello completo di Azure Resource Manager può essere simile al seguente:

```json
{
    "$schema": "http://schema.management.azure.com/schemas/2014-04-01-preview/deploymentTemplate.json#",
    "contentVersion": "0.9.0.0"
    },
    "resources": [
        {
            "apiVersion": "2017-03-01",
            "name": "contoso",
            "type": "Microsoft.ApiManagement/service",
            "location": "[resourceGroup().location]",
            "tags": {},
            "sku": {
                "name": "Developer",
                "capacity": "1"
            },
            "properties": {
                "publisherEmail": "admin@contoso.com",
                "publisherName": "Contoso"
            },
            "identity": { 
                "type": "systemAssigned" 
            }
        }
    ]
}
```
## <a name="use-the-managed-service-identity-to-access-other-resources"></a>Usare l'identità del servizio gestita per accedere ad altre risorse

> [!NOTE]
> Attualmente l'identità del servizio gestita può essere usata per ottenere i certificati da Azure Key Vault per i nomi di dominio personalizzati di Gestione API. Altri scenari saranno supportati a breve.
> 
>


### <a name="obtain-a-certificate-from-azure-key-vault"></a>Ottenere un certificato da Azure Key Vault

#### <a name="prerequisites"></a>prerequisiti
1. L'istanza di Key Vault contenente il certificato PFX deve trovarsi nella stessa sottoscrizione di Azure e nello stesso gruppo di risorse del servizio Gestione API. Si tratta di un requisito del modello di Azure Resource Manager. 
2. Il contenuto del segreto deve essere di tipo *application/x-pkcs12*. Per caricare il certificato è possibile usare lo script seguente:

```powershell
$pfxFilePath = "PFX_CERTIFICATE_FILE_PATH" # Change this path 
$pwd = "PFX_CERTIFICATE_PASSWORD" # Change this password 
$flag = [System.Security.Cryptography.X509Certificates.X509KeyStorageFlags]::Exportable 
$collection = New-Object System.Security.Cryptography.X509Certificates.X509Certificate2Collection 
$collection.Import($pfxFilePath, $pwd, $flag) 
$pkcs12ContentType = [System.Security.Cryptography.X509Certificates.X509ContentType]::Pkcs12 
$clearBytes = $collection.Export($pkcs12ContentType) 
$fileContentEncoded = [System.Convert]::ToBase64String($clearBytes) 
$secret = ConvertTo-SecureString -String $fileContentEncoded -AsPlainText –Force 
$secretContentType = 'application/x-pkcs12' 
Set-AzureKeyVaultSecret -VaultName KEY_VAULT_NAME -Name KEY_VAULT_SECRET_NAME -SecretValue $Secret -ContentType $secretContentType
```

> [!Important]
> Se non viene fornita la versione dell'oggetto del certificato, Gestione API otterrà automaticamente la versione più recente del certificato dopo il caricamento in Azure Key Vault. 

L'esempio seguente mostra un modello di Azure Resource Manager che contiene i passaggi seguenti:

1. Creare un'istanza di Gestione API con un'identità del servizio gestita.
2. Aggiornare i criteri di accesso dell'istanza di Azure Key Vault e consentire all'istanza di Gestione API di ottenere i segreti da essa.
3. Aggiornare l'istanza di Gestione API impostando un nome di dominio personalizzato tramite un certificato ottenuto dall'istanza di Key Vault.

```json
{
    "$schema": "http://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "publisherEmail": {
            "type": "string",
            "minLength": 1,
            "metadata": {
                "description": "The email address of the owner of the service"
            }
        },
        "publisherName": {
            "type": "string",
            "defaultValue": "Contoso",
            "minLength": 1,
            "metadata": {
                "description": "The name of the owner of the service"
            }
        },
        "sku": {
            "type": "string",
            "allowedValues": ["Developer",
            "Standard",
            "Premium"],
            "defaultValue": "Developer",
            "metadata": {
                "description": "The pricing tier of this API Management service"
            }
        },
        "skuCount": {
            "type": "int",
            "defaultValue": 1,
            "metadata": {
                "description": "The instance size of this API Management service."
            }
        },
        "keyVaultName": {
            "type": "string",
            "metadata": {
                "description": "Name of the vault"
            }
        },
        "proxyCustomHostname1": {
            "type": "string",
            "metadata": {
                "description": "Proxy Custom hostname."
            }
        },
        "keyVaultIdToCertificate": {
            "type": "string",
            "metadata": {
                "description": "Reference to the KeyVault certificate."
            }
        }
    },
    "variables": {
        "apiManagementServiceName": "[concat('apiservice', uniqueString(resourceGroup().id))]",
        "apimServiceIdentityResourceId": "[concat(resourceId('Microsoft.ApiManagement/service', variables('apiManagementServiceName')),'/providers/Microsoft.ManagedIdentity/Identities/default')]"
    },
    "resources": [{
        "apiVersion": "2017-03-01",
        "name": "[variables('apiManagementServiceName')]",
        "type": "Microsoft.ApiManagement/service",
        "location": "[resourceGroup().location]",
        "tags": {
            
        },
        "sku": {
            "name": "[parameters('sku')]",
            "capacity": "[parameters('skuCount')]"
        },
        "properties": {
            "publisherEmail": "[parameters('publisherEmail')]",
            "publisherName": "[parameters('publisherName')]"
        },
        "identity": {
            "type": "systemAssigned"
        }
    },
    {
        "type": "Microsoft.KeyVault/vaults/accessPolicies",
        "name": "[concat(parameters('keyVaultName'), '/add')]",
        "apiVersion": "2015-06-01",        
      "dependsOn": [
        "[resourceId('Microsoft.ApiManagement/service', variables('apiManagementServiceName'))]"
      ],
        "properties": {
            "accessPolicies": [{
                "tenantId": "[reference(variables('apimServiceIdentityResourceId'), '2015-08-31-PREVIEW').tenantId]",
                "objectId": "[reference(variables('apimServiceIdentityResourceId'), '2015-08-31-PREVIEW').principalId]",
                "permissions": {
                    "secrets": ["get"]
                }
            }]
        }
    },
    { 
      "apiVersion": "2017-05-10", 
      "name": "apimWithKeyVault", 
      "type": "Microsoft.Resources/deployments",
      "dependsOn": [
        "[resourceId('Microsoft.ApiManagement/service', variables('apiManagementServiceName'))]"
      ],
      "properties": { 
        "mode": "incremental", 
        "templateLink": {
          "uri": "https://raw.githubusercontent.com/solankisamir/arm-templates/master/basicapim.keyvault.json",
          "contentVersion": "1.0.0.0"
        }, 
        "parameters": {
            "publisherEmail": { "value": "[parameters('publisherEmail')]"},
            "publisherName": { "value": "[parameters('publisherName')]"},
            "sku": { "value": "[parameters('sku')]"},
            "skuCount": { "value": "[parameters('skuCount')]"},
            "proxyCustomHostname1": {"value" : "[parameters('proxyCustomHostname1')]"},
            "keyVaultIdToCertificate": {"value" : "[parameters('keyVaultIdToCertificate')]"}
        }
      } 
    }]
}
```

## <a name="next-steps"></a>Passaggi successivi

Altre informazioni sull'identità del servizio gestito di Azure:

* [Identità del servizio gestito per le risorse di Azure](../active-directory/msi-overview.md)
* [Modelli di Gestione risorse di Azure](https://github.com/Azure/azure-quickstart-templates)

