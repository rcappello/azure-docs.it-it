---
title: Panoramica degli endpoint di servizio di rete virtuale per il server di Database di Azure per MySQL | Microsoft Docs
description: Questo articolo descrive il funzionamento degli endpoint di servizio di rete virtuale per il server di Database di Azure per MySQL.
services: mysql
author: mbolz
ms.author: mbolz
manager: jhubbard
editor: jasonwhowell
ms.service: mysql
ms.topic: conceptual
ms.date: 5/29/2018
ms.openlocfilehash: 652657c8891f2320c026251ffa32e4787028ee18
ms.sourcegitcommit: 266fe4c2216c0420e415d733cd3abbf94994533d
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 06/01/2018
ms.locfileid: "34659552"
---
# <a name="use-virtual-network-service-endpoints-and-rules-for-azure-database-for-mysql"></a>Usare gli endpoint e le regole di servizio di rete virtuale per Database di Azure per MySQL

Le *regole di rete virtuale* rappresentano una funzionalità di sicurezza del firewall che consente di definire se il server di Database di Azure per MySQL accetta le comunicazioni inviate da subnet specifiche nelle reti virtuali. Questo articolo spiega i motivi per cui la funzione delle regole di rete virtuale è talvolta la scelta ideale per consentire le comunicazioni con il server di Database di Azure per MySQL.

Per creare una regola di rete virtuale, devono innanzitutto essere disponibili una [rete virtuale][vm-virtual-network-overview] (VNet) e un [endpoint di servizio di rete virtuale][vm-virtual-network-service-endpoints-overview-649d] a cui la regola possa fare riferimento. La figura seguente illustra il funzionamento di un endpoint di servizio di rete virtuale con Database di Azure per MySQL:

![Esempio del funzionamento di un endpoint di servizio di rete virtuale](media/concepts-data-access-and-security-vnet/vnet-concept.png)

> [!NOTE]
> Per Database di Azure per MySQL, questa funzionalità è disponibile in anteprima pubblica in tutte le aree del cloud pubblico di Azure in cui viene distribuito Database di Azure per MySQL.

<a name="anch-terminology-and-description-82f" />

## <a name="terminology-and-description"></a>Terminologia e descrizione

**Rete virtuale:** è possibile associare reti virtuali alla sottoscrizione di Azure.

**Subnet:** una rete virtuale contiene **subnet**. Le macchine virtuali (VM) di Azure esistenti vengono assegnate a subnet. Una subnet può contenere varie VM o altri nodi di calcolo. I nodi di calcolo esterni alla rete virtuale non possono accedervi, a meno che non si configuri la sicurezza in modo da consentirne l'accesso.

**Endpoint di servizio di rete virtuale:** un [endpoint di servizio di rete virtuale][vm-virtual-network-service-endpoints-overview-649d] è una subnet in cui i valori delle proprietà includono uno o più nomi formali di tipi di servizi Azure. Questo articolo è incentrato sul nome del tipo **Microsoft.Sql**, che fa riferimento al servizio Azure denominato Database SQL. Questo tag di servizio si applica ai servizi di Database di Azure per MySQL e PostgreSQL. È importante tenere presente che, quando si applica il tag di servizio **Microsoft.Sql** a un endpoint di servizio di rete virtuale, viene configurato il traffico dell'endpoint per tutti i server di Database SQL di Azure, Database di Azure per MySQL e Database di Azure per PostgreSQL nella subnet. 

**Regola di rete virtuale:** una regola di rete virtuale per il server di Database di Azure per MySQL è una subnet presente nell'elenco di controllo di accesso (ACL) del server di Database di Azure per MySQL. Per essere inclusa nell'elenco ACL del server di Database di Azure per MySQL, la subnet deve contenere il nome tipo **Microsoft.Sql**.

Una regola di rete virtuale indica al server di Database di Azure per MySQL di accettare le comunicazioni da ogni nodo che si trova nella subnet.







<a name="anch-benefits-of-a-vnet-rule-68b" />

## <a name="benefits-of-a-virtual-network-rule"></a>Vantaggi di una regola di rete virtuale

Finché non si interviene, le VM nelle subnet non possono comunicare con il server di Database di Azure per MySQL. Un'azione che stabilisce la comunicazione è la creazione di una regola della rete virtuale. La base logica per la scelta dell'approccio delle regole di rete virtuale richiede una discussione di confronto riguardo le opzioni di sicurezza concorrenti offerte dal firewall.

