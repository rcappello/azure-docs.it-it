---
title: Esempi dell'interfaccia della riga di comando di Azure - Creare un set di scalabilità di macchine virtuali | Microsoft Docs
description: Esempi dell'interfaccia della riga di comando di Azure
services: virtual-machine-scale-sets
documentationcenter: ''
author: zr-msft
manager: jeconnoc
editor: ''
tags: azure-resource-manager
ms.assetid: ''
ms.service: virtual-machine-scale-sets
ms.devlang: azurecli
ms.topic: sample
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 03/27/2018
ms.author: zarhoads
ms.custom: mvc
ms.openlocfilehash: 98617b2823cb4b17bf65621f302a0ea63ebda5fa
ms.sourcegitcommit: 62759a225d8fe1872b60ab0441d1c7ac809f9102
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 10/19/2018
ms.locfileid: "49468144"
---
# <a name="create-a-virtual-machine-scale-set-with-the-azure-cli"></a>Creare un set di scalabilità di macchine virtuali con l'interfaccia della riga di comando di Azure
Questo script crea un set di scalabilità di macchine virtuali di Azure con sistema operativo Ubuntu e le relative risorse di rete, incluso un servizio di bilanciamento del carico. Dopo aver eseguito lo script, è possibile accedere alle istanze di macchina virtuale tramite SSH.

[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a>Script di esempio
[!code-azurecli-interactive[main](../../../cli_scripts/virtual-machine-scale-sets/simple-scale-set/simple-scale-set.sh "Create a simple virtual machine scale set")]

## <a name="clean-up-deployment"></a>Pulire la distribuzione
Eseguire questo comando per rimuovere il gruppo di risorse, il set di scalabilità e tutte le risorse correlate.

```azurecli-interactive
az group delete --name myResourceGroup
```

## <a name="script-explanation"></a>Spiegazione dello script
Questo script usa i comandi seguenti per creare un gruppo di risorse, il set di scalabilità di macchine virtuali e tutte le risorse correlate. Ogni comando della tabella include collegamenti alla documentazione specifica del comando.

| Comando | Note |
|---|---|
| [az group create](/cli/azure/ad/group#az_ad_group_create) | Consente di creare un gruppo di risorse in cui sono archiviate tutte le risorse. |
| [az vmss create](/cli/azure/vmss#az_vmss_create) | Crea il set di scalabilità di macchine virtuali e lo connette alla rete virtuale, alla subnet e al gruppo di sicurezza di rete. Per distribuire il traffico a più istanze di macchina virtuale, viene anche creato un servizio di bilanciamento del carico. Questo comando specifica anche l'immagine della macchina virtuale da usare e le credenziali di amministrazione.  |
| [az group delete](/cli/azure/ad/group#delete) | Consente di eliminare un gruppo di risorse incluse tutte le risorse annidate. |

## <a name="next-steps"></a>Passaggi successivi
Per altre informazioni sull'interfaccia della riga di comando di Azure, vedere la [documentazione sull'interfaccia della riga di comando di Azure](https://docs.microsoft.com/cli/azure/overview).

Altri esempi di script dell'interfaccia della riga di comando di Azure per i set di scalabilità di macchine virtuali sono disponibili nella [documentazione dei set di scalabilità di macchine virtuali di Azure](../cli-samples.md).