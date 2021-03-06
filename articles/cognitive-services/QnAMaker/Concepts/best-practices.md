---
title: Procedure consigliate - QnA Maker
titlesuffix: Azure Cognitive Services
description: Usare queste procedure consigliate per migliorare la knowledge base e fornire risultati migliori per gli utenti finali dell'applicazione/chat bot.
services: cognitive-services
author: tulasim88
manager: cgronlun
ms.service: cognitive-services
ms.component: qna-maker
ms.topic: article
ms.date: 09/24/2018
ms.author: tulasim
ms.openlocfilehash: cb171a666a4a54660a3bf54b8f26aed23f60d249
ms.sourcegitcommit: 4ecc62198f299fc215c49e38bca81f7eb62cdef3
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 09/24/2018
ms.locfileid: "47036304"
---
# <a name="best-practices"></a>Procedure consigliate
Il [ciclo di vita di sviluppo della knowledge base](../Concepts/development-lifecycle-knowledge-base.md) fornisce informazioni sulla gestione della KB dall'inizio alla fine. Usare queste procedure consigliate per migliorare la knowledge base e fornire risultati migliori per gli utenti finali dell'applicazione/chat bot.

## <a name="extraction"></a>Estrazione
Il servizio QnA Maker migliora continuamente gli algoritmi di estrazione di domande e risposte dal contenuto, espandendo l'elenco di file e formati di pagina HTML supportati. Seguire le [linee guida](../Concepts/data-sources-supported.md) per l'estrazione di dati in base al tipo di documento. 

In generale, le pagine di domande frequenti devono essere autonome e non combinate con altre informazioni. I manuali di prodotti devono avere titoli chiari e preferibilmente una pagina di indice. 

## <a name="chit-chat"></a>Chit Chat
Aggiungere una chit-chat al bot, per renderlo più colloquiale e accattivante con uno sforzo minimo. È possibile aggiungere facilmente un set di dati chit-chat per 3 personalità predefinite quando si crea la KB, con possibilità di apportare modifiche in qualsiasi momento. Come [aggiungere chit-chat alla KB](../How-To/chit-chat-knowledge-base.md). 

### <a name="choosing-a-personality"></a>Scelta della personalità
Chit chat è supportata per 3 personalità predefinite: 

|Personalità|
|--|
|Il professionista|
|L'amico|
|Lo spiritoso|

Le risposte possono andare da quelle formali a quelle informali e irriverenti. È consigliabile selezionare la personalità più allineata al tono desiderato per il bot. È possibile visualizzare i set di dati, sceglierne una che serva come base per il bot e quindi personalizzare le risposte. 

### <a name="edit-bot-specific-questions"></a>Modifica delle domande specifiche per i bot
Esistono alcune domande specifiche per i bot che fanno parte del set di dati chit-chat e a cui sono state associate risposte generiche. Modificare queste risposte per riflettere al meglio i dettagli del bot. 

È consigliabile rendere le seguenti QnA di chit-chat più specifiche:

* Chi si sta autenticando?
* Cosa fare
* Quanti anni hai?
* Chi ti ha creato?
* Ciao
   

## <a name="rankingscoring"></a>Classificazione e assegnazione dei punteggi
Assicurarsi di usare al meglio le funzionalità di classificazione supportate da QnA Maker. In questo modo sarà possibile migliorare la probabilità che una specifica query utente riceva una risposta appropriata.

### <a name="choosing-a-threshold"></a>Scelta della soglia
Il punteggio di attendibilità predefinito che viene usato come soglia è 50, ma è possibile modificarlo per la KB in base alle esigenze. Poiché ogni KB è diversa, occorre testare e scegliere la soglia più adatta alla propria KB. Per altre informazioni, vedere il [punteggio di attendibilità](../Concepts/confidence-score.md). 


