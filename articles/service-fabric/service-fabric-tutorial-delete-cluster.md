---
title: Eliminare un cluster di Service Fabric in Azure | Microsoft Docs
description: In questa esercitazione si apprenderà come eliminare un cluster di Service Fabric ospitato in Azure e tutte le risorse che contiene. È possibile eliminare il gruppo di risorse che contiene il cluster o eliminare le risorse in modo selettivo.
services: service-fabric
documentationcenter: .net
author: rwike77
manager: timlt
editor: ''
ms.assetid: ''
ms.service: service-fabric
ms.devlang: dotNet
ms.topic: tutorial
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 09/26/2018
ms.author: ryanwi
ms.custom: mvc
ms.openlocfilehash: 70c5fa5de627b69623b1cce6929615f4e99e2a05
ms.sourcegitcommit: b7e5bbbabc21df9fe93b4c18cc825920a0ab6fab
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 09/27/2018
ms.locfileid: "47410822"
---
# <a name="tutorial-remove-a-service-fabric-cluster-running-in-azure"></a>Esercitazione: Rimuovere un cluster di Service Fabric in esecuzione in Azure

Questa esercitazione è la quarta di una serie e illustra come eliminare un cluster di Service Fabric in esecuzione in Azure. Per eliminare completamente un cluster di Service Fabric, è necessario eliminare anche le risorse usate dal cluster. Sono disponibili due opzioni: eliminare il gruppo di risorse che contiene il cluster (in modo da rimuovere la risorsa cluster e le altre risorse del gruppo) oppure eliminare la specifica risorsa cluster e le risorse associate (ma non le altre risorse del gruppo).

In questa esercitazione si apprenderà come:

> [!div class="checklist"]
> * Eliminare un gruppo di risorse e tutte le risorse che contiene
> * Eliminare risorse da un gruppo di risorse in modo selettivo

In questa serie di esercitazioni si apprenderà come:
> [!div class="checklist"]
> * Creare [un cluster di Windows](service-fabric-tutorial-create-vnet-and-windows-cluster.md) o un [cluster di Linux](service-fabric-tutorial-create-vnet-and-linux-cluster.md) protetto in Azure usando un modello
> * [Aumentare o ridurre un cluster](service-fabric-tutorial-scale-cluster.md)
> * [Aggiornare il runtime di un cluster](service-fabric-tutorial-upgrade-cluster.md)
> * Eliminazione di un cluster

## <a name="prerequisites"></a>Prerequisiti

Prima di iniziare questa esercitazione:

* Se non si ha una sottoscrizione di Azure, creare un [account gratuito](https://azure.microsoft.com/free/?WT.mc_id=A261C142F)
* Installare il [modulo Azure PowerShell 4.1 o versioni successive](https://docs.microsoft.com/powershell/azure/install-azurerm-ps) o [l'interfaccia della riga di comando di Azure](/cli/azure/install-azure-cli).
* Creare [un cluster di Windows](service-fabric-tutorial-create-vnet-and-windows-cluster.md) o un [cluster di Linux](service-fabric-tutorial-create-vnet-and-linux-cluster.md) protetto in Azure

## <a name="delete-the-resource-group-containing-the-service-fabric-cluster"></a>Eliminare il gruppo di risorse che contiene il cluster di Service Fabric
Il modo più semplice per eliminare il cluster e tutte le risorse che utilizza consiste nell'eliminare il gruppo di risorse.

Accedere ad Azure e selezionare l'ID della sottoscrizione da usare per rimuovere il cluster.  È possibile trovare l'ID della sottoscrizione accedendo al [portale di Azure](http://portal.azure.com). Eliminare il gruppo di risorse e tutte le risorse cluster usando il cmdlet [Remove-AzureRmResourceGroup](/powershell/module/azurerm.resources/remove-azurermresourcegroup) o il comando [az group delete](/cli/azure/group?view=azure-cli-latest#az_group_delete).

```powershell
Connect-AzureRmAccount
Set-AzureRmContext -SubscriptionId <guid>
$groupname = "sfclustertutorialgroup"
Remove-AzureRmResourceGroup -Name $groupname -Force
```

```azurecli
az login
az account set --subscription <guid>
ResourceGroupName="sfclustertutorialgroup"
az group delete --name $ResourceGroupName
```

## <a name="selectively-delete-the-cluster-resource-and-the-associated-resources"></a>Eliminare la risorsa cluster e le risorse associate in modo selettivo
Se nel gruppo sono incluse solo le risorse correlate al cluster Service Fabric da eliminare, è più semplice eliminare l'intero gruppo di risorse. Se si vogliono eliminare le risorse del gruppo di risorse in modo selettivo, mantenendo le risorse non associate al cluster, seguire questa procedura.

Elencare le risorse nel gruppo di risorse:

```powershell
Connect-AzureRmAccount
Set-AzureRmContext -SubscriptionId <guid>
$groupname = "sfclustertutorialgroup"
Get-AzureRmResource -ResourceGroupName $groupname | ft
```

```azurecli
az login
az account set --subscription <guid>
ResourceGroupName="sfclustertutorialgroup"
az resource list --resource-group $ResourceGroupName
```

Per ogni risorsa da eliminare, eseguire lo script seguente:

```powershell
Remove-AzureRmResource -ResourceName "<name of the Resource>" -ResourceType "<Resource Type>" -ResourceGroupName $groupname -Force
```

```azurecli
az resource delete --name "<name of the Resource>" --resource-type "<Resource Type>" --resource-group $ResourceGroupName
```

Per eliminare la risorsa cluster, eseguire lo script seguente:

```powershell
Remove-AzureRmResource -ResourceName "<name of the Resource>" -ResourceType "Microsoft.ServiceFabric/clusters" -ResourceGroupName $groupname -Force
```

```azurecli
az resource delete --name "<name of the Resource>" --resource-type "Microsoft.ServiceFabric/clusters" --resource-group $ResourceGroupName
```

## <a name="next-steps"></a>Passaggi successivi

Questa esercitazione illustra come:

> [!div class="checklist"]
> * Eliminare un gruppo di risorse e tutte le risorse che contiene
> * Eliminare risorse da un gruppo di risorse in modo selettivo

Una volta completata questa esercitazione, è possibile continuare con il percorso seguente:
* Informazioni su come esaminare e gestire un cluster di Service Fabric con [Service Fabric Explorer](service-fabric-visualizing-your-cluster.md).
* Informazioni su come [applicare patch al sistema operativo Windows](service-fabric-patch-orchestration-application.md) o [applicare patch al sistema operativo Linux](service-fabric-patch-orchestration-application-linux.md) dei nodi del cluster.
* Informazioni su come aggregare e raccogliere eventi per i [cluster di Windows](service-fabric-diagnostics-event-aggregation-wad.md) o i [cluster di Linux](service-fabric-diagnostics-event-aggregation-lad.md) e su come [configurare Log Analytics](service-fabric-diagnostics-oms-setup.md) per monitorare gli eventi dei cluster.