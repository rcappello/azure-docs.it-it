---
title: Usare la rete WAN virtuale di Azure per creare connessioni ExpressRoute ad ambienti Azure e locali | Microsoft Docs
description: Questa esercitazione mostra come usare la rete WAN virtuale di Azure per creare connessioni ExpressRoute ad ambienti Azure e locali.
services: virtual-wan
author: cherylmc
ms.service: virtual-wan
ms.topic: tutorial
ms.date: 10/5/2018
ms.author: cherylmc
Customer intent: As someone with a networking background, I want to connect my corporoate on-premises network(s) to my VNets using Virtual WAN and ExpressRoute.
ms.openlocfilehash: 10b73843e2ca2e0ee0af766ef1ad7ee9cbf61f94
ms.sourcegitcommit: 67abaa44871ab98770b22b29d899ff2f396bdae3
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 10/08/2018
ms.locfileid: "48854606"
---
# <a name="tutorial-create-an-expressroute-association-using-azure-virtual-wan-preview"></a>Esercitazione: Creare un'associazione ExpressRoute con la rete WAN virtuale di Azure (anteprima)

Questa esercitazione illustra come usare la rete WAN virtuale per connettersi alle risorse in Azure tramite un'associazione e un circuito ExpressRoute. Per altre informazioni sulla rete WAN virtuale, vedere la [panoramica sulla rete WAN virtuale](virtual-wan-about.md).

In questa esercitazione si apprenderà come:

> [!div class="checklist"]
> * Creare una rete WAN virtuale
> * Creare un hub
> * Trovare e associare un circuito all'hub
> * Associare il circuito a uno o più hub
> * Connettere una rete virtuale a un hub
> * Visualizzare la rete WAN virtuale
> * Visualizzare lo stato di integrità delle risorse
> * Monitorare una connessione

