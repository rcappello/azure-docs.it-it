---
title: Configurare lead relativi ai clienti | Microsoft Docs
description: Configurare i lead relativi ai clienti nel portale Cloud Partner.
services: Azure, Marketplace, Cloud Partner Portal,
documentationcenter: ''
author: dan-wesley
manager: Patrick.Butler
editor: ''
ms.assetid: ''
ms.service: marketplace
ms.workload: ''
ms.tgt_pltfrm: ''
ms.devlang: ''
ms.topic: conceptual
ms.date: 09/14/2018
ms.author: pbutlerm
ms.openlocfilehash: 997727acd1bbaf17577160bb996aad7e21d49c86
ms.sourcegitcommit: 9eaf634d59f7369bec5a2e311806d4a149e9f425
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 10/05/2018
ms.locfileid: "48807538"
---
<a name="get-customer-leads"></a>Ottenere lead
==================

Questo articolo illustra come creare i lead dei clienti usando il portale Cloud Partner. È possibile connettere i lead al sistema CRM e integrarli nella pipeline di vendita.

## <a name="leads"></a>Clienti potenziali

I lead sono clienti interessati o che stanno distribuendo i prodotti dal [Microsoft Azure Marketplace](https://azuremarketplace.microsoft.com/) o da [AppSource](https://appsource.microsoft.com).

### <a name="azure-marketplace"></a>Azure Marketplace

1.  Il cliente esegue un "test drive" dell'offerta. I test drive sono un'opportunità accelerata per condividere immediatamente la propria attività con potenziali clienti senza limiti di ingresso. Tutti i test drive generano un lead per un cliente interessato a provare il prodotto per ottenere altre informazioni. Per altre informazioni sui test drive, vedere l'articolo sui [test drive del Microsoft Azure Marketplace](https://azuremarketplace.azureedge.net/documents/azure-marketplace-test-drive-program.pdf).

    ![Esempi di test drive di Microsoft Azure Marketplace](./media/cloud-partner-portal-get-customer-leads/test-drive-offer.png)
 

<!-- -->

2.  Il cliente accetta di condividere le informazioni dopo aver selezionato "Scarica adesso". Questo è un lead di **interesse iniziale**, in cui si condividono le informazioni su un cliente che ha espresso interesse nel ricevere il prodotto. Il lead si trova al vertice del grafico a imbuto relativo all'acquisizione dei clienti.

    ![Opzione "Scarica adesso"](./media/cloud-partner-portal-get-customer-leads/get-it-now-button.png)

3.  Il cliente seleziona "Acquisto" nel [portale di Azure](https://portal.azure.com/) per ottenere il prodotto. Questo è un lead **attivo**, in cui si condividono le informazioni relative a un cliente che ha iniziato a distribuire un prodotto.

    ![Opzione "Acquisto"](./media/cloud-partner-portal-get-customer-leads/purchase-button.png)


### <a name="appsource"></a>AppSource

1.  Il cliente ha fatto un "Test drive" per l'offerta. I test drive sono un'opportunità accelerata per condividere immediatamente la propria attività con potenziali clienti senza limiti di ingresso. Tutti i test drive generano un lead di un cliente interessato a provare il prodotto e ricevere altre informazioni. Per altre informazioni sui test drive vedere l'articolo sui [test drive del Marketplace di AppSource](https://appsource.microsoft.com/blogs/want-to-try-an-app-take-a-test-drive).

    ![Esempio di test drive](./media/cloud-partner-portal-get-customer-leads/test-drive-offer-2.png)

2.  Il cliente accetta di condividere le informazioni dopo aver selezionato "Scarica adesso". Questo è un lead di **interesse iniziale**, in cui si condividono informazioni su un cliente che ha espresso interesse nell'ottenere un prodotto. Il lead si trova al vertice del grafico a imbuto relativo all'acquisizione dei clienti.

      ![Opzione "Scarica adesso"](./media/cloud-partner-portal-get-customer-leads/get-it-now-button-2.png)


3.  Il cliente seleziona "Contattami" sull'offerta. Questo è un lead **attivo**, in cui si condividono informazioni su un cliente che ha chiesto di ricevere altre informazioni sul prodotto.

    ![Opzione "Desidero essere contattato"](./media/cloud-partner-portal-get-customer-leads/contact-me-image.png)

<a name="lead-data"></a>Dati lead
---------

Ogni lead ricevuto durante il processo di acquisizione del cliente presenta dati in campi specifici. Poiché si otterranno lead dai vari passaggi, il modo migliore per gestire i lead è deduplicare e personalizzare i follow-up. In questo modo, ogni cliente riceve un messaggio appropriato e si crea una relazione univoca.

### <a name="lead-source"></a>Origine lead

Il formato per un'origine lead è **Origine**-**Azione** |  **Offerta**

**Origini**: "AzureMarketplace", "AzurePortal", "TestDrive" e "AppSource (SPZA)"

**Azioni**:
- "INS": Installazione. Questa azione si trova in Azure Marketplace o AppSource quando un cliente acquista il prodotto.
- "PLT": significa Versione di valutazione condotta dal partner. Questa azione si trova in AppSource quando un cliente usa l'opzione "Contattami".
- "DNC": non contattare. L'azione si trova in AppSource quando un partner che è stato elencato in modo incrociato nella pagina app riceve una richiesta per essere contattato. Viene condiviso l'annuncio che il cliente è stato elencato nell'app, ma non deve essere contattato.
- "Crea": questa azione si trova solo nel portale di Azure e si genera quando un cliente acquista l'offerta dal proprio account.
- "StartTestDrive": questa azione riguarda solo i test drive e si genera quando un cliente avvia il test drive.

**Offerte**

Gli esempi seguenti mostrano identificatori univoci assegnati a un server di pubblicazione e a un'offerta specifica: checkpoint.check-point-r77-10sg-byol, bitnami.openedxcypress, and docusign.3701c77e-1cfa-4c56-91e6-3ed0b622145a.


### <a name="customer-info"></a>Informazioni sui clienti

I campi nell'esempio seguente mostrano le informazioni sul cliente contenute in un lead.
- Nome: John
- Cognome: Smith
- E-mail: jsmith\@microsoft.com
- Telefono: 1234567890
- Paese: Stati Uniti
- Azienda: Microsoft
- Posizione: CTO

>[!Note]
>Non tutti i dati dell'esempio precedente sono sempre disponibili per ogni lead.

Microsoft si è impegnata attivamente nel miglioramento dei lead, pertanto se un campo dati non viene visualizzato ma si desidera visualizzarlo qui [inviare i commenti a Microsoft](mailto:AzureMarketOnboard@microsoft.com).

<a name="how-to-connect-your-crm-system-with-the-cloud-partner-portal"></a>Come connettere il sistema CRM con il portale cloud per i partner
------------------------------------------------------------

Per iniziare a ottenere lead, è stato creato il connettore di gestione di lead nel portale Cloud Partner in modo che si possano inserire agevolmente le informazioni di CRM per creare la connessione. A questo punto è possibile sfruttare facilmente i lead generati dal marketplace senza un notevole sforzo di progettazione per integrarli con un sistema esterno.

![Connettore di gestione di lead](./media/cloud-partner-portal-get-customer-leads/lead-management-connector.png)

I lead possono essere scritti in un'ampia gamma di sistemi CRM o direttamente in una tabella di Archiviazione di Azure in cui è possibile gestirli come si desidera. Tutti i seguenti collegamenti forniscono istruzioni per la connessione a provider di destinazione di lead:

-   [Dynamics CRM Online](./cloud-partner-portal-lead-management-instructions-dynamics.md): per ottenere le istruzioni sulle modalità di configurazione di Dynamics CRM Online per ottenere i lead.
-   [Marketo](./cloud-partner-portal-lead-management-instructions-marketo.md): per ottenere istruzioni sull'impostazione della configurazione dei lead di Marketo e ottenere i lead.
-    [Salesforce](./cloud-partner-portal-lead-management-instructions-salesforce.md): per ottenere istruzioni sulle impostazioni dell'istanza Salesforce e ottenere i lead.
-    [Tabella di Azure](./cloud-partner-portal-lead-management-instructions-azure-table.md): per ottenere le istruzioni per la configurazione dell'account di archiviazione di Azure e ottenere i lead in una tabella di Azure.
-   [Endpoint HTTPS](./cloud-partner-portal-lead-management-instructions-https.md): per ottenere le istruzioni su come configurare l'endpoint HTTPS per ottenere i lead.

Dopo la configurazione del provider di destinazione del lead e la pubblicazione dell'offerta, la connessione sarà convalidata e verrà inviato un lead di prova. Quando si visualizza l'offerta prima della distribuzione, è inoltre possibile testare la connessione lead quando si tenta di acquisire l'offerta nell'ambiente di anteprima. È importante assicurarsi che le impostazioni dei lead rimangano aggiornate affinché nessun lead venga perso. Pertanto, assicurarsi di aggiornare le connessioni ogni volta che c'è una modifica da parte dell'utente.

<a name="what-next"></a>Come procedere?
----------

Una eseguita la configurazione tecnica, è necessario incorporare i lead nelle vendite attuali, nella strategia di marketing e nei processi operativi. L'intento è quello di comprendere meglio il processo complessivo di vendita e di collaborare con l'utente per creare lead di alta qualità e dari sufficienti a garantire il successo dell'utente. Ogni commento su come ottimizzare e migliorare i lead inviati con dati aggiuntivi per contribuire ad avere clienti di successo è apprezzato. Invitiamo a [fornire feedback](mailto:AzureMarketOnboard@microsoft.com) e suggerimenti per consentire al team delle vendite di sviluppare i lead del Marketplace in modo ottimale.
