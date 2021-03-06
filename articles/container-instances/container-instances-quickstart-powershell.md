---
title: "Guida introduttiva: eseguire un'applicazione in Istanze di contenitore di Azure"
description: In questa guida introduttiva si userà Azure PowerShell per distribuire un'applicazione in esecuzione in un contenitore Docker in Istanze di contenitore di Azure
services: container-instances
author: dlepow
ms.service: container-instances
ms.topic: quickstart
ms.date: 10/02/2018
ms.author: danlep
ms.custom: mvc
ms.openlocfilehash: 33444e810a2deebee11e535c73ce3e249f42b340
ms.sourcegitcommit: 67abaa44871ab98770b22b29d899ff2f396bdae3
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 10/08/2018
ms.locfileid: "48854644"
---
# <a name="quickstart-run-an-application-in-azure-container-instances"></a>Guida introduttiva: eseguire un'applicazione in Istanze di contenitore di Azure

Le Istanze di contenitore di Azure consentono di eseguire i contenitori Docker in Azure in modo semplice e rapido, senza la necessità di distribuire macchine virtuali o usare una piattaforma di orchestrazione di contenitori completa come Kubernetes. In questa guida introduttiva viene usato il portale di Azure per creare un contenitore Windows in Azure e renderne disponibile l'applicazione con un nome di dominio completo (FQDN). Pochi secondi dopo aver eseguito un comando di distribuzione singola, è possibile passare all'applicazione in esecuzione:

![App distribuita in Istanze di contenitore di Azure visualizzata nel browser][qs-powershell-01]

Se non si ha una sottoscrizione di Azure, creare un [account gratuito](https://azure.microsoft.com/free/) prima di iniziare.

[!INCLUDE [cloud-shell-powershell.md](../../includes/cloud-shell-powershell.md)]

Se si sceglie di installare e usare PowerShell in locale, per questa esercitazione è necessario il modulo Azure PowerShell versione 5.5 o successiva. Eseguire `Get-Module -ListAvailable AzureRM` per trovare la versione. Se è necessario eseguire l'aggiornamento, vedere [Installare e configurare Azure PowerShell](/powershell/azure/install-azurerm-ps). Se si esegue PowerShell in locale, è anche necessario eseguire `Connect-AzureRmAccount` per creare una connessione con Azure.

## <a name="create-a-resource-group"></a>Creare un gruppo di risorse

Le Istanze di contenitore di Azure, analogamente a tutte le risorse di Azure, devono essere distribuite in un gruppo di risorse. I gruppi di risorse consentono di organizzare e gestire le risorse di Azure correlate.

Per iniziare, creare un gruppo di risorse denominato *myResourceGroup* nell'area *eastus* con il comando [New-AzureRmResourceGroup][New-AzureRmResourceGroup] seguente:

 ```azurepowershell-interactive
New-AzureRmResourceGroup -Name myResourceGroup -Location EastUS
```

## <a name="create-a-container"></a>Creare un contenitore

Dopo aver creato il gruppo di risorse, è possibile eseguire un contenitore in Azure. Per creare un'istanza di contenitore con Azure PowerShell, specificare il nome del gruppo di risorse, il nome dell'istanza di contenitore e l'immagine del contenitore Docker con il cmdlet [New-AzureRmContainerGroup][New-AzureRmContainerGroup]. È possibile esporre i contenitori in Internet specificando una o più porte da aprire, un'etichetta del nome DNS o entrambi. In questa guida introduttiva si distribuisce un contenitore con un'etichetta del nome DNS che ospita IIS (Internet Information Services) in esecuzione in Nano Server.

Eseguire il comando seguente per avviare un'istanza di contenitore. Il valore `-DnsNameLabel` deve essere univoco all'interno dell'area di Azure in cui si crea l'istanza. Se si riceve il messaggio di errore "L'etichetta del nome DNS non è disponibile", provare con un'etichetta del nome DNS diversa.

 ```azurepowershell-interactive
New-AzureRmContainerGroup -ResourceGroupName myResourceGroup -Name mycontainer -Image microsoft/iis:nanoserver -OsType Windows -DnsNameLabel aci-demo-win
```

Entro pochi secondi si dovrebbe ricevere una risposta da Azure. Inizialmente, il valore `ProvisioningState` del contenitore è **Creazione in corso**, ma dovrebbe passare a  **	Operazione completata** entro un minuto o due. Controllare lo stato di distribuzione con il cmdlet [Get-AzureRmContainerGroup][Get-AzureRmContainerGroup]:

 ```azurepowershell-interactive
Get-AzureRmContainerGroup -ResourceGroupName myResourceGroup -Name mycontainer
```

Lo stato di provisioning, il nome di dominio completo (FQDN) e l'indirizzo IP del contenitore vengono visualizzati nell'output del cmdlet:

```console
PS Azure:\> Get-AzureRmContainerGroup -ResourceGroupName myResourceGroup -Name mycontainer


ResourceGroupName        : myResourceGroup
Id                       : /subscriptions/<Subscription ID>/resourceGroups/myResourceGroup/providers/Microsoft.ContainerInstance/containerGroups/mycontainer
Name                     : mycontainer
Type                     : Microsoft.ContainerInstance/containerGroups
Location                 : eastus
Tags                     :
ProvisioningState        : Creating
Containers               : {mycontainer}
ImageRegistryCredentials :
RestartPolicy            : Always
IpAddress                : 52.226.19.87
DnsNameLabel             : aci-demo-win
Fqdn                     : aci-demo-win.eastus.azurecontainer.io
Ports                    : {80}
OsType                   : Windows
Volumes                  :
State                    : Pending
Events                   : {}
```

Quando il valore `ProvisioningState` del contenitore è **Operazione completata**, passare al relativo indirizzo `Fqdn` nel browser. Se viene visualizzata una pagina Web simile all'immagine seguente, congratulazioni! È stata completata la distribuzione di un'applicazione in esecuzione in un contenitore Docker in Azure.

![IIS distribuito con Istanze di contenitore di Azure visualizzato nel browser][qs-powershell-01]

## <a name="clean-up-resources"></a>Pulire le risorse

Quando il contenitore non è più necessario, rimuoverlo con il cmdlet [Remove-AzureRmContainerGroup][Remove-AzureRmContainerGroup]:

 ```azurepowershell-interactive
Remove-AzureRmContainerGroup -ResourceGroupName myResourceGroup -Name mycontainer
```

## <a name="next-steps"></a>Passaggi successivi

In questa guida introduttiva è stata creata un'istanza di contenitore di Azure da un'immagine nel registro nell'hub Docker pubblico. Per provare a creare un'immagine del contenitore e a distribuirla da un registro contenitori di Azure privato, passare all'esercitazione su Istanze di contenitore di Azure.

> [!div class="nextstepaction"]
> [Esercitazione su Istanze di contenitore di Azure](./container-instances-tutorial-prepare-app.md)

<!-- IMAGES -->
[qs-powershell-01]: ./media/container-instances-quickstart-powershell/qs-powershell-01.png

<!-- LINKS -->
[New-AzureRmResourceGroup]: /powershell/module/azurerm.resources/new-azurermresourcegroup
[New-AzureRmContainerGroup]: /powershell/module/azurerm.containerinstance/new-azurermcontainergroup
[Get-AzureRmContainerGroup]: /powershell/module/azurerm.containerinstance/get-azurermcontainergroup
[Remove-AzureRmContainerGroup]: /powershell/module/azurerm.containerinstance/remove-azurermcontainergroup