> [!IMPORTANT]
> L'anteprima pubblica viene messa a disposizione senza contratto di servizio e non deve essere usata per i carichi di lavoro di produzione. Alcune funzionalità potrebbero non essere supportate, potrebbero avere funzioni limitate o potrebbero non essere disponibili in tutte le località di Azure. Vedere [Condizioni supplementari per l'uso delle anteprime di Microsoft Azure](https://azure.microsoft.com/support/legal/preview-supplemental-terms/).
>

## <a name="before-you-begin"></a>Prima di iniziare

[!INCLUDE [Before you begin](../../includes/virtual-wan-tutorial-vwan-before-include.md)]

## <a name="register"></a>Registrare questa funzionalità

Prima di poter configurare la rete WAN virtuale, è necessario registrare la sottoscrizione nell'anteprima. In caso contrario, non sarà possibile utilizzare la rete WAN virtuale nel portale. Per eseguire la registrazione, inviare un messaggio di posta elettronica all'indirizzo **azurevirtualwan@microsoft.com** con l'ID della sottoscrizione. Si riceverà un messaggio di posta elettronica dopo la registrazione della sottoscrizione.

**Considerazioni sull'anteprima:**

* Disponibilità a livello di area: Stati Uniti centro-occidentali
* Il circuito ExpressRoute deve essere abilitato in un paese che supporta il servizio [Copertura globale di ExpressRoute](https://docs.microsoft.com/azure/expressroute/expressroute-faqs#where-is-expressroute-global-reach-supported)

## <a name="vnet"></a>1. Creare una rete virtuale

[!INCLUDE [Create a virtual network](../../includes/virtual-wan-tutorial-vnet-include.md)]

## <a name="openvwan"></a>2. Creare una rete WAN virtuale

In un browser passare al [portale di Azure (anteprima)](http://aka.ms/azurevirtualwanpreviewfeatures) e accedere con l'account Azure.

[!INCLUDE [Create a virtual WAN](../../includes/virtual-wan-tutorial-vwan-include.md)]

### <a name="getting-started-page"></a>Pagina introduttiva

[!INCLUDE [Create a virtual WAN](../../includes/virtual-wan-tutorial-gettingstarted-include.md)]

## <a name="hub"></a>3. Creare un hub

[!INCLUDE [Create a virtual WAN](../../includes/virtual-wan-tutorial-hub-include.md)]

## <a name="hub"></a>4. Trovare e associare un circuito all'hub

1. Selezionare la rete WAN virtuale e in **Virtual WAN Architecture** (Architettura di rete WAN virtuale) selezionare **Circuiti ExpressRoute**.
2. Se il circuito ExpressRoute è nella stessa sottoscrizione della rete WAN virtuale, fare clic su **Select ExpressRoute circuit** (Seleziona circuito ExpressRoute) nella sottoscrizione in uso. 
3. Usando il menu a discesa, selezionare il circuito ExpressRoute da associare all'hub.
4. Se il circuito ExpressRoute non è nella stessa sottoscrizione o sono stati forniti [una chiave di autorizzazione e un ID peer](../expressroute/expressroute-howto-linkvnet-portal-resource-manager.md), selezionare **Find a circuit redeeming an authorization key** (Trova un circuito riscattando una chiave di autorizzazione).
5. Immettere i dettagli seguenti:
* **Chiave di autorizzazione** - Generata dal proprietario del circuito come descritto in precedenza
* **URI del circuito peer** - URI del circuito fornito dal proprietario del circuito che costituisce l'identificatore univoco per il circuito
* **Peso del routing** - [Peso del routing](../expressroute/expressroute-optimize-routing.md) consente di preferire determinati percorsi quando allo stesso hub sono connessi più circuiti da diverse località di peering
6. Fare clic su **Find circuit** (Trova circuito) e selezionare il circuito, se disponibile.
7. Selezionare uno o più hub dall'elenco a discesa e fare clic su **Salva**

## <a name="vnet"></a>5. Connettere la rete virtuale a un hub

In questo passaggio si crea la connessione di peering tra l'hub e una rete virtuale. Ripetere questi passaggi per ogni rete virtuale a cui ci si vuole connettere.

1. Nella pagina della rete WAN virtuale fare clic su **Connessione rete virtuale**.
2. Nella pagina di connessione alla rete virtuale fare clic su **+ Aggiungi connessione**.
3. Nella pagina **Aggiungi connessione** compilare i campi seguenti:

    * **Nome connessione** - Specificare un nome per la connessione.
    * **Hub** - Selezionare l'hub che si vuole associare a questa connessione.
    * **Sottoscrizione** - Verificare la sottoscrizione.
    * **Rete virtuale** - Selezionare la rete virtuale che si vuole connettere all'hub. La rete virtuale non può avere un gateway di rete virtuale già esistente.


## <a name="viewwan"></a>6. Visualizzare la rete WAN virtuale

1. Passare alla rete WAN virtuale.
2. Nella pagina Panoramica ogni punto sulla mappa rappresenta un hub. Passare il mouse su qualsiasi punto per visualizzare il riepilogo dell'integrità dell'hub.
3. Nella sezione degli hub e delle connessioni è possibile visualizzare lo stato dell'hub, il sito, l'area, lo stato della connessione VPN e i byte in entrata e in uscita.

## <a name="viewhealth"></a>7. Visualizzare l'integrità delle risorse

1. Passare alla rete WAN.
2. Nella pagina della rete WAN, nella sezione **Supporto e risoluzione dei problemi** fare clic su **Integrità** e visualizzare la risorsa.

## <a name="connectmon"></a>8. Monitorare una connessione

Creare una connessione per monitorare la comunicazione tra una macchina virtuale di Azure e un sito remoto. Per informazioni su come configurare un monitoraggio della connessione, vedere [Monitorare la comunicazione di rete](~/articles/network-watcher/connection-monitor.md). Il campo di origine è l'IP della macchina virtuale in Azure e l'IP di destinazione è l'indirizzo IP del sito.

## <a name="cleanup"></a>9. Pulire le risorse

Quando queste risorse non sono più necessarie, è possibile usare [Remove-AzureRmResourceGroup](/powershell/module/azurerm.resources/remove-azurermresourcegroup) per rimuovere il gruppo di risorse e tutte le risorse in esso contenute. Sostituire "myResourceGroup" con il nome del gruppo di risorse specifico ed eseguire il comando di PowerShell seguente:

```azurepowershell-interactive
Remove-AzureRmResourceGroup -Name myResourceGroup -Force
```

## <a name="next-steps"></a>Passaggi successivi

In questa esercitazione si è appreso come:

> [!div class="checklist"]
> * Creare una rete WAN virtuale
> * Creare un hub
> * Trovare e associare un circuito all'hub
> * Associare il circuito a uno o più hub
> * Connettere una rete virtuale a un hub
> * Visualizzare la rete WAN virtuale
> * Visualizzare lo stato di integrità delle risorse
> * Monitorare una connessione

Per altre informazioni sulla rete WAN virtuale, vedere la [panoramica sulla rete WAN virtuale](virtual-wan-about.md).
