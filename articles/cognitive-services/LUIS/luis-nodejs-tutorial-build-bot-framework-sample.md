---
title: Bot LUIS con Node.js - Bot per app Web - Bot Framework SDK 3.0
titleSuffix: Azure Cognitive Services
description: Compilare un bot integrato con un'applicazione LUIS usando Bot Framework.
services: cognitive-services
author: diberry
manager: cgronlun
ms.service: cognitive-services
ms.component: language-understanding
ms.topic: article
ms.date: 09/24/2018
ms.author: diberry
ms.openlocfilehash: 0bd191da3f2625bc202ee66100e7dac25d9d65de
ms.sourcegitcommit: 4ecc62198f299fc215c49e38bca81f7eb62cdef3
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 09/24/2018
ms.locfileid: "47042330"
---
# <a name="luis-bot-in-nodejs"></a>Bot LUIS in Node.js

Usando Node.js, creare un chat bot integrato con Language Understanding (LUIS). Questo bot chat utilizza il dominio di HomeAutomation precompilato per implementare rapidamente una soluzione di bot. Il bot viene compilato con Bot Framework 3.x e il bot per app Web di Azure.

## <a name="prerequisite"></a>Prerequisito

Prima di creare il bot, seguire i passaggi descritti in [Creare un'app](./luis-get-started-create-app.md) per compilare l'app LUIS.

Il bot risponde alle finalità dal dominio HomeAutomation presenti nell'app LUIS. Per ognuna di queste finalità, l'app LUIS fornisce una finalità mappata a essa. Il bot fornisce una finestra di dialogo che gestisce la finalità rilevata da LUIS.

| Finalità | Espressione di esempio | Funzionalità bot |
|:----:|:----------:|---|
| HomeAutomation.TurnOn | Turn on the lights (Accendi le luci). | Il bot richiama `TurnOnDialog` quando viene rilevato `HomeAutomation.TurnOn`. In questa finestra di dialogo è possibile richiamare un servizio IoT per accendere un dispositivo e indicare all'utente che il dispositivo si è acceso. |
| HomeAutomation.TurnOff | Turn off the bedroom lights (Spegni le luci della camera da letto). | Il bot richiama `TurnOffDialog` quando viene rilevato `HomeAutomation.TurnOff`. In questa finestra di dialogo è possibile richiamare un servizio IoT per spegnere un dispositivo e indicare all'utente che il dispositivo si è spento. |


## <a name="create-a-language-understanding-bot-with-bot-service"></a>Creare un bot LUIS (Language Understanding) con il servizio Bot

1. Nel [portale di Azure](https://portal.azure.com) selezionare **Create new resource** (Crea nuova risorsa) nel pannello menu e selezionare **See all** (Visualizza tutto).

    ![Create new resource (Crea nuova risorsa)](./media/luis-tutorial-node-bot/bot-service-creation.png)

2. Nella casella di ricerca cercare **Web App Bot** (Bot app Web). 

    ![Create new resource (Crea nuova risorsa)](./media/luis-tutorial-node-bot/bot-service-selection.png)

3. Nel pannello **Bot Servizio** (Servizio bot) fornire le informazioni richieste e selezionare **Create** (Crea). Il servizio bot e l'app LUIS vengono creati e distribuiti in Azure. Se si desidera usare il [priming del riconoscimento vocale](https://docs.microsoft.com/bot-framework/bot-service-manage-speech-priming), rivedere i [requisiti della regione](luis-resources-faq.md#what-luis-regions-support-bot-framework-speech-priming) prima di creare il bot. 
    * Impostare il **nome dell'app** sul nome del bot. Il nome viene usato come sottodominio durante la distribuzione del bot nel cloud, ad esempio mynotesbot.azurewebsites.net. <!-- This name is also used as the name of the LUIS app associated with your bot. Copy it to use later, to find the LUIS app associated with the bot. -->
    * Selezionare la sottoscrizione, il [gruppo di risorse](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-overview), il piano di servizio dell'app e la [posizione](https://azure.microsoft.com/regions/).
    * Come **modello del bot**, selezionare:
        * **SDK v3**
        * **Node.JS**
        * **Comprensione del linguaggio**
    * Selezionare la **posizione dell'app LUIS**. Si tratta della [regione][LUIS] in cui viene creata l'app.
    * Selezionare la casella di controllo di conferma per le note legali. Il contenuto delle note legali si trova sotto la casella di controllo.

    ![Pannello Bot Service (Servizio bot)](./media/luis-tutorial-node-bot/bot-service-setting-callout-template.png)


4. Confermare che il servizio bot è stato distribuito.
    * Fare clic su Notifications (Notifiche), ovvero l'icona a forma di campanello posta in alto nel portale di Azure. La notifica cambierà da **Deployment started** (Distribuzione iniziata) a **Deployment succeeded** (Distribuzione completata).
    * Dopo che la notifica è cambiata in **Deployment succeeded** (Distribuzione completata), selezionare **Go to resource** (Vai alla risorsa) in quella notifica.

## <a name="try-the-default-bot"></a>Provare il bot predefinito

Confermare che il bot è stato distribuito controllando le **notifiche**. La notifica cambierà da **Deployment in progress...** (Distribuzione in corso) in **Deployment succeeded** (Distribuzione completata). Selezionare il pulsante **Go to resource** (Vai alla risorsa) per aprire il pannello risorse del bot.

<!-- this step isn't supposed to be necessary -->
## <a name="install-npm-resources"></a>Installare le risorse NPM
Installare i pacchetti NPM eseguendo i passaggi seguenti:

1. Selezionare **Build** (Compila) dalla sezione **Bot Management** (Gestione bot) del Web App Bot. 

2. Verrà visualizzata una seconda finestra del browser. Selezionare **Open online code editor** (Apri editor di codice online).

3. Nella barra di spostamento superiore selezionare il nome del bot app Web `homeautomationluisbot`. 

4. Nell'elenco a discesa selezionare **Open Kudu Console** (Apri console Kudu).

5. Verrà visualizzata una nuova finestra del browser. Nella console immettere il comando seguente:

    ```
    cd site\wwwroot && npm install
    ```

    Attendere il completamento del processo di installazione. Tornare alla prima finestra del browser. 

## <a name="test-in-web-chat"></a>Test in Web Chat (Testa nella chat Web)
Dopo aver completato la registrazione del bot, selezionare **Test in Web Chat** (Testa nella chat Web) per aprire il riquadro Web Chat (Chat Web). Digitare "hello" (Ciao) nella chat Web.

  ![Testare il bot nella chat Web](./media/luis-tutorial-node-bot/bot-service-web-chat.png)

Il bot risponde dicendo "You have reached Greeting. You said: hello" (Hai raggiunto Saluti. Hai detto ciao). Questo conferma che il bot ha ricevuto il messaggio e che lo ha passato a un'app LUIS predefinita che ha creato. Questa app LUIS predefinita ha rilevato una finalità Greeting (Saluti). Nel passaggio successivo si connetterà il bot all'app LUIS creata in precedenza anziché a quella predefinita.

## <a name="connect-your-luis-app-to-the-bot"></a>Connettere l'app LUIS al bot

Aprire **Application Settings** (Impostazioni applicazione) nella prima finestra del browser e modificare il campo **LuisAppId** (ID app LUIS) inserendo l'ID della propria app LUIS.

  ![Aggiornare l'ID dell'app LUIS in Azure](./media/luis-tutorial-node-bot/bot-service-app-id.png)

Se non si dispone dell'ID dell'app LUIS, accedere al sito Web [LUIS](luis-reference-regions.md) usando lo stesso account usato per accedere ad Azure. Selezionare **My apps** (App personali). 

1. Trovare l'app LUIS creata in precedenza che contiene le finalità e le entità del dominio HomeAutomation.

2. Nella pagina **Settings** (Impostazioni) per l'app LUIS trovare e copiare l'ID app.

3. Se non è ancora stato eseguito il training dell'app, selezionare il pulsante **Train** (Esegui il training) in alto a destra per eseguire il training dell'app.

4. Se l'app non è ancora stata pubblicata, selezionare **PUBLISH** (Pubblica) nella barra di spostamento superiore per aprire la pagina **Publish** (Pubblica). Selezionare lo slot di produzione e il pulsante **Publish** (Pubblica).

## <a name="modify-the-bot-code"></a>Modificare il codice del bot

Accedere alla seconda finestra del browser se è ancora aperta altrimenti alla prima, selezionare **Build** (Compila) e infine scegliere **Open online code editor** (Apri editor di codice online).

   ![Aprire l'editor di codice online](./media/luis-tutorial-node-bot/bot-service-build.png)

Nell'editor di codice aprire `app.js`. Contiene il codice seguente:

```javascript
/*-----------------------------------------------------------------------------
A simple Language Understanding (LUIS) bot for the Microsoft Bot Framework. 
-----------------------------------------------------------------------------*/

var restify = require('restify');
var builder = require('botbuilder');
var botbuilder_azure = require("botbuilder-azure");

// Setup Restify Server
var server = restify.createServer();
server.listen(process.env.port || process.env.PORT || 3978, function () {
   console.log('%s listening to %s', server.name, server.url); 
});
  
// Create chat connector for communicating with the Bot Framework Service
var connector = new builder.ChatConnector({
    appId: process.env.MicrosoftAppId,
    appPassword: process.env.MicrosoftAppPassword,
    openIdMetadata: process.env.BotOpenIdMetadata 
});

// Listen for messages from users 
server.post('/api/messages', connector.listen());

/*----------------------------------------------------------------------------------------
* Bot Storage: This is a great spot to register the private state storage for your bot. 
* We provide adapters for Azure Table, CosmosDb, SQL Azure, or you can implement your own!
* For samples and documentation, see: https://github.com/Microsoft/BotBuilder-Azure
* ---------------------------------------------------------------------------------------- */

var tableName = 'botdata';
var azureTableClient = new botbuilder_azure.AzureTableClient(tableName, process.env['AzureWebJobsStorage']);
var tableStorage = new botbuilder_azure.AzureBotStorage({ gzipData: false }, azureTableClient);

// Create your bot with a function to receive messages from the user
// This default message handler is invoked if the user's utterance doesn't
// match any intents handled by other dialogs.
var bot = new builder.UniversalBot(connector, function (session, args) {
    session.send('You reached the default message handler. You said \'%s\'.', session.message.text);
});

bot.set('storage', tableStorage);

// Make sure you add code to validate these fields
var luisAppId = process.env.LuisAppId;
var luisAPIKey = process.env.LuisAPIKey;
var luisAPIHostName = process.env.LuisAPIHostName || 'westus.api.cognitive.microsoft.com';

const LuisModelUrl = 'https://' + luisAPIHostName + '/luis/v2.0/apps/' + luisAppId + '?subscription-key=' + luisAPIKey;

// Create a recognizer that gets intents from LUIS, and add it to the bot
var recognizer = new builder.LuisRecognizer(LuisModelUrl);
bot.recognizer(recognizer);

// Add a dialog for each intent that the LUIS app recognizes.
// See https://docs.microsoft.com/bot-framework/nodejs/bot-builder-nodejs-recognize-intent-luis 
bot.dialog('GreetingDialog',
    (session) => {
        session.send('You reached the Greeting intent. You said \'%s\'.', session.message.text);
        session.endDialog();
    }
).triggerAction({
    matches: 'Greeting'
})

bot.dialog('HelpDialog',
    (session) => {
        session.send('You reached the Help intent. You said \'%s\'.', session.message.text);
        session.endDialog();
    }
).triggerAction({
    matches: 'Help'
})

bot.dialog('CancelDialog',
    (session) => {
        session.send('You reached the Cancel intent. You said \'%s\'.', session.message.text);
        session.endDialog();
    }
).triggerAction({
    matches: 'Cancel'
})
```

Le finalità esistenti in app.js sono ignorate. È possibile lasciarle invariate. 

## <a name="add-a-dialog-that-matches-homeautomationturnon"></a>Aggiungere una finestra di dialogo che corrisponda a HomeAutomation.TurnOn

Copiare il codice seguente e aggiungerlo a `app.js`.

```javascript
bot.dialog('TurnOn',
    (session) => {
        session.send('You reached the TurnOn intent. You said \'%s\'.', session.message.text);
        session.endDialog();
    }
).triggerAction({
    matches: 'HomeAutomation.TurnOn'
})
```

L'opzione [matches][matches] (corrisponde a) nella [triggerAction][triggerAction] associata alla finestra di dialogo specifica il nome della finalità. Il riconoscimento viene eseguito ogni volta che il bot riceve un'espressione dall'utente. Se la finalità con il punteggio più alto rilevata corrisponde a `triggerAction` associato a una finestra di dialogo, il bot richiama quella finestra di dialogo.

## <a name="add-a-dialog-that-matches-homeautomationturnoff"></a>Aggiungere una finestra di dialogo che corrisponda a HomeAutomation.TurnOff

Copiare il codice seguente e aggiungerlo a `app.js`.

```javascript
bot.dialog('TurnOff',
    (session) => {
        session.send('You reached the TurnOff intent. You said \'%s\'.', session.message.text);
        session.endDialog();
    }
).triggerAction({
    matches: 'HomeAutomation.TurnOff'
})
```
## <a name="test-the-bot"></a>Testare il bot

Nel portale di Azure selezionare **Test in Web Chat** (Testa nella chat Web) per testare il bot. Digitare messaggi quali "Turn on the lights" (Accendi le luci) e "turn off my heater" (spegni il riscaldamento) per richiamare le finalità aggiunte.
   ![Testare il bot HomeAutomation nella chat Web](./media/luis-tutorial-node-bot/bot-service-chat-results.png)

> [!TIP]
> Se si ritiene che il bot non riconosca sempre la finalità o le entità corrette, migliorare le prestazioni dell'app LUIS fornendo un maggior numero di espressioni di esempio per eseguirne il training. È possibile rieseguire il training dell'app LUIS senza alcuna modifica al codice del bot. Vedere [Aggiungere espressioni di esempio](https://docs.microsoft.com/azure/cognitive-services/LUIS/add-example-utterances) ed [eseguire il training e il test dell'app LUIS](https://docs.microsoft.com/azure/cognitive-services/LUIS/luis-interactive-test).

## <a name="learn-more-about-bot-framework"></a>Ulteriori informazioni su Bot Framework
Ulteriori informazioni su [Bot Framework](https://dev.botframework.com/) e [3.x](https://github.com/Microsoft/BotBuilder) e [4.x](https://github.com/Microsoft/botbuilder-js) SDK.

## <a name="next-steps"></a>Passaggi successivi

<!-- From trying the bot, you can see that the recognizer can trigger interruption of the currently active dialog. Allowing and handling interruptions is a flexible design that accounts for what users really do. Learn more about the various actions you can associate with a recognized intent.--> È possibile provare ad aggiungere altre finalità, ad esempio Help (Guida), Cancel (Annulla) e Greeting (Saluti), all'app LUIS. Aggiungere finestre di dialogo per le nuove finalità e testarle usando il bot. 

<!-- 
> [!NOTE] 
> The default LUIS app that the template created contains example utterances for Cancel, Greeting, and Help intents. In the list of apps, find the app that begins with the name specified in **App name** in the **Bot Service** blade when you created the Bot Service. -->

> [!div class="nextstepaction"]
> [Aggiungere finalità](./luis-how-to-add-intents.md)
> [Priming del riconoscimento vocale](https://docs.microsoft.com/bot-framework/bot-service-manage-speech-priming)


[intentDialog]: https://docs.botframework.com/node/builder/chat-reference/classes/_botbuilder_d_.intentdialog.html

[intentDialog_matches]: https://docs.botframework.com/node/builder/chat-reference/classes/_botbuilder_d_.intentdialog.html#matches 

[NotesSample]: https://github.com/Microsoft/BotFramework-Samples/tree/master/docs-samples/Node/basics-naturalLanguage

[triggerAction]: https://docs.botframework.com/en-us/node/builder/chat-reference/classes/_botbuilder_d_.dialog.html#triggeraction

[confirmPrompt]: https://docs.botframework.com/node/builder/chat-reference/interfaces/_botbuilder_d_.itriggeractionoptions.html#confirmprompt

[waterfall]: bot-builder-nodejs-dialog-manage-conversation-flow.md#manage-conversation-flow-with-a-waterfall

[session_userData]: https://docs.botframework.com/node/builder/chat-reference/classes/_botbuilder_d_.session.html#userdata

[EntityRecognizer_findEntity]: https://docs.botframework.com/node/builder/chat-reference/classes/_botbuilder_d_.entityrecognizer.html#findentity

[matches]: https://docs.botframework.com/en-us/node/builder/chat-reference/interfaces/_botbuilder_d_.itriggeractionoptions.html#matches

[LUISAzureDocs]: https://docs.microsoft.com/azure/cognitive-services/LUIS/Home

[Dialog]: https://docs.botframework.com/node/builder/chat-reference/classes/_botbuilder_d_.dialog.html

[IntentRecognizerSetOptions]: https://docs.botframework.com/node/builder/chat-reference/interfaces/_botbuilder_d_.iintentrecognizersetoptions.html

[LuisRecognizer]: https://docs.botframework.com/node/builder/chat-reference/classes/_botbuilder_d_.luisrecognizer

[LUISConcepts]: https://docs.botframework.com/node/builder/guides/understanding-natural-language/

[DisambiguationSample]: https://github.com/Microsoft/BotBuilder/tree/master/Node/examples/feature-onDisambiguateRoute

[IDisambiguateRouteHandler]: https://docs.botframework.com/node/builder/chat-reference/interfaces/_botbuilder_d_.idisambiguateroutehandler.html

[RegExpRecognizer]: https://docs.botframework.com/node/builder/chat-reference/classes/_botbuilder_d_.regexprecognizer.html

[AlarmBot]: https://github.com/Microsoft/BotBuilder/blob/master/Node/examples/basics-naturalLanguage/app.js

[LUISBotSample]: https://github.com/Microsoft/BotBuilder-Samples/tree/master/Node/intelligence-LUIS

[UniversalBot]: https://docs.botframework.com/node/builder/chat-reference/classes/_botbuilder_d_.universalbot.html


<!-- Old Links -->
[Github-BotFramework-Emulator-Download]: https://aka.ms/bot-framework-emulator
[Github-LUIS-Samples]: https://github.com/Microsoft/LUIS-Samples
[Github-LUIS-Samples-node-hotel-bot]: https://github.com/Microsoft/LUIS-Samples/tree/master/bot-integration-samples/hotel-finder/nodejs
[NodeJs]: https://nodejs.org/
[BFPortal]: https://dev.botframework.com/
[RegisterInstructions]: https://docs.microsoft.com/bot-framework/portal-register-bot
[BotFramework]: https://docs.microsoft.com/bot-framework/
[LUIS]: https://docs.microsoft.com/azure/cognitive-services/luis/luis-reference-regions

