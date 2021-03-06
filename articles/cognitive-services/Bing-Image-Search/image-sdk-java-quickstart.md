---
title: "Guida introduttiva: cercare immagini con l'SDK di Ricerca immagini Bing per Java"
description: Usare questa guida introduttiva per effettuare la prima ricerca di immagini tramite l'SDK di Ricerca immagini Bing, che consiste in un wrapper per l'API e contiene le stesse funzionalità. Questa semplice applicazione Java invia una query di ricerca di immagini, analizza la risposta JSON e visualizza l'URL della prima immagine restituita.
titleSuffix: Azure Cognitive Services
services: cognitive-services
author: aahill
manager: cgronlun
ms.service: cognitive-services
ms.component: bing-image-search
ms.topic: quickstart
ms.date: 08/28/2018
ms.author: aahi
ms.openlocfilehash: 36f59e1c405ef9e5cf69a19e49d69a3adfdc4636
ms.sourcegitcommit: cf606b01726df2c9c1789d851de326c873f4209a
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 09/19/2018
ms.locfileid: "46298184"
---
# <a name="quickstart-search-for-images-with-the-bing-image-search-sdk-and-java"></a>Guida introduttiva: cercare immagini con l'SDK di Ricerca immagini Bing e Java

Usare questa guida introduttiva per effettuare la prima ricerca di immagini tramite l'SDK di Ricerca immagini Bing, che consiste in un wrapper per l'API e contiene le stesse funzionalità. Questa semplice applicazione Java invia una query di ricerca di immagini, analizza la risposta JSON e visualizza l'URL della prima immagine restituita.

Il codice sorgente per questo esempio è disponibile in [GitHub](https://github.com/Azure-Samples/cognitive-services-java-sdk-samples/tree/master/Search/BingImageSearch/Quickstart) con annotazioni aggiuntive e altre informazioni sulla gestione degli errori.

## <a name="prerequisites"></a>Prerequisiti

La versione più recente di [Java Development Kit](http://www.oracle.com/technetwork/java/javase/downloads/index.html) (JDK)

Installare le dipendenze dell'SDK di Ricerca immagini Bing usando Maven, Gradle o un altro sistema di gestione delle dipendenze. Il file POM di Maven richiede la dichiarazione seguente:

```xml
 <dependencies>
    <dependency>
      <groupId>com.microsoft.azure.cognitiveservices</groupId>
      <artifactId>azure-cognitiveservices-imagesearch</artifactId>
      <version>0.0.1-beta-SNAPSHOT</version>
    </dependency>
 </dependencies>
```

[!INCLUDE [cognitive-services-bing-image-search-signup-requirements](../../../includes/cognitive-services-bing-image-search-signup-requirements.md)]

## <a name="create-and-initialize-the-application"></a>Creare e inizializzare l'applicazione

1. Creare un nuovo progetto Java nell'ambiente di sviluppo integrato o nell'editor preferito e aggiungere le importazioni seguenti all'implementazione della classe:

    ```java
    import com.microsoft.azure.cognitiveservices.search.imagesearch.BingImageSearchAPI;
    import com.microsoft.azure.cognitiveservices.search.imagesearch.BingImageSearchManager;
    import com.microsoft.azure.cognitiveservices.search.imagesearch.models.ImageObject;
    import com.microsoft.azure.cognitiveservices.search.imagesearch.models.ImagesModel;
    ```

2. Nel metodo principale creare variabili per la chiave di sottoscrizione e per il termine di ricerca. Creare quindi un'istanza del client di Ricerca immagini Bing.

    ```java
    final String subscriptionKey = "COPY_YOUR_KEY_HERE";
    String searchTerm = "canadian rockies";
    //Image search client
    BingImageSearchAPI client = BingImageSearchManager.authenticate(subscriptionKey);
    ```

## <a name="send-a-search-request-to-the-bing-image-search-api"></a>Inviare una richiesta di ricerca all'API Ricerca immagini Bing

1. Tramite `bingImages().search()`, inviare la richiesta HTTP contenente la query di ricerca. Salvare la risposta come `ImagesModel`.
    ```java
    ImagesModel imageResults = client.bingImages().search()
                .withQuery(searchTerm)
                .withMarket("en-us")
                .execute();
    ```

## <a name="parse-and-view-the-result"></a>Analizzare e visualizzare il risultato

Analizzare le immagini restituite nella risposta.
Se la risposta contiene i risultati della ricerca, archiviare il primo risultato e stamparne i dettagli, ad esempio l'URL di anteprima e l'URL originale, insieme al numero totale di immagini restituite.  

```java
if (imageResults != null && imageResults.value().size() > 0) {
    // Image results
    ImageObject firstImageResult = imageResults.value().get(0);

    System.out.println(String.format("Total number of images found: %d", imageResults.value().size()));
    System.out.println(String.format("First image thumbnail url: %s", firstImageResult.thumbnailUrl()));
    System.out.println(String.format("First image content url: %s", firstImageResult.contentUrl()));
}
else {
        System.out.println("Couldn't find image results!");
    }
}
```

## <a name="next-steps"></a>Passaggi successivi

> [!div class="nextstepaction"]
> [Esercitazione sull'app a singola pagina di Ricerca immagini Bing](https://docs.microsoft.com/azure/cognitive-services/bing-image-search/tutorial-bing-image-search-single-page-app)

## <a name="see-also"></a>Vedere anche 

* [Informazioni su Ricerca immagini Bing](https://docs.microsoft.com/azure/cognitive-services/bing-image-search/overview)  
* [Provare una demo interattiva online](https://azure.microsoft.com/services/cognitive-services/bing-image-search-api/)  
* [Ottenere gratuitamente una chiave di accesso per Servizi cognitivi](https://azure.microsoft.com/try/cognitive-services/?api=bing-image-search-api)
* [Esempi Java per l'SDK di Servizi cognitivi di Azure](https://github.com/Azure-Samples/cognitive-services-java-sdk-samples)
* [Documentazione di Servizi cognitivi di Azure](https://docs.microsoft.com/azure/cognitive-services)
* [Informazioni di riferimento per l'API Ricerca immagini Bing](https://docs.microsoft.com/rest/api/cognitiveservices/bing-images-api-v7-reference)
