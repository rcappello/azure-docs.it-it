---
title: Come sfogliare i video disponibili - Ricerca video Bing
titlesuffix: Azure Cognitive Services
description: Illustra come sfogliare tutti i video che possono essere restituiti da Bing.
services: cognitive-services
author: swhite-msft
manager: cgronlun
ms.service: cognitive-services
ms.component: bing-video-search
ms.topic: conceptual
ms.date: 04/15/2017
ms.author: scottwhi
ms.openlocfilehash: 9b030312c562d1c0a6cbacfc7f424289dee2e8de
ms.sourcegitcommit: ad08b2db50d63c8f550575d2e7bb9a0852efb12f
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 09/26/2018
ms.locfileid: "47225566"
---
# <a name="paging-videos"></a>Sfogliare i video

Quando si chiama l'API Ricerca video, Bing restituisce un elenco di risultati. L'elenco è un subset del numero totale di risultati pertinenti alla query. Per ottenere il numero totale stimato di risultati disponibili, accedere al campo [totalEstimatedMatches](https://docs.microsoft.com/rest/api/cognitiveservices/bing-video-api-v7-reference#videos-totalestimatedmatches) dell'oggetto risposta.  
  
L'esempio seguente illustra il campo `totalEstimatedMatches` incluso in una risposta Video.  
  
```  
{
    "_type" : "Videos",
    "webSearchUrl" : "https:\/\/www.bing.com\/cr?IG=81EF7545D56...",
    "totalEstimatedMatches" : 1000,
    "value" : [...]
}  
```  
  
Per sfogliare tutti i video disponibili, usare i parametri di query [count](https://docs.microsoft.com/rest/api/cognitiveservices/bing-video-api-v7-reference#count) e [offset](https://docs.microsoft.com/rest/api/cognitiveservices/bing-video-api-v7-reference#offset).  
  
Il parametro `count` specifica il numero di risultati da restituire nella risposta. Il numero massimo di risultati che è possibile richiedere nella risposta è 105. Il valore predefinito è 35. Il numero effettivo restituito può essere inferiore a quello richiesto.

Il parametro `offset` specifica il numero di risultati da ignorare. `offset` è in base zero e deve essere inferiore a (`totalEstimatedMatches` - `count`).  
  
Per visualizzare 20 video per pagina, impostare `count` su 20 e `offset` su 0 per ottenere la prima pagina di risultati. Per ogni pagina successiva, aumentare `offset` di 20 (ad esempio, 20, 40).  

Di seguito viene illustrato un esempio che richiede 20 video che iniziano in corrispondenza dell'offset 40.  
  
```  
GET https://api.cognitive.microsoft.com/bing/v7.0/videos/search?q=sailing+dinghies&count=20&offset=40&mkt=en-us HTTP/1.1  
Ocp-Apim-Subscription-Key: 123456789ABCDE  
Host: api.cognitive.microsoft.com  
```  

Se il valore predefinito di `count` risulta appropriato per l'implementazione, è sufficiente specificare il parametro di query `offset`.  
  
```  
GET https://api.cognitive.microsoft.com/bing/v7.0/videos/search?q=sailing+dinghies&offset=40&mkt=en-us HTTP/1.1  
Ocp-Apim-Subscription-Key: 123456789ABCDE  
Host: api.cognitive.microsoft.com  
```  

In genere, restituendo una pagina di 35 video per volta, il parametro di query `offset` viene impostato su 0 nella prima richiesta e quindi `offset` viene incrementato di 35 in ogni richiesta successiva. Tuttavia, alcuni dei risultati nella risposta successiva potrebbero essere duplicati della risposta precedente. Ad esempio, i primi due video nella risposta possono essere gli stessi ultimi due video della risposta precedente.

Per eliminare i risultati duplicati, usare il campo [nextOffset](https://docs.microsoft.com/rest/api/cognitiveservices/bing-video-api-v7-reference#videos-nextoffset) dell'oggetto `Videos`.

Se ad esempio si vuole restituire una pagina di 30 video per volta, impostare `count` su 30 e `offset` su 0 nella prima richiesta. Nella richiesta successiva sarà sufficiente impostare il parametro di query `offset` sul valore `nextOffset`.


> [!NOTE]
> Il paging si applica solo alla ricerca di video (/videos/search) e non alle informazioni dettagliate sui video (/videos/details) o ai video di tendenza (/videos/trending).