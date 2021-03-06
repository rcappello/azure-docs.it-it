---
title: Ciclo di vita di sviluppo di una knowledge base - QnA Maker
titleSuffix: Azure Cognitive Services
description: QnA Maker apprende meglio in un ciclo iterativo di modifiche ai modelli, esempi di espressioni, pubblicazione e raccolta dei dati dalle query degli endpoint.
services: cognitive-services
author: tulasim88
manager: cgronlun
ms.service: cognitive-services
ms.component: qna-maker
ms.topic: article
ms.date: 09/12/2018
ms.author: tulasim
ms.openlocfilehash: 5af829b3355c6d68bace959b66f9511877d08b83
ms.sourcegitcommit: 4ecc62198f299fc215c49e38bca81f7eb62cdef3
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 09/24/2018
ms.locfileid: "47040915"
---
# <a name="knowledge-base-lifecycle"></a>Ciclo di vita della knowledge base
QnA Maker apprende meglio in un ciclo iterativo di modifiche ai modelli, esempi di espressioni, pubblicazione e raccolta dei dati dalle query degli endpoint. 

![Ciclo di creazione](../media/qnamaker-concepts-lifecycle/kb-lifecycle.png)

## <a name="creating-a-qna-maker-knowledge-base"></a>Creazione di una knowledge base di QnA Maker
L'endpoint della knowledge base (KB) di QnA Maker fornisce una risposta scelta in base alla corrispondenza migliore per una query utente basata sul contenuto della KB. La creazione di una knowledge base è un'operazione occasionale di configurazione di un repository di contenuti con domande, risposte e i metadati associati. È possibile creare una knowledge effettuando una ricerca per indicizzazione nel contenuto pre-esistente, ad esempio pagine di domande frequenti, manuali di prodotti o coppie strutturate di domande e risposte. Leggere le informazioni su come [creare una knowledge base](../How-To/create-knowledge-base.md).

## <a name="testing-and-updating-the-knowledge-base"></a>Test e aggiornamento della knowledge base
La knowledge base è pronta per i test dopo essere stata popolata con il contenuto, a livello editoriale o tramite estrazione automatica. I test possono essere eseguiti tramite il pannello **Test** immettendo query utente comuni e verificando che le risposte restituite siano quelle previste e abbiano un punteggio di attendibilità sufficiente. È possibile aggiungere domande alternative per correggere eventuali problemi di punteggio di attendibilità basso. È anche possibile aggiungere nuove risposte quando una query restituisce la risposta predefinita che indica che non è stata trovata nessuna corrispondenza nella KB. Questo ciclo serrato di test-aggiornamento continua finché non si è soddisfatti dei risultati. Leggere le informazioni su come [testare la knowledge base](../How-To/test-knowledge-base.md).

Per KB di grandi dimensioni, i test possono essere automatizzati tramite le API generateAnswer. 

## <a name="publish-the-knowledge-base"></a>Pubblicare la knowledge base
Una volta testata la knowledge base, è possibile pubblicarla. La pubblicazione inserisce la versione più recente della knowledge base testata in un indice di Ricerca di Azure dedicato che rappresenta la knowledge base **pubblicata**. Viene inoltre creato un endpoint che può essere chiamato nell'applicazione o nel chat bot.

In questo modo, eventuali modifiche apportate alla versione di test della knowledge base non influiscono sulla versione pubblicata, che potrebbe essere in uso in un'applicazione di produzione.

Ognuna di queste knowledge base può essere scelta come destinazione per i test separatamente. Usando le API, è possibile scegliere come destinazione la versione di test della knowledge base con il flag `isTest=true` nella chiamata generateAnswer.

Leggere le informazioni su come [pubblicare la knowledge base](../How-To/publish-knowledge-base.md).

## <a name="monitor-usage"></a>Monitorare l'utilizzo
Per poter registrare i log di chat del servizio, è necessario abilitare Application Insights quando si [crea un servizio QnA Maker](../How-To/set-up-qnamaker-service-azure.md).

È possibile ottenere diverse analisi relative all'utilizzo del servizio. Leggere altre informazioni su come usare Application Insights per ottenere [analisi per il servizio QnA Maker](../How-To/get-analytics-knowledge-base.md).

In base alle informazioni ottenute dall'analisi, apportare [aggiornamenti alla knowledge base](../How-To/edit-knowledge-base.md) come appropriato.

## <a name="next-steps"></a>Passaggi successivi

> [!div class="nextstepaction"]
> [Punteggio di attendibilità](./confidence-score.md)

## <a name="see-also"></a>Vedere anche  

[Knowledge base](./knowledge-base.md)
[Panoramica di QnA Maker](../Overview/overview.md)
