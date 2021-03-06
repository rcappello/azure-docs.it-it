---
title: Creare un bot QnA con il servizio Azure Bot - QnA Maker
titleSuffix: Azure Cognitive Services
description: Questo tutorial illustra in modo guidato la compilazione di un bot QnA con il servizio Azure Bot v3 sul portale di Azure.
services: cognitive-services
author: tulasim88
manager: cgronlun
ms.service: cognitive-services
ms.component: qna-maker
ms.topic: article
ms.date: 09/12/2018
ms.author: tulasim
ms.openlocfilehash: 30400b04ec08d936242b022f10cf1485e009e6d2
ms.sourcegitcommit: ccdea744097d1ad196b605ffae2d09141d9c0bd9
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 10/23/2018
ms.locfileid: "49647324"
---
# <a name="create-a-qna-bot-with-azure-bot-service-v3"></a>Creare un bot QnA con il servizio Azure Bot v3
Questo tutorial illustra in modo guidato la compilazione di un bot QnA con il servizio Azure Bot v3 sul portale di Azure.

## <a name="prerequisite"></a>Prerequisito
Prima della compilazione, seguire i passaggi in [Creare una knowledge base](../How-To/create-knowledge-base.md) per creare un servizio QnA Maker con domande e risposte.

Il bot risponde alle domande della knowledge base create dall'utente, tramite il QnAMakerDialog.

## <a name="create-a-qna-bot"></a>Creazione di un bot QnA
1. Nel [portale di Azure](https://portal.azure.com) selezionare **Crea una risorsa** nel pannello menu, quindi scegliere **Visualizza tutto**.

    ![Creazione di servizi bot](../media/qnamaker-tutorials-create-bot/bot-service-creation.png)

2. Nella casella di ricerca, cercare **App Web Bot**.

    ![Selezione del servizio bot](../media/qnamaker-tutorials-create-bot/bot-service-selection.png)

3. Nel **pannello Servizio Bot** specificare le informazioni richieste:

    - Impostare il **nome dell'app** sul nome del bot. Il nome viene usato come sottodominio durante la distribuzione del bot nel cloud, ad esempio mynotesbot.azurewebsites.net.
    - Selezionare la sottoscrizione, il gruppo di risorse, il piano di servizio dell'app e la posizione.

4. Per vedere le istruzioni per la creazione di un bot per domande e risposte con v4 SDK, vedere il [modello di bot QnA v4](https://aka.ms/qna-bot-v4). Per usare i modelli v3, selezionare la versione di SDK di **SDK v3** e la lingua SDK del **C#** oppure **Node. js**.

    ![impostazioni di sdk di bot](../media/qnamaker-tutorials-create-bot/bot-v3.png)

5. Selezionare il modello **domande e risposte** per il campo modello di Bot, quindi salvare le impostazioni del modello selezionando **seleziona**.

    ![Selezione del servizio bot](../media/qnamaker-tutorials-create-bot/bot-v3-template.png)

6. Rivedere le impostazioni e quindi selezionare **Crea**. In questo modo viene creato e distribuito il servizio bot con QnAMakerDialog in Azure.

    ![Selezione del servizio bot](../media/qnamaker-tutorials-create-bot/bot-blade-settings-v3.png)

7. Confermare che il servizio robot è stato distribuito.

    - Selezionare le **notifiche** (l'icona a forma di campanello visibile nella parte superiore del portale di Azure). La notifica cambierà da **Distribuzione iniziata** a **Distribuzione completata**.
    - Dopo che la notifica è cambiata in **Distribuzione completata**, selezionare **Vai alla risorsa** in quella notifica.

## <a name="chat-with-the-bot"></a>Chat con il bot
Selezionando **Vai alla risorsa** consente di passare al pannello della risorsa del bot.

Dopo aver completato la registrazione del bot, fare clic su **Testa nella chat Web** per aprire il riquadro Chat Web. Digitare "ciao" nella chat Web.

![Chat Web con bot QnA](../media/qnamaker-tutorials-create-bot/qna-bot-web-chat.PNG)

Il bot risponde con "Per favore imposta QnAKnowledgebaseId e QnASubscriptionKey nelle Impostazioni app". Scopri come ottenerli in https://aka.ms/qnaabssetup". Questa risposta conferma che il bot QnA ha ricevuto il messaggio, ma non c'è ancora una knowledge base QnA Maker associata. Ciò sarà effettuato nel passaggio successivo.

## <a name="connect-your-qna-maker-knowledge-base-to-the-bot"></a>Connessione della knowledge base QnA Maker al bot

1. Aprire **Impostazioni applicazione** e modificare i campi **QnAKnowledgebaseId**, **QnAAuthKey** e **QnAEndpointHostName** affinché contengano i valori della knowledge base QnA Maker.

    ![app settings](../media/qnamaker-tutorials-create-bot/application-settings.PNG)

2. Ottenere l'ID della knowledge base, l'url host e la chiave di endpoint dalla scheda delle impostazioni della knowledge base in https://qnamaker.ai.
    - Accedere al [QnA Maker](https://qnamaker.ai)
    - Accedere alla knowledge base
    - Fare clic sulla scheda **Impostazioni**
    - **Pubblicare** la knowledge base, se non è stato già fatto

    ![Valori QnA Maker](../media/qnamaker-tutorials-create-bot/qnamaker-settings-kbid-key.PNG)

> [!NOTE]
> Se si desidera connettere la versione di anteprima della knowledge base con il bot QnA, impostare il valore di **Ocp-Apim-sottoscrizione-Key** su **QnAAuthKey**. Lasciare il **QnAEndpointHostName** vuoto.

## <a name="test-the-bot"></a>Test del bot
Nel portale di Azure, fare clic su **Testa nella chat Web** per testare il bot. 

![Bot QnA Maker](../media/qnamaker-tutorials-create-bot/qna-bot-web-chat-response.PNG)

Il bot QnA risponde ora dalla knowledge base.

## <a name="next-steps"></a>Passaggi successivi

> [!div class="nextstepaction"]
> [Integrare di QnA Maker e Language Understanding](./integrate-qnamaker-luis.md)

## <a name="see-also"></a>Vedere anche 

- [Gestire la knowledge base](https://qnamaker.ai)
- [Abilitare i bot nei diversi canali](https://docs.microsoft.com/azure/bot-service/bot-service-manage-channels)
