---
title: Diagnosticare e risolvere i problemi nell'ambiente Time Series Insights | Microsoft Docs
description: In questo articolo viene descritto come diagnosticare e risolvere i problemi più comuni riscontrati nell'ambiente Azure Time Series Insights.
ms.service: time-series-insights
services: time-series-insights
author: ashannon7
ms.author: anshan
manager: cshankar
ms.reviewer: v-mamcge, jasonh, kfile, anshan
ms.workload: big-data
ms.topic: troubleshooting
ms.date: 04/09/2018
ms.openlocfilehash: b05b824d8d35351030ca466566f14e4249d4b99d
ms.sourcegitcommit: 4de6a8671c445fae31f760385710f17d504228f8
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 08/08/2018
ms.locfileid: "39626621"
---
# <a name="diagnose-and-solve-problems-in-your-time-series-insights-environment"></a>Diagnosticare e risolvere i problemi nell'ambiente Time Series Insights

## <a name="problem-1-no-data-is-shown"></a>Problema 1: non viene visualizzato alcun dato
Ecco alcuni motivi per cui i dati potrebbero non essere visualizzati nello [strumento di esplorazione di Azure Time Series Insights](https://insights.timeseries.azure.com):

### <a name="possible-cause-a-event-source-data-is-not-in-json-format"></a>Causa possibile A: i dati dell'origine evento non sono in formato JSON
Azure Time Series Insights supporta solo dati in formato JSON. Per alcuni esempi di dati in formato JSON, vedere [Forme JSON supportate](time-series-insights-send-events.md#supported-json-shapes).

### <a name="possible-cause-b-event-source-key-is-missing-a-required-permission"></a>Causa possibile B: la chiave dell'origine evento non dispone di un'autorizzazione obbligatoria
* Per un hub IoT è necessario indicare la chiave con l'autorizzazione di **connessione al servizio**.

   ![Autorizzazione di connessione al servizio hub IoT](media/diagnose-and-solve-problems/iothub-serviceconnect-permissions.png)

   Come illustrato nell'immagine precedente, entrambi i criteri **iothubowner** e **service** possono funzionare, in quanto entrambi dispongono dell'autorizzazione di **connessione al servizio**.
   
* Per un hub eventi è necessario fornire la chiave con l'autorizzazione di **ascolto**.

   ![Autorizzazione di ascolto per l'hub eventi](media/diagnose-and-solve-problems/eventhub-listen-permissions.png)

   Come illustrato nell'immagine precedente, entrambi i criteri **read** e **manage** potrebbero funzionare, in quanto entrambi dispongono dell'autorizzazione di **ascolto**.

### <a name="possible-cause-c-the-consumer-group-provided-is-not-exclusive-to-time-series-insights"></a>Causa possibile C: il gruppo di consumer fornito è non esclusivo di Time Series Insights
Durante la registrazione di un hub IoT o un hub eventi viene specificato il gruppo di consumer da usare per la lettura dei dati. Questo gruppo di consumer **non** deve essere condiviso. Se viene condiviso, l'hub eventi sottostante disconnette automaticamente uno dei lettori in modo casuale. Specificare un gruppo di consumer univoco per la lettura dei dati da parte di Time Series Insights.

## <a name="problem-2-some-data-is-shown-but-some-is-missing"></a>Problema 2: vengono visualizzati solo alcuni dati
Se i dati risultano parzialmente visibili, mentre altri sembrano in ritardo, è necessario considerare le possibili cause seguenti:

### <a name="possible-cause-a-your-environment-is-getting-throttled"></a>Causa possibile A: l'ambiente è in fase di limitazione
Si tratta di un problema comune quando viene effettuato il provisioning di ambienti dopo la creazione di un'origine eventi con dati.  Gli hub IoT di Azure e Hub eventi archiviano i dati per un massimo di sette giorni.  Time Series Insights partirà sempre dall'evento meno recente (FIFO), all'interno dell'origine eventi.  Pertanto, se sono presenti cinque milioni di eventi in un'origine eventi quando ci si connette a un ambiente di Time Series Insights a singola unità S1, Time Series Insights leggerà circa un milione di eventi al giorno.  Apparentemente, ciò potrebbe essere interpretato come un periodo di latenza di cinque giorni per Time Series Insights.  Quello che accade in effetti, è che l'ambiente viene limitato.  In presenza di vecchi eventi nell'origine eventi, è possibile scegliere tra due approcci:

- Modificare i limiti di conservazione dell'origine eventi per eliminare vecchi eventi che non si vuole visualizzare in Time Series Insights
- Eseguire il provisioning di un ambiente di dimensioni maggiori, in termini di numero di unità, per aumentare la velocità effettiva per i vecchi eventi.  Ritornando all'esempio precedente, se lo stesso ambiente S1 venisse esteso a cinque unità per un giorno, sarebbe possibile recuperare entro tale giorno.  Se la produzione di eventi di stato costante è di circa 1 milione o meno al giorno, è possibile ridurre la capacità per gli eventi tornando a una unità dopo essersi messi in pari.  

La limitazione viene applicata in base alla capacità e al tipo di SKU dell'ambiente. Tutte le origini evento all'interno dell'ambiente condividono questa capacità. Se l'origine evento dell'hub IoT e dell'hub eventi esegue il push dei dati oltre il limite imposto, si verificheranno una limitazione e un ritardo.

Il diagramma seguente mostra un ambiente Time Series Insights con uno SKU S1 e una capacità pari a 3. È consentito l'ingresso di 3 milioni di eventi al giorno.

![Capacità corrente dello SKU dell'ambiente](media/diagnose-and-solve-problems/environment-sku-current-capacity.png)

Si supponga, ad esempio, che questo ambiente stia inserendo messaggi provenienti da un hub eventi. Osservare la velocità in ingresso, illustrata nel diagramma seguente:

![Velocità di ingresso di esempio per un hub eventi](media/diagnose-and-solve-problems/eventhub-ingress-rate.png)

Come illustrato nel diagramma, la frequenza in ingresso giornaliera è pari a circa 67.000 messaggi. Questa velocità si traduce approssimativamente in 46 messaggi al minuto. Se ogni messaggio dell'hub eventi viene appiattito a un singolo evento Time Series Insights, questo ambiente non sperimenterà alcuna limitazione. Se ogni messaggio dell'hub eventi viene appiattito a 100 eventi Time Series Insights , devono essere inseriti 4.600 eventi ogni minuto. Un ambiente SKU S1 con una capacità pari a 3 consente l'ingresso di soli 2.100 eventi al minuto (1 milione di eventi al giorno = 700 eventi al minuto in 3 unità = 2.100 eventi al minuto). Pertanto si osserverà un ritardo dovuto alla limitazione. 

Per una descrizione generale di come funziona la logica di appiattimento, vedere [Forme JSON supportate](time-series-insights-send-events.md#supported-json-shapes).

### <a name="recommended-resolution-steps-for-excessive-throttling"></a>Passaggi consigliati per la risoluzione dei problemi relativi alla limitazione eccessiva
Per correggere il ritardo, aumentare la capacità SKU dell'ambiente. Per altre informazioni, vedere [Come scalare l'ambiente Time Series Insights](time-series-insights-how-to-scale-your-environment.md).

### <a name="possible-cause-b-initial-ingestion-of-historical-data-is-causing-slow-ingress"></a>Causa possibile B: l'inserimento iniziale dei dati cronologici rallenta il traffico in ingresso
Se ci si connette a un'origine evento esistente, è probabile che l'hub IoT o l'hub eventi contenga già dati. L'ambiente inizia a eseguire il pull dei dati dall'inizio del periodo di conservazione dei messaggi dell'origine evento.

Questo comportamento è quello predefinito e non è possibile eseguirne l'override. Potrebbe attivarsi la limitazione e potrebbe essere necessario un po' di tempo per l'inserimento dei dati cronologici.

#### <a name="recommended-resolution-steps-of-large-initial-ingestion"></a>Passaggi consigliati per la risoluzione dei problemi relativi all'inserimento iniziale di grandi quantità di dati
Per correggere il ritardo, procedere come segue:
1. Aumentare la capacità SKU fino al valore massimo consentito (10 in questo caso). Dopo aver aumentato la capacità, il processo di ingresso inizia a essere molto più veloce. È possibile vedere tale rapidità nel grafico della disponibilità nello [strumento di esplorazione di Time Series Insights](https://insights.timeseries.azure.com). La maggiore capacità sarà addebitata.
2. Dopo aver recuperato il ritardo, diminuire nuovamente la capacità SKU secondo la velocità di ingresso normale.

## <a name="problem-3-my-event-sources-timestamp-property-name-setting-doesnt-work"></a>Problema 3: l'impostazione del *nome della proprietà Timestamp* dell'origine evento non funziona
Verificare che il nome e il valore siano conformi alle regole seguenti:
* Il nome della proprietà Timestamp _fa distinzione fra maiuscole e minuscole_.
* Il valore della proprietà Timestamp proveniente dall'origine evento, come stringa JSON, deve avere il formato _aaaa-MM-ggTHH:mm:ss.FFFFFFFK_. Un esempio di tale stringa è "2008-04-12T12:53Z".

Il modo più semplice per garantire l'acquisizione e il corretto funzionamento del *nome della proprietà Timestamp* consiste nell'usare TSI Explorer.  All'interno di TSI Explorer, usando il grafico, selezionare un periodo di tempo dopo aver specificato il *nome della proprietà Timestamp*.  Fare clic con il pulsante destro del mouse sulla selezione e scegliere *Esplora eventi*.  La prima intestazione di colonna deve essere il *nome della proprietà Timestamp* e deve avere *($ts)* accanto alla parola *Timestamp*, invece di:
- *(abc)* , che indicherebbe che Time Series Insights sta leggendo i valori dei dati come stringhe
- *Icona del calendario*, che indicherebbe che Time Series Insights sta leggendo i valori dei dati come *datetime*
- *#*, che indicherebbe che Time Series Insights sta leggendo i valori dei dati come Integer


## <a name="next-steps"></a>Passaggi successivi
- Per ulteriore assistenza, avviare una conversazione nel [forum MSDN](https://social.msdn.microsoft.com/Forums/home?forum=AzureTimeSeriesInsights) o in [Stack Overflow](https://stackoverflow.com/questions/tagged/azure-timeseries-insights). 
- È anche possibile usare le opzioni di supporto assistito disponibili nella pagina [Opzioni di supporto tecnico per Microsoft Azure](https://azure.microsoft.com/support/options/).
