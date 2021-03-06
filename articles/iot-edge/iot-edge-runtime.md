---
title: Informazioni sul runtime di Azure IoT Edge| Microsoft Docs
description: Informazioni sul runtime di Azure IoT Edge e su come potenzia i dispositivi perimetrali
author: kgremban
manager: timlt
ms.author: kgremban
ms.date: 08/13/2018
ms.topic: conceptual
ms.service: iot-edge
services: iot-edge
ms.openlocfilehash: 9c9c04a8310a46605cf5733131db1418b7cb7f7a
ms.sourcegitcommit: ad08b2db50d63c8f550575d2e7bb9a0852efb12f
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 09/26/2018
ms.locfileid: "47218785"
---
# <a name="understand-the-azure-iot-edge-runtime-and-its-architecture"></a>Informazioni sul runtime di Azure IoT Edge e sulla relativa architettura

Il runtime di IoT Edge è una raccolta di programmi che devono essere installati in un dispositivo affinché possa essere considerato come dispositivo IoT Edge. I componenti del runtime di IoT Edge collettivamente abilitano i dispositivi di IoT Edge alla ricezione del codice da eseguire sul dispositivo perimetrale e ne comunicano i risultati. 

Nei dispositivi IoT Edge, il runtime di IoT Edge esegue le funzioni seguenti:

* Installa e aggiorna i carichi di lavoro nel dispositivo.
* Mantiene gli standard di sicurezza di Azure IoT Edge sul dispositivo.
* Garantisce che [i moduli di IoT Edge][lnk-modules] siano sempre in esecuzione.
* Segnala l'integrità dei moduli al cloud per il monitoraggio remoto.
* Facilita la comunicazione tra i dispositivi foglia downstream e i dispositivi IoT Edge.
* Facilita la comunicazione tra i moduli sul dispositivo IoT Edge.
* Facilita la comunicazione tra il dispositivo IoT Edge e il cloud.

![Il runtime di IoT Edge comunica informazioni approfondite e l'integrità del modulo all'hub IoT][1]

Le responsabilità del runtime di IoT Edge rientrano in due categorie: comunicazione e gestione dei moduli. Questi due ruoli vengono eseguiti da due componenti che sono alla base del runtime di IoT Edge. L'hub di IoT Edge è responsabile della comunicazione, mentre l'agente di IoT Edge gestisce la distribuzione e il monitoraggio dei moduli. 

Sia l'hub Edge che l'agente di Edge sono moduli, proprio come gli altri moduli in esecuzione nei dispositivi IoT Edge. 

## <a name="iot-edge-hub"></a>Hub di IoT Edge

L'hub di Edge è uno dei due moduli che costituiscono il runtime di Azure IoT Edge. Opera come un proxy locale per l'hub IoT esponendo gli stessi endpoint del protocollo dell'hub IoT. Questa coerenza implica che i client, siano essi dispositivi o moduli, possono connettersi al runtime di IoT Edge esattamente come si connetterebbero all'hub IoT. 

>[!NOTE]
>L'hub di Edge supporta i client che si connettono tramite MQTT o AMQP. Non supporta i client che usano HTTP. 

L'hub di Edge non è una versione completa dell'hub IoT in esecuzione in locale. Esistono alcune operazioni che l'hub di Edge delega automaticamente all'hub IoT. Ad esempio, l'hub di Edge inoltra le richieste di autenticazione all'hub IoT quando un dispositivo tenta di connettersi per la prima volta. Dopo aver stabilito la prima connessione, le informazioni di sicurezza vengono memorizzate nella cache locale dall'hub di Edge. Le connessioni successive da tale dispositivo vengono consentite senza dover eseguire l'autenticazione nel cloud. 

>[!NOTE]
>Il runtime deve essere connesso ogni volta che si prova a eseguire l'autenticazione di un dispositivo.

Per ridurre la larghezza di banda usata dalla soluzione IoT Edge, l'hub di Edge ottimizza il numero effettivo di connessioni eseguite nel cloud. L'hub di Edge accetta le connessioni logiche dai client quali moduli o dispositivi foglia e le combina per avere un'unica connessione fisica nel cloud. I dettagli di questo processo sono trasparenti per il resto della soluzione. Ai client sembra di avere ognuno la propria la connessione al cloud ma in realtà usano tutti la stessa connessione. 

