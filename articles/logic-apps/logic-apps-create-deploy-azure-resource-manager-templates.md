---
title: Creare app per la logica con modelli di Azure Resource Manager - App per la logica di Azure| Microsoft Docs
description: Creare e distribuire flussi di lavoro delle app per la logica con i modelli di Azure Resource Manager in App per la logica di Azure
services: logic-apps
ms.service: logic-apps
ms.suite: integration
author: ecfan
ms.author: estfan
ms.reviewer: klam, LADocs
ms.topic: article
ms.assetid: 7574cc7c-e5a1-4b7c-97f6-0cffb1a5d536
ms.date: 10/15/2017
ms.openlocfilehash: 70af92c2afd450d357bf9f30187ef200334698ba
ms.sourcegitcommit: 2ad510772e28f5eddd15ba265746c368356244ae
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 08/28/2018
ms.locfileid: "43124718"
---
# <a name="create-and-deploy-logic-apps-with-azure-resource-manager-templates"></a>Creare e distribuire app con i modelli di Azure Resource Manager

App per la logica di Azure offre modelli di Azure Resource Manager che è possibile usare non solo per creare app per la logica per automatizzare i flussi di lavoro, ma anche per definire le risorse e i parametri usati per la distribuzione. È possibile usare questo modello per i propri scenari aziendali o personalizzarlo in base alle esigenze. Sono disponibili altre informazioni sul [modello di Resource Manager per le app per la logica](https://github.com/Azure/azure-quickstart-templates/blob/master/101-logic-app-create/azuredeploy.json) e sulla [struttura e la sintassi del modello di Azure Resource Manager](../azure-resource-manager/resource-group-authoring-templates.md).

## <a name="define-the-logic-app"></a>Definire l'app per la logica

Questo esempio di definizione di app per la logica viene eseguito ogni ora ed effettua il ping del percorso specificato nel parametro `testUri`.
Il modello usa i valori del parametro per il nome dell'app per la logica (```logicAppName```) e il percorso in cui effettuare il ping per il test (```testUri```). Altre informazioni sulla [definizione di questi parametri nel modello](#define-parameters). Il modello imposta inoltre il percorso dell'app per la logica sullo stesso percorso del gruppo di risorse di Azure. 

``` json
{
   "type": "Microsoft.Logic/workflows",
   "apiVersion": "2016-06-01",
   "name": "[parameters('logicAppName')]",
   "location": "[resourceGroup().location]",
   "tags": {
      "displayName": "LogicApp"
   },
   "properties": {
      "definition": {
         "$schema": "https://schema.management.azure.com/schemas/2016-06-01/Microsoft.Logic.json",
         "contentVersion": "1.0.0.0",
         "parameters": {
            "testURI": {
               "type": "string",
               "defaultValue": "[parameters('testUri')]"
            }
         },
         "triggers": {
            "Recurrence": {
               "type": "Recurrence",
               "recurrence": {
                  "frequency": "Hour",
                  "interval": 1
               }
            }
         },
         "actions": {
            "Http": {
              "type": "Http",
              "inputs": {
                  "method": "GET",
                  "uri": "@parameters('testUri')"
              },
              "runAfter": {}
           }
         },
         "outputs": {}
      },
      "parameters": {}
   }
}
``` 

<a name="define-parameters"></a>

### <a name="define-parameters"></a>Definire i parametri

[!INCLUDE [app-service-logic-deploy-parameters](../../includes/app-service-logic-deploy-parameters.md)]

Di seguito sono riportate le descrizioni dei parametri disponibili nel modello:

| Parametro | DESCRIZIONE | Esempio di definizione JSON | 
| --------- | ----------- | ----------------------- | 
| `logicAppName` | Definisce il nome dell'app per la logica creata dal modello. | "logicAppName": { "type": "string", "metadata": { "description": "myExampleLogicAppName" } } |
| `testUri` | Definisce il percorso in cui effettuare il ping per il test. | "testUri": { "type": "string", "defaultValue": "http://azure.microsoft.com/status/feed/"} | 
||||

Altre informazioni sull'[API REST per la definizione e le proprietà del flusso di lavoro delle app per la logica](https://docs.microsoft.com/rest/api/logic/workflows) e sulla [creazione di definizioni di app per la logica con JSON](logic-apps-author-definitions.md).

## <a name="deploy-logic-apps-automatically"></a>Distribuire automaticamente le app per la logica

Per creare e distribuire automaticamente un'app per la logica in Azure, scegliere **Distribuisci in Azure** qui:

[![Distribuzione in Azure](./media/logic-apps-create-deploy-azure-resource-manager-templates/deploybutton.png)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F101-logic-app-create%2Fazuredeploy.json)

Con questa azione si accede al portale di Azure in cui è possibile inserire i dettagli dell'app per la logica e apportare modifiche al modello o ai parametri. Ad esempio, il portale di Azure richiede questi dettagli:

* Nome della sottoscrizione di Azure
* Gruppo di risorse da usare
* Percorso dell'app per la logica
* Un nome per l'app per la logica
* Un URI di test
* Accettazione dei termini e delle condizioni specificati

## <a name="deploy-logic-apps-with-commands"></a>Distribuire le app per la logica con i comandi

[!INCLUDE [app-service-deploy-commands](../../includes/app-service-deploy-commands.md)]

### <a name="powershell"></a>PowerShell

```
New-AzureRmResourceGroupDeployment -TemplateUri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/101-logic-app-create/azuredeploy.json -ResourceGroupName ExampleDeployGroup
``` 

### <a name="azure-cli"></a>Interfaccia della riga di comando di Azure

```
azure group deployment create --template-uri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/101-logic-app-create/azuredeploy.json -g ExampleDeployGroup
```

## <a name="get-support"></a>Supporto

* In caso di domande, visitare il [forum di App per la logica di Azure](https://social.msdn.microsoft.com/Forums/en-US/home?forum=azurelogicapps).
* Per votare o inviare idee relative alle funzionalità, visitare il [sito dei commenti e suggerimenti degli utenti di App per la logica](http://aka.ms/logicapps-wish).

## <a name="next-steps"></a>Passaggi successivi

> [!div class="nextstepaction"]
> [Monitorare le app per la logica](../logic-apps/logic-apps-monitor-your-logic-apps.md)