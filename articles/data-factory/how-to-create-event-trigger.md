---
title: Creare trigger basati su eventi in Azure Data Factory | Microsoft Docs
description: Informazioni su come creare un trigger in Azure Data Factory per l'esecuzione di una pipeline in risposta a un evento.
services: data-factory
documentationcenter: ''
author: douglaslMS
manager: craigg
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: conceptual
ms.date: 07/23/2018
ms.author: douglasl
ms.openlocfilehash: 38fbb62de60bc5604210c8ad7339368a04967c27
ms.sourcegitcommit: 0bb8db9fe3369ee90f4a5973a69c26bff43eae00
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 10/08/2018
ms.locfileid: "48867053"
---
# <a name="create-a-trigger-that-runs-a-pipeline-in-response-to-an-event"></a>Creare un trigger che esegue una pipeline in risposta a un evento

Questo articolo descrive i trigger basati su eventi che è possibile creare nelle pipeline di Data Factory.

Un'architettura guidata dagli eventi è un comune modello di integrazione dei dati che implica produzione, rilevamento, utilizzo e risposta agli eventi. Negli scenari di integrazione dei dati è spesso necessario che i clienti di Data Factory attivino pipeline in base agli eventi. Data Factory è ora integrato con [Griglia di eventi di Azure](https://azure.microsoft.com/services/event-grid/), che consente di attivare pipeline su un evento.

Per un'introduzione di dieci minuti e una dimostrazione di questa funzionalità, guardare il video seguente:

