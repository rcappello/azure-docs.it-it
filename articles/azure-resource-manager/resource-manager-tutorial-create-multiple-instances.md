---
title: Creare più istanze di risorse tramite Azure Resource Manager | Microsoft Docs
description: Informazioni su come creare un modello di Azure Resource Manager per creare più istanze di risorse di Azure.
services: azure-resource-manager
documentationcenter: ''
author: mumian
manager: dougeby
editor: tysonn
ms.service: azure-resource-manager
ms.workload: multiple
ms.tgt_pltfrm: na
ms.devlang: na
ms.date: 09/10/2018
ms.topic: tutorial
ms.author: jgao
ms.openlocfilehash: 63a18a6ae0ee4c6e0a01bd7ac4a26a4fb89746c2
ms.sourcegitcommit: 3150596c9d4a53d3650cc9254c107871ae0aab88
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 09/28/2018
ms.locfileid: "47419489"
---
# <a name="tutorial-create-multiple-resource-instances-using-resource-manager-templates"></a>Esercitazione: Creare più istanze della risorsa usando i modelli di Resource Manager

Informazioni su come eseguire un'iterazione del modello di Gestione risorse di Azure per creare più istanze di una risorsa di Azure. Nell'ultima esercitazione, è stato modificato un modello esistente per creare un account di archiviazione di Azure crittografato. In questa esercitazione, si modifica lo stesso modello per creare tre istanze di account di archiviazione.

> [!div class="checklist"]
> * Aprire un modello di avvio rapido
> * Modificare il modello
> * Distribuire il modello

Se non si ha una sottoscrizione di Azure, [creare un account gratuito](https://azure.microsoft.com/free/) prima di iniziare.

## <a name="prerequisites"></a>Prerequisiti

Per completare l'esercitazione di questo articolo, sono necessari gli elementi seguenti:

* [Visual Studio Code](https://code.visualstudio.com/).
* Estensione Strumenti di Azure Resource Manager. Per eseguire l'installazione, vedere [Installare l'estensione Strumenti di Azure Resource Manager](./resource-manager-quickstart-create-templates-use-visual-studio-code.md#prerequisites).

## <a name="open-a-quickstart-template"></a>Aprire un modello di avvio rapido

Il modello usato in questa guida introduttiva è denominato [Create a standard storage account](https://azure.microsoft.com/resources/templates/101-storage-account-create/) (Creare un account di archiviazione Standard). Il modello definisce una risorsa account di archiviazione di Azure.

1. In Visual Studio Code selezionare **File**>**Apri file**.
2. In **Nome file** incollare l'URL seguente:

    ```url
    https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/101-storage-account-create/azuredeploy.json
    ```
3. Selezionare **Apri** per aprire il file.
4. Selezionare **File**>**Salva con nome** per salvare il file con il nome **azuredeploy.json** nel computer locale.

## <a name="edit-the-template"></a>Modificare il modello

L'obiettivo di questa esercitazione consiste nell'usare un'iterazione di risorse per creare tre account di archiviazione.  Il modello di esempio crea solo un account di archiviazione. 

Da Visual Studio Code, apportare le quattro modifiche seguenti:

![Azure Resource Manager crea più istanze](./media/resource-manager-tutorial-create-multiple-instances/resource-manager-template-create-multiple-instances.png)

1. Aggiungere un elemento `copy` alla definizione di risorsa dell'account di archiviazione. Nell'elemento copy si specifica il numero di iterazioni e un nome per questo ciclo. Il valore del conteggio deve essere un numero intero positivo e non può essere maggiore di 800.
2. La funzione `copyIndex()` restituisce l'iterazione attuale nel ciclo. `copyIndex()` è in base zero. Per eseguire l'offset del valore di indice, è possibile passare un valore nella funzione copyIndex(). Ad esempio, *copyIndex(1)*.
3. Eliminare l'elemento **variabili**, in quanto non è più usato.
4. Eliminare l'elemento **output**.

Il modello completato è simile a:

```json
{
  "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
  "contentVersion": "1.0.0.0",
  "parameters": {
    "storageAccountType": {
      "type": "string",
      "defaultValue": "Standard_LRS",
      "allowedValues": [
        "Standard_LRS",
        "Standard_GRS",
        "Standard_ZRS",
        "Premium_LRS"
      ],
      "metadata": {
        "description": "Storage Account type"
      }
    },
    "location": {
      "type": "string",
      "defaultValue": "[resourceGroup().location]",
      "metadata": {
        "description": "Location for all resources."
      }
    }
  },
  "resources": [
    {
      "type": "Microsoft.Storage/storageAccounts",
      "name": "[concat(copyIndex(),'storage', uniqueString(resourceGroup().id))]",
      "apiVersion": "2018-02-01",
      "location": "[parameters('location')]",
      "sku": {
        "name": "[parameters('storageAccountType')]"
      },
      "kind": "Storage",
      "properties": {},
      "copy": {
        "name": "storagecopy",
        "count": 3
      }
    }
  ]
}
```

Per altre informazioni sulla creazione di più istanze, vedere [Distribuire più istanze di una risorsa o proprietà nei modelli di Azure Resource Manager](./resource-group-create-multiple.md).

## <a name="deploy-the-template"></a>Distribuire il modello

Vedere la sezione [Distribuire il modello](./resource-manager-quickstart-create-templates-use-visual-studio-code.md#deploy-the-template) della guida introduttiva di Visual Studio Code per la procedura di distribuzione.

Per elencare tutti e tre gli account di archiviazione, omettere il --parametro nome:

# <a name="clitabcli"></a>[Interfaccia della riga di comando](#tab/CLI)
```cli
az storage account list --resource-group <ResourceGroupName>
```

# <a name="powershelltabpowershell"></a>[PowerShell](#tab/PowerShell)

```powershell
Get-AzureRmStorageAccount -ResourceGroupName <ResourceGroupName>
```

---

Confrontare i nomi degli account di archiviazione con la definizione del nome nel modello.

## <a name="clean-up-resources"></a>Pulire le risorse

Quando non sono più necessarie, eseguire la pulizia delle risorse di Azure distribuite eliminando il gruppo di risorse.

1. Nel portale di Azure selezionare **Gruppo di risorse** nel menu a sinistra.
2. Immettere il nome del gruppo di risorse nel campo **Filtra per nome**.
3. Selezionare il nome del gruppo di risorse.  Nel gruppo di risorse verranno visualizzate in totale sei risorse.
4. Selezionare **Elimina gruppo di risorse** nel menu in alto.

## <a name="next-steps"></a>Passaggi successivi

In questa esercitazione è stato descritto come creare più istanze dell'account di archiviazione. Finora è stato creato un account di archiviazione o più istanze dell'account di archiviazione. Nell'esercitazione successiva verrà sviluppato un modello con più risorse e più tipi di risorse. alcune con risorse dipendenti.

> [!div class="nextstepaction"]
> [Creare le risorse dipendenti](./resource-manager-tutorial-create-templates-with-dependent-resources.md)
