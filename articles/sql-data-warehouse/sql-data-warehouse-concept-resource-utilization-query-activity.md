---
title: Facilità di gestione e monitoraggio di SQL Data Warehouse di Azure - Attività di query, utilizzo delle risorse | Microsoft Docs
description: Informazioni sulle funzionalità disponibili per gestire e monitorare Azure SQL Data Warehouse. Usare il portale di Azure e Dynamic Management View (DMV, viste a gestione dinamica) per comprendere l'attività di query e l'utilizzo delle risorse del data warehouse.
services: sql-data-warehouse
author: kevinvngo
manager: craigg
ms.service: sql-data-warehouse
ms.topic: conceptual
ms.component: manage
ms.date: 08/26/2018
ms.author: kevin
ms.reviewer: igorstan
ms.openlocfilehash: c783045d242725ee19dfe7e0baee13625d986312
ms.sourcegitcommit: 2b2129fa6413230cf35ac18ff386d40d1e8d0677
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 08/30/2018
ms.locfileid: "43246495"
---
# <a name="monitoring-resource-utilization-and-query-activity-in-azure-sql-data-warehouse"></a>Monitoraggio dell'attività di query e dell'utilizzo delle risorse in Azure SQL Data Warehouse
Azure SQL Data Warehouse offre una ricca esperienza di monitoraggio nel portale di Azure per esplorare informazioni dettagliate sul carico di lavoro del data warehouse. Il portale di Azure è lo strumento consigliato per il monitoraggio del data warehouse, in quanto fornisce periodi di conservazione, avvisi, raccomandazioni, grafici personalizzabili, nonché dashboard di metriche e registri configurabili. Il portale consente inoltre l'integrazione con altri servizi di monitoraggio di Azure come Operations Management Suite (OMS) x /Log Analytics e Monitoraggio di Azure per fornire un'esperienza di monitoraggio olistica non solo al data warehouse, ma anche all'intera piattaforma Azure analitica per un'esperienza di monitoraggio integrata. Questa documentazione descrive le funzionalità di monitoraggio disponibili per ottimizzare e gestire la piattaforma analitica con SQL Data Warehouse. 

## <a name="resource-utilization"></a>Utilizzo delle risorse 
Le seguenti metriche di integrità sono disponibili nel portale di Azure.

| Nome della metrica                           | DESCRIZIONE     | Tipo di aggregazione |
| --------------------------------------- | ---------------- | --------------------------------------- |
| Percentuale CPU                          | Utilizzo della CPU in tutti i nodi per il data warehouse | Massima      |
| Percentuale di I/O di dati                      | Utilizzo di I/O in tutti i nodi per il data warehouse | Massima   |
| Connessioni riuscite                  | Numero di connessioni ai dati riuscite | Totale            |
| Connessioni non riuscite                      | Numero di connessioni al data warehouse non riuscite | Totale            |
| Blocco da parte del firewall                     | Numero di accessi al data warehouse bloccati | Totale            |
| Limite DWU                              | Obiettivo del livello di servizio del data warehouse | Massima   |
| Percentuale DWU                          | Valore massimo tra percentuale di CPU e percentuale di I/O | Massima   |
| Uso DWU                                | Limite DWU * percentuale DWU | Massima   |
| Percentuale dei riscontri nella cache | (Riscontri nella cache/Mancato riscontro nella cache) * 100, dove "riscontri nella cache" è la somma di tutte le occorrenze di segmenti columnstore della cache SSD locale e "mancato riscontro nella cache" è il mancato riscontro di segmenti columnstore nella cache SSD locale sommato tra tutti i nodi | Massima |
| Percentuale della cache utilizzata | (Cache usata/Capacità della cache) * 100, dove "cache usata" è la somma di tutti i byte nella cache SSD locale in tutti i nodi e "capacità della cache" è la somma della capacità di archiviazione della cache SSD locale in tutti i nodi | Massima |

## <a name="query-activity"></a>Attività di query
Per un'esperienza programmatica durante il monitoraggio di SQL Data Warehouse tramite T-SQL, il servizio fornisce un set di viste a gestione dinamica (DMV). Queste viste sono utili durante la risoluzione dei problemi e l'identificazione dei colli di bottiglia nelle prestazioni con il carico di lavoro.

Per visualizzare l'elenco delle viste a gestione dinamica fornite da SQL Data Warehouse, fare riferimento a questa [documentazione](https://docs.microsoft.com/azure/sql-data-warehouse/sql-data-warehouse-reference-tsql-system-views#sql-data-warehouse-dynamic-management-views-dmvs). 

## <a name="metrics-and-diagnostics-logging"></a>Metriche e registrazione diagnostica
Le metriche e i registri possono essere esportati in [Operations Management Suite](https://azure.microsoft.com/resources/videos/operations-management-suite-oms-overview/) (OMS), in particolare i componenti di [Log Analytics](https://docs.microsoft.com/azure/log-analytics/log-analytics-overview); ed è possibile accedervi a livello di programmatico tramite [Ricerca log](https://docs.microsoft.com/azure/log-analytics/log-analytics-tutorial-viewdata).


> [!NOTE]
> A partire da agosto 2018, i registri vengono implementati in SQL Data Warehouse

## <a name="next-steps"></a>Passaggi successivi
Le seguenti guide introduttive descrivono scenari e casi d'uso comuni in cui avviene il monitoraggio e la gestione del data warehouse:

- [Monitorare il carico di lavoro del data warehouse con viste a gestione dinamica](https://docs.microsoft.com/azure/sql-data-warehouse/sql-data-warehouse-manage-monitor)

