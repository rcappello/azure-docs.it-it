---
title: Esportazione ed eliminazione dei dati dei clienti - Language Understanding - LUIS
titleSuffix: Azure Cognitive Services
description: Language Understanding Intelligent Service (LUIS) conserva i contenuti dei clienti per consentire il funzionamento del servizio, ma l'utente LUIS ha il controllo completo su visualizzazione, esportazione ed eliminazione dei propri dati. A tale scopo, sono disponibili il portale Web LUIS o le API programmatiche LUIS.
services: cognitive-services
author: diberry
manager: cgronlun
ms.service: cognitive-services
ms.component: language-understanding
ms.topic: conceptual
ms.date: 09/10/2018
ms.author: diberry
ms.openlocfilehash: bfd168d5c56bc800831c402a23bb1a506fa15221
ms.sourcegitcommit: 55952b90dc3935a8ea8baeaae9692dbb9bedb47f
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 10/09/2018
ms.locfileid: "48883891"
---
# <a name="export-and-delete-your-customer-data-in-language-understanding-luis-in-cognitive-services"></a>Esportare ed eliminare i dati dei clienti in Language Understanding (LUIS) in Servizi cognitivi

## <a name="summary-of-customer-data-request-features"></a>Riepilogo delle funzionalità di richiesta dei dati dei clienti
Language Understanding Intelligent Service (LUIS) conserva i contenuti dei clienti per consentire il funzionamento del servizio, ma l'utente LUIS ha il controllo completo su visualizzazione, esportazione ed eliminazione dei propri dati. A tale scopo, sono disponibili il [portale](luis-reference-regions.md) Web LUIS o le [API programmatiche LUIS](https://westus.dev.cognitive.microsoft.com/docs/services/5890b47c39e2bb17b84a55ff/operations/5890b47c39e2bb052c5b9c2f).

[!INCLUDE [GDPR-related guidance](../../../includes/gdpr-intro-sentence.md)]

I contenuti dei clienti vengono archiviati e crittografati in archivi Azure a livello di area di Microsoft e includono:

- Contenuti degli account utente raccolti al momento della registrazione
- Dati di training necessari per compilare i modelli (ovvero finalità ed entità)
- Query degli utenti registrate in fase di esecuzione per consentire di migliorare i modelli utente
  - Gli utenti possono disattivare la registrazione delle query aggiungendo `&log=false` alla richiesta. Informazioni dettagliate sono disponibili [qui](luis-resources-faq.md#how-can-i-disable-the-logging-of-utterances)

## <a name="deleting-customer-data"></a>Eliminazione dei dati dei clienti
Gli utenti LUIS hanno il controllo completo per l'eliminazione di qualsiasi contenuto utente, tramite il portale Web LUIS o le API programmatiche LUIS. Nella tabella seguente sono disponibili i collegamenti per entrambe le opzioni:

| | **Account utente** | **Applicazione** | **Espressione/i** | **Query utente finale** |
| --- | --- | --- | --- | --- |
| **Portale** | [Collegamento](luis-how-to-account-settings.md) | [Collegamento](luis-how-to-start-new-app.md#delete-app) | [Collegamento](luis-how-to-start-new-app.md#delete-app) | [Collegamento](luis-how-to-start-new-app.md#delete-app) |
| **API** | [Collegamento](https://westus.dev.cognitive.microsoft.com/docs/services/5890b47c39e2bb17b84a55ff/operations/5890b47c39e2bb052c5b9c4c) | [Collegamento](https://westus.dev.cognitive.microsoft.com/docs/services/5890b47c39e2bb17b84a55ff/operations/5890b47c39e2bb052c5b9c39) | [Collegamento](https://westus.dev.cognitive.microsoft.com/docs/services/5890b47c39e2bb17b84a55ff/operations/5890b47c39e2bb052c5b9c0b) | [Collegamento](https://westus.dev.cognitive.microsoft.com/docs/services/5890b47c39e2bb17b84a55ff/operations/58b6f32139e2bb139ce823c9) |


## <a name="exporting-customer-data"></a>Esportazione dei dati dei clienti
Gli utenti LUIS hanno il controllo completo per la visualizzazione dei dati nel portale, che tuttavia devono essere esportati tramite le API programmatiche LUIS. Nella tabella seguente sono disponibili i collegamenti relativi all'esportazione dei dati tramite le API programmatiche LUIS:

| | **Account utente** | **Applicazione** | **Espressione/i** | **Query utente finale** |
| --- | --- | --- | --- | --- |
| **API** | [Collegamento](https://westus.dev.cognitive.microsoft.com/docs/services/5890b47c39e2bb17b84a55ff/operations/5890b47c39e2bb052c5b9c48) | [Collegamento](https://westus.dev.cognitive.microsoft.com/docs/services/5890b47c39e2bb17b84a55ff/operations/5890b47c39e2bb052c5b9c40) | [Collegamento](https://westus.dev.cognitive.microsoft.com/docs/services/5890b47c39e2bb17b84a55ff/operations/5890b47c39e2bb052c5b9c0a) | [Collegamento](https://westus.dev.cognitive.microsoft.com/docs/services/5890b47c39e2bb17b84a55ff/operations/5890b47c39e2bb052c5b9c36) |


## <a name="next-steps"></a>Passaggi successivi

> [!div class="nextstepaction"]
> [Informazioni di riferimento sulle aree di LUIS](./luis-reference-regions.md)
