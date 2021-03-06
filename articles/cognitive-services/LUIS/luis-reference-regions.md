---
title: Regioni ed endpoint di pubblicazione - LUIS
titleSuffix: Azure Cognitive Services
description: La regione in cui si pubblica l'app LUIS corrisponde alla regione o alla posizione specificata nel portale di Azure quando si crea una chiave endpoint LUIS di Azure. Quando si pubblica un'app, LUIS genera automaticamente un URL endpoint per la regione associata alla chiave. Per pubblicare un'app LUIS in più regioni, è necessaria almeno una chiave per regione.
services: cognitive-services
author: diberry
manager: cgronlun
ms.service: cognitive-services
ms.component: language-understanding
ms.topic: article
ms.date: 09/11/2018
ms.author: diberry
ms.openlocfilehash: 205a17a985986aab8039afe824e7e872a9885169
ms.sourcegitcommit: 4ecc62198f299fc215c49e38bca81f7eb62cdef3
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 09/24/2018
ms.locfileid: "47039412"
---
# <a name="regions-and-keys"></a>Regioni e chiavi

La regione in cui si pubblica l'app LUIS corrisponde alla regione o alla posizione specificata nel portale di Azure quando si crea una chiave endpoint LUIS di Azure. Quando si [pubblica un'app](./luis-how-to-publish-app.md), LUIS genera automaticamente un URL endpoint per la regione associata alla chiave. Per pubblicare un'app LUIS in più regioni, è necessaria almeno una chiave per regione. 

## <a name="luis-website"></a>Sito Web LUIS
Esistono tre siti Web LUIS, in base alla regione. La creazione e la pubblicazione devono avvenire nella stessa regione. 

|LUIS|Region|
|--|--|
|[www.luis.ai][www.luis.ai]|Dati<br>non Europa<br>non Australia|
|[au.luis.ai][au.luis.ai]|Australia|
|[au.luis.ai][eu.luis.ai]|Europa|

## <a name="regions-and-azure-resources"></a>Regioni e risorse di Azure
L'app è pubblicata in tutte le regioni associate alle risorse LUIS aggiunte nel portale di LUIS. Ad esempio, per un'app creata su [www.luis.ai][www.luis.ai], se si crea una risorsa di LUIS in **westus** e la si aggiunge all'app come risorsa, l'app sarà pubblicata in tale regione. 

## <a name="public-apps"></a>App pubbliche
Un'app pubblica viene pubblicata in tutte le regioni in modo che un utente con una chiave di risorsa LUIS basata su regione possa accedere all'app in qualsiasi regione associata la propria chiave di risorsa.

## <a name="publishing-regions"></a>Regioni di pubblicazione

Le app LUIS create in https://www.luis.ai possono essere pubblicate in tutti gli endpoint, ad eccezione delle regioni [europea](#publishing-to-europe) e [australiana](#publishing-to-australia). 

L'app della regione di creazione può essere pubblicata solo in una regione di pubblicazione corrispondente. Se l'app si trova nella regione di creazione errata, esportarla e importarla nella regione di creazione corretta per la regione di pubblicazione. 

 Regione globale | Regione di creazione<br>`API region name` | Regione di pubblicazione e query<br>`API region name`   |   Sito Web LUIS | Formato URL endpoint   |
