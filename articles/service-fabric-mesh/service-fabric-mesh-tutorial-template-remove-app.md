---
title: Esercitazione - Rimuovere un'app in esecuzione in Azure Service Fabric Mesh | Microsoft Docs
description: In questa esercitazione si apprenderà come rimuovere un'applicazione in esecuzione in Service Fabric Mesh e come eliminare le relative risorse.
services: service-fabric-mesh
documentationcenter: .net
author: rwike77
manager: jeconnoc
editor: ''
ms.assetid: ''
ms.service: service-fabric-mesh
ms.devlang: dotNet
ms.topic: tutorial
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 09/15/2018
ms.author: ryanwi
ms.custom: mvc, devcenter
ms.openlocfilehash: f366413ae5f758601dfebc2a29ff848feb756083
ms.sourcegitcommit: 32d218f5bd74f1cd106f4248115985df631d0a8c
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 09/24/2018
ms.locfileid: "46960431"
---
# <a name="tutorial-remove-an-application-and-resources"></a>Esercitazione: Rimuovere un'applicazione e le relative risorse

Questa è la quarta di una serie di esercitazioni. Si apprenderà come rimuovere un'applicazione in esecuzione [precedentemente distribuita in Service Fabric Mesh](service-fabric-mesh-tutorial-template-deploy-app.md). 

Nella quarta parte della serie si apprenderà come:

> [!div class="checklist"]
> * Eliminare un'app in esecuzione in Service Fabric Mesh
> * Eliminare le risorse dell'applicazione

In questa serie di esercitazioni si apprenderà come:
> [!div class="checklist"]
> * [Distribuire un'applicazione in Service Fabric Mesh usando un modello](service-fabric-mesh-tutorial-template-deploy-app.md)
> * [Ridimensionare un'applicazione in esecuzione in Service Fabric Mesh](service-fabric-mesh-tutorial-template-scale-services.md)
> * [Aggiornare un'applicazione in esecuzione in Service Fabric Mesh](service-fabric-mesh-tutorial-template-upgrade-app.md)
> * Rimuovere un'applicazione

[!INCLUDE [preview note](./includes/include-preview-note.md)]

## <a name="prerequisites"></a>Prerequisiti

Prima di iniziare questa esercitazione:

* Se non si ha una sottoscrizione di Azure, è possibile creare un [account gratuito](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) prima di iniziare.

* Aprire [Azure Cloud Shell](service-fabric-mesh-howto-setup-cli.md) o [installare l'interfaccia della riga di comando di Azure CLI e l'interfaccia della riga di comando di Service Fabric Mesh in locale](service-fabric-mesh-howto-setup-cli.md#install-the-service-fabric-mesh-cli-locally).

## <a name="delete-the-resource-group-and-all-the-resources"></a>Eliminare il gruppo di risorse e tutte le relative risorse

Quando tutte le risorse create non sono più necessarie, eliminarle. In precedenza, è stato [creato un nuovo gruppo di risorse](service-fabric-mesh-tutorial-template-deploy-app.md#create-a-container-registry) per ospitare l'istanza di Registro contenitori di Azure e le risorse dell'applicazione Service Fabric Mesh.  È possibile eliminare questo gruppo di risorse. Con questa operazione vengono eliminate tutte le risorse associate.

```azurecli
az group delete --resource-group myResourceGroup
```

```powershell
Remove-AzureRmResourceGroup -Name myResourceGroup
```

## <a name="individually-delete-the-resources"></a>Eliminare le risorse singolarmente
È anche possibile eliminare l'istanza di Registro contenitori di Azure, l'applicazione Service Fabric Mesh e le risorse di rete singolarmente.

Per eliminare l'istanza di Registro contenitori di Azure:

```azurecli
az acr delete --resource-group myResourceGroup --name myContainerRegistry
```

Per eliminare l'applicazione Service Fabric Mesh:

```azurecli
az mesh app delete --resource-group myResourceGroup --name todolistapp
```

Per eliminare la rete:
```azurecli
az mesh network delete --resource-group myResourceGroup --name todolistappNetwork
```

## <a name="next-steps"></a>Passaggi successivi

In questa parte dell'esercitazione si è appreso come:

> [!div class="checklist"]
> * Eliminare un'app in esecuzione in Service Fabric Mesh
> * Eliminare le risorse dell'applicazione