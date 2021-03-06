---
title: Creare query per i messaggi B2B in Log Analytics - App per la logica di Azure | Microsoft Docs
description: Creare query per monitorare i messaggi AS2, X12 ed EDIFACT con Log Analytics per App per la logica di Azure
services: logic-apps
ms.service: logic-apps
ms.suite: integration
author: divyaswarnkar
ms.author: divswa
ms.reviewer: jonfan, estfan, LADocs
ms.topic: article
ms.date: 06/19/2018
ms.openlocfilehash: baccd255fc2812eae0de3a98dfcef3dcbc7e1b46
ms.sourcegitcommit: 2ad510772e28f5eddd15ba265746c368356244ae
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 08/28/2018
ms.locfileid: "43124271"
---
# <a name="create-queries-for-tracking-as2-x12-and-edifact-messages-in-log-analytics-for-azure-logic-apps"></a>Creare query per il monitoraggio dei messaggi AS2, X12 ed EDIFACT in Log Analytics per App per la logica di Azure

Per trovare i messaggi AS2, X12 o EDIFACT che si vuole monitorare con [Azure Log Analytics](../log-analytics/log-analytics-overview.md), è possibile creare query per filtrare le azioni in base a criteri specifici. Ad esempio, è possibile trovare i messaggi in base a un numero di controllo interscambio specifico.

## <a name="requirements"></a>Requisiti

* Un'app per la logica configurata con la registrazione diagnostica. Informazioni su [come creare un'app per la logica](../logic-apps/quickstart-create-first-logic-app-workflow.md) e [come configurare la registrazione per tale app per la logica](../logic-apps/logic-apps-monitor-your-logic-apps.md#azure-diagnostics).

* Un account di integrazione configurato con il monitoraggio e la registrazione. Informazioni su [come creare un account di integrazione](../logic-apps/logic-apps-enterprise-integration-create-integration-account.md) e [come configurare il monitoraggio e la registrazione per tale account](../logic-apps/logic-apps-monitor-b2b-message.md).

* Se non è già stato fatto, [pubblicare i dati di diagnostica in Log Analytics](../logic-apps/logic-apps-track-b2b-messages-omsportal.md) e [configurare la verifica dei messaggi in Log Analytics](../logic-apps/logic-apps-track-b2b-messages-omsportal.md).

> [!NOTE]
> Soddisfatti i requisiti precedenti, sarà disponibile un'area di lavoro in Log Analytics. È consigliabile usare la stessa area di lavoro per tenere traccia delle comunicazioni B2B in Log Analytics. 
>  
> Se non si dispone di un'area di lavoro di Log Analytics, vedere [Creare un'area di lavoro di Log Analytics](../log-analytics/log-analytics-quick-create-workspace.md).

## <a name="create-message-queries-with-filters-in-log-analytics"></a>Creare query per i messaggi con i filtri in Log Analytics

Questo esempio illustra come trovare i messaggi in base a un numero di controllo interscambio.

> [!TIP] 
> Se si conosce il nome dell'area di lavoro di Log Analytics, passare alla home page dell'area di lavoro (`https://{your-workspace-name}.portal.mms.microsoft.com`) e iniziare dal passaggio 4. Altrimenti iniziare dal passaggio 1.

