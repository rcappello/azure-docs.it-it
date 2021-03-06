---
title: Come sfogliare le immagini disponibili | Microsoft Docs
description: Illustra come sfogliare tutte le immagini che possono essere restituite da Bing.
services: cognitive-services
author: swhite-msft
manager: ehansen
ms.assetid: 3C8423F8-41E0-4F89-86B6-697E840610A7
ms.service: cognitive-services
ms.component: bing-image-search
ms.topic: article
ms.date: 04/15/2017
ms.author: scottwhi
ms.openlocfilehash: a74ee817e84be5bb563c5fdaf25afc1dc14732e5
ms.sourcegitcommit: 95d9a6acf29405a533db943b1688612980374272
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 06/23/2018
ms.locfileid: "35372745"
---
# <a name="paging-results"></a>Risultati di paging

Quando si chiama l'API Ricerca immagini, Bing restituisce un elenco di risultati. L'elenco è un subset del numero totale di risultati pertinenti alla query. Per ottenere il numero totale stimato di risultati disponibili, accedere al campo [totalEstimatedMatches](https://docs.microsoft.com/rest/api/cognitiveservices/bing-images-api-v7-reference#totalestimatedmatches) dell'oggetto risposta.  
  
L'esempio seguente illustra il campo `totalEstimatedMatches` incluso in una risposta Images.  
  
```json
{
    "_type" : "Images",
    "webSearchUrl" : "https:\/\/www.bing.com\/cr?IG=73118C8...",
    "totalEstimatedMatches" : 838,
    "value" : [...]  
}  
```  
  
Per sfogliare tutte le immagini disponibili, usare i parametri di query [count](https://docs.microsoft.com/rest/api/cognitiveservices/bing-images-api-v7-reference#count) e [offset](https://docs.microsoft.com/rest/api/cognitiveservices/bing-images-api-v7-reference#offset).  
  
Il parametro `count` specifica il numero di risultati da restituire nella risposta. Il numero massimo di risultati che è possibile richiedere nella risposta è 150. Il valore predefinito è 35. Il numero effettivo restituito può essere inferiore a quello richiesto.

Il parametro `offset` specifica il numero di risultati da ignorare. `offset` è in base zero e deve essere inferiore a (`totalEstimatedMatches` - `count`).  
  
Per visualizzare 20 immagini per pagina, impostare `count` su 20 e `offset` su 0 per ottenere la prima pagina di risultati. Di seguito viene illustrato un esempio che richiede 20 immagini che iniziano in corrispondenza dell'offset 40.  
  
```  
GET https://api.cognitive.microsoft.com/bing/v7.0/images/search?q=sailing+dinghies&count=20&offset=40&mkt=en-us HTTP/1.1  
Ocp-Apim-Subscription-Key: 123456789ABCDE  
Host: api.cognitive.microsoft.com  
```  

Se il valore predefinito di `count` risulta appropriato per l'implementazione, è sufficiente specificare il parametro di query `offset`.  
  
```  
GET https://api.cognitive.microsoft.com/bing/v7.0/images/search?q=sailing+dinghies&offset=40&mkt=en-us HTTP/1.1  
Ocp-Apim-Subscription-Key: 123456789ABCDE  
Host: api.cognitive.microsoft.com  
```  
  
Si potrebbe pensare che, restituendo una pagina di 35 immagini per volta, il parametro di query `offset` venga impostato su 0 nella prima richiesta e che quindi `offset` venga incrementato di 35 in ogni richiesta successiva. Tuttavia, alcuni dei risultati nella risposta successiva potrebbero essere duplicati della risposta precedente. Ad esempio, le prime due immagini nella risposta possono essere le stesse ultime due immagini della risposta precedente.

Per eliminare i risultati duplicati, usare il campo [nextOffset](https://docs.microsoft.com/rest/api/cognitiveservices/bing-images-api-v7-reference#nextoffset) dell'oggetto `Images`. Il campo `nextOffset` indica l'`offset` da usare per la richiesta successiva. Se ad esempio si vuole restituire una pagina di 30 immagini per volta, impostare `count` su 30 e `offset` su 0 nella prima richiesta. Nella richiesta successiva impostare `count` su 30 e `offset` sul valore dell'elemento `nextOffset` della risposta precedente. Per restituire una pagina di dati precedente, è consigliabile mantenere uno stack degli offset precedenti e prelevare il più recente.

> [!NOTE]
> Il paging si applica solo alla ricerca di immagini (/images/search) e non alle informazioni dettagliate sulle immagini o alle immagini di tendenza (/images/trending).