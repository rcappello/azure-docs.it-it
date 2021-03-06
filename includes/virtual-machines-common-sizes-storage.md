---
title: File di inclusione
description: File di inclusione
services: virtual-machines
author: jonbeck7
ms.service: virtual-machines
ms.topic: include
ms.date: 07/06/2018
ms.author: azcspmt;jonbeck;cynthn
ms.custom: include file
ms.openlocfilehash: 961f82cd4970abfdd11a30b2847a14f8ff1880b0
ms.sourcegitcommit: f31bfb398430ed7d66a85c7ca1f1cc9943656678
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 09/28/2018
ms.locfileid: "47454596"
---
Le dimensioni delle macchine virtuali ottimizzate per l'archiviazione offrono una velocità effettiva e di I/O elevata per i dischi e sono ideali per i database NoSQL, SQL e Big Data. Questo articolo offre informazioni sul numero di vCPU, dischi dati e schede di rete, oltre che sulla velocità effettiva di archiviazione e sulla larghezza di banda della rete per ogni dimensione di questo raggruppamento. 

La serie Ls offre fino a 32 vCPU e usa il [processore Intel® Xeon® della famiglia E5 v3](http://www.intel.com/content/www/us/en/processors/xeon/xeon-e5-solutions.html). La serie Ls offre le stesse prestazioni CPU della serie G/GS ed è dotato di 8 GiB di memoria per ogni vCPU.  Le macchine virtuali serie Ls sono ideali per le applicazioni che richiedono bassa latenza, velocità effettiva elevata e spazio di archiviazione su disco locale di grandi dimensioni. 

I casi d'uso di esempio includono database NoSQL come Cassandra, MongoDB, Cloudera e Redis, data warehousing e database transazionali di grandi dimensioni.

> [!NOTE]
> La serie Ls è ottimizzata per l'uso del disco temporaneo collegato alla macchina virtuale invece dei dischi dati permanenti. I valori elevati di velocità effettiva e operazioni di I/O al secondo del disco temporaneo rendono la serie Ls ideale per gli archivi NoSQL come Apache Cassandra e MongoDB che replicano i dati tra più macchine virtuali per ottenere persistenza in caso di errore di una singola macchina virtuale. La serie Ls non supporta la creazione di una cache locale per aumentare il numero di operazioni di I/O al secondo che è possibile ottenere tramite i dischi dati permanenti.

## <a name="ls-series"></a>Serie Ls

ACU: 180-240

Archiviazione Premium: supportata

Memorizzazione nella cache Archiviazione Premium: non supportata
 
| Dimensione          | vCPU | Memoria: GiB | GiB di archiviazione temp (unità SSD) | Valore massimo per dischi di dati | Velocità effettiva massima di archiviazione temporanea: IOPS/Mbps | Max velocità effettiva del disco non memorizzato nella cache: IOPS/MBps | Schede di interfaccia di rete max/larghezza di banda della rete prevista (Mbps) | 
|---------------|-----------|-------------|--------------------------|----------------|-------------------------------------------------------------|-------------------------------------------|------------------------------| 
| Standard_L4s   | 4    | 32   | 678   | 16    | 20,000 / 200   | 5.000/125        | 2 / 4,000  | 
| Standard_L8s   | 8    | 64   | 1,388 | 32   | 40,000 / 400   | 10.000/250       | 4 / 8,000  | 
| Standard_L16s  | 16   | 128  | 2,807 | 64   | 80.000 / 800   | 20.000/500       | 8 / 16000 | 
| Standard_L32s <sup>1</sup> | 32   | 256  | 5,630 | 64   | 160,000 / 1,600   | 40.000/1.000     | 8 / 20,000 | 
 

La massima velocità effettiva del disco possibile con le macchine virtuali serie Ls può essere limitata dal numero, dalle dimensioni e dallo striping dei dischi collegati. Per altre informazioni, vedere [Archiviazione Premium: archiviazione ad alte prestazioni per carichi di lavoro delle macchine virtuali di Azure](../articles/virtual-machines/windows/premium-storage.md).

<sup>1</sup> L'istanza è isolata e prevede hardware dedicato per un singolo cliente.

## <a name="size-table-definitions"></a>Definizioni delle tabelle delle dimensioni

- La capacità di archiviazione viene visualizzata in unità di GiB o 1.024^3 byte. Quando si confrontano dischi misurati in GB (1.000^3 byte) con dischi misurati in GiB (1.024^3), tenere presente che i valori di capacità specificati in GiB potrebbero apparire inferiori. Ad esempio, 1.023 GiB = 1.098,4 GB
- La velocità effettiva del disco viene misurata in operazioni di input/output al secondo (IOPS) e MBps, dove il valore di MBps corrisponde a 10^6 byte al secondo.
- Se si vogliono ottenere prestazioni ottimali per le macchine virtuali, è necessario limitare il numero di dischi dati a 2 per ogni vCPU.
- La **larghezza di banda della rete prevista** è la [larghezza di banda aggregata massima allocata per ogni tipo di VM](../articles/virtual-network/virtual-machine-network-throughput.md) in tutte le schede di interfaccia di rete, per tutte le destinazioni. I limiti massimi non sono garantiti, ma hanno lo scopo di fornire indicazioni per la selezione del tipo di VM corretto per l'applicazione desiderata. Le prestazioni di rete effettive dipenderanno da svariati fattori, tra cui congestione della rete, carichi dell'applicazione e impostazioni di rete. Per informazioni sull'ottimizzazione della velocità effettiva della rete, vedere [Ottimizzazione della velocità effettiva di rete per Windows e Linux](../articles/virtual-network/virtual-network-optimize-network-bandwidth.md). Per realizzare le prestazioni di rete previste in Linux o Windows, potrebbe essere necessario selezionare una versione specifica o ottimizzare la VM. Per altre informazioni, vedere [Come eseguire test affidabili della velocità effettiva della macchina virtuale](../articles/virtual-network/virtual-network-bandwidth-testing.md).