|-----|------|------|------|------|
| Asia | Stati Uniti occidentali<br>`westus`| Asia orientale<br>`eastasia`     | [www.luis.ai][www.luis.ai] |  https://eastasia.api.cognitive.microsoft.com/luis/v2.0/apps/YOUR-APP-ID?subscription-key=YOUR-SUBSCRIPTION-KEY   |
| Asia | Stati Uniti occidentali<br>`westus`| Asia sud-orientale<br>`souteastasia`     | [www.luis.ai][www.luis.ai] |   https://southeastasia.api.cognitive.microsoft.com/luis/v2.0/apps/YOUR-APP-ID?subscription-key=YOUR-SUBSCRIPTION-KEY   |
| *[Australia](#publishing-to-australia) | Australia orientale<br>`australiaeast`| Australia orientale<br>`australiaeast`     |   [au.luis.ai][au.luis.ai] | https://australiaeast.api.cognitive.microsoft.com/luis/v2.0/apps/YOUR-APP-ID?subscription-key=YOUR-SUBSCRIPTION-KEY   |
| *[Europa](#publishing-to-europe)| Europa occidentale<br>`westeurope`| Europa settentrionale<br>`northeurope`     | [au.luis.ai][eu.luis.ai]|  https://northeurope.api.cognitive.microsoft.com/luis/v2.0/apps/YOUR-APP-ID?subscription-key=YOUR-SUBSCRIPTION-KEY   | 
| *[Europa](#publishing-to-europe) | Europa occidentale<br>`westeurope`| Europa occidentale<br>`westeurope`     | [au.luis.ai][eu.luis.ai]|  https://westeurope.api.cognitive.microsoft.com/luis/v2.0/apps/YOUR-APP-ID?subscription-key=YOUR-SUBSCRIPTION-KEY   | 
| America del Nord | Stati Uniti occidentali<br>`westus` | Stati Uniti orientali<br>`eastus`      |[www.luis.ai][www.luis.ai] |   https://eastus.api.cognitive.microsoft.com/luis/v2.0/apps/YOUR-APP-ID?subscription-key=YOUR-SUBSCRIPTION-KEY   |
| America del Nord | Stati Uniti occidentali<br>`westus` | Stati Uniti orientali 2<br>`eastus2`     | [www.luis.ai][www.luis.ai] |  https://eastus2.api.cognitive.microsoft.com/luis/v2.0/apps/YOUR-APP-ID?subscription-key=YOUR-SUBSCRIPTION-KEY   |
| America del Nord | Stati Uniti occidentali<br>`westus` | Stati Uniti centro-meridionali<br>`southcentralus`     | [www.luis.ai][www.luis.ai] |  https://southcentralus.api.cognitive.microsoft.com/luis/v2.0/apps/YOUR-APP-ID?subscription-key=YOUR-SUBSCRIPTION-KEY   | 
| America del Nord | Stati Uniti occidentali<br>`westus` | Stati Uniti centro-occidentali<br>`westcentralus`     |[www.luis.ai][www.luis.ai] |  https://westcentralus.api.cognitive.microsoft.com/luis/v2.0/apps/YOUR-APP-ID?subscription-key=YOUR-SUBSCRIPTION-KEY   |
| America del Nord | Stati Uniti occidentali<br>`westus` | Stati Uniti occidentali<br>`westus`  |  [www.luis.ai][www.luis.ai] | https://westus.api.cognitive.microsoft.com/luis/v2.0/apps/YOUR-APP-ID?subscription-key=YOUR-SUBSCRIPTION-KEY  |
| America del Nord | Stati Uniti occidentali<br>`westus` | Stati Uniti occidentali 2<br>`westus2`    | [www.luis.ai][www.luis.ai] |  https://westus2.api.cognitive.microsoft.com/luis/v2.0/apps/YOUR-APP-ID?subscription-key=YOUR-SUBSCRIPTION-KEY  |
| America del Sud | Stati Uniti occidentali<br>`westus` | Brasile meridionale<br>`brazilsouth`     | [www.luis.ai][www.luis.ai] |  https://brazilsouth.api.cognitive.microsoft.com/luis/v2.0/apps/YOUR-APP-ID?subscription-key=YOUR-SUBSCRIPTION-KEY   |

## <a name="publishing-to-europe"></a>Pubblicazione in Europa

Per pubblicare nelle regioni europee, creare le app LUIS solo in https://eu.luis.ai. Se si tenta di pubblicare in qualsiasi altra regione usando una chiave nella regione europea, viene visualizzato un messaggio di avviso. Usare invece https://eu.luis.ai. Le app LUIS create in [https://eu.luis.ai][eu.luis.ai] non vengono migrate automaticamente in altre regioni. Esportare e importare l'app LUIS per eseguirne la migrazione.

## <a name="publishing-to-australia"></a>Pubblicazione in Australia

Per pubblicare nelle regioni australiane, creare le app LUIS solo in https://au.luis.ai. Se si tenta di pubblicare in qualsiasi altra regione usando una chiave nella regione australiana, viene visualizzato un messaggio di avviso. Usare invece https://au.luis.ai. Le app LUIS create in [https://au.luis.ai][au.luis.ai] non vengono migrate automaticamente in altre regioni. Esportare e importare l'app LUIS per eseguirne la migrazione.

## <a name="endpoints"></a>Endpoint

LUIS dispone attualmente di 2 endpoint: uno per la creazione e uno per l'analisi del testo.

|Scopo|URL|
|--|--|
|Creazione|`https://{region}.api.cognitive.microsoft.com/luis/api/v2.0/apps/{appID}/`|
|Analisi del testo (query di stima)|`https://{region}.api.cognitive.microsoft.com/luis/v2.0/apps/{appId}?q={q}[&timezoneOffset][&verbose][&spellCheck][&staging][&bing-spell-check-subscription-key][&log]`|

La tabella seguente illustra i parametri indicati con parentesi graffe `{}` nella tabella precedente.

|Parametro|Scopo|
|--|--|
|region|Area di Azure - per la creazione e la pubblicazione sono disponibili aree diverse|
|appID|ID dell'app LUIS usato nella route dell'URL e disponibile nel dashboard dell'app|
|q|testo dell'espressione inviato dall'applicazione client, ad esempio chatbot|


## <a name="next-steps"></a>Passaggi successivi

> [!div class="nextstepaction"]
> [Riferimento a entità predefinite](./luis-reference-prebuilt-entities.md)

 [www.luis.ai]: https://www.luis.ai
 [au.luis.ai]: https://au.luis.ai
 [eu.luis.ai]: https://eu.luis.ai