---
title: Metriche del database SQL di Azure e registrazione diagnostica | Microsoft Docs
description: Informazioni sulla configurazione del database SQL di Azure per archiviare le statistiche sull'uso delle risorse, sulla connettività e sull'esecuzione delle query.
services: sql-database
ms.service: sql-database
ms.subservice: performance
ms.custom: ''
ms.devlang: ''
ms.topic: conceptual
author: danimir
ms.author: v-daljep
ms.reviewer: carlrab
manager: craigg
ms.date: 09/20/2018
ms.openlocfilehash: bf9185ece171ef0595aa3470fd52b839eb5d6136
ms.sourcegitcommit: 51a1476c85ca518a6d8b4cc35aed7a76b33e130f
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 09/25/2018
ms.locfileid: "47165960"
---
# <a name="azure-sql-database-metrics-and-diagnostics-logging"></a>Metriche del database SQL di Azure e registrazione diagnostica 

Database SQL di Azure e database di istanza gestita può creare log di diagnostica e metriche per facilitare il monitoraggio delle prestazioni. È possibile configurare un database per trasmettere l'utilizzo delle risorse, ruoli di lavoro e sessioni e connettività in una di queste risorse di Azure:

* **Analisi SQL di Azure**: usato come soluzione di monitoraggio delle prestazioni intelligenti del database di Azure integrato con funzionalità di creazione di report e avvisi e mitigazione.
* **Hub eventi di Azure**: usata per l'integrazione dei dati di telemetria di database SQL con soluzioni di monitoraggio personalizzate o pipeline attive.
* **Archiviazione di Azure**: usata per l'archiviazione di enormi quantità di dati di telemetria a un costo conveniente.

    ![Architettura](./media/sql-database-metrics-diag-logging/architecture.png)

## <a name="enable-logging-for-a-database"></a>Abilitare la registrazione per un database

Le metriche e la registrazione diagnostica sul Database SQL o di istanza gestita non sono abilitate per impostazione predefinita. È possibile abilitare e gestire le metriche e la registrazione di telemetria diagnostica su un database usando uno dei metodi seguenti:

- Portale di Azure
- PowerShell
- Interfaccia della riga di comando di Azure
- API REST di Monitoraggio di Azure 
- Modello di Azure Resource Manager

Quando si abilitano le metriche e la registrazione diagnostica, è necessario specificare la risorsa di Azure in cui saranno raccolti i dati selezionati. Le opzioni disponibili includono:

- Analitica SQL
- Hub eventi
- Archiviazione 

È possibile eseguire il provisioning di una nuova risorsa di Azure o selezionare una risorsa esistente. Dopo aver selezionato una risorsa, usando un'opzione delle impostazioni di diagnostica del database, è necessario specificare i dati da raccogliere. Le opzioni disponibili, con supporto per il Database SQL di Azure e database in istanza gestita includono:

| Dati di telemetria di monitoraggio | Supporto del database SQL di Azure | Database nel supporto per Istanza gestita |
| :------------------- | ------------------- | ------------------- |
| [Tutte le metriche](sql-database-metrics-diag-logging.md#all-metrics): contiene la percentuale DTU/CPU, limite DTU/CPU, percentuale lettura dati fisici, percentuale scrittura log, riuscito/non riuscito/bloccato dalle connessioni firewall, percentuale sessioni, percentuale ruoli di lavoro, risorsa di archiviazione, percentuale di archiviazione, percentuale di archiviazione XTP. | Yes | No  |
| [QueryStoreRuntimeStatistics](sql-database-metrics-diag-logging.md#query-store-runtime-statistics): contiene le informazioni sulle statistiche di runtime delle query, ad esempio l'uso della CPU e le statistiche sulla durata delle query. | Yes | Yes |
| [QueryStoreWaitStatistics](sql-database-metrics-diag-logging.md#query-store-wait-statistics): contiene le informazioni sulle statistiche di attesa delle query che indicano le cause di attesa delle query, ad esempio CPU, log o blocchi. | Yes | Yes |
| [Errors](sql-database-metrics-diag-logging.md#errors-dataset): contiene le informazioni sugli errori SQL che si sono verificati in questo database. | Yes | No  |
| [DatabaseWaitStatistics](sql-database-metrics-diag-logging.md#database-wait-statistics-dataset): contiene informazioni sul tempo di attesa trascorso da un database per tipi di attesa diversi. | Yes | No  |
| [Timeouts](sql-database-metrics-diag-logging.md#time-outs-dataset): contiene informazioni sui timeout che si sono verificati in un database. | Yes | No  |
| [Blocks](sql-database-metrics-diag-logging.md#blockings-dataset): contiene informazioni sugli eventi di blocco che si sono verificati in un database. | Yes | No  |
| [SQLInsights](sql-database-metrics-diag-logging.md#intelligent-insights-dataset): contiene Intelligent Insights nelle prestazioni. [Altre informazioni su Intelligent Insights](sql-database-intelligent-insights.md). | Yes | Yes |

**Si noti**: per usare i log di controllo e SQLSecurityAuditEvents, anche se queste opzioni sono disponibili all'interno di impostazioni di diagnostica del database, questi log devono essere abilitati solo attraverso la soluzione **Controllo SQL** per la configurazione del flusso di dati di telemetria per la risorsa di archiviazione, hub eventi o Log Analytics.

Se si seleziona Hub eventi o un account di archiviazione, è possibile specificare criteri di conservazione. Questi criteri eliminano i dati antecedenti a un periodo selezionato. Se si specifica Log Analytics, i criteri di conservazione dipendono dal piano tariffario selezionato. Per altre informazioni, vedere [Prezzi di Log Analytics](https://azure.microsoft.com/pricing/details/log-analytics/). 

## <a name="enable-logging-for-elastic-pools-or-managed-instance"></a>Abilitare la registrazione per i pool elastici o istanza gestita

Le metriche e la diagnostica che registrano pool elastici o istanza gestita non sono abilitate per impostazione predefinita. È possibile abilitare e gestire le metriche e la registrazione di dati di telemetria di diagnostica per istanza gestita o un pool elastico. I dati seguenti sono disponibili per la raccolta:

| Dati di telemetria di monitoraggio | Supporto pool elastico | Supporto per Istanza gestita |
| :------------------- | ------------------- | ------------------- |
| [Tutte le metriche](sql-database-metrics-diag-logging.md#all-metrics) (pool elastico): contiene percentuale eDTU/CPU, limite eDTU/CPU, limite eDTU, percentuale lettura dati fisici, percentuale scrittura log, percentuale sessioni, percentuale ruoli di lavoro, risorsa di archiviazione, percentuale di archiviazione, limite di archiviazione, percentuale di archiviazione XTP. | Yes | N/D |
| [ResourceUsageStats](sql-database-metrics-diag-logging.md#resource-usage-stats) (istanza gestita): contiene il numero di vCore, percentuale CPU media, richieste IO, byte letti/scritti, spazio di archiviazione riservato, spazio di archiviazione usato. | N/D | Yes |

Per le metriche e le categorie di log supportate dai vari servizi di Azure, è consigliabile leggere:

* [Panoramica delle metriche in Microsoft Azure](../monitoring-and-diagnostics/monitoring-overview-metrics.md)
* [Panoramica dei log di diagnostica di Azure](../monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs.md) 

### <a name="azure-portal"></a>Portale di Azure

- Per abilitare la raccolta delle metriche e dei log di diagnostica nel database SQL o nel database di istanza gestita, passare al database e fare clic su **Impostazioni di diagnostica**. Selezionare **+ Aggiungi impostazione di diagnostica** per configurare una nuova impostazione, o **Modifica impostazione** per modificare un'impostazione esistente.

   ![Abilitazione nel portale di Azure](./media/sql-database-metrics-diag-logging/enable-portal.png)

- Creare nuove impostazioni o modificare le impostazioni di diagnostica esistenti per il **database SQL di Azure** selezionando la destinazione e la telemetria.

   ![Impostazioni di diagnostica](./media/sql-database-metrics-diag-logging/diagnostics-portal.png)

- Creare nuove impostazioni o modificare le impostazioni di diagnostica esistenti per il **database SQL di Azure** selezionando la destinazione e la telemetria.

   ![Impostazioni di diagnostica](./media/sql-database-metrics-diag-logging/diagnostics-portal-mi.png)

### <a name="powershell"></a>PowerShell

Per abilitare le metriche e la registrazione diagnostica con PowerShell, usare i comandi seguenti:

- Per abilitare la memorizzazione dei log di diagnostica in un account di archiviazione, usare questo comando:

   ```powershell
   Set-AzureRmDiagnosticSetting -ResourceId [your resource id] -StorageAccountId [your storage account id] -Enabled $true
   ```

   L'ID account di archiviazione è l'ID risorsa per l'account di archiviazione a cui devono essere inviati i log.

- Per abilitare lo streaming dei log di diagnostica in un Hub eventi, usare questo comando:

   ```powershell
   Set-AzureRmDiagnosticSetting -ResourceId [your resource id] -ServiceBusRuleId [your service bus rule id] -Enabled $true
   ```

   L'ID regola del bus di servizio di Azure è una stringa nel formato seguente:

   ```powershell
   {service bus resource ID}/authorizationrules/{key name}
   ``` 

- Per consentire l'invio dei log di diagnostica a un'area di lavoro di Log Analytics, usare questo comando:

   ```powershell
   Set-AzureRmDiagnosticSetting -ResourceId [your resource id] -WorkspaceId [resource id of the log analytics workspace] -Enabled $true
   ```

- È possibile ottenere l'ID risorsa dell'area di lavoro di Log Analytics usando il comando seguente:

   ```powershell
   (Get-AzureRmOperationalInsightsWorkspace).ResourceId
   ```

È possibile combinare questi parametri per abilitare più opzioni di output.

### <a name="to-configure-multiple-azure-resources"></a>Per configurare più risorse di Azure

Per supportare più sottoscrizioni, usare lo script di PowerShell contenuto in [Enable Azure resource metrics logging using PowerShell](https://blogs.technet.microsoft.com/msoms/2017/01/17/enable-azure-resource-metrics-logging-using-powershell/) (Abilitare la registrazione delle metriche sulle risorse di Azure usando PowerShell).

Specificare l'ID risorsa dell'area di lavoro &lt;$WSID&gt; come parametro quando si esegue lo script (Enable-AzureRMDiagnostics.ps1) per inviare i dati di diagnostica da più risorse all'area di lavoro. Per ottenere l'ID dell'area di lavoro &lt;$WSID&gt; a cui inviare i dati di diagnostica, sostituire &lt;subID&gt; con l'ID sottoscrizione, &lt;RG_NAME&gt; con il nome del gruppo di risorse e &lt;WS_NAME&gt; con il nome dell'area di lavoro nello script seguente.

- Per configurare più risorse di Azure, usare i comandi seguenti:

    ```powershell
    PS C:\> $WSID = "/subscriptions/<subID>/resourcegroups/<RG_NAME>/providers/microsoft.operationalinsights/workspaces/<WS_NAME>"
    PS C:\> .\Enable-AzureRMDiagnostics.ps1 -WSID $WSID
    ```

### <a name="azure-cli"></a>Interfaccia della riga di comando di Azure

Per abilitare le metriche e la registrazione diagnostica con l'interfaccia della riga di comando di Azure, usare i comandi seguenti:

- Per abilitare la memorizzazione dei log di diagnostica in un account di archiviazione, usare questo comando:

   ```azurecli-interactive
   azure insights diagnostic set --resourceId <resourceId> --storageId <storageAccountId> --enabled true
   ```

   L'ID account di archiviazione è l'ID risorsa per l'account di archiviazione a cui devono essere inviati i log.

- Per abilitare lo streaming dei log di diagnostica in un Hub eventi, usare questo comando:

   ```azurecli-interactive
   azure insights diagnostic set --resourceId <resourceId> --serviceBusRuleId <serviceBusRuleId> --enabled true
   ```

   L'ID regola del bus di servizio è una stringa nel formato seguente:

   ```azurecli-interactive
   {service bus resource ID}/authorizationrules/{key name}
   ```

- Per consentire l'invio dei log di diagnostica a un'area di lavoro di Log Analytics, usare questo comando:

   ```azurecli-interactive
   azure insights diagnostic set --resourceId <resourceId> --workspaceId <resource id of the log analytics workspace> --enabled true
   ```

È possibile combinare questi parametri per abilitare più opzioni di output.

### <a name="rest-api"></a>API REST

Informazioni su come [modificare le impostazioni di diagnostica usando l'API REST di Monitoraggio di Azure](https://docs.microsoft.com/rest/api/monitor/diagnosticsettings). 

### <a name="resource-manager-template"></a>Modello di Resource Manager

Informazioni su come [abilitare le impostazioni di diagnostica durante la creazione di risorse con un modello di Resource Manager](../monitoring-and-diagnostics/monitoring-enable-diagnostic-logs-using-template.md). 

## <a name="stream-into-log-analytics"></a>Eseguire lo streaming in Log Analytics 
I log di diagnostica e le metriche del database SQL possono essere trasmessi in Log Analytics con l'opzione **Invia a Log Analytics** integrata nel portale. È anche possibile abilitare Log Analytics usando un'impostazione di diagnostica tramite i cmdlet PowerShell, l'interfaccia della riga di comando di Azure o l'API REST di Monitoraggio di Azure.

### <a name="installation-overview"></a>Panoramica dell'installazione

Monitorare una flotta del database SQL è semplice con Log Analytics. Sono necessari tre passaggi:

1. Creare una risorsa Log Analytics.

2. Configurare i database per registrare le metriche e i log di diagnostica nella risorsa Log Analytics creata.

3. Installare la soluzione **Analisi SQL di Azure** da Azure Marketplace.

### <a name="create-a-log-analytics-resource"></a>Creare una risorsa Log Analytics

1. Selezionare **Creare una risorsa** nel menu a sinistra.

2. Selezionare **Monitoraggio e gestione**.

3. Selezionare **Log Analytics**.

4. Compilare il modulo Log Analytics con le informazioni aggiuntive necessarie: nome dell'area di lavoro, sottoscrizione, gruppo di risorse, posizione e livello di prezzo.

   ![Log Analytics](./media/sql-database-metrics-diag-logging/log-analytics.png)

### <a name="configure-databases-to-record-metrics-and-diagnostics-logs"></a>Configurare i database per registrare le metriche e i log di diagnostica

Il modo più semplice per configurare la posizione in cui i database registrano le metriche è tramite il portale di Azure. Nel portale passare alla risorsa del database SQL e selezionare **Impostazioni di diagnostica**. 

### <a name="install-the-sql-analytics-solution-from-the-gallery"></a>Installare la soluzione Analisi SQL dalla raccolta

1. Dopo aver creato la risorsa Log Analytics con i dati trasmessi al suo interno, installare una soluzione Analisi SQL. Nella home page, dal menu laterale selezionare **Raccolta di soluzioni**. Nella raccolta selezionare la soluzione **Analisi SQL di Azure** e **Aggiungi**.

   ![Soluzione di monitoraggio](./media/sql-database-metrics-diag-logging/monitoring-solution.png)

2. Nella home page appare il riquadro **Analisi SQL di Azure**. Selezionare questo riquadro per aprire il dashboard di Analisi SQL.

### <a name="use-the-sql-analytics-solution"></a>Usare la soluzione Analisi SQL

Analisi SQL è un dashboard gerarchico che consente di spostarsi nella gerarchia di risorse del database SQL. Per informazioni su come usare la soluzione Analisi SQL, vedere [Monitorare un database SQL usando la soluzione Analisi SQL](../log-analytics/log-analytics-azure-sql.md).

## <a name="stream-into-event-hubs"></a>Trasmettere un flusso a Hub eventi

I log di diagnostica e le metriche del database SQL possono essere trasmessi in Hub eventi con l'opzione **Invia a Log Analytics** integrata nel portale. È anche possibile abilitare l'ID regola del bus di servizio usando un'impostazione di diagnostica tramite i cmdlet PowerShell, l'interfaccia della riga di comando di Azure o l'API REST di Monitoraggio di Azure. 

### <a name="what-to-do-with-metrics-and-diagnostics-logs-in-event-hubs"></a>Cosa fare con le metriche e i log di diagnostica in Hub eventi
Dopo aver eseguito lo streaming dei dati selezionati in Hub eventi, sarà possibile iniziare a valutare scenari di monitoraggio avanzati. Hub eventi funge da ingresso per una pipeline di eventi. Dopo aver raccolto i dati in un hub eventi, potranno essere trasformati e archiviati usando qualsiasi provider di analisi in tempo reale o adattatore di invio in batch/archiviazione. Hub eventi separa la produzione di un flusso di eventi dal consumo di tali eventi. In questo modo, i consumer eventi possono accedere agli eventi in una pianificazione personalizzata. Per altre informazioni sugli hub eventi, vedere:

- [Che cos'è Hub eventi?](../event-hubs/event-hubs-what-is-event-hubs.md)
- [Introduzione all'Hub eventi](../event-hubs/event-hubs-csharp-ephcs-getstarted.md)


Ecco alcuni esempi di come è possibile usare la funzionalità di trasmissione:

* **Visualizzare l'integrità del servizio mediante la trasmissione di dati sul "percorso critico" a Power BI**. Con Hub eventi, Analisi di flusso e Power BI è possibile trasformare facilmente i dati di metriche e diagnostica in informazioni quasi in tempo reale sui servizi di Azure. Per una panoramica della configurazione di un hub eventi, dell'elaborazione dei dati con Analisi di flusso e dell'uso di Power BI come output, vedere [Analisi di flusso e Power BI](../stream-analytics/stream-analytics-power-bi-dashboard.md).

* **Eseguire lo streaming dei log in stream di registrazione e telemetria di terze parti**. Usando lo streaming di Hub eventi è possibile trasmettere le metriche e i log di diagnostica a diverse soluzioni di monitoraggio e analisi di log di terze parti. 

* **Compilare una piattaforma di registrazione e telemetria personalizzata**. Se è disponibile una piattaforma di telemetria personalizzata o si intende crearne una, le caratteristiche di pubblicazione-sottoscrizione con scalabilità elevata di Hub eventi offrono grande flessibilità per l'inserimento dei log di diagnostica. [Vedere la guida all'uso dell'hub eventi in una piattaforma di telemetria su scala globale di Dan Rosanova](https://azure.microsoft.com/documentation/videos/build-2015-designing-and-sizing-a-global-scale-telemetry-platform-on-azure-event-Hubs/).

## <a name="stream-into-storage"></a>Streaming in Archiviazione

I log di diagnostica e le metriche del database SQL possono essere archiviati in Archiviazione usando l'opzione **Archivia in un account di archiviazione** integrata nel portale. È anche possibile abilitare Archiviazione usando un'impostazione di diagnostica tramite i cmdlet PowerShell, l'interfaccia della riga di comando di Azure o l'API REST di Monitoraggio di Azure.

### <a name="schema-of-metrics-and-diagnostics-logs-in-the-storage-account"></a>Schema delle metriche e dei log di diagnostica nell'account di archiviazione

Dopo aver configurato la raccolta delle metriche e dei log di diagnostica, verrà creato un contenitore di archiviazione nell'account di archiviazione selezionato quando sono disponibili le prime righe di dati. La struttura di questi BLOB è:

```powershell
insights-{metrics|logs}-{category name}/resourceId=/SUBSCRIPTIONS/{subscription ID}/ RESOURCEGROUPS/{resource group name}/PROVIDERS/Microsoft.SQL/servers/{resource_server}/ databases/{database_name}/y={four-digit numeric year}/m={two-digit numeric month}/d={two-digit numeric day}/h={two-digit 24-hour clock hour}/m=00/PT1H.json
```
    
O, più semplicemente:

```powershell
insights-{metrics|logs}-{category name}/resourceId=/{resource Id}/y={four-digit numeric year}/m={two-digit numeric month}/d={two-digit numeric day}/h={two-digit 24-hour clock hour}/m=00/PT1H.json
```

Ad esempio, un nome del BLOB per l'opzione Tutte le metriche potrebbe essere:

```powershell
insights-metrics-minute/resourceId=/SUBSCRIPTIONS/s1id1234-5679-0123-4567-890123456789/RESOURCEGROUPS/TESTRESOURCEGROUP/PROVIDERS/MICROSOFT.SQL/ servers/Server1/databases/database1/y=2016/m=08/d=22/h=18/m=00/PT1H.json
```

Se si vuole registrare i dati dal pool elastico, il nome del BLOB è leggermente diverso:

```powershell
insights-{metrics|logs}-{category name}/resourceId=/SUBSCRIPTIONS/{subscription ID}/ RESOURCEGROUPS/{resource group name}/PROVIDERS/Microsoft.SQL/servers/{resource_server}/ elasticPools/{elastic_pool_name}/y={four-digit numeric year}/m={two-digit numeric month}/d={two-digit numeric day}/h={two-digit 24-hour clock hour}/m=00/PT1H.json
```

### <a name="download-metrics-and-logs-from-storage"></a>Scaricare le metriche e i log da Archiviazione

Informazioni su come [scaricare le metriche e i log di diagnostica da Archiviazione](../storage/blobs/storage-quickstart-blobs-dotnet.md#download-the-sample-application).

## <a name="metrics-and-logs-available"></a>Le metriche e i log disponibili

Trovare il contenuto dettagliato dei dati di telemetria di monitoraggio delle metriche e log disponibili per il database SQL di Azure, i pool elastici, l'istanza gestita e i database nell'istanza gestita.

## <a name="all-metrics"></a>Tutte le metriche

### <a name="all-metrics-for-elastic-pools"></a>Tutte le metriche per i pool elastici

|**Risorsa**|**Metriche**|
|---|---|
|Pool elastico|Percentuale eDTU, eDTU usata, limite eDTU, percentuale CPU, percentuale lettura dati fisici, percentuale scrittura log, percentuale sessioni, percentuale ruoli di lavoro, risorsa di archiviazione, percentuale di archiviazione, limite di archiviazione, percentuale di archiviazione XTP |

### <a name="all-metrics-for-azure-sql-database"></a>Tutti le metriche per il database SQL di Azure

|**Risorsa**|**Metriche**|
|---|---|
|database SQL di Azure|Percentuale DTU, DTU usata, limite DTU, percentuale CPU, percentuale lettura dati fisici, percentuale scrittura log, riuscito/non riuscito/bloccato dalle connessioni firewall, percentuale sessioni, percentuale ruoli di lavoro, risorsa di archiviazione, percentuale di archiviazione, percentuale di archiviazione XTP, deadlock |

## <a name="logs"></a>Log

### <a name="logs-for-managed-instance"></a>Log per istanza gestita

### <a name="resource-usage-stats"></a>Statistiche sull'utilizzo delle risorse

|Proprietà|DESCRIZIONE|
|---|---|
|TenantId|ID tenant.|
|SourceSystem|Always: Azure|
|TimeGenerated [UTC]|Timestamp di quando è stato registrato il log.|
|type|Always: AzureDiagnostics|
|ResourceProvider|Nome del provider di risorse. Always: MICROSOFT.SQL|
|Categoria|Nome della categoria. Sempre: ResourceUsageStats|
|Risorsa|Nome della risorsa.|
|ResourceType|Nome del tipo di risorsa. Sempre: MANAGEDINSTANCES|
|SubscriptionId|GUID della sottoscrizione a cui appartiene il database.|
|ResourceGroup|Nome del gruppo di risorse a cui appartiene il database.|
|LogicalServerName_s|Nome dell'istanza gestita.|
|ResourceId|URI della risorsa.|
|SKU_s|Codice di riferimento del prodotto di istanza gestita|
|virtual_core_count_s|Numero di vCore disponibili|
|avg_cpu_percent_s|Percentuale CPU Media|
|reserved_storage_mb_s|Capacità di archiviazione riservata in istanza gestita|
|storage_space_used_mb_s|Spazio di archiviazione utilizzato in istanza gestita|
|io_requests_s|Numero IOPS|
|io_bytes_read_s|Byte IOPS letti|
|io_bytes_written_s|Byte di IOPS scritti|

### <a name="logs-for-azure-sql-database-and-managed-instance-database"></a>Log per il database SQL e il database di istanza gestita

### <a name="query-store-runtime-statistics"></a>Statistiche di runtime di Query Store

|Proprietà|DESCRIZIONE|
|---|---|
|TenantId|ID tenant.|
|SourceSystem|Always: Azure|
|TimeGenerated [UTC]|Timestamp di quando è stato registrato il log.|
|type|Always: AzureDiagnostics|
|ResourceProvider|Nome del provider di risorse. Always: MICROSOFT.SQL|
|Categoria|Nome della categoria. Always: QueryStoreRuntimeStatistics|
|OperationName|Nome dell'operazione. Always: QueryStoreRuntimeStatisticsEvent|
|Risorsa|Nome della risorsa.|
|ResourceType|Nome del tipo di risorsa. Always: SERVERS/DATABASES|
|SubscriptionId|GUID della sottoscrizione a cui appartiene il database.|
|ResourceGroup|Nome del gruppo di risorse a cui appartiene il database.|
|LogicalServerName_s|Nome server a cui appartiene il database.|
|ElasticPoolName_s|Nome del pool elastico a cui appartiene il database, se esistente.|
|DatabaseName_s|Nome del database.|
|ResourceId|URI della risorsa.|
|query_hash_s|Hash di query.|
|query_plan_hash_s|Hash del piano di query.|
|statement_sql_handle_s|Punto di controllo dell'istruzione SQL.|
|interval_start_time_d|Datetimeoffset iniziale dell'intervallo in numero di tick da 1900-1-1.|
|interval_end_time_d|Datetimeoffset finale dell'intervallo in numero di tick da 1900-1-1.|
|logical_io_writes_d|Numero totale di scritture di I/O logiche.|
|max_logical_io_writes_d|Numero massimo di scritture di I/O logiche per esecuzione.|
|physical_io_reads_d|Numero totale di letture di I/O fisiche.|
|max_physical_io_reads_d|Numero massimo letture di I/O logiche per esecuzione.|
|logical_io_reads_d|Numero totale di letture di I/O logiche.|
|max_logical_io_reads_d|Numero massimo letture di I/O logiche per esecuzione.|
|execution_type_d|Tipo di esecuzione.|
|count_executions_d|Numero di esecuzioni della query.|
|cpu_time_d|Tempo totale della CPU usato dalla query in microsecondi.|
|max_cpu_time_d|Consumer massimo del tempo di CPU di una singola esecuzione in microsecondi.|
|dop_d|Somma dei gradi di parallelismo.|
|max_dop_d|Massimo grado parallelismo usato per una singola esecuzione.|
|rowcount_d|Numero di righe totali restituite.|
|max_rowcount_d|Numero massimo di righe restituite in una singola esecuzione.|
|query_max_used_memory_d|Quantità totale di memoria usata in KB.|
|max_query_max_used_memory_d|Quantità massima di memoria usata da una singola esecuzione in KB.|
|duration_d|Tempo di esecuzione totale in microsecondi.|
|max_duration_d|Tempo massimo di esecuzione di una singola esecuzione.|
|num_physical_io_reads_d|Numero totale di letture fisiche.|
|max_num_physical_io_reads_d|Numero massimo di scritture fisiche per esecuzione.|
|log_bytes_used_d|Quantità totale di byte di log usati.|
|max_log_bytes_used_d|Quantità massima di byte di log usati per esecuzione.|
|query_id_d|ID della query in Query Store.|
|plan_id_d|ID del piano in Query Store.|

Altre informazioni sui [dati delle statistiche di runtime di Query Store](https://docs.microsoft.com/sql/relational-databases/system-catalog-views/sys-query-store-runtime-stats-transact-sql).

### <a name="query-store-wait-statistics"></a>Statistiche relative alle attese di Query Store

|Proprietà|DESCRIZIONE|
|---|---|
|TenantId|ID tenant.|
|SourceSystem|Always: Azure|
|TimeGenerated [UTC]|Timestamp di quando è stato registrato il log.|
|type|Always: AzureDiagnostics|
|ResourceProvider|Nome del provider di risorse. Always: MICROSOFT.SQL|
|Categoria|Nome della categoria. Always: QueryStoreWaitStatistics|
|OperationName|Nome dell'operazione. Always: QueryStoreWaitStatisticsEvent|
|Risorsa|Nome della risorsa|
|ResourceType|Nome del tipo di risorsa. Always: SERVERS/DATABASES|
|SubscriptionId|GUID della sottoscrizione a cui appartiene il database.|
|ResourceGroup|Nome del gruppo di risorse a cui appartiene il database.|
|LogicalServerName_s|Nome server a cui appartiene il database.|
|ElasticPoolName_s|Nome del pool elastico a cui appartiene il database, se esistente.|
|DatabaseName_s|Nome del database.|
|ResourceId|URI della risorsa.|
|wait_category_s|Categoria dell'attesa.|
|is_parameterizable_s|La query è parametrizzabile.|
|statement_type_s|Tipo di istruzione.|
|statement_key_hash_s|Hash della chiave di istruzione.|
|exec_type_d|Tipo di esecuzione.|
|total_query_wait_time_ms_d|Tempo di attesa totale della query nella categoria di attesa specifica.|
|max_query_wait_time_ms_d|Tempo di attesa massimo della query nella singola esecuzione nella categoria di attesa specifica.|
|query_param_type_d|0|
|query_hash_s|Hash di query in Query Store.|
|query_plan_hash_s|Hash del piano di query in Query Store.|
|statement_sql_handle_s|Handle di istruzione in Query Store.|
|interval_start_time_d|Datetimeoffset iniziale dell'intervallo in numero di tick da 1900-1-1.|
|interval_end_time_d|Datetimeoffset finale dell'intervallo in numero di tick da 1900-1-1.|
|count_executions_d|Numero di esecuzioni della query.|
|query_id_d|ID della query in Query Store.|
|plan_id_d|ID del piano in Query Store.|

Altre informazioni sui [dati delle statistiche di attesa di Query Store](https://docs.microsoft.com/sql/relational-databases/system-catalog-views/sys-query-store-wait-stats-transact-sql).

### <a name="errors-dataset"></a>Set di dati di errori

|Proprietà|DESCRIZIONE|
|---|---|
|TenantId|ID tenant.|
|SourceSystem|Always: Azure|
|TimeGenerated [UTC]|Timestamp di quando è stato registrato il log.|
|type|Always: AzureDiagnostics|
|ResourceProvider|Nome del provider di risorse. Always: MICROSOFT.SQL|
|Categoria|Nome della categoria. Always: Errors|
|OperationName|Nome dell'operazione. Always: ErrorEvent|
|Risorsa|Nome della risorsa|
|ResourceType|Nome del tipo di risorsa. Always: SERVERS/DATABASES|
|SubscriptionId|GUID della sottoscrizione a cui appartiene il database.|
|ResourceGroup|Nome del gruppo di risorse a cui appartiene il database.|
|LogicalServerName_s|Nome server a cui appartiene il database.|
|ElasticPoolName_s|Nome del pool elastico a cui appartiene il database, se esistente.|
|DatabaseName_s|Nome del database.|
|ResourceId|URI della risorsa.|
|Message|Messaggio di errore in testo normale.|
|user_defined_b|È il bit di errore definito dall'utente.|
|error_number_d|Codice di errore.|
|Gravità|Gravità dell'errore.|
|state_d|Stato dell'errore.|
|query_hash_s|Hash di query della query non riuscita, se disponibile.|
|query_plan_hash_s|Hash del piano di query della query non riuscita, se disponibile.|

Altre informazioni sui [messaggi di errore di SQL Server](https://msdn.microsoft.com/library/cc645603.aspx).

### <a name="database-wait-statistics-dataset"></a>Set di dati delle statistiche di attesa del database

|Proprietà|DESCRIZIONE|
|---|---|
|TenantId|ID tenant.|
|SourceSystem|Always: Azure|
|TimeGenerated [UTC]|Timestamp di quando è stato registrato il log.|
|type|Always: AzureDiagnostics|
|ResourceProvider|Nome del provider di risorse. Always: MICROSOFT.SQL|
|Categoria|Nome della categoria. Always: DatabaseWaitStatistics|
|OperationName|Nome dell'operazione. Always: DatabaseWaitStatisticsEvent|
|Risorsa|Nome della risorsa|
|ResourceType|Nome del tipo di risorsa. Always: SERVERS/DATABASES|
|SubscriptionId|GUID della sottoscrizione a cui appartiene il database.|
|ResourceGroup|Nome del gruppo di risorse a cui appartiene il database.|
|LogicalServerName_s|Nome server a cui appartiene il database.|
|ElasticPoolName_s|Nome del pool elastico a cui appartiene il database, se esistente.|
|DatabaseName_s|Nome del database.|
|ResourceId|URI della risorsa.|
|wait_type_s|Nome del tipo di attesa.|
|start_utc_date_t [UTC]|Ora di inizio del periodo misurato.|
|end_utc_date_t [UTC]|Ora di fine del periodo misurato.|
|delta_max_wait_time_ms_d|Tempo massimo tempo di attesa per esecuzione|
|delta_signal_wait_time_ms_d|Tempo di attesa totale del segnale.|
|delta_wait_time_ms_d|Tempo di attesa totale nel periodo.|
|delta_waiting_tasks_count_d|Numero di attività in attesa.|

Altre informazioni sulle [statistiche di attesa del database](https://docs.microsoft.com/sql/relational-databases/system-dynamic-management-views/sys-dm-os-wait-stats-transact-sql).

### <a name="time-outs-dataset"></a>Set di dati dei timeout

|Proprietà|DESCRIZIONE|
|---|---|
|TenantId|ID tenant.|
|SourceSystem|Always: Azure|
|TimeGenerated [UTC]|Timestamp di quando è stato registrato il log.|
|type|Always: AzureDiagnostics|
|ResourceProvider|Nome del provider di risorse. Always: MICROSOFT.SQL|
|Categoria|Nome della categoria. Always: Timeouts|
|OperationName|Nome dell'operazione. Always: TimeoutEvent|
|Risorsa|Nome della risorsa|
|ResourceType|Nome del tipo di risorsa. Always: SERVERS/DATABASES|
|SubscriptionId|GUID della sottoscrizione a cui appartiene il database.|
|ResourceGroup|Nome del gruppo di risorse a cui appartiene il database.|
|LogicalServerName_s|Nome server a cui appartiene il database.|
|ElasticPoolName_s|Nome del pool elastico a cui appartiene il database, se esistente.|
|DatabaseName_s|Nome del database.|
|ResourceId|URI della risorsa.|
|error_state_d|Codice di stato dell'errore.|
|query_hash_s|Hash di query, se disponibile.|
|query_plan_hash_s|Hash del piano di query, se disponibile.|

### <a name="blockings-dataset"></a>Set di dati dei blocchi

|Proprietà|DESCRIZIONE|
|---|---|
|TenantId|ID tenant.|
|SourceSystem|Always: Azure|
|TimeGenerated [UTC]|Timestamp di quando è stato registrato il log.|
|type|Always: AzureDiagnostics|
|ResourceProvider|Nome del provider di risorse. Always: MICROSOFT.SQL|
|Categoria|Nome della categoria. Always: Blocks|
|OperationName|Nome dell'operazione. Always: BlockEvent|
|Risorsa|Nome della risorsa|
|ResourceType|Nome del tipo di risorsa. Always: SERVERS/DATABASES|
|SubscriptionId|GUID della sottoscrizione a cui appartiene il database.|
|ResourceGroup|Nome del gruppo di risorse a cui appartiene il database.|
|LogicalServerName_s|Nome server a cui appartiene il database.|
|ElasticPoolName_s|Nome del pool elastico a cui appartiene il database, se esistente.|
|DatabaseName_s|Nome del database.|
|ResourceId|URI della risorsa.|
|lock_mode_s|Modalità di blocco usata dalla query.|
|resource_owner_type_s|Proprietario del blocco.|
|blocked_process_filtered_s|Report XML del processo bloccato.|
|duration_d|Durata del blocco in microsecondi.|

### <a name="deadlocks-dataset"></a>Set di dati di deadlock

|Proprietà|DESCRIZIONE|
|---|---|
|TenantId|ID tenant.|
|SourceSystem|Always: Azure|
|TimeGenerated [UTC] |Timestamp di quando è stato registrato il log.|
|type|Always: AzureDiagnostics|
|ResourceProvider|Nome del provider di risorse. Always: MICROSOFT.SQL|
|Categoria|Nome della categoria. Always: Deadlocks|
|OperationName|Nome dell'operazione. Always: DeadlockEvent|
|Risorsa|Nome della risorsa.|
|ResourceType|Nome del tipo di risorsa. Always: SERVERS/DATABASES|
|SubscriptionId|GUID della sottoscrizione a cui appartiene il database.|
|ResourceGroup|Nome del gruppo di risorse a cui appartiene il database.|
|LogicalServerName_s|Nome server a cui appartiene il database.|
|ElasticPoolName_s|Nome del pool elastico a cui appartiene il database, se esistente.|
|DatabaseName_s|Nome del database. |
|ResourceId|URI della risorsa.|
|deadlock_xml_s|XML del report di deadlock.|

### <a name="automatic-tuning-dataset"></a>Set di dati di ottimizzazione automatica

|Proprietà|DESCRIZIONE|
|---|---|
|TenantId|ID tenant.|
|SourceSystem|Always: Azure|
|TimeGenerated [UTC]|Timestamp di quando è stato registrato il log.|
|type|Always: AzureDiagnostics|
|ResourceProvider|Nome del provider di risorse. Always: MICROSOFT.SQL|
|Categoria|Nome della categoria. Always: AutomaticTuning|
|Risorsa|Nome della risorsa.|
|ResourceType|Nome del tipo di risorsa. Always: SERVERS/DATABASES|
|SubscriptionId|GUID della sottoscrizione a cui appartiene il database.|
|ResourceGroup|Nome del gruppo di risorse a cui appartiene il database.|
|LogicalServerName_s|Nome server a cui appartiene il database.|
|LogicalDatabaseName_s|Nome del database.|
|ElasticPoolName_s|Nome del pool elastico a cui appartiene il database, se esistente.|
|DatabaseName_s|Nome del database.|
|ResourceId|URI della risorsa.|
|RecommendationHash_s|Hash univoco della raccomandazione di ottimizzazione automatica.|
|OptionName_s|Operazione di ottimizzazione automatica.|
|Schema_s|Schema del database.|
|Table_s|Tabella interessata.|
|IndexName_s|Nome dell'indice.|
|IndexColumns_s|Nome della colonna.|
|IncludedColumns_s|Colonne incluse.|
|EstimatedImpact_s|Impatto stimato del file JSON delle raccomandazioni di ottimizzazione automatica.|
|Event_s|Tipo di evento di ottimizzazione automatica.|
|Timestamp_t|Timestamp dell'ultimo aggiornamento.|

### <a name="intelligent-insights-dataset"></a>Set di dati di Intelligent Insights
Altre informazioni sul [formato di log di Intelligent Insights](sql-database-intelligent-insights-use-diagnostics-log.md).

## <a name="next-steps"></a>Passaggi successivi

Per informazioni su come abilitare la registrazione e comprendere le categorie di metriche e di log supportate dai vari servizi di Azure, leggere:

 * [Panoramica delle metriche in Microsoft Azure](../monitoring-and-diagnostics/monitoring-overview-metrics.md)
 * [Panoramica dei log di diagnostica di Azure](../monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs.md)

Per informazioni su Hub eventi, leggere:

* [Che cos'è l'hub di eventi di Azure?](../event-hubs/event-hubs-what-is-event-hubs.md)
* [Introduzione all'Hub eventi](../event-hubs/event-hubs-csharp-ephcs-getstarted.md)

Per informazioni su Archiviazione, leggere come [scaricare le metriche e i log di diagnostica da Archiviazione](../storage/blobs/storage-quickstart-blobs-dotnet.md#download-the-sample-application).
