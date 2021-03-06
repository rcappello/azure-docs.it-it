---
title: Che cos'è il monitoraggio di Azure Active Directory? (anteprima) | Microsoft Docs
description: Offre una panoramica generale sul monitoraggio di Azure Active Directory.
services: active-directory
documentationcenter: ''
author: priyamohanram
manager: mtillman
editor: ''
ms.assetid: e2b3d8ce-708a-46e4-b474-123792f35526
ms.service: active-directory
ms.devlang: na
ms.topic: overview
ms.tgt_pltfrm: na
ms.workload: identity
ms.component: report-monitor
ms.date: 09/24/2018
ms.author: priyamo
ms.reviewer: dhanyahk
ms.openlocfilehash: 82cd29cf1a635d1cd613d289a5d8db6ef54ee661
ms.sourcegitcommit: b4a46897fa52b1e04dd31e30677023a29d9ee0d9
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 10/17/2018
ms.locfileid: "49398741"
---
# <a name="what-is-azure-active-directory-monitoring-preview"></a>Che cos'è il monitoraggio di Azure Active Directory? (anteprima)

Con il monitoraggio di Azure Active Directory (Azure AD) è ora possibile indirizzare i log attività di Azure AD a endpoint diversi, dove sarà poi possibile conservarli per l'uso a lungo termine o integrarli con strumenti per informazioni di sicurezza e gestione degli eventi di terze parti per ottenere informazioni dettagliate sull'ambiente.

Attualmente, è possibile indirizzare i log a:

- Un account di archiviazione di Azure.
- Un hub eventi di Azure, in modo da poterli integrare con le istanze di Splunk e Sumologic.
- Un'area di lavoro di Azure Log Analytics, in cui è possibile analizzare i dati, creare dashboard e generare avvisi per eventi specifici.


## <a name="diagnostic-settings-configuration"></a>Configurazione delle impostazioni di diagnostica

Per configurare le impostazioni di monitoraggio per i log attività di Azure AD, accedere prima di tutto al [portale di Azure](https://portal.azure.com) e quindi selezionare **Azure Active Directory**. A questo punto, è possibile accedere alla pagina di configurazione delle impostazioni di diagnostica in due modi:

* Selezionare **Impostazioni di diagnostica** dalla sezione **Monitoraggio**.

    ![Impostazioni di diagnostica](./media/overview-monitoring/diagnostic-settings.png)
    
* Selezionare **Log di controllo** oppure **Accessi** e quindi selezionare **Esporta impostazioni**. 

    ![Esportazione impostazioni](./media/overview-monitoring/export-settings.png)


## <a name="route-logs-to-storage-account"></a>Indirizzare i log all'account di archiviazione

Tramite l'indirizzamento dei log a un account di archiviazione di Azure, è possibile conservarli per più tempo rispetto al periodo di conservazione predefinito indicato nei [criteri di conservazione di Azure Active Directory](reference-reports-data-retention.md). Informazioni su come [indirizzare i dati all'account di archiviazione](quickstart-azure-monitor-route-logs-to-storage-account.md).

## <a name="stream-logs-to-event-hub"></a>Eseguire lo streaming dei log in un hub eventi

L'indirizzamento dei log a un hub eventi di Azure consente l'integrazione con strumenti per informazioni di sicurezza e gestione degli eventi di terze parti, come Splunk e Sumologic. Questa integrazione consente di combinare i dati di log attività di Azure AD con altri dati gestiti dallo strumento per informazioni di sicurezza e gestione degli eventi, con la possibilità di ottenere quindi informazioni dettagliate più estese per il proprio ambiente. Informazioni su come [trasmettere i log a un hub eventi](tutorial-azure-monitor-stream-logs-to-event-hub.md).

## <a name="send-logs-to-log-analytics"></a>Inviare log a Log Analytics

[Log Analytics](https://docs.microsoft.com/azure/log-analytics/log-analytics-overview) è una soluzione che consente di consolidare i dati di monitoraggio da diverse origini e include un linguaggio di query e un motore di analisi che consentono di ottenere informazioni dettagliate sul funzionamento delle applicazioni e delle risorse. Con l'invio dei log attività di Azure AD a Log Analytics, è possibile recuperare e monitorare i dati rapidamente, nonché generare avvisi in modo efficace per i dati raccolti. Informazioni su come [inviare dati a Log Analytics](howto-integrate-activity-logs-with-log-analytics.md).

È anche possibile installare le visualizzazioni predefinite per i log attività di Azure AD per il monitoraggio di scenari comuni relativi agli accessi e agli eventi di controllo. Informazioni su come [installare e usare le visualizzazioni di Log Analytics per i log attività di Azure AD](howto-install-use-log-analytics-views.md).

## <a name="next-steps"></a>Passaggi successivi

* [Log attività in Monitoraggio di Azure](concept-activity-logs-azure-monitor.md)
* [Trasmettere i log di Azure AD a un hub eventi di Azure](tutorial-azure-monitor-stream-logs-to-event-hub.md)
* [Inviare log a Log Analytics](howto-integrate-activity-logs-with-log-analytics.md)