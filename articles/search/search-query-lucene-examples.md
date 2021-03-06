---
title: Esempi di query Lucene per Ricerca di Azure | Microsoft Docs
description: Sintassi di query Lucene per la ricerca fuzzy, la ricerca per prossimità, l'aumento priorità termini, la ricerca basata su espressioni regolari e le ricerche con caratteri jolly in un servizio Ricerca di Azure.
author: LiamCa
manager: pablocas
tags: Lucene query analyzer syntax
services: search
ms.service: search
ms.topic: conceptual
ms.date: 07/16/2018
ms.author: liamca
ms.openlocfilehash: d90a7b2d12a147b8020abbd51ef055f0e70471fb
ms.sourcegitcommit: f86e5d5b6cb5157f7bde6f4308a332bfff73ca0f
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 07/31/2018
ms.locfileid: "39365429"
---
# <a name="lucene-syntax-query-examples-for-building-advanced-queries-in-azure-search"></a>Esempi di query con sintassi Lucene per compilare query avanzate in Ricerca di Azure
Quando si compilano query per Ricerca di Azure, è possibile sostituire il [parser di query semplice](https://docs.microsoft.com/rest/api/searchservice/simple-query-syntax-in-azure-search) predefinito con il [parser di query Lucene in Ricerca di Azure](https://docs.microsoft.com/rest/api/searchservice/lucene-query-syntax-in-azure-search) per formulare definizioni di query avanzate e specializzate. 

Il parser di query Lucene supporta costrutti di query più complessi, ad esempio query con ambito campo, ricerche fuzzy e con caratteri jolly, ricerche di prossimità, aumento priorità termini e ricerche basate su espressioni regolari. La potenza aggiuntiva implica requisiti di elaborazione aggiuntivi. In questo articolo vengono illustrati esempi di operazioni di query disponibili quando si usa la sintassi completa.

> [!Note]
> Molte delle costruzioni di query specializzate possibili attraverso la sintassi di query Lucene completa non vengono [analizzate dal punto di vista del testo](https://docs.microsoft.com/azure/search/search-lucene-query-architecture#stage-2-lexical-analysis), fatto che può sembrare sorprendente se ci si aspetta lo stemming o la lemmatizzazione. L'analisi lessicale viene eseguita solo su termini completi, la query di un termine o di una locuzione. I tipi di query con termini incompleti, ad esempio query di prefisso, di caratteri jolly, di espressioni regolari, fuzzy, vengono aggiunte direttamente alla struttura della query, ignorando la fase di analisi. L'unica trasformazione eseguita per i termini di una query incompleta è la conversione in lettere minuscole. 
>

## <a name="formulate-requests-in-postman"></a>Formulare richieste in Postman

Negli esempi seguenti viene usato un indice di ricerca delle opportunità di lavoro a New York City (NYC Jobs) disponibili in un set di dati fornito dall'iniziativa [City of New York OpenData](https://nycopendata.socrata.com/). Questi dati non devono essere considerati attuali o completi. L'indice si trova in un servizio sandbox fornito da Microsoft, il che significa che non è necessario disporre di una sottoscrizione di Azure o del servizio Ricerca di Azure per provare queste query.

Ciò che è necessario è Postman o uno strumento equivalente per rilasciare una richiesta HTTP su GET. Per ulteriori informazioni, vedere [Test con client REST](search-fiddler.md).

### <a name="set-the-request-header"></a>Impostare l'intestazione della richiesta

1. Nell'intestazione della richiesta impostare **Content-Type** su `application/json`.

2. Aggiungere una **chiave API** e impostarla su questa stringa: `252044BE3886FE4A8E3BAA4F595114BB`. Si tratta di una chiave di query per il servizio di ricerca sandbox che ospita l'indice NYC Jobs.

Dopo aver specificato l'intestazione della richiesta, è possibile riusarla per tutte le query in questo articolo, cambiando solo la stringa **search=**. 

  ![Intestazione della richiesta Postman](media/search-query-lucene-examples/postman-header.png)

### <a name="set-the-request-url"></a>Impostare l'URL della richiesta

La richiesta è un comando GET abbinato a un URL contenente l'endpoint Ricerca di Azure e la stringa di ricerca.

  ![Intestazione della richiesta Postman](media/search-query-lucene-examples/postman-basic-url-request-elements.png)

La composizione dell'URL include gli elementi seguenti:

+ **`https://azs-playground.search.windows.net/`** è un servizio di ricerca sandbox gestito dal team di sviluppo Ricerca di Azure. 
+ **`indexes/nycjobs/`** è l'indice NYC Jobs nella raccolta di indici di quel servizio. Sia il nome di servizio sia l'indice sono necessari nella richiesta.
+ **`docs`** è la raccolta di documenti contenenti tutti i documenti disponibili per la ricerca. La chiave API della query fornita nell'intestazione della richiesta funziona solo nelle operazioni di lettura destinate alla raccolta di documenti.
+ **`api-version=2017-11-11`** imposta la versione dell'API, un parametro obbligatorio per ogni richiesta.
+ **`search=*`** è la stringa di query, che nella query iniziale è null, che restituisce i primi 50 risultati (per impostazione predefinita).

## <a name="send-your-first-query"></a>Inviare la prima query

Come fase di verifica, incollare la seguente richiesta in GET e fare clic su **Invia**. I risultati vengono restituiti come documenti JSON dettagliati. È possibile copiare e incollare questo URL nel primo esempio riportato di seguito.

  ```http
  https://azs-playground.search.windows.net/indexes/nycjobs/docs?api-version=2017-11-11&search=*
  ```

La stringa di query, **`search=*`**, è una ricerca non specificata equivalente a una ricerca null o vuota. Non è particolarmente utile, ma è la ricerca più semplice che sia possibile eseguire.

Se lo si desidera, è possibile aggiungere **`$count=true`** all'URL per restituire un conteggio dei documenti corrispondenti ai criteri di ricerca. In una stringa di ricerca vuota sono tutti i documenti nell'indice (2802 nel caso di NYC Jobs).

## <a name="how-to-invoke-full-lucene-parsing"></a>Come richiamare l'analisi completa di Lucene

Aggiungere **queryType=full** per richiamare la sintassi di query completa che sostituisce la sintassi di query semplice predefinita. 

```GET
https://azs-playground.search.windows.net/indexes/nycjobs/docs?api-version=2017-11-11&queryType=full&search=*
```

Tutti gli esempi in questo articolo specificano il parametro di ricerca **queryType=full**, che indica che la sintassi completa viene gestita dal parser di query Lucene. 

## <a name="example-1-field-scoped-query"></a>Esempio 1: query con ambito campo

La prima query non è una dimostrazione della sintassi Lucene completa (funziona tanto per la sintassi semplice quanto per quella completa), ma con questo esempio intendiamo introdurre un concetto di query di riferimento che produce una risposta JSON ragionevolmente leggibile. In breve, la query punta solo al campo *business_title* e specifica che vengano restituite solo le qualifiche professionali. 

```GET
https://azs-playground.search.windows.net/indexes/nycjobs/docs?api-version=2017-11-11&$count=true&searchFields=business_title&$select=business_title&queryType=full&search=*
```

Il parametro **searchFields** limita la ricerca al solo campo della qualifica professionale (business_title). Il parametro **select** determina i campi che vengono inclusi nel set di risultati.

La risposta per questa query deve essere simile alla seguente schermata.

  ![Risposta di esempio di Postman](media/search-query-lucene-examples/postman-sample-results.png)

Si noti che il punteggio della ricerca viene restituito per ogni documento anche se non è stato specificato. Questo perché il punteggio di ricerca è composto da metadati, il cui valore indica l'ordine dei risultati. Si ottengono punteggi uniformi pari a 1 in assenza di un ordine perché la ricerca non è una ricerca full-text o perché non vi sono criteri da applicare. Per la ricerca null, non vi sono criteri e le righe restituite hanno un ordine arbitrario. Poiché i criteri di ricerca assumono più definizioni, i punteggi di ricerca si convertono in valori significativi.

## <a name="example-2-in-field-filtering"></a>Esempio 2: filtro nel campo

La sintassi Lucene completa supporta espressioni in un campo. Questa query cerca business_title che contengono il termine senior ma non junior:

```GET
https://azs-playground.search.windows.net/indexes/nycjobs/docs?api-version=2017-11-11&$count=true&searchFields=business_title&$select=business_title&queryType=full&search=business_title:senior+NOT+junior
```

Specificando una costruzione **fieldname:searchterm**, è possibile definire un'operazione di query con campo, dove il campo è una singola parola e il termine di ricerca è una singola parola o frase, facoltativamente con operatori booleani. Ecco alcuni esempi:

* business_title:(senior NOT junior)
* state:("New York" AND "New Jersey")

Assicurarsi di inserire più stringhe racchiuse tra virgolette se si vuole che entrambe le stringhe siano valutate come una singola entità, come in questo caso per la ricerca di due città distinte nel campo "location". Assicurarsi anche che l'operatore sia in lettere maiuscole, come NOT e AND.

Il campo specificato in **nomecampo:terminericerca** deve essere un campo ricercabile. Per informazioni dettagliate sull'uso di attributi dell'indice nelle definizioni campo, vedere [Creare l'indice (API REST del servizio Ricerca di Azure)](https://docs.microsoft.com/rest/api/searchservice/create-index) .

## <a name="example-3-fuzzy-search"></a>Esempio 3: ricerca fuzzy

La sintassi Lucene completa supporta anche la ricerca fuzzy, basata sui termini che hanno una costruzione simile. Per eseguire una ricerca fuzzy, aggiungere il simbolo tilde `~` alla fine di una parola con un parametro facoltativo, un valore compreso tra 0 e 2, che specifica la distanza di edit. Ad esempio, `blue~` o `blue~1` restituirà blue, blues e glue.

Questa query cerca le opportunità di lavoro con il termine "associate" (scritto erroneamente di proposito):

```GET
https://azs-playground.search.windows.net/indexes/nycjobs/docs?api-version=2017-11-11&$count=true&searchFields=business_title&$select=business_title&queryType=full&search=business_title:asosiate~
```

Secondo la [documentazione di Lucene](https://lucene.apache.org/core/4_10_2/queryparser/org/apache/lucene/queryparser/classic/package-summary.html), le ricerche fuzzy si basano sulla [distanza di Damerau-Levenshtein](https://en.wikipedia.org/wiki/Damerau%e2%80%93Levenshtein_distance).

> [!Note]
> Le query fuzzy non vengono [analizzate](https://docs.microsoft.com/azure/search/search-lucene-query-architecture#stage-2-lexical-analysis). I tipi di query con termini incompleti, ad esempio query di prefisso, di caratteri jolly, di espressioni regolari, fuzzy, vengono aggiunte direttamente alla struttura della query, ignorando la fase di analisi. L'unica trasformazione eseguita per i termini di una query incompleta è la conversione in lettere minuscole.
>

## <a name="example-4-proximity-search"></a>Esempio 4: ricerca di prossimità
Le ricerche per prossimità vengono usate per trovare termini che si trovano vicini in un documento. Inserire un carattere tilde "~" alla fine di una frase seguito dal numero di parole che creano il limite di prossimità. Ad esempio, "hotel airport"~5 troverà i termini hotel e airport entro 5 parole di distanza una dall'altra in un documento.

In questa query per le opportunità di lavoro contenenti il termine "senior analyst" separato da non più di una parola:

```GET
https://azs-playground.search.windows.net/indexes/nycjobs/docs?api-version=2017-11-11&$count=true&searchFields=business_title&$select=business_title&queryType=full&search=business_title:%22senior%20analyst%22~1
```

Riprovare rimuovendo le parole tra il termine "senior analyst". Si noti che vengono restituiti 8 documenti per questa query, rispetto ai 10 per la query precedente.

```GET
https://azs-playground.search.windows.net/indexes/nycjobs/docs?api-version=2017-11-11&$count=true&searchFields=business_title&$select=business_title&queryType=full&search=business_title:%22senior%20analyst%22~0
```

## <a name="example-5-term-boosting"></a>Esempio 5: aumento priorità termine
Questa definizione si riferisce alla termine si riferisce alla classificazione più alta di un documento se contiene il termine con aumento di priorità, rispetto a documenti che non contengono il termine. Per aumentare la priorità di un termine, usare il carattere accento circonflesso "^", con un fattore di aumento di priorità (un numero) alla fine del termine da cercare. 

In questa query "before" cercare le opportunità di lavoro con il termine *computer analyst* e si noti che non vi sono risultati con le parole *computer* e *analyst*, eppure i lavori *computer* sono i primi risultati.

```GET
https://azs-playground.search.windows.net/indexes/nycjobs/docs?api-version=2017-11-11&$count=true&searchFields=business_title&$select=business_title&queryType=full&search=business_title:computer%20analyst
```

Nella query "after", ripetere la ricerca, questa volta aumentando la priorità dei risultati con il termine *analyst* rispetto al termine *computer* se nessuna delle due parole esiste. 

```GET
https://azs-playground.search.windows.net/indexes/nycjobs/docs?api-version=2017-11-11&$count=true&searchFields=business_title&$select=business_title&queryType=full&search=business_title:computer%20analyst%5e2
```
Una versione maggiormente leggibile della query precedente è `search=business_title:computer analyst^2`. Per una query di lavoro `^2` viene codificato come `%5E2`, più difficile da vedere.

L'aumento priorità dei termini si differenzia dai profili di punteggio per il fatto che questi ultimi aumentano la priorità di alcuni campi e non di termini specifici. L'esempio seguente illustra le differenze.

Considerare un profilo di punteggio che migliora le corrispondenze in un determinato campo, ad esempio **genre** (genere) nell'esempio musicstoreindex. L'aumento di priorità di un termine si usa per assegnare a determinati termini di ricerca una priorità maggiore rispetto ad altri. Ad esempio, "rock^2 electronic" aumenta la priorità nell'indice dei documenti che contengono tali termini di ricerca nel campo **genre** rispetto a quelli con altri campi ricercabili. Inoltre, i documenti che contengono il termine di ricerca "rock" verranno classificati con una priorità superiore rispetto all'altro termine di ricerca "electronic" come risultato il valore di priorità del termine (2).

Quando si imposta il fattore, maggiore è il fattore di aumento, maggiore è la rilevanza del termine relativamente ad altri termini di ricerca. Per impostazione predefinita, il fattore di aumento di priorità è 1. Anche se il fattore di aumento di priorità deve essere positivo, può essere minore di 1 (ad esempio 0,2).


## <a name="example-6-regex"></a>Esempio 6: Regex

Una ricerca con espressione regolare trova una corrispondenza in base al contenuto incluso tra le barre "/", come indicato nella [classe RegExp](http://lucene.apache.org/core/4_10_2/core/org/apache/lucene/util/automaton/RegExp.html).

In questa query cercare le opportunità di lavoro con il termine Senior o Junior: `search=business_title:/(Sen|Jun)ior/``.

```GET
https://azs-playground.search.windows.net/indexes/nycjobs/docs?api-version=2017-11-11&$count=true&searchFields=business_title&$select=business_title&queryType=full&search=business_title:/(Sen|Jun)ior/
```
> [!Note]
> Le query Regex non vengono [analizzate](https://docs.microsoft.com/azure/search/search-lucene-query-architecture#stage-2-lexical-analysis). L'unica trasformazione eseguita per i termini di una query incompleta è la conversione in lettere minuscole.
>

## <a name="example-7-wildcard-search"></a>Esempio 7: ricerca con caratteri jolly
È possibile usare una sintassi generalmente riconosciuta per ricerche con caratteri jolly per trovare più caratteri (\*) o un singolo carattere (?). Si noti che il parser di query Lucene supporta l'utilizzo di questi simboli con un singolo termine, non una frase.

In questa query cercare le opportunità di lavoro che contengono il prefisso 'prog' che include le qualifiche professionali con i termini programming e programmer.

```GET
https://azs-playground.search.windows.net/indexes/nycjobs/docs?api-version=2017-11-11&$count=true&searchFields=business_title&$select=business_title&queryType=full&search=business_title:prog*
```
Non è possibile usare un carattere * o ? come primo carattere di una ricerca.

> [!Note]
> Le query con caratteri jolly non vengono [analizzate](https://docs.microsoft.com/azure/search/search-lucene-query-architecture#stage-2-lexical-analysis). L'unica trasformazione eseguita per i termini di una query incompleta è la conversione in lettere minuscole.
>

## <a name="next-steps"></a>Passaggi successivi
Provare a specificare il parser di query Lucene nel codice. I collegamenti seguenti illustrano come configurare le query di ricerca per .NET e l'API REST. I collegamenti usano la sintassi semplice predefinita, quindi è necessario applicare quanto appreso in questo articolo per specificare il parametro **queryType**.

* [Eseguire query su un indice di Ricerca di Azure con .NET SDK](search-query-dotnet.md)
* [Eseguire query su un indice di Ricerca di Azure con l'API REST](search-query-rest-api.md)

Un riferimento alla sintassi aggiuntivo, l'architettura di query e gli esempi sono disponibili nei seguenti collegamenti:

+ [Esempi di query con sintassi semplice](search-query-simple-examples.md)
+ [Funzionamento della ricerca full-text in Ricerca di Azure](search-lucene-query-architecture.md)
+ [Sintassi di query semplice](https://docs.microsoft.com/rest/api/searchservice/simple-query-syntax-in-azure-search)
+ [Full Lucene query syntax](https://docs.microsoft.com/rest/api/searchservice/lucene-query-syntax-in-azure-search) (Sintassi di query completa Lucene)