---
title: Configurare le regole in uscita e il bilanciamento del carico in Load Balancer Standard usando l'interfaccia della riga di comando di Azure | Microsoft Docs
description: Questo articolo illustra come configurare le regole in uscita e il bilanciamento del carico in Load Balancer Standard usando l'interfaccia della riga di comando di Azure.
services: load-balancer
documentationcenter: na
author: KumudD
manager: jpconnock
tags: azure-resource-manager
ms.service: load-balancer
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 09/24/2018
ms.author: kumud
ms.openlocfilehash: a6d442452fe5ffc61648b3c004c03f1756f8f57e
ms.sourcegitcommit: 51a1476c85ca518a6d8b4cc35aed7a76b33e130f
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 09/25/2018
ms.locfileid: "47160656"
---
# <a name="configure-load-balancing-and-outbound-rules-in-standard-load-balancer-using-azure-cli"></a>Configurare le regole in uscita e il bilanciamento del carico in Load Balancer Standard usando l'interfaccia della riga di comando di Azure

Questa guida introduttiva mostra come configurare le regole in uscita in Load Balancer Standard usando l'interfaccia della riga di comando di Azure.  

Al termine, la risorsa Load Balancer conterrà due front-end e le regole associate agli stessi: uno per connessioni in entrata e l'altro per connessioni in uscita.  Ogni front-end fa riferimento a un indirizzo IP pubblico e in questo scenario viene utilizzato un indirizzo IP pubblico diverso per connessioni in entrata e in uscita.   La regola di bilanciamento del carico offre solo il bilanciamento del carico in entrata e la regola in uscita controlla la NAT in uscita fornita per la macchina virtuale.

[!INCLUDE [cloud-shell-try-it.md](../../includes/cloud-shell-try-it.md)] 