> [!VIDEO https://channel9.msdn.com/Shows/Azure-Friday/Event-based-data-integration-with-Azure-Data-Factory/player]


> [!NOTE]
> L'integrazione descritta in questo articolo dipende dalla [Griglia di eventi di Azure](https://azure.microsoft.com/services/event-grid/). Verificare che la sottoscrizione sia registrata con il provider di risorse di Griglia di eventi. Per altre informazioni, vedere [Provider e tipi di risorse](../azure-resource-manager/resource-manager-supported-services.md#portal).

## <a name="data-factory-ui"></a>Interfaccia utente di Data Factory

### <a name="create-a-new-event-trigger"></a>Creare un nuovo trigger di evento

Un tipico evento è costituito dall'arrivo di un file o dall'eliminazione di un file nell'account di archiviazione di Azure. È possibile creare un trigger che risponde a questo evento nella pipeline di Data Factory.

> [!NOTE]
> Questa integrazione supporta solo gli account di archiviazione della versione 2 (utilizzo generico).

![Creare un nuovo trigger di evento](media/how-to-create-event-trigger/event-based-trigger-image1.png)

### <a name="configure-the-event-trigger"></a>Configurare il trigger di evento

Con le proprietà **Percorso BLOB inizia con** e **Percorso BLOB termina con** è possibile specificare i contenitori, le cartelle e i nomi di BLOB per cui si vuole ricevere eventi. È possibile usare svariati modelli per le due proprietà **Percorso BLOB inizia con** e **Percorso BLOB termina con**, come mostrato negli esempi più avanti in questo articolo. Almeno una di queste due proprietà è obbligatoria.

![Configurare il trigger di evento](media/how-to-create-event-trigger/event-based-trigger-image2.png)

### <a name="select-the-event-trigger-type"></a>Selezionare il tipo di trigger di evento

Non appena il file arriva nel percorso di archiviazione e viene creato il BLOB corrispondente, questo evento attiva ed esegue la pipeline di Data Factory. È possibile creare un trigger che risponde a un evento di creazione di BLOB, a un evento di eliminazione di BLOB oppure a entrambi nelle pipeline di Data Factory.

![Selezionare il tipo di trigger come evento](media/how-to-create-event-trigger/event-based-trigger-image3.png)

### <a name="map-trigger-properties-to-pipeline-parameters"></a>Eseguire il mapping di proprietà di un trigger ai parametri della pipeline

Quando un trigger di evento viene generato per un blob specifico, l'evento acquisisce il nome file e il percorso della cartella del blob nelle proprietà `@triggerBody().folderPath` e `@triggerBody().fileName`. Per usare i valori di queste proprietà in una pipeline, è necessario mappare le proprietà per i parametri della pipeline. Dopo il mapping delle proprietà per i parametri, è possibile accedere ai valori acquisiti dal trigger attraverso l'espressione `@pipeline().parameters.parameterName` attraverso la pipeline.

![Mapping di proprietà di un trigger ai parametri della pipeline](media/how-to-create-event-trigger/event-based-trigger-image4.png)

Ad esempio, nella schermata precedente. il trigger viene configurato per essere attivato quando viene creato un percorso blob che termina con `.csv` nell'Account di archiviazione. Di conseguenza, quando un blob con estensione `.csv` viene creato in un punto qualsiasi nell'Account di archiviazione, le proprietà `folderPath` e `fileName` acquisiscono la posizione del nuovo blob. Ad esempio, `@triggerBody().folderPath` ha un valore pari a `/containername/foldername/nestedfoldername` e `@triggerBody().fileName` ha un valore pari a `filename.csv`. Il mapping di questi valori viene eseguito secondo i parametri della pipeline `sourceFolder` e `sourceFile`. È possibile usarli attraverso tutta la pipeline come `@pipeline().parameters.sourceFolder` e `@pipeline().parameters.sourceFile` rispettivamente.

## <a name="json-schema"></a>Schema JSON

La tabella seguente offre una panoramica degli elementi dello schema correlati ai trigger basati su elenchi:

| **Elemento JSON** | **Descrizione** | **Tipo** | **Valori consentiti** | **Obbligatorio** |
| ---------------- | --------------- | -------- | ------------------ | ------------ |
| **scope** | ID risorsa di Azure Resource Manager dell'account di archiviazione. | string | ID Azure Resource Manager | Yes |
| **eventi** | Tipo di eventi che provocano l'attivazione del trigger. | Array    | Microsoft.Storage.BlobCreated, Microsoft.Storage.BlobDeleted | Sì, qualsiasi combinazione. |
| **blobPathBeginsWith** | Il percorso del BLOB deve iniziare con il modello fornito per l'attivazione del trigger. Ad esempio, '/records/blobs/december/' attiva solo il trigger per i BLOB nella cartella december all'interno del contenitore records. | string   | | È necessario specificare almeno una di queste proprietà: blobPathBeginsWith, blobPathEndsWith. |
| **blobPathEndsWith** | Il percorso del BLOB deve terminare con il modello fornito per l'attivazione del trigger. Ad esempio, 'december/boxes.csv' attiva solo il trigger per i BLOB denominati boxes in una cartella december. | string   | | È necessario specificare almeno una di queste proprietà: blobPathBeginsWith, blobPathEndsWith. |

## <a name="examples-of-event-based-triggers"></a>Esempi di trigger basati su eventi

Questa sezione contiene alcuni esempi di impostazioni di trigger basati su eventi.

-   **Percorso BLOB inizia con**('/nomecontenitore/'): riceve gli eventi per qualsiasi BLOB nel contenitore.
-   **Il percorso BLOB inizia con**("/nomecontenitore/blobs/nomecartella"): riceve gli eventi per tutti i BLOB nel contenitore nomecontenitore e nella cartella nomecartella.
-   **Il percorso BLOB inizia con**("/nomecontenitore/blobs/nomecartella/file.txt"): riceve gli eventi per un BLOB denominato file.txt nella cartella nomecartella all'interno del contenitore nomecontenitore.
-   **Percorso BLOB termina con**('file.txt'): riceve gli eventi per un BLOB denominato file.txt in qualsiasi percorso.
-   **Il percorso BLOB termina con**("/nomecontenitore/blobs/file.txt"): riceve gli eventi per un BLOB denominato file.txt nel contenitore nomecontenitore.
-   **Percorso BLOB termina con**('nomecartella/file.txt'): riceve gli eventi per un BLOB denominato file.txt nella cartella nomecartella all'interno di qualsiasi contenitore.

> [!NOTE]
> È necessario includere il segmento `/blobs/` del percorso ogni volta che si specifica il contenitore e la cartella, il contenitore e il file o il contenitore, la cartella e il file.

## <a name="next-steps"></a>Passaggi successivi
Per informazioni dettagliate sui trigger, vedere [Esecuzione e trigger di pipeline](concepts-pipeline-execution-triggers.md#triggers).