### <a name="a-allow-access-to-azure-services"></a>A. Possibilità di accedere ai servizi di Azure

Il riquadro Sicurezza connessione contiene un pulsante **ON/OFF** con l'etichetta **Consenti l'accesso a Servizi di Azure**. L'impostazione **ON** consente le comunicazioni da tutti gli indirizzi IP di Azure e tutte le subnet di Azure. Questi indirizzi IP o subnet di Azure potrebbero non essere di proprietà dell'utente. Questa impostazione **ON** è probabilmente più aperta rispetto al livello desiderato per l'istanza di Database di Azure per MySQL. La funzione delle regole della rete virtuale offre un controllo molto più granulare.

### <a name="b-ip-rules"></a>B. Regole IP

Il firewall di Database di Azure per MySQL consente di specificare gli intervalli di indirizzi IP da cui vengono accettate le comunicazioni nell'istanza di Database di Azure per MySQL. Questo approccio è ideale per gli indirizzi IP stabili esterni alla rete privata di Azure, ma molti nodi all'interno della rete privata di Azure sono configurati con indirizzi IP *dinamici*. Gli indirizzi IP dinamici potrebbero cambiare, ad esempio al riavvio di una macchina virtuale. Sarebbe inutile specificare un indirizzo IP dinamico in una regola del firewall, in un ambiente di produzione.

È possibile recuperare l'opzione IP ottenendo un indirizzo IP *statico* per la macchina virtuale. Per i dettagli, vedere [Configurare indirizzi IP privati per una VM mediante il portale di Azure][vm-configure-private-ip-addresses-for-a-virtual-machine-using-the-azure-portal-321w].

Tuttavia, l'approccio IP statico può diventare difficile da gestire ed è dispendioso a livello di scalabilità. Le regole di rete virtuale sono più semplici da creare e gestire.

### <a name="c-cannot-yet-have-azure-database-for-mysql-on-a-subnet-without-defining-a-service-endpoint"></a>C. Non è ancora possibile disporre di Database di Azure per MySQL su una subnet, se non si definisce un endpoint di servizio

Se il server **Microsoft.Sql** è un nodo in una subnet nella rete virtuale, tutti i nodi all'interno della rete virtuale possono comunicare con il server di Database di Azure per MySQL. In questo caso, le VM possono comunicare con Database di Azure per MySQL senza richiedere regole di rete virtuale o IP.

Tuttavia, a partire da maggio 2018, il servizio Database di Azure per MySQL non è ancora tra i servizi che possono essere assegnati direttamente a una subnet.

<a name="anch-details-about-vnet-rules-38q" />

## <a name="details-about-virtual-network-rules"></a>Dettagli sulle regole di rete virtuale

Questa sezione illustra alcuni dettagli sulle regole di rete virtuale.

### <a name="only-one-geographic-region"></a>Una sola area geografica

Un endpoint del servizio Rete virtuale si applica a una sola area di Azure. L'endpoint non consente ad altre aree di accettare le comunicazioni dalla subnet.

Ogni regola della rete virtuale è limitata all'area a cui si applica il relativo endpoint sottostante.

### <a name="server-level-not-database-level"></a>A livello di server, non a livello di database

Ogni regola di rete virtuale si applica all'intero server di Database di Azure per MySQL, non solo a un determinato database nel server. In altre parole, la regola della rete virtuale si applica a livello di server, non a livello di database.

### <a name="security-administration-roles"></a>Ruoli di amministrazione di sicurezza

I ruoli di sicurezza sono distinti nell'amministrazione degli endpoint del servizio Rete virtuale. Ogni ruolo indicato di seguito deve svolgere determinate azioni:

- **Amministratore di rete:**&nbsp; attivare l'endpoint.
- **Amministratore di database:** &nbsp; aggiornare l'elenco di controllo di accesso (ACL) per aggiungere la subnet specificata al server di Database di Azure per MySQL.

*Alternativa del controllo degli accessi in base al ruolo:*

I ruoli di amministratore di rete e amministratore di database hanno più funzionalità di quelle necessarie a gestire le regole di rete virtuale. È necessario solo un subset delle relative funzionalità.

È possibile scegliere di usare il [controllo degli accessi in base al ruolo (RBAC)] [ rbac-what-is-813s] in Azure per creare un singolo ruolo personalizzato che contiene solo il subset necessario di funzionalità. È possibile usare il ruolo personalizzato anziché coinvolgere l'amministratore di rete o di database. La superficie di attacco dell'esposizione a rischi per la sicurezza è ridotta se si aggiunge un utente a un ruolo personalizzato, anziché aggiungere l'utente agli altri due ruoli di amministratore principali.

> [!NOTE]
> In alcuni casi, Database di Azure per MySQL e la subnet della rete virtuale sono in sottoscrizioni diverse. In questi casi è necessario garantire le configurazioni seguenti:
> - Entrambe le sottoscrizioni devono essere nello stesso tenant di Azure Active Directory.
> - L'utente ha le autorizzazioni necessarie per avviare le operazioni, ad esempio abilitare gli endpoint di servizio e aggiungere una subnet della rete virtuale al server specificato.

## <a name="limitations"></a>Limitazioni

Per Database di Azure per MySQL, la funzionalità delle regole di rete virtuale presenta le limitazioni seguenti:

- Nel firewall per Database di Azure per MySQL ogni regola di rete virtuale fa riferimento a una subnet. Tutte queste subnet cui viene fatto riferimento devono essere ospitate nella stessa area geografica che ospita Database di Azure per MySQL.

- Ogni server di Database di Azure per MySQL può includere fino a 128 voci ACL per qualsiasi rete virtuale specificata.

- Le regole di rete virtuale si applicano solo alle reti virtuali di Azure Resource Manager e non alle reti con un [modello di distribuzione classica][arm-deployment-model-568f].

- L'attivazione degli endpoint di servizio di rete virtuale su Database di Azure per MySQL tramite il tag di servizio **Microsoft.Sql** abilita anche gli endpoint per tutti i servizi di Database di Azure: Database di Azure per MySQL, Database di Azure per PostgreSQL, Database SQL di Azure e Azure SQL Data Warehouse.

- In fase di anteprima pubblica, le operazioni di spostamento della rete virtuale non sono supportate. Per spostare una regola di rete virtuale, rilasciarla e ricrearla.

- Gli endpoint di servizio di rete virtuale sono supportati solo per i server per utilizzo generico e ottimizzati per la memoria.

- Nel firewall, gli intervalli di indirizzi IP si applicano ai seguenti elementi di rete, ma non le regole di rete virtuale:
    - [VPN (rete privata virtuale) da sito a sito (S2S)][vpn-gateway-indexmd-608y]
    - Ambiente locale tramite [ExpressRoute][expressroute-indexmd-744v]

## <a name="expressroute"></a>ExpressRoute

Se la rete è connessa alla rete di Azure con [ExpressRoute][expressroute-indexmd-744v], ogni circuito è configurato con due indirizzi IP pubblici in Microsoft Edge. I due indirizzi IP vengono usati per connettersi ai servizi Microsoft, ad esempio ad Archiviazione di Azure, usando il peering pubblico di Azure.

Per consentire le comunicazioni tra il circuito e Database di Azure per MySQL, è necessario creare regole di rete IP per gli indirizzi IP pubblici dei circuiti. Per trovare gli indirizzi IP pubblici del circuito ExpressRoute, aprire un ticket di supporto in ExpressRoute tramite il portale di Azure.

## <a name="related-articles"></a>Articoli correlati
- [Reti virtuali di Azure][vm-virtual-network-overview]
- [Endpoint di servizio di rete virtuale di Azure][vm-virtual-network-service-endpoints-overview-649d]

## <a name="next-steps"></a>Passaggi successivi
Per articoli relativi alla creazione di regole di rete virtuale, vedere:
- [Creare e gestire le regole di rete virtuale per Database di Azure per MySQL tramite il portale di Azure](howto-manage-vnet-using-portal.md)
- [Creare e gestire le regole di rete virtuale per Database di Azure per MySQL tramite l'interfaccia della riga di comando di Azure](howto-manage-vnet-using-cli.md)

<!-- Link references, to text, Within this same Github repo. -->
[arm-deployment-model-568f]: ../azure-resource-manager/resource-manager-deployment-model.md

[vm-virtual-network-overview]: ../virtual-network/virtual-networks-overview.md

[vm-virtual-network-service-endpoints-overview-649d]: ../virtual-network/virtual-network-service-endpoints-overview.md

[vm-configure-private-ip-addresses-for-a-virtual-machine-using-the-azure-portal-321w]: ../virtual-network/virtual-networks-static-private-ip-arm-pportal.md

[rbac-what-is-813s]: ../active-directory/role-based-access-control-what-is.md

[vpn-gateway-indexmd-608y]: ../vpn-gateway/index.yml

[expressroute-indexmd-744v]: ../expressroute/index.yml