Se si sceglie di installare e usare l'interfaccia della riga di comando in locale, per questa esercitazione è necessario eseguire l'interfaccia della riga di comando di Azure versione 2.0.28 o successiva. Per trovare la versione, eseguire `az --version`. Se è necessario eseguire l'installazione o l'aggiornamento, vedere [Installare l'interfaccia della riga di comando di Azure 2.0]( /cli/azure/install-azure-cli).

## <a name="create-resource-group"></a>Creare un gruppo di risorse

Come prima cosa creare un gruppo di risorse con [az group create](https://docs.microsoft.com/cli/azure/group#create). Un gruppo di risorse di Azure è un contenitore logico in cui le risorse di Azure vengono distribuite e gestite.

L'esempio seguente crea un gruppo di risorse denominato *myresourcegroupoutbound* nella posizione *eastus2*:

```azurecli-interactive
  az group create \
    --name myresourcegroupoutbound \
    --location eastus2
```
## <a name="create-virtual-network"></a>Creare una rete virtuale
Creare una rete virtuale denominata *myvnetoutbound* con una subnet denominata *mysubnetoutbound* nel gruppo *myresourcegroupoutbound* con il comando [az network vnet create](https://docs.microsoft.com/cli/azure/network/vnet#create).

```azurecli-interactive
  az network vnet create \
    --resource-group myresourcegroupoutbound \
    --name myvnetoutbound \
    --address-prefix 192.168.0.0/16 \
    --subnet-name mysubnetoutbound
    --subnet-prefix 192.168.0.0/24
```

## <a name="create-inbound-public-ip-address"></a>Creare un indirizzo IP pubblico in entrata 

Per accedere all'app Web in Internet, assegnare un indirizzo IP pubblico al servizio di bilanciamento del carico. Un'istanza di Load Balancer Standard supporta solo indirizzi IP pubblici standard. Usare il comando [az network public-ip create](https://docs.microsoft.com/cli/azure/network/public-ip#create) per creare un indirizzo IP pubblico standard denominato *mypublicipinbound* in *myresourcegroupoutbound*.

```azurecli-interactive
  az network public-ip create --resource-group myresourcegroupoutbound --name mypublicipinbound --sku standard
```

## <a name="create-outbound-public-ip-address"></a>Creare un indirizzo IP pubblico in uscita 

Creare un indirizzo IP standard per la configurazione in uscita front-end di Load Balancer usando il comando [az network public-ip create](https://docs.microsoft.com/cli/azure/network/public-ip#create) denominato *mypublicipoutbound* in *myresourcegroupoutbound*.

```azurecli-interactive
  az network public-ip create --resource-group myresourcegroupoutbound --name mypublicipoutbound --sku standard
```


## <a name="create-azure-load-balancer"></a>Creare un Azure Load Balancer

Questa sezione descrive dettagliatamente come creare e configurare i componenti seguenti del servizio di bilanciamento del carico:
  - Un IP front-end che riceve il traffico di rete in ingresso sul servizio di bilanciamento del carico.
  - Un poll back-end a cui il pool IP front-end invia il traffico di rete con carico bilanciato.
  - Un probe di integrità che determina l'integrità delle istanze delle macchine virtuali back-end.
  - Una regola di bilanciamento del carico in entrata che definisce come verrà distribuito il traffico alle macchine virtuali.
  - Una regola di bilanciamento del carico in uscita che definisce come verrà distribuito il traffico alle macchine virtuali.

### <a name="create-load-balancer"></a>Crea servizio di bilanciamento del carico

Usare il comando [az network lb create](https://docs.microsoft.com/cli/azure/network/lb?view=azure-cli-latest#create) per creare un Load Balancer con l'indirizzo IP in entrata denominato *lb*, che include una configurazione IP front-end denominata *myfrontendinbound* e un pool back-end denominato *bepool*, associato all'indirizzo IP pubblico *mypublicipinbound* creato nel passaggio precedente.

```azurecli-interactive
  az network lb create \
    --resource-group myresourcegroupoutbound \
    --name lb \
    --sku standard \
    --backend-pool-name bepool \
    --frontend-ip-name myfrontendinbound \
    --location eastus2 \
    --public-ip-address mypublicipinbound   
  ```

### <a name="create-outbound-frontend-ip"></a>Creare un indirizzo IP front-end in uscita
Creare la configurazione IP front-end in uscita per il Load Balancer usando il comando [az network lb frontend-ip create](https://docs.microsoft.com/cli/azure/network/lb?view=azure-cli-latest#create) che include una configurazione IP front-end in uscita denominata *myfrontendoutbound* associata all'indirizzo IP pubblico *mypublicipoutbound*

```azurecli-interactive
  az network lb frontend-ip create \
    --resource-group myresourcegroupoutbound \
    --name myfrontendoutbound \
    --lb-name lb \
    --public-ip-address mypublicipoutbound 
  ```

### <a name="create-health-probe"></a>Creare un probe integrità

Un probe di integrità controlla tutte le istanze di una macchina virtuale per assicurarsi che possano inviare il traffico di rete. L'istanza della macchina virtuale con controlli di probe falliti non viene rimossa dal servizio di bilanciamento del carico fino a quando non è nuovamente online e il controllo dei probe ne certifica l'integrità. Creare un probe di integrità con il comando [az network lb probe create](https://docs.microsoft.com/cli/azure/network/lb/probe?view=azure-cli-latest#create) per monitorare l'integrità delle macchine virtuali. 

```azurecli-interactive
  az network lb probe create \
    --resource-group myresourcegroupoutbound \
    --lb-name lb \
    --name http \
    --protocol http \
    --port 80 \
    --path /  
```

### <a name="create-load-balancing-rule"></a>Creare le regole di bilanciamento del carico

Una regola di bilanciamento del carico definisce la configurazione IP front-end per il traffico in entrata e il pool IP back-end che riceve il traffico, insieme alle porte di origine e di destinazione necessarie. Creare una regola di bilanciamento del carico *myinboundlbrule* con il comando [az network lb rule create](https://docs.microsoft.com/cli/azure/network/lb/rule?view=azure-cli-latest#create) per l'ascolto sulla porta 80 nel pool front-end *myfrontendinbound* e l'invio del traffico di rete con carico bilanciato al pool di indirizzi back-end *bepool* sempre tramite la porta 80. 

>[!NOTE]
>Questa regola di bilanciamento del carico disabilita l'(S)NAT automatico in uscita con il parametro --disable-outbound-snat. Il NAT in uscita viene fornito solo dalla regola in uscita.

```azurecli-interactive
az network lb rule create \
--resource-group myresourcegroupoutbound \
--lb-name lb \
--name inboundlbrule \
--protocol tcp \
--frontend-port 80 \
--backend-port 80 \
--probe http \
--frontend-ip-name myfrontendinbound \
--backend-pool-name bepool \
--disable-outbound-snat
```

### <a name="create-outbound-rule"></a>Creare una regola in uscita

Una regola in uscita definisce l'IP front-end pubblico, rappresentato dal pool front-end *myfrontendoutbound*, che verrà usato per tutto il traffico NAT in uscita, nonché per il pool back-end a cui si applica questa regola.  Creare una regola in uscita *myoutboundrule* per la traduzione della rete in uscita di tutte le macchine virtuali (configurazioni IP NIC) nel pool back-end *bepool*.  Inoltre, il comando seguente modifica il timeout di inattività in uscita da 4 a 15 minuti e alloca le porte SNAT 10000 anziché 1024.  Esaminare [Regole in uscita](https://aka.ms/lboutboundrules) per altri dettagli.

```azurecli-interactive
az network lb outbound-rule create \
 --resource-group myresourcegroupoutbound \
 --lb-name lb \
 --name outboundrule \
 --frontend-ip-configs myfrontendoutbound \
 --protocol All \
 --idle-timeout 15 \
 --outbound-ports 10000 \
 --address-pool bepool
```

A questo punto è possibile procedere con l'aggiunta delle macchine virtuali al poll back-end *bepool* aggiornando la configurazione IP delle relative risorse NIC.

## <a name="clean-up-resources"></a>Pulire le risorse

Quando non sono più necessari, è possibile rimuovere il gruppo di risorse, il servizio di bilanciamento del carico e tutte le risorse correlate tramite il comando [az group delete](/cli/azure/group#az-group-delete).

```azurecli-interactive 
  az group delete --name myresourcegroupoutbound
```

## <a name="next-steps"></a>Passaggi successivi
In questo articolo è stato creato un Load Balancer Standard e sono state configurate entrambe le regole di bilanciamento del traffico in entrata e un probe di integrità per le macchine virtuali nel pool back-end. Per altre informazioni su Azure Load Balancer, passare alle esercitazioni su Azure Load Balancer.

> [!div class="nextstepaction"]
> [Esercitazioni su Azure Load Balancer](tutorial-load-balancer-standard-public-zone-redundant-portal.md)