### <a name="add-alternate-questions"></a>Aggiungere domande alternative
Le [domande alternative](../How-To/edit-knowledge-base.md) aumentano la probabilità di una corrispondenza con una query utente. Le domande alternative sono utili quando ci sono più modi per porre la stessa domanda. Ciò può includere modifiche alla struttura della frase e allo stile delle parole.

|Query originale|Query alternative|Modifica| 
|--|--|--|
|È disponibile il parcheggio?|Si dispone di parcheggio?|struttura della frase|
 |Ciao|Ehi<br>Salve!|stile delle parole o gergo|

### <a name="use-metadata-filters"></a>Usare filtri dei metadati
I [metadati](../How-To/edit-knowledge-base.md) aiutano a restringere i risultati di una query utente in base ai filtri. La risposta della knowledge base può essere diversa in base al tag di metadati, anche se la query è la stessa. Ad esempio, la domanda *"Dove si trova il parcheggio?"* può avere una risposta diversa se la posizione del ramo relativo al ristorante è diverso, ovvero se i metadati sono *Posizione: Seattle* anziché *Posizione: Redmond*.

### <a name="use-synonyms"></a>Usare sinonimi
Sebbene, in parte, sia disponibile il supporto per i sinonimi in lingua inglese, usare [variazioni delle parole](https://westus.dev.cognitive.microsoft.com/docs/services/5a93fcf85b4ccd136866eb37/operations/5ac266295b4ccd1554da75fd) per aggiungere sinonimi alle parole chiave che accettano una forma diversa. I sinonimi devono essere aggiunti a livello di servizio in QnA Maker e condivisi da tutte le knowledge base nel servizio.

|Parola originale|Sinonimi|
|--|--|
|acquistare|acquisto<br>netbanking<br>servizi bancari NET|

### <a name="use-distinct-words-to-differentiate-questions"></a>Usare parole diverse per distinguere le domande
Gli algoritmi di corrispondenza e classificazione di QnA Maker, che mettono in corrispondenza una query utente con una domanda nella knowledge base, funzionano meglio se ogni domanda risponde a esigenze diverse. La ripetizione dello stesso set di parole tra domande riduce la probabilità di scelta della risposta corretta per una determinata query utente che usa tali parole. 

Ad esempio, si potrebbero avere due QnA separate con le domande seguenti:

|QnA|
|--|
|dove si *trova* il parcheggio|
|dove si *trova* il bancomat|

Poiché queste due QnA sono formulate con parole molto simili, questa analogia potrebbe causare punteggi molto simili per molte query utente che hanno formula *"dove si `<x>` trova"*. Provare invece a differenziare chiaramente con query quali *"dov'è il parcheggio"* e *"dov'è il bancomat"*, evitando parole come "trova" che potrebbe ricorrere in molte domande nella KB. 


## <a name="collaborate"></a>Collaborare
QnA Maker permette agli utenti di [collaborare](../How-to/collaborate-knowledge-base.md) a una knowledge base. Per accedere alle knowledge base, gli utenti necessitano dell'accesso al gruppo di risorse di QnA Maker in Azure. Alcune organizzazioni potrebbero voler assegnare all'esterno le attività di modifica e manutenzione della knowledge base, mantenendo comunque la possibilità di proteggere l'accesso alle risorse di Azure. Questo modello di approvazione dell'editor di testo può essere ottenuto configurando due [servizi QnA Maker](../How-to/set-up-qnamaker-service-azure.md) identici in diverse sottoscrizioni e se si seleziona uno per il ciclo di test di modifica. Una volta completati i test, il contenuto della knowledge base può essere trasferito con un processo di [importazione-esportazione](../Tutorials/migrate-knowledge-base.md) al servizio QnA Maker del responsabile approvazione che infine pubblicherà la knowledge base e aggiornerà l'endpoint.

## <a name="next-steps"></a>Passaggi successivi

> [!div class="nextstepaction"]
> [Modificare una knowledge base](../How-to/edit-knowledge-base.md)