![L'hub di Edge funge da gateway tra più dispositivi fisici e il cloud][2]

L'hub di Edge può determinare se è connesso all'hub IoT. Se la connessione viene persa, l'hub di Edge salva i messaggi o gli aggiornamenti gemelli in locale. Quando viene ristabilita la connessione, tutti i dati vengono sincronizzati. Il percorso usato per la cache temporanea è determinato da una proprietà del modulo gemello dell'hub di Edge. Le dimensioni della cache non sono limitate e aumentano fino a quando il dispositivo ha capacità di archiviazione. 

### <a name="module-communication"></a>Comunicazione del modulo

L'hub di Edge facilita la comunicazione da modulo a modulo. L'uso dell'hub di Edge come broker consente ai moduli di rimanere indipendenti. Per i moduli è sufficiente specificare gli input su cui accettano i messaggi e gli output su cui scrivono i messaggi. Uno sviluppatore di soluzioni quindi unisce gli input e gli output in modo che i moduli elaborino i dati nell'ordine specifico per tale soluzione. 

![L'hub di Edge facilita la comunicazione da modulo a modulo][3]

Per inviare i dati all'hub di Edge, un modulo chiama il metodo SendEventAsync. Il primo argomento specifica su quale output inviare il messaggio. Lo pseudocodice seguente invia un messaggio su output1:

   ```csharp
   ModuleClient client = new ModuleClient.CreateFromEnvironmentAsync(transportSettings); 
   await client.OpenAsync(); 
   await client.SendEventAsync(“output1”, message); 
   ```

Per ricevere un messaggio, registrare un callback che elabori i messaggi in arrivo in un input specifico. Lo pseudocodice seguente registra la funzione messageProcessor da usare per l'elaborazione di tutti i messaggi ricevuti in input1:

   ```csharp
   await client.SetEventHandlerAsync(“input1”, messageProcessor, userContext);
   ```

Lo sviluppatore di soluzioni è responsabile dell'indicazione delle regole che determinano la modalità in cui l'hub di Edge passa i messaggi tra i moduli. Le regole di routing sono definite nel cloud e propagate all'hub di Edge nel dispositivo gemello. La stessa sintassi per le route dell'hub IoT viene usata per definire le route tra i moduli di Azure IoT Edge. 

<!--- For more info on how to declare routes between modules, see []. --->   

![Route tra i moduli][4]

## <a name="iot-edge-agent"></a>Agente di IoT Edge

L'agente di IoT Edge è l'altro modulo che costituisce il runtime di Azure IoT Edge. È responsabile della creazione di istanze per i moduli, ne garantisce la continua esecuzione e segnala lo stato dei moduli all'hub IoT. Analogamente a qualsiasi altro modulo, l'agente di Edge usa il modulo gemello per archiviare i dati di configurazione. 

Il [daemon di sicurezza di IoT Edge](iot-edge-security-manager.md) avvia l'agente Edge all'avvio del dispositivo. L'agente recupera il modulo gemello dall'hub IoT e controlla il manifesto della distribuzione. Il manifesto della distribuzione è un file JSON che dichiara i moduli da avviare. 

Ogni elemento nel manifesto della distribuzione contiene informazioni specifiche su un modulo e viene usato dall'agente di Edge per il controllo del ciclo di vita del modulo. Di seguito sono riportate alcune delle proprietà più interessanti: 

* **settings.image**: l'immagine del contenitore usato dall'agente di Edge per avviare il modulo. Se l'immagine è protetta da password, l'agente di Edge deve essere configurato con le credenziali per il registro contenitori. È possibile configurare in remoto le credenziali per il registro contenitori usando il manifesto della distribuzione o aggiornando il file `config.yaml` nella cartella di programma IoT Edge del dispositivo Edge.
* **settings.createOptions**: una stringa che viene passata direttamente al daemon Docker all'avvio del contenitore di un modulo. L'aggiunta di opzioni di Docker in questa proprietà consente di avere opzioni avanzate come l'inoltro o il montaggio di volumi da parte della porta nel contenitore di un modulo.  
* **status**: lo stato in cui l'agente di Edge inserisce il modulo. Questo valore viene in genere impostato su *in esecuzione* perché la maggior parte degli utenti desidera che l'agente di Edge avvii immediatamente tutti i moduli nel dispositivo. Tuttavia, è possibile specificare lo stato iniziale di un modulo da arrestare e attendere un secondo momento per fare in modo che l'agente di Edge lo avvii. L'agente di Edge segnala lo stato di ciascun modulo al cloud nelle proprietà segnalate. Una differenza tra la proprietà desiderata e la proprietà segnalata è indicativa del comportamento errato di un dispositivo. Gli stati supportati sono:
   * Download in corso
   * In esecuzione
   * Non integro
   * Operazione non riuscita
   * Arrestato
* **restartPolicy**: la modalità in cui l'agente di Edge riavvia un modulo. I valori possibili sono:
   * Mai: l'agente di Edge non riavvia mai il modulo.
   * onFailure: se il modulo si blocca, l'agente di Edge lo riavvia. Se il modulo viene chiuso correttamente, l'agente di Edge non lo riavvia.
   * Non integro: se il modulo si blocca o viene considerato non integro, l'agente di Edge lo riavvia.
   * Sempre: se il modulo si blocca, viene considerato non integro o si arresta, l'agente di Edge lo riavvia. 

L'agente di IoT Edge invia la risposta runtime all'hub IoT. Ecco un elenco di risposte possibili:
  * 200 - OK
  * 400 - La configurazione della distribuzione è in formato non corretto o non valida.
  * 417 - Il dispositivo non ha un set di configurazione di distribuzione.
  * 412 - La versione dello schema nella configurazione della distribuzione non è valida.
  * 406 - Il dispositivo Edge è offline o non invia report sullo stato.
  * 500 - Si è verificato un errore del runtime Edge.

### <a name="security"></a>Sicurezza

L'agente di IoT Edge svolge un ruolo fondamentale nella protezione di un dispositivo di IoT Edge. Ad esempio, esegue azioni come la verifica di un'immagine del modulo prima di avviarla. 

Per altre informazioni sul framework di sicurezza di Azure IoT Edge, vedere [IoT Edge Security Manager](iot-edge-security-manager.md)

## <a name="next-steps"></a>Passaggi successivi

[Informazioni sui certificati Azure IoT Edge][lnk-certs]

<!-- Images -->
[1]: ./media/iot-edge-runtime/Pipeline.png
[2]: ./media/iot-edge-runtime/Gateway.png
[3]: ./media/iot-edge-runtime/ModuleEndpoints.png
[4]: ./media/iot-edge-runtime/ModuleEndpointsWithRoutes.png

<!-- Links -->
[lnk-certs]: iot-edge-certs.md
