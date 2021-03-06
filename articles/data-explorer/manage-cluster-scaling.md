---
title: Ridimensionamento di un cluster di Esplora dati di Azure per rispondere al cambiamento della domanda
description: Questo articolo descrive la procedura per aumentare e ridurre il numero di istanze di un cluster di Esplora dati di Azure in base al cambiamento della domanda.
author: orspod
ms.author: v-orspod
ms.reviewer: mblythe
ms.service: data-explorer
services: data-explorer
ms.topic: conceptual
ms.date: 09/24/2018
ms.openlocfilehash: 59a6a94e2906413423a4ae03a7c1c115b2ec0cc0
ms.sourcegitcommit: 4ecc62198f299fc215c49e38bca81f7eb62cdef3
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 09/24/2018
ms.locfileid: "47046164"
---
# <a name="manage-cluster-scaling-to-accommodate-changing-demand"></a>Gestire il ridimensionamento di un cluster per rispondere al cambiamento della domanda

Ridimensionare un cluster in modo appropriato è fondamentale per garantire le prestazioni di Esplora dati di Azure. Ma in un cluster non è possibile prevedere la domanda con un'accuratezza del 100%. La scelta di dimensioni statiche per un cluster può portare al suo sottoutilizzo o sovrautilizzo e nessuna delle due condizioni è ideale. Un approccio migliore consiste nel *ridimensionare* il cluster, aumentandone o diminuendone la capacità in base al cambiamento della domanda. Questo articolo illustra come gestire il ridimensionamento di un cluster.

Passare al cluster e in **Impostazioni** selezionare **Scale out** (Aumenta istanze). In **Configura** selezionare **Abilita scalabilità automatica**.

![Abilitare il ridimensionamento automatico](media/manage-cluster-scaling/enable-autoscale.png)

La figura seguente mostra il flusso dei passaggi successivi. Sotto la figura sono disponibili maggiori dettagli.

![Regola di ridimensionamento](media/manage-cluster-scaling/scale-rule.png)

1. In **Nome impostazione di scalabilità automatica** specificare un nome, ad esempio *Scale-out: cache utilization* (Scalabilità orizzontale: utilizzo della cache).

1. In **Modalità di ridimensionamento** selezionare **Ridimensiona in base a una metrica**. Questa modalità assicura la scalabilità dinamica. È anche possibile selezionare **Ridimensiona in base a un numero di istanze specifico**.

1. Selezionare **Aggiungi una regola**.

1. Nella sezione **Regola di ridimensionamento** sulla destra specificare i valori per ogni impostazione.

    | Impostazione | Descrizione e valore |
    | --- | --- | --- |
    | **Aggregazione temporale** | Selezionare un criterio di aggregazione, ad esempio **Media**. |
    | **Nome metrica** | Selezionare la metrica su cui si vuole basare l'operazione di ridimensionamento, ad esempio **Utilizzo della cache**. |
    | **Statistica intervallo di tempo** | Scegliere tra **Medio**, **Minimo**, **Massimo** e **Somma**. |
    | **Operatore** | Scegliere l'opzione appropriata, ad esempio **Maggiore o uguale a**. |
    | **Soglia** | Scegliere un valore appropriato. Ad esempio, per l'utilizzo della cache 80% è un buon punto di partenza. |
    | **Duration** | Scegliere un periodo di tempo appropriato da considerare per il calcolo delle metriche. Iniziare con il valore predefinito di dieci minuti. |
    | **Operazione** | Scegliere l'opzione appropriata per ridurre o aumentare il numero di istanze. |
    | **Numero di istanze** | Scegliere il numero di nodi o istanze da aggiungere o rimuovere quando viene soddisfatta una condizione di metrica. |
    | **Disattiva regole dopo (minuti)** | Scegliere un intervallo di tempo appropriato per l'attesa tra le operazioni di ridimensionamento. Iniziare con il valore predefinito di cinque minuti. |
    |  |  |

1. Selezionare **Aggiungi**.

1. Nella sezione **Limiti per le istanze** a sinistra specificare i valori per ogni impostazione.

    | Impostazione | Descrizione e valore |
    | --- | --- | --- |
    | *Minimi* | Numero di istanze al di sotto del quale non verrà effettuato il ridimensionamento del cluster, indipendentemente dall'utilizzo. |
    | *Massimo* | Numero di istanze al di sopra del quale non verrà effettuato il ridimensionamento del cluster, indipendentemente dall'utilizzo. |
    | *Default* | Numero predefinito di istanze, usato in caso di problemi durante la lettura delle metriche delle risorse. |
    |  |  |

1. Selezionare **Salva**.

È stata configurata un'operazione per aumentare il numero di istanze del cluster di Esplora dati di Azure. Aggiungere un'altra regola per configurare un'operazione per ridurne il numero. In questo modo il cluster può essere ridimensionato in modo dinamico in base alle metriche di utilizzo specificate.

Se occorre assistenza per problemi con il ridimensionamento di un cluster, aprire una richiesta di supporto nel [portale di Azure](https://portal.azure.com).