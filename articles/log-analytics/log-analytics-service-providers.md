---
title: Log Analytics per provider di servizi | Microsoft Docs
description: Log Analytics aiuta i provider dei servizi gestiti (MSP), le aziende di grandi dimensioni, i fornitori di software indipendenti (ISV) e i provider di servizi di hosting a gestire e monitorare i server nell'infrastruttura cloud o locale del cliente.
services: log-analytics
documentationcenter: ''
author: MeirMen
manager: jochan
editor: ''
ms.assetid: c07f0b9f-ec37-480d-91ec-d9bcf6786464
ms.service: log-analytics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: conceptual
ms.date: 07/05/2018
ms.author: meirm
ms.component: na
ms.openlocfilehash: ad0a3b8e0ee5f1114ea1db95cfe2f4176b8e2ddb
ms.sourcegitcommit: aa988666476c05787afc84db94cfa50bc6852520
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 07/10/2018
ms.locfileid: "37931991"
---
# <a name="log-analytics-for-service-providers"></a>Log Analytics per provider di servizi
Log Analytics aiuta i provider dei servizi gestiti (MSP), le aziende di grandi dimensioni, i fornitori di software indipendenti (ISV) e i provider di servizi di hosting a gestire e monitorare i server nell'infrastruttura cloud o locale del cliente. 

Le aziende di grandi dimensioni hanno molti punti in comune con i provider di servizi, soprattutto quando c'è un team IT centralizzato che si occupa della gestione dell'IT per molte business unit diverse tra loro. Per semplicità, in questo documento si usa il termine *provider di servizi* ma la stessa funzionalità è disponibile anche per le aziende e gli altri clienti.