1. Nel [portale di Azure](https://portal.azure.com) scegliere **Tutti i servizi**. Cercare "Log Analytics" e quindi scegliere **Log Analytics**, come illustrato qui:

   ![Trovare Log Analytics](media/logic-apps-track-b2b-messages-omsportal-query-filter-control-number/browseloganalytics.png)

2. In **Log Analytics** trovare e selezionare l'area di lavoro di Log Analytics.

   ![Selezionare l'area di lavoro di Log Analytics](media/logic-apps-track-b2b-messages-omsportal-query-filter-control-number/selectla.png)

3. In **Gestione** scegliere **Ricerca log**.

   ![Scegliere Ricerca log](media/logic-apps-track-b2b-messages-omsportal-query-filter-control-number/azure-portal-page.png)

4. Nella casella di ricerca inserire il campo che si vuole trovare e premere **Invio**. Quando si inizia a digitare, Log Analytics mostra le corrispondenze e operazioni che è possibile usare. Altre informazioni su [come trovare i dati in Log Analytics](../log-analytics/log-analytics-log-searches.md).

   Questo esempio cerca gli eventi con **Type=AzureDiagnostics**.

   ![Iniziare a digitare una stringa di query](media/logic-apps-track-b2b-messages-omsportal-query-filter-control-number/oms-start-query.png)

5. Nella barra a sinistra scegliere l'intervallo di tempo che si vuole visualizzare. Per aggiungere un filtro alla query, scegliere **+Aggiungi**.

   ![Aggiungere un filtro alla query](media/logic-apps-track-b2b-messages-omsportal-query-filter-control-number/query1.png)

6. In **Aggiungi filtri** immettere il nome del filtro per trovare quello desiderato. Selezionare il filtro e scegliere **+Aggiungi**.

   Per trovare il numero di controllo interscambio, questo esempio cerca la parola "interscambio" e seleziona **event_record_messageProperties_interchangeControlNumber_s** come filtro.

   ![Selezionare il filtro](media/logic-apps-track-b2b-messages-omsportal-query-filter-control-number/oms-query-add-filter.png)

7. Nella barra a sinistra selezionare il valore del filtro che si vuole usare e scegliere **Applica**.

   Questo esempio consente di selezionare il numero di controllo interscambio per i messaggi desiderati.

   ![Selezionare il valore del filtro](media/logic-apps-track-b2b-messages-omsportal-query-filter-control-number/oms-query-select-filter-value.png)

8. Tornare ora alla query che si sta creando. La query viene aggiornata con l'evento e il valore del filtro selezionati. Vengono ora filtrati anche i risultati precedenti.

    ![Tornare alla query con i risultati filtrati](media/logic-apps-track-b2b-messages-omsportal-query-filter-control-number/oms-query-filtered-results.png)

<a name="save-oms-query"></a>

## <a name="save-your-query-for-future-use"></a>Per salvare la query per un uso futuro

1. Dalla query nella pagina **Ricerca log** scegliere **Salva**. Assegnare un nome alla query, selezionare una categoria e scegliere **Salva**.

   ![Assegnare un nome e una categoria alla query](media/logic-apps-track-b2b-messages-omsportal-query-filter-control-number/oms-query-save.png)

2. Per visualizzare la query, scegliere **Preferiti**.

   ![Scegliere "Preferiti"](media/logic-apps-track-b2b-messages-omsportal-query-filter-control-number/oms-query-favorites.png)

3. In **Ricerche salvate** selezionare la query per visualizzare i risultati. Per aggiornare la query e trovare risultati diversi, modificare la query.

   ![Selezionare la query](media/logic-apps-track-b2b-messages-omsportal-query-filter-control-number/oms-log-search-find-favorites.png)

## <a name="find-and-run-saved-queries-in-log-analytics"></a>Trovare ed eseguire le query salvate in Log Analytics

1. Aprire la home page dell'area di lavoro di Log Analytics (`https://{your-workspace-name}.portal.mms.microsoft.com`) e scegliere **Ricerca log**.

   ![Nella home page dell'area di lavoro di Log Analytics scegliere "Ricerca log"](media/logic-apps-track-b2b-messages-omsportal-query-filter-control-number/logsearch.png)

   -oppure-

   ![Dal menu scegliere "Ricerca log"](media/logic-apps-track-b2b-messages-omsportal-query-filter-control-number/logsearch-2.png)

2. Nella home page **Ricerca log** scegliere **Preferiti**.

   ![Scegliere "Preferiti"](media/logic-apps-track-b2b-messages-omsportal-query-filter-control-number/oms-log-search-favorites.png)

3. In **Ricerche salvate** selezionare la query per visualizzare i risultati. Per aggiornare la query e trovare risultati diversi, modificare la query.

   ![Selezionare la query](media/logic-apps-track-b2b-messages-omsportal-query-filter-control-number/oms-log-search-find-favorites.png)

## <a name="next-steps"></a>Passaggi successivi

* [Schemi di rilevamento AS2](../logic-apps/logic-apps-track-integration-account-as2-tracking-schemas.md)
* [Schemi di rilevamento X12](../logic-apps/logic-apps-track-integration-account-x12-tracking-schema.md)
* [Schemi di rilevamento personalizzati](../logic-apps/logic-apps-track-integration-account-custom-tracking-schema.md)