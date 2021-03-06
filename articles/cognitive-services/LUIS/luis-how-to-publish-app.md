---
title: Pubblicare l'app LUIS sull'endpoint di stima
titleSuffix: Azure Cognitive Services
description: Dopo aver compilato ed eseguito il test dell'app LUIS attiva, renderla disponibile per l'applicazione client effettuandone la pubblicazione sull'endpoint.
services: cognitive-services
author: diberry
manager: cgronlun
ms.service: cognitive-services
ms.component: language-understanding
ms.topic: conceptual
ms.date: 09/10/2018
ms.author: diberry
ms.openlocfilehash: 6eb48fd0f3290fbc3a249bc3880c809ace9f9ddb
ms.sourcegitcommit: 55952b90dc3935a8ea8baeaae9692dbb9bedb47f
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 10/09/2018
ms.locfileid: "48886488"
---
# <a name="publish-your-trained-app"></a>Pubblicare l'app sottoposta a training

Dopo aver compilato ed eseguito il test dell'app LUIS attiva, renderla disponibile per l'applicazione client effettuandone la pubblicazione sull'endpoint. 

<a name="publish-your-trained-app-to-an-http-endpoint"></a>

## <a name="publishing"></a>Pubblicazione

Per pubblicare l'endpoint, selezionare **Pubblica** nel pannello superiore a destra. 

![Barra di spostamento superiore destra](./media/luis-how-to-publish-app/publish-top-nav-bar.png)

Selezionare lo slot corretto quando viene visualizzata la finestra popup: staging o produzione. Usando due slot di pubblicazione è possibile avere due diverse versioni con endpoint pubblicati oppure la stessa versione su due endpoint diversi. 

L'app è pubblicata in tutte le regioni associate alle risorse LUIS aggiunte nel portale di LUIS. Ad esempio, per un'app creata su [www.luis.ai](https://www.luis.ai), se si crea una risorsa di LUIS in **westus** e la si aggiunge all'app come risorsa, l'app sarà pubblicata in tale regione. Per altre informazioni sulle aree del servizio LUIS, vedere [Aree](luis-reference-regions.md).
 
![Finestra popup di pubblicazione](./media/luis-how-to-publish-app/publish-pop-up.png)

Dopo aver pubblicato correttamente l'app, nella parte superiore del browser viene visualizzata una notifica di operazione riuscita verde. La barra di notifica verde include anche un collegamento agli endpoint. 

![Finestra popup di pubblicazione](./media/luis-how-to-publish-app/publish-success.png)

Se è necessario l'URL dell'endpoint, selezionare il collegamento. È anche possibile ottenere gli URL di endpoint selezionando **Gestisci** nel menu in alto, quindi selezionare **Chiavi e endpoint** nel menu a sinistra. 

## <a name="configuring-publish-settings"></a>Configurazione delle impostazioni di pubblicazione

Configurare le impostazioni di pubblicazione selezionando **Gestisci** nella barra di spostamento in alto a destra, quindi selezionando **Impostazioni di pubblicazione**. 

![Impostazioni di pubblicazione](./media/luis-how-to-publish-app/publish-settings.png)

### <a name="publish-after-enabling-sentiment-analysis"></a>Pubblicazione dopo l'abilitazione dell'analisi dei sentiment

<a name="enable-sentiment-analysis"></a>

L'analisi dei sentiment consente a LUIS di integrarsi con [Analisi del testo](https://azure.microsoft.com/services/cognitive-services/text-analytics/) per specificare la valutazione e la frase chiave. 

Non è necessario specificare una chiave di analisi del testo e non è previsto alcun addebito per questo servizio al proprio account Azure. Dopo averla selezionata, questa impostazione è permanente. 

I dati sentiment sono un punteggio compreso tra 1 e 0 che indica il sentiment positivo (più vicino a 1) o negativo (più vicino a 0) dei dati.

Per altre informazioni sulla risposta dell'endpoint JSON con l'analisi del sentiment, vedere [Analisi del sentiment](luis-concept-data-extraction.md#sentiment-analysis)



## <a name="next-steps"></a>Passaggi successivi

* Vedere [Gestire le chiavi](./luis-how-to-manage-keys.md) per aggiungere chiavi alla chiave di sottoscrizione di Azure in LUIS e per impostare la chiave del controllo ortografico Bing e includere tutte le finalità nei risultati.
* Per istruzioni su come testare l'app pubblicata nella console di test, vedere [Eseguire il training e testare l'app](luis-interactive-test.md).