Per i partner e i provider di servizi che fanno parte del programma [Cloud Solution Provider (CSP)](https://partner.microsoft.com/Solutions/cloud-reseller-overview), Log Analytics è uno dei servizi di Azure disponibili in una [sottoscrizione di Azure CSP](https://docs.microsoft.com/azure/cloud-solution-provider/overview/azure-csp-overview). 

## <a name="architectures-for-service-providers"></a>Architetture per i provider di servizi

Le aree di lavoro di Log Analytics consentono all'amministratore di controllare il flusso e l'isolamento dei log e di creare un'architettura di log in grado di soddisfare le esigenze aziendali specifiche. [Questo articolo](https://docs.microsoft.com/en-us/azure/log-analytics/log-analytics-manage-access) descrive le considerazioni generali per la gestione dell'area di lavoro. Per i provider di servizi possono essere presenti considerazioni aggiuntive.

Esistono tre possibili architetture relative alle aree di lavoro di Log Analytics:

### <a name="1-distributed---logs-are-stored-in-workspaces-located-in-the-customers-tenant"></a>1. Distribuita - I log vengono archiviati nelle aree di lavoro che si trovano nel tenant del cliente 

In questa architettura l'area di lavoro viene distribuita nel tenant del cliente usato per tutti i log del cliente stesso. Agli amministratori del provider di servizi viene concesso l'accesso all'area di lavoro tramite le autorizzazioni di [utenti guest di Azure Active Directory (B2B)](https://docs.microsoft.com/en-us/azure/active-directory/b2b/what-is-b2b). Per accedere a tali aree di lavoro, l'amministratore del provider di servizi deve passare alla directory del cliente nel portale di Azure.

I vantaggi di questa architettura sono i seguenti:
* Il cliente può gestire l'accesso ai log tramite il proprio [accesso basato sui ruoli](https://docs.microsoft.com/en-us/azure/role-based-access-control/overview).
* Ogni cliente può definire impostazioni diverse per la propria area di lavoro, ad esempio in termini di conservazione e di limitazione sull'uso dei dati.
* Isolamento tra i clienti in termini di normative e conformità.
* Il costo per ogni area di lavoro viene addebitato nella sottoscrizione del cliente.
* I log possono essere raccolti da tutti i tipi di risorse, non solo in base all'agente. È possibile usare, ad esempio, il controllo di Azure.

Gli svantaggi di questa architettura sono i seguenti:
* È più difficile per il provider di servizi gestire contemporaneamente un numero elevato di tenant dei clienti.
* Gli amministratori del provider di servizi devono eseguire il provisioning per la directory dei clienti.
* Il provider di servizi non può analizzare i dati dei clienti.

### <a name="2-central---logs-are-stored-in-workspace-located-in-the-service-provider-tenant"></a>2. Centrale - I log vengono archiviati nell'area di lavoro che si trova nel tenant del provider di servizi

In questa architettura i log non vengono archiviati nel tenant del cliente, ma solo in una posizione centrale nell'ambito di una sottoscrizione del provider di servizi. Gli agenti installati su macchine virtuali del cliente sono configurati per inviare i log all'area di lavoro tramite l'ID e la chiave privata dell'area di lavoro.

I vantaggi di questa architettura sono i seguenti:
* Facilità di gestione di un numero elevato di clienti e di integrarli in diversi sistemi back-end.
* Il provider di servizi dispone della proprietà completa dei log e dei diversi elementi, ad esempio funzioni e query salvate.
* Il provider di servizio può eseguire funzioni di analisi su tutti i clienti.

Gli svantaggi di questa architettura sono i seguenti:
* Questa architettura è applicabile solo ai dati di macchine virtuale basati su agenti e non può essere usata con origini dati PaaS, SaaS e dell'infrastruttura di Microsoft Azure.
* Potrebbe essere difficile separare i dati tra i clienti quando sono uniti in una singola area di lavoro. L'unico metodo per eseguire questa operazione è quello di usare il nome di dominio completo del computer (FQDN) o l'ID sottoscrizione di Azure. 
* Tutti i dati di tutti i clienti verranno archiviati nella stessa area con un'unica fattura e con le stesse impostazioni di conservazione e di configurazione.
* Per i servizi PaaS e di infrastruttura di Microsoft Azure, ad esempio Diagnostica di Azure e il controllo di Azure, l'area di lavoro deve essere nello stesso tenant della risorsa in modo che i logo non vengano inviati all'area di lavoro centrale.
* Tutti gli agenti di macchine virtuali di tutti i clienti vengono autenticati nell'area di lavoro centrale usando lo stesso ID e la stessa chiave dell'area di lavoro. Non esiste alcun metodo per bloccare i log di un cliente specifico senza interrompere l'attività di altri clienti.


### <a name="3-hybrid---logs-are-stored-in-workspace-located-in-the-customers-tenant-and-some-of-them-are-pulled-to-a-central-location"></a>3. Ibrida - I log vengono archiviati nell'area di lavoro che si trova nel tenant del cliente e per alcuni viene eseguito il pull in una posizione centrale.

La terza architettura è una combinazione delle due opzioni. Tale architettura si basa su quella distribuita in cui i log sono locali per ogni cliente, usando tuttavia un meccanismo per creare un repository centrale di log. Per una parte dei log viene eseguito il pull in una posizione centrale per la creazione di report e analitica. Questa parte può essere costituita da un numero ridotto di tipi di dati o da un riepilogo dell'attività, ad esempio statistiche giornaliere.

Per implementare la posizione centrale in Log Analytics, sono disponibili due opzioni:

1. Area di lavoro centrale: il provider di servizi può creare un'area di lavoro nel proprio tenant e usare uno script che usi l'[API di query](https://dev.loganalytics.io/) con l'[API di raccolta dati](log-analytics-data-collector-api.md) per spostare i dati dalle diverse aree di lavoro nella posizione centrale. Un'alternativa all'uso degli script consiste nell'usare l'[app per la logica di Azure](https://docs.microsoft.com/en-us/azure/logic-apps/logic-apps-overview).

2. Power BI come posizione centrale: Power BI può agire come posizione centrale quando le diverse aree di lavoro esportano i dati tramite l'integrazione tra Log Analytics e [Power BI](log-analytics-powerbi.md). 


## <a name="next-steps"></a>Passaggi successivi
* Automatizzare la creazione e la configurazione delle aree di lavoro usando i [modelli di Resource Manager](log-analytics-template-workspace-configuration.md)
* Automatizzare la creazione delle aree di lavoro usando [PowerShell](log-analytics-powershell-workspace-configuration.md) 
* Usare la funzione [Avvisi](log-analytics-alerts.md) per l'integrazione con i sistemi esistenti
* Generare report di riepilogo usando [Power BI](log-analytics-powerbi.md)

