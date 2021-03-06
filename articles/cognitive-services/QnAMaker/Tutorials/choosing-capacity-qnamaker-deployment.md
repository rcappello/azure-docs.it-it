---
title: 'Capacità risorsa per la distribuzione: QnA Maker'
titleSuffix: Azure Cognitive Services
description: Guida alla scelta della capacità per la distribuzione di QnA Maker
services: cognitive-services
author: tulasim88
manager: cgronlun
ms.service: cognitive-services
ms.component: qna-maker
ms.topic: article
ms.date: 09/12/2018
ms.author: tulasim
ms.openlocfilehash: 582ace641cadbc7ad3a622def07f70ed51ccac53
ms.sourcegitcommit: f20e43e436bfeafd333da75754cd32d405903b07
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 10/17/2018
ms.locfileid: "49389803"
---
# <a name="choosing-capacity-for-your-qna-maker-deployment"></a>Scelta della capacità per la distribuzione di QnA Maker

Il servizio QnA Maker stabilisce una dipendenza da tre risorse di Azure:
1.  Servizio app (per il runtime)
2.  Ricerca di Azure (per l'archiviazione di domande e risposte)
3.  App Insights (facoltativo, per archiviare log di chat e dati di telemetria)

Prima di creare il servizio QnA Maker, è necessario stabilire quale livello dei servizi precedenti soddisfa le proprie esigenze. 

Ci sono generalmente tre parametri da considerare:
1. **La velocità effettiva che il servizio deve fornire**: scegliere il [piano app](https://azure.microsoft.com/pricing/details/app-service/plans/) appropriato per il servizio app in base alle proprie esigenze. È possibile [aumentare](https://docs.microsoft.com/azure/app-service/web-sites-scale) o ridurre le prestazioni dell'app. Ciò influenzerà anche la scelta dello SKU di Ricerca di Azure. Per altri dettagli, vedere [qui](https://docs.microsoft.com/azure/search/search-sku-tier).

2. **Dimensioni e numero di Knowledge Base**: scegliere lo [SKU di Ricerca di Azure](https://azure.microsoft.com/pricing/details/search/) appropriato per lo scenario. È possibile pubblicare N-1 Knowledge Base in un particolare livello, dove N è il numero massimo di indici consentiti nel livello. Verificare anche le dimensioni massime e il numero di documenti consentiti per ogni livello.

3. **Numero di documenti come origini**: lo SKU gratuito del servizio di gestione di QnA Maker limita a 3 (1 MB ciascuno) il numero di documenti gestibili tramite il portale e le API. Lo SKU Standard non pone limiti al numero di documenti gestibili. Per informazioni dettagliate, vedere [qui](https://aka.ms/qnamaker-pricing).

La tabella seguente indica alcune linee guida generali.

|                        | Gestione di QnA Maker | Servizio app | Ricerca di Azure | Limitazioni                      |
| ---------------------- | -------------------- | ----------- | ------------ | -------------------------------- |
| Sperimentazione        | SKU gratuito             | Livello gratuito   | Livello gratuito    | Pubblicazione di massimo 2 Knowledge Base, dimensioni 50 MB  |
| Ambiente di sviluppo/test   | SKU Standard         | Condiviso      | Basic        | Pubblicazione di massimo 14 Knowledge Base, dimensioni 2 GB    |
| Ambiente di produzione | SKU Standard         | Basic       | Standard     | Pubblicazione di massimo 49 Knowledge Base, dimensioni 25 GB |

Per l'aggiornamento dello stack di QnA Maker, vedere [Aggiornare il servizio QnA Maker](../How-To/upgrade-qnamaker-service.md).

## <a name="next-steps"></a>Passaggi successivi

> [!div class="nextstepaction"]
> [Aggiornare il servizio QnA Maker](../How-To/upgrade-qnamaker-service.md)
