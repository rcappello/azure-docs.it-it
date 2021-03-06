---
title: Domande frequenti su Monitoraggio di Azure | Microsoft Docs
description: Monitoraggio di Azure per le macchine virtuali è una soluzione di Azure che combina il monitoraggio dell'integrità e delle prestazioni del sistema operativo delle macchine virtuali di Azure, nonché l'individuazione automatica dei componenti e delle dipendenze delle applicazioni con altre risorse e mappa la comunicazione tra questi elementi. Questo articolo fornisce le risposte alle domande frequenti.
services: azure-monitor
documentationcenter: ''
author: mgoedtel
manager: carmonm
editor: tysonn
ms.assetid: ''
ms.service: azure-monitor
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 09/19/2018
ms.author: magoedte
ms.openlocfilehash: 308a447ff99cd11ad6a28df0bdb515764b0f546b
ms.sourcegitcommit: cc4fdd6f0f12b44c244abc7f6bc4b181a2d05302
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 09/25/2018
ms.locfileid: "47063456"
---
# <a name="azure-monitor-for-vms-frequently-asked-questions"></a>Domande frequenti su Monitoraggio di Azure per le macchine virtuali
Le Domande frequenti Microsoft sono un elenco di domande frequenti su Monitoraggio di Azure per le macchine virtuali in Microsoft Azure. Per altre domande sulla soluzione, visitare il [forum di discussione](https://feedback.azure.com/forums/34192--general-feedback) e inviare le proprie domande. Se una domanda viene posta più volte, viene aggiunta a questo articolo per poter essere recuperata in modo rapido e semplice.

## <a name="can-i-onboard-to-an-existing-workspace"></a>È possibile eseguire l'onboarding in un'area di lavoro esistente?
Se le macchine virtuali sono già connesse a un'area di lavoro di Log Analytics, è possibile continuare a usare tale area di lavoro quando si esegue l'onboarding per Monitoraggio di Azure per le macchine virtuali, purché si trovi in una delle aree supportate elencate [qui](monitoring-vminsights-onboard.md#prerequisites).

Quando si esegue l'onboarding, si configurano i contatori delle prestazioni per l'area di lavoro in modo che tutte le macchine virtuali che inviano dati all'area di lavoro inizino a raccogliere queste informazioni per la visualizzazione e l'analisi in Monitoraggio di Azure per le macchine virtuali.  Di conseguenza, verranno visualizzati i dati sulle prestazioni di tutte le macchine virtuali connesse all'area di lavoro selezionata.  Le funzionalità di integrità e mappa sono abilitate solo per le macchine virtuali specificate per l'onboarding.

Per altre informazioni sui contatori delle prestazioni abilitati, vedere il nostro articolo sull'[onboarding](monitoring-vminsights-onboard.md).

## <a name="can-i-onboard-to-a-new-workspace"></a>È possibile eseguire l'onboarding in una nuova area di lavoro? 
Se le macchine virtuali non attualmente connesse a un'area di lavoro di Log Analytics esistente, è necessario crearne una nuova per archiviare i dati.  La creazione di una nuova area di lavoro predefinita avviene automaticamente nel caso in cui si configuri una singola macchina virtuale di Azure per Monitoraggio di Azure per le macchine virtuali tramite il portale di Azure.

Se si sceglie di usare il metodo basato su script, i passaggi sono illustrati nell'articolo sull'[onboarding](monitoring-vminsights-onboard.md). 

## <a name="what-do-i-do-if-my-vm-is-already-reporting-to-an-existing-workspace"></a>Cosa occorre fare se la macchina virtuale invia già informazioni a un'area di lavoro esistente?
Se già si raccolgono dati dalle macchine virtuali, è possibile che sia già stato configurato l'invio di dati a un'area di lavoro di Log Analytics esistente.  Se quest'area di lavoro è in una delle aree supportate, è possibile abilitare Monitoraggio di Azure per le macchine virtuali per tale area di lavoro preesistente.  Se l'area di lavoro già in uso non si trova in una delle aree supportate, non è attualmente possibile eseguire l'onboarding per Monitoraggio di Azure per le macchine virtuali.  Microsoft sta lavorando attivamente per supportare altre aree.

>[!NOTE]
>Microsoft configura i contatori delle prestazioni per l'area di lavoro con effetto su tutte le macchine virtuali che inviano informazioni all'area di lavoro, anche se non si è scelto di eseguirne l'onboarding per Monitoraggio di Azure per le macchine virtuali. Per altre informazioni sulla configurazione dei contatori delle prestazioni per l'area di lavoro, vedere la [documentazione](../log-analytics/log-analytics-data-sources-performance-counters.md). Per informazioni sui contatori configurati per Monitoraggio di Azure per le macchine virtuali, vedere la [documentazione sull'onboarding](monitoring-vminsights-onboard.md#performance-counters-enabled).  

## <a name="why-did-my-vm-fail-to-onboard"></a>Perché la macchina virtuale non è riuscita a eseguire l'onboarding?
Quando si esegue l'onboarding di una macchina virtuale di Azure dal portale di Azure, si verificano i passaggi seguenti:

* Viene creata un'area di lavoro di Log Analytics predefinita, se tale opzione è stata selezionata.
* I contatori delle prestazioni vengono configurati per l'area di lavoro selezionata. Se questo passaggio non riesce, si noterà che alcuni grafici delle prestazioni e alcune tabelle non contengono i dati relativi alla macchina virtuale di cui è stato eseguito l'onboarding. Per risolvere il problema, è possibile eseguire lo script di PowerShell documentato [qui](monitoring-vminsights-onboard.md#enable-with-powershell).
* L'agente di Log Analytics viene installato nelle macchine virtuali di Azure mediante un'estensione VM, se necessario.  
* Dependency Agent per la mappa di Monitoraggio di Azure per le macchine virtuali viene installato nelle macchine virtuali di Azure mediante un'estensione, se necessario.  
* I componenti di Monitoraggio di Azure che supportano la funzionalità Integrità vengono configurati, se necessario, e la macchina virtuale viene configurata per l'invio dei dati sull'integrità.

Durante il processo di onboarding, viene controllato lo stato di ciascun passaggio, visualizzando una notifica nel portale.  La configurazione dell'area di lavoro e l'installazione dell'agente richiedono in genere 5-10 minuti.  La visualizzazione dei dati di monitoraggio e sull'integrità nel portale richiedere altri 5-10 minuti.  

Se l'onboarding è stato avviato e vengono visualizzati dei messaggi che indicano che occorre eseguire l'onboarding della macchina virtuale, attendere 30 minuti affinché la macchina virtuale completi il processo. 

## <a name="i-dont-see-some-or-any-data-in-the-performance-charts-for-my-vm"></a>I grafici delle prestazioni della macchina virtuale non contengono alcuni dati o non ne contengono affatto
Se non compaiono i dati sulle prestazioni nella tabella del disco o in alcuni grafici delle prestazioni, è possibile che i contatori delle prestazioni non siano stati configurati nell'area di lavoro. Per risolvere il problema, eseguire lo [script di PowerShell](monitoring-vminsights-onboard.md#enable-with-powershell) seguente.

## <a name="how-is-azure-monitor-for-vms-map-feature-different-from-service-map"></a>In cosa differisce la funzionalità di mappa di Monitoraggio di Azure per le macchine virtuali da Mapping dei servizi?
La funzionalità di mappa di Monitoraggio di Azure per le macchine virtuali si basa su Mapping dei servizi, ma presenta le differenze seguenti:

* È possibile accedere alla vista della mappa dal pannello VM e da Monitoraggio di Azure per le macchine virtuali in Monitoraggio di Azure.
* Le connessioni nella mappa ora sono selezionabili e mostrano i dati delle metriche di connessione nel pannello laterale relativo alla connessione selezionata.
* È disponibile una nuova API che consente di creare le mappe in modo da supportare meglio quelle più complesse.
* Le macchine virtuali monitorate sono ora incluse nel nodo del gruppo client e il grafico ad anello mostra la proporzione tra le macchine virtuali monitorate e non monitorate presenti nel gruppo.  Può anche essere utilizzato per filtrare l'elenco delle macchine quando il gruppo viene espanso.
* Le macchine virtuali monitorate sono ora incluse nei nodi del gruppo di porte server e il grafico ad anello mostra la proporzione tra le macchine monitorate e non monitorate presenti nel gruppo.  Può anche essere utilizzato per filtrare l'elenco delle macchine quando il gruppo viene espanso.
* Lo stile della mappa è stato aggiornato per maggiore coerenza con la mappa delle app di Application Insights.
* I pannelli laterali sono stati aggiornati, ma non dispongono ancora del set completo di integrazioni supportate in Mapping dei servizi, ovvero Gestione aggiornamenti, Rilevamento modifiche, Sicurezza e Service Desk. 
* L'opzione per la scelta dei gruppi e delle macchine di cui eseguire il mapping è stata aggiornata e ora supporta sottoscrizioni, gruppi di risorse, set di scalabilità delle macchine virtuali di Azure e servizi cloud.
* Non è possibile creare nuovi gruppi di macchine di Mapping dei servizi nella funzionalità Monitoraggio di Azure per le macchine virtuali.  

## <a name="why-do-my-performance-charts-show-dotted-lines"></a>Perché nei grafici delle prestazioni appaiono delle linee tratteggiate?

I motivi possono essere vari.  Nei casi in cui sia presente un vuoto nella raccolta di dati, le linee si presentano tratteggiate.  Se è stata modificata la frequenza di campionamento dei dati per i contatori delle prestazioni abilitati (l'impostazione predefinita prevede la raccolta di dati ogni 60 secondi), è possibile che appaiano delle linee punteggiate nel grafico quando si sceglie un intervallo di tempo ristretto per il grafico e la frequenza di campionamento è inferiore alle dimensioni del bucket usate nel grafico (ad esempio, la frequenza di campionamento è ogni 10 minuti e ogni bucket del grafico è di 5 minuti).  Se si sceglie di visualizzare un intervallo di tempo più ampio, le linee del grafico appariranno continue e non tratteggiate.

## <a name="are-groups-supported-with-azure-monitor-for-vms"></a>I gruppi sono supportati con Monitoraggio di Azure per le macchine virtuali?
La funzionalità delle prestazioni supporta i gruppi basati sulle risorse evidenziate all'interno di un'area di lavoro specifica, nonché il raggruppamento basato su un particolare set di scalabilità di macchine virtuali di Azure e servizio cloud.

## <a name="how-do-i-see-the-details-for-what-is-driving-the-95th-percentile-line-in-the-aggregate-performance-charts"></a>Come visualizzare i dettagli alla base della linea del 95° percentile nei grafici delle prestazioni in forma aggregata?
Per impostazione predefinita, l'elenco è ordinato in modo da mostrare le macchine virtuali con il valore più elevato per il 95° percentile in relazione alla metrica selezionata, ad eccezione del grafico della memoria disponibile, che mostra le macchine con il valore più basso per il 5° percentile.  Se si fa clic sul grafico, appare la visualizzazione **elenco delle prime N** con la metrica appropriata selezionata.

## <a name="how-does-the-map-feature-handle-duplicate-ips-across-different-vnets-and-subnets"></a>In che modo la funzionalità di mappa gestisce gli indirizzi IP duplicati su reti virtuali e subnet diverse?
Se si duplicano gli intervalli IP con le VM o i set di scalabilità di macchine virtuali di Azure su subnet e reti virtuali, la mappa di Monitoraggio di Azure per le macchine virtuali potrebbe mostrare informazioni non corrette. Si tratta di un problema noto ed è in corso l'analisi delle opzioni per migliorare questa esperienza.

## <a name="does-map-feature-support-ipv6"></a>La funzionalità di mappa supporta il protocollo IPv6?
La funzionalità di mappa supporta attualmente solo il protocollo IPv4 ed è in corso l'analisi del supporto per IPv6. È supportato anche il protocollo IPv4 con a tunneling all'interno di IPv6.

## <a name="when-i-load-a-map-for-a-resource-group-or-other-large-group-the-map-is-difficult-to-view"></a>Quando si carica una mappa per un gruppo di risorse o un altro gruppo di grandi dimensioni, la mappa è di difficile visualizzazione
Anche se sono stati apportati miglioramenti alla mappa per gestire le configurazioni complesse e di grandi dimensioni, ci rendiamo conto che una mappa può contenere molti nodi, connessioni e nodi che funzionano come cluster.  Microsoft si impegna a migliorare costantemente il supporto per aumentare la scalabilità.   

## <a name="why-does-the-network-chart-on-the-performance-tab-look-different-than-the-network-chart-on-the-azure-vm-overview-page"></a>Perché il grafico di rete nella scheda Prestazioni ha un aspetto diverso rispetto al grafico di rete nella pagina di panoramica della VM di Azure?

La pagina di panoramica di una VM di Azure mostra i grafici basati sulla misurazione dell'attività dell'host nella VM guest.  Per il grafico di rete nella panoramica della VM di Azure, viene visualizzato solo il traffico che verrà fatturato  e non è incluso il traffico tra reti virtuali.  I dati e i grafici visualizzati per Monitoraggio di Azure per le macchine virtuali si basano sui dati ottenuti dalla VM guest e il grafico di rete mostra tutto il traffico TCP/IP in ingresso e in uscita verso tale VM, incluso quello tra reti virtuali.

## <a name="next-steps"></a>Passaggi successivi
Vedere [Eseguire l'onboarding di Monitoraggio di Azure per le macchine virtuali](monitoring-vminsights-onboard.md) per informazioni sui requisiti e i metodi per abilitare il monitoraggio delle macchine virtuali.
