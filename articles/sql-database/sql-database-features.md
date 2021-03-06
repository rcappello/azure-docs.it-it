---
title: Confronto tra le funzionalità del database SQL di Azure | Microsoft Docs
description: Questo articolo mette a confronto le funzionalità di SQL Server disponibili nei diversi tipi del database SQL di Azure.
services: sql-database
ms.service: sql-database
ms.subservice: ''
ms.custom: ''
ms.devlang: ''
ms.topic: conceptual
author: jovanpop-msft
ms.author: jovanpop
ms.reviewer: bonova, carlrab
manager: craigg
ms.date: 09/25/2018
ms.openlocfilehash: b68e65bdcefcabb2804b259cff45e0a8719f7ab7
ms.sourcegitcommit: 0bb8db9fe3369ee90f4a5973a69c26bff43eae00
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 10/08/2018
ms.locfileid: "48870517"
---
# <a name="feature-comparison-azure-sql-database-versus-sql-server"></a>Confronto tra le funzionalità: database SQL di Azure e SQL Server 

Il database SQL di Azure ha una base di codice in comune con SQL Server. Le funzionalità di SQL Server supportate dal database SQL di Azure dipendono dal tipo di database creato. Con il database SQL di Azure, è possibile creare un database come parte di un'[istanza gestita](sql-database-managed-instance.md) oppure creare un database che faccia parte di un server logico e, facoltativamente, sia inserito in un pool elastico. 

Microsoft introduce costantemente nuove funzionalità per il database SQL di Azure. Visitare la pagina Web Aggiornamenti di Azure per ottenere informazioni sugli aggiornamenti più recenti usando questi filtri:

* Filtrato per [servizio Database SQL](https://azure.microsoft.com/updates/?service=sql-database).
* Filtrato per Disponibilità generale [annunci](http://azure.microsoft.com/updates/?service=sql-database&update-type=general-availability) per le funzionalità del database SQL.

## <a name="sql-server-feature-support-in-azure-sql-database"></a>Supporto delle funzionalità di SQL Server nel database SQL di Azure

La tabella seguente elenca le principali funzionalità di SQL Server. Per ogni funzionalità viene specificato se questa è parzialmente o completamente supportata e viene riportato un collegamento ad altre informazioni. 

| **Funzionalità di SQL** | **Supportata nel database SQL di Azure/server logico** | **Supportata nel database SQL di Azure/Istanza gestita di database SQL di Azure (livello Business Critical attualmente in anteprima)** |
| --- | --- | --- |
| [Always Encrypted](https://docs.microsoft.com/sql/relational-databases/security/encryption/always-encrypted-database-engine) | Sì. Vedere [Archivio certificati](sql-database-always-encrypted.md) e [Insieme di credenziali delle chiavi](sql-database-always-encrypted-azure-key-vault.md) | Sì. Vedere [Archivio certificati](sql-database-always-encrypted.md) e [Insieme di credenziali delle chiavi](sql-database-always-encrypted-azure-key-vault.md) |
| [Gruppi di disponibilità AlwaysOn](https://docs.microsoft.com/sql/database-engine/availability-groups/windows/always-on-availability-groups-sql-server) | La [disponibilità elevata](sql-database-high-availability.md) è inclusa in ogni database. Il ripristino di emergenza è trattato in [Panoramica della continuità aziendale del database SQL di Azure](sql-database-business-continuity.md) | La [disponibilità elevata](sql-database-high-availability.md) è inclusa in ogni database. Il ripristino di emergenza è trattato in [Panoramica della continuità aziendale del database SQL di Azure](sql-database-business-continuity.md) |
| [Collegamento di un database](https://docs.microsoft.com/sql/relational-databases/databases/attach-a-database) | No  | No  |
| [ruoli dell'applicazione](https://docs.microsoft.com/sql/relational-databases/security/authentication-access/application-roles) | Yes | Yes |
|[Controllo](https://docs.microsoft.com/sql/relational-databases/security/auditing/sql-server-audit-database-engine) | [Sì](sql-database-auditing.md)| [Sì](sql-database-managed-instance-auditing.md) |
| [Backup automatici](sql-database-automated-backups.md) | Yes | Yes |
| [Ottimizzazione automatica (uso forzato del piano)](https://docs.microsoft.com/sql/relational-databases/automatic-tuning/automatic-tuning)| [Sì](sql-database-automatic-tuning.md)| [Sì](https://docs.microsoft.com/sql/relational-databases/automatic-tuning/automatic-tuning) |
| [Ottimizzazione automatica (indici)](https://docs.microsoft.com/sql/relational-databases/automatic-tuning/automatic-tuning)| [Sì](sql-database-automatic-tuning.md)| No  |
| [Azure Data Studio](https://docs.microsoft.com/sql/azure-data-studio/what-is) | Yes | Yes |
| [File BACPAC (esportazione)](https://docs.microsoft.com/sql/relational-databases/data-tier-applications/export-a-data-tier-application) | Sì. Vedere [Esportazione di un database SQL](sql-database-export.md) | No  |
| [File BACPAC (importazione)](https://docs.microsoft.com/sql/relational-databases/data-tier-applications/import-a-bacpac-file-to-create-a-new-user-database) | Sì. Vedere [Importazione di un database SQL](sql-database-import.md) | No  |
| [Comando BACKUP](https://docs.microsoft.com/sql/t-sql/statements/backup-transact-sql) | No, solo backup automatici avviati dal sistema, vedere [Backup automatici](sql-database-automated-backups.md) | Backup automatici avviati dal sistema e backup di sola copia avviati dall'utente, vedere le [differenze relative al backup](sql-database-managed-instance-transact-sql-information.md#backup) |
| [Funzioni predefinite](https://docs.microsoft.com/sql/t-sql/functions/functions) | Supportate per la maggior parte. Vedere le singole funzioni | Sì, vedere le [differenze relative a stored procedure, funzioni e trigger](sql-database-managed-instance-transact-sql-information.md#stored-procedures-functions-triggers) |
| [Change Data Capture](https://docs.microsoft.com/sql/relational-databases/track-changes/about-change-data-capture-sql-server) | No  | Yes |
| [Rilevamento modifiche](https://docs.microsoft.com/sql/relational-databases/track-changes/about-change-tracking-sql-server) | Yes |Yes |
| [Istruzioni sulle regole di confronto](https://docs.microsoft.com/sql/t-sql/statements/collations) | Yes | Yes |
| [Indici columnstore](https://docs.microsoft.com/sql/relational-databases/indexes/columnstore-indexes-overview) | Sì, [livello Premium, livello Standard; S3 e versioni successive, livello Utilizzo generico e livelli Business Critical](https://docs.microsoft.com/sql/relational-databases/indexes/columnstore-indexes-overview) |Yes |
| [Common Language Runtime (CLR)](https://docs.microsoft.com/sql/relational-databases/clr-integration/common-language-runtime-clr-integration-programming-concepts) | No  | Sì, vedere le [differenze relative a CLR](sql-database-managed-instance-transact-sql-information.md#clr) |
| [Database indipendenti](https://docs.microsoft.com/sql/relational-databases/databases/contained-databases) | Yes | Yes |
| [Utenti indipendenti](https://docs.microsoft.com/sql/relational-databases/security/contained-database-users-making-your-database-portable) | Yes | Yes |
| [Parole chiave degli elementi del linguaggio per il controllo di flusso](https://docs.microsoft.com/sql/t-sql/language-elements/control-of-flow) | Yes | Yes |
| [Query tra database](https://docs.microsoft.com/sql/relational-databases/linked-servers/linked-servers-database-engine) | No, vedere [Query elastiche](sql-database-elastic-query-overview.md) | Sì, oltre a [Query elastiche](sql-database-elastic-query-overview.md) |
| [Transazioni tra database](https://docs.microsoft.com/sql/relational-databases/linked-servers/linked-servers-database-engine) | No  | Sì, vedere [Linked server differences](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance-transact-sql-information#linked-servers) (Differenze dei server collegati) |
| [Cursori](https://docs.microsoft.com/sql/t-sql/language-elements/cursors-transact-sql) | Yes |Yes | 
| [Compressione dei dati](https://docs.microsoft.com/sql/relational-databases/data-compression/data-compression) | Yes |Yes |
| [Posta elettronica database](https://docs.microsoft.com/sql/relational-databases/database-mail/database-mail) | No  | Yes |
| [Servizio Migrazione del database](https://docs.microsoft.com/sql/dma/dma-overview) | Yes | Yes |
| [Mirroring del database](https://docs.microsoft.com/sql/database-engine/database-mirroring/database-mirroring-sql-server) | No  | No  |
| [Impostazioni di configurazione del database](https://docs.microsoft.com/sql/t-sql/statements/alter-database-scoped-configuration-transact-sql) | Yes | Yes |
| [Data Quality Services (DQS)](https://docs.microsoft.com/sql/data-quality-services/data-quality-services) | No  | No  |
| [Snapshot del database](https://docs.microsoft.com/sql/relational-databases/databases/database-snapshots-sql-server) | No  | No  |
| [Tipi di dati](https://docs.microsoft.com/sql/t-sql/data-types/data-types-transact-sql) | Yes |Yes |
| [Istruzioni DBCC](https://docs.microsoft.com/sql/t-sql/database-console-commands/dbcc-transact-sql) | Supportate per la maggior parte. Vedere le singole istruzioni | Sì, vedere le [differenze relative a DBCC](sql-database-managed-instance-transact-sql-information.md#dbcc) |
| [Istruzioni DDL](https://docs.microsoft.com/sql/t-sql/statements/statements) | Supportate per la maggior parte. Vedere le singole istruzioni | Sì, vedere le [differenze relative a T-SQL](sql-database-managed-instance-transact-sql-information.md) |
| [Trigger DDL](https://docs.microsoft.com/sql/relational-databases/triggers/ddl-triggers) | Solo database |  Yes |
| [Viste partizionate distribuite](https://docs.microsoft.com/sql/t-sql/statements/create-view-transact-sql#partitioned-views) | No  | Yes |
| [Transazioni distribuite - MS DTC](https://docs.microsoft.com/sql/relational-databases/native-client-ole-db-transactions/supporting-distributed-transactions) | No. Vedere [Transazioni elastiche](sql-database-elastic-transactions-overview.md) |  No. Vedere [Transazioni elastiche](sql-database-elastic-transactions-overview.md) |
| [Istruzioni DML](https://docs.microsoft.com/sql/t-sql/queries/queries) | Yes | Yes |
| [Trigger DML](https://docs.microsoft.com/sql/relational-databases/triggers/create-dml-triggers) | Supportate per la maggior parte. Vedere le singole istruzioni |  Yes |
| [Viste a gestione dinamica](https://docs.microsoft.com/sql/relational-databases/system-dynamic-management-views/system-dynamic-management-views) | Supportate nella maggior parte dei casi, vedere singole viste a gestione dinamica |  Sì, vedere le [differenze relative a T-SQL](sql-database-managed-instance-transact-sql-information.md) |
|[Maschera dati dinamica](https://docs.microsoft.com/sql/relational-databases/security/dynamic-data-masking)|[Sì](sql-database-dynamic-data-masking-get-started.md)| [Sì](sql-database-dynamic-data-masking-get-started.md) |
| [Pool elastici](sql-database-elastic-pool.md) | Yes | Predefinito. Una singola istanza gestita può avere più database che condividono lo stesso pool di risorse |
| [Notifiche degli eventi](https://docs.microsoft.com/sql/relational-databases/service-broker/event-notifications) | No. Vedere [Avvisi](sql-database-insights-alerts-portal.md) | Yes |
| [Espressioni](https://docs.microsoft.com/sql/t-sql/language-elements/expressions-transact-sql) |Yes | Yes |
| [Eventi estesi](https://docs.microsoft.com/sql/relational-databases/extended-events/extended-events) | Supportati in alcuni casi. Vedere [Eventi estesi nel database SQL](sql-database-xevent-db-diff-from-svr.md) | Sì, vedere le [differenze relative agli eventi estesi](sql-database-managed-instance-transact-sql-information.md#extended-events) |
| [Stored procedure estese](https://docs.microsoft.com/sql/relational-databases/extended-stored-procedures-programming/creating-extended-stored-procedures) | No  | No  |
[File e gruppi di file](https://docs.microsoft.com/sql/relational-databases/databases/database-files-and-filegroups) | Solo gruppi di file primari | Yes |
| [Filestream](https://docs.microsoft.com/sql/relational-databases/blob/filestream-sql-server) | No  | No  |
| [Ricerca full-text](https://docs.microsoft.com/sql/relational-databases/search/full-text-search) |  I word breaker di terze parti non sono supportati |I word breaker di terze parti non sono supportati |
| [Funzioni](https://docs.microsoft.com/sql/t-sql/functions/functions) | Supportate per la maggior parte. Vedere le singole funzioni | Sì, vedere le [differenze relative a stored procedure, funzioni e trigger](sql-database-managed-instance-transact-sql-information.md#stored-procedures-functions-triggers) |
| [Ripristino geografico](sql-database-recovery-using-backups.md#geo-restore) | Sì, solo livelli di servizio Utilizzo generico e Business Critical | No, è possibile ripristinare i backup completi COPY_ONLY eseguiti periodicamente, vedere le [differenze relative al backup](sql-database-managed-instance-transact-sql-information.md#backup) e le [differenze relative al ripristino](sql-database-managed-instance-transact-sql-information.md#restore-statement). |
| [Replica geografica](sql-database-geo-replication-overview.md) | Sì, solo livelli di servizio Utilizzo generico e Business Critical| No  |
| [Elaborazione del grafico](https://docs.microsoft.com/sql/relational-databases/graphs/sql-graph-overview) | Yes | Yes |
| [Ottimizzazione in memoria](https://docs.microsoft.com/sql/relational-databases/in-memory-oltp/in-memory-oltp-in-memory-optimization) | Sì, [solo livelli Premium e Business critical](sql-database-in-memory.md) | Sì, [solo livello Business Critical - attualmente in anteprima](sql-database-managed-instance.md) |
| [Supporto di dati JSON](https://docs.microsoft.com/sql/relational-databases/json/json-data-sql-server) | [Sì](https://docs.microsoft.com/azure/sql-database/sql-database-json-features) | [Sì](https://docs.microsoft.com/azure/sql-database/sql-database-json-features) |
| [Elementi del linguaggio](https://docs.microsoft.com/sql/t-sql/language-elements/language-elements-transact-sql) | Supportati per la maggior parte. Vedere i singoli elementi |  Sì, vedere le [differenze relative a T-SQL](sql-database-managed-instance-transact-sql-information.md) |
| [Server collegati](https://docs.microsoft.com/sql/relational-databases/linked-servers/linked-servers-database-engine) | No. Vedere [Query elastica](sql-database-elastic-query-horizontal-partitioning.md) | Solo per SQL Server e il database SQL |
| [Log shipping](https://docs.microsoft.com/sql/database-engine/log-shipping/about-log-shipping-sql-server) | La [disponibilità elevata](sql-database-high-availability.md) è inclusa in ogni database. Il ripristino di emergenza è trattato in [Panoramica della continuità aziendale del database SQL di Azure](sql-database-business-continuity.md) |La [disponibilità elevata](sql-database-high-availability.md) è inclusa in ogni database. Il ripristino di emergenza è trattato in [Panoramica della continuità aziendale del database SQL di Azure](sql-database-business-continuity.md) |
| [Master Data Services (MDS)](https://docs.microsoft.com/sql/master-data-services/master-data-services-overview-mds) | No  | No  |
| [Registrazione minima nell'importazione bulk](https://docs.microsoft.com/sql/relational-databases/import-export/prerequisites-for-minimal-logging-in-bulk-import) | No  | No  |
| [Modifica dei dati di sistema](https://docs.microsoft.com/sql/relational-databases/databases/system-databases) | No  | Yes |
| [Operazioni online sugli indici](https://docs.microsoft.com/sql/relational-databases/indexes/perform-index-operations-online) | Yes | Yes |
| [OPENDATASOURCE](https://docs.microsoft.com/sql/t-sql/functions/opendatasource-transact-sql)|No |Sì, vedere le [differenze relative a T-SQL](sql-database-managed-instance-transact-sql-information.md)|
| [OPENJSON](https://docs.microsoft.com/sql/t-sql/functions/openjson-transact-sql)|Yes|Yes|
| [OPENQUERY](https://docs.microsoft.com/sql/t-sql/functions/openquery-transact-sql)|No |Sì, vedere le [differenze relative a T-SQL](sql-database-managed-instance-transact-sql-information.md)|
| [OPENROWSET](https://docs.microsoft.com/sql/t-sql/functions/openrowset-transact-sql)|No |Sì, vedere le [differenze relative a T-SQL](sql-database-managed-instance-transact-sql-information.md)|
| [OPENXML](https://docs.microsoft.com/sql/t-sql/functions/openxml-transact-sql)|Yes|Yes|
| [Operatori](https://docs.microsoft.com/sql/t-sql/language-elements/operators-transact-sql) | Supportati per la maggior parte. Vedere i singoli operatori |Sì, vedere le [differenze relative a T-SQL](sql-database-managed-instance-transact-sql-information.md) |
| [Partizionamento](https://docs.microsoft.com/sql/relational-databases/partitions/partitioned-tables-and-indexes) | Yes | Yes |
| [Ripristino temporizzato di un database](https://docs.microsoft.com/sql/relational-databases/backup-restore/restore-a-sql-server-database-to-a-point-in-time-full-recovery-model) | Sì, solo livelli di servizio Utilizzo generico e Business Critical - vedere [Ripristino di un database SQL](sql-database-recovery-using-backups.md#point-in-time-restore) | Sì. Vedere [Ripristino di un database SQL](sql-database-recovery-using-backups.md#point-in-time-restore) |
| [PolyBase](https://docs.microsoft.com/sql/relational-databases/polybase/polybase-guide) | No  | No  |
| [Gestione basata su criteri](https://docs.microsoft.com/sql/relational-databases/policy-based-management/administer-servers-by-using-policy-based-management) | No  | No  |
| [Predicati](https://docs.microsoft.com/sql/t-sql/queries/predicates) | Yes | Yes |
| [Servizi R](https://docs.microsoft.com/sql/advanced-analytics/r-services/sql-server-r-services) | Versione di anteprima; vedere [Novità di Machine Learning](https://docs.microsoft.com/sql/advanced-analytics/what-s-new-in-sql-server-machine-learning-services)  | No  |
| [Resource Governor](https://docs.microsoft.com/sql/relational-databases/resource-governor/resource-governor) | No  | Yes |
| [Istruzioni RESTORE](https://docs.microsoft.com/sql/t-sql/statements/restore-statements-for-restoring-recovering-and-managing-backups-transact-sql) | No  | Sì, vedere le [differenze relative al ripristino](sql-database-managed-instance-transact-sql-information.md#restore-statement) |
| [Ripristino del database da backup](https://docs.microsoft.com/sql/relational-databases/backup-restore/back-up-and-restore-of-sql-server-databases#restore-data-backups) | Solo da backup automatici, vedere [Ripristino di un database SQL](sql-database-recovery-using-backups.md) | Da backup automatici, vedere [Ripristino di un database SQL](sql-database-recovery-using-backups.md), e da backup completi, vedere le [differenze relative al backup](sql-database-managed-instance-transact-sql-information.md#backup) |
| [Sicurezza a livello di riga](https://docs.microsoft.com/sql/relational-databases/security/row-level-security) | Yes | Yes |
| [Ricerca semantica](https://docs.microsoft.com/sql/relational-databases/search/semantic-search-sql-server) | No  | No  |
| [Numeri di sequenza](https://docs.microsoft.com/sql/relational-databases/sequence-numbers/sequence-numbers) | Yes | Yes |
| [Service Broker](https://docs.microsoft.com/sql/database-engine/configure-windows/sql-server-service-broker) | No  | Sì, vedere le [differenze relative a Service Broker](sql-database-managed-instance-transact-sql-information.md#service-broker) |
| [Impostazioni di configurazione del server](https://docs.microsoft.com/sql/database-engine/configure-windows/server-configuration-options-sql-server) | No  | Sì, vedere le [differenze relative a T-SQL](sql-database-managed-instance-transact-sql-information.md) |
| [Istruzioni SET](https://docs.microsoft.com/sql/t-sql/statements/set-statements-transact-sql) | Supportate per la maggior parte. Vedere le singole istruzioni | Sì, vedere le [differenze relative a T-SQL](sql-database-managed-instance-transact-sql-information.md)|
| [SMO](https://docs.microsoft.com/sql/relational-databases/server-management-objects-smo/sql-server-management-objects-smo-programming-guide) | Yes | Yes |
| [Spatial](https://docs.microsoft.com/sql/relational-databases/spatial/spatial-data-sql-server) | Yes | Yes |
| [Sincronizzazione dati SQL](sql-database-get-started-sql-data-sync.md) | Yes | No  |
| [Agente SQL Server](https://docs.microsoft.com/sql/ssms/agent/sql-server-agent) | No. Vedere [Processi elastici](sql-database-elastic-jobs-getting-started.md) | Sì, vedere le [differenze relative a SQL Server Agent](sql-database-managed-instance-transact-sql-information.md#sql-server-agent) |
| [SQL Server Analysis Services (SSAS)](https://docs.microsoft.com/sql/analysis-services/analysis-services) | No, vedere [Azure Analysis Services](https://azure.microsoft.com/services/analysis-services/) | No. Vedere [Azure Analysis Services](https://azure.microsoft.com/services/analysis-services/) |
| [Controllo di SQL Server](https://docs.microsoft.com/sql/relational-databases/security/auditing/sql-server-audit-database-engine) | No. Vedere [Controllo del database SQL](sql-database-auditing.md) | Sì, vedere le [differenze relative al controllo](sql-database-managed-instance-transact-sql-information.md#auditing) |
| [SQL Server Data Tools (SSDT)](https://docs.microsoft.com/sql/ssdt/download-sql-server-data-tools-ssdt) | Yes | Yes |
| [SQL Server Integration Services (SSIS)](https://docs.microsoft.com/sql/integration-services/sql-server-integration-services) | Sì, con SSIS gestito nell'ambiente di Azure Data Factory in cui i pacchetti vengono archiviati nel database SSISDB ospitato dal database SQL di Azure ed eseguiti nel runtime di integrazione SSIS di Azure vedere [Creare il runtime di integrazione SSIS di Azure in Azure Data Factory](https://docs.microsoft.com/azure/data-factory/create-azure-ssis-integration-runtime). <br/><br/>Per comparare le funzioni SSIS nel database SQL come parte di un server logico e di un'istanza gestita, vedere [Comparare il server logico e l'istanza gestita del database SQL](../data-factory/create-azure-ssis-integration-runtime.md#compare-sql-database-logical-server-and-sql-database-managed-instance). | Sì, con SSIS gestito nell'ambiente di Azure Data Factory in cui i pacchetti vengono archiviati nel database SSISDB ospitato da Istanza gestita ed eseguiti nel runtime di integrazione SSIS di Azure vedere [Creare il runtime di integrazione SSIS di Azure in Azure Data Factory](https://docs.microsoft.com/azure/data-factory/create-azure-ssis-integration-runtime). <br/><br/>Per comparare le funzioni SSIS nel database SQL come parte di un'istanza gestita, vedere [Comparare il server logico e l'istanza gestita del database SQL](../data-factory/create-azure-ssis-integration-runtime.md#compare-sql-database-logical-server-and-sql-database-managed-instance). |
| [SQL Server Management Studio (SSMS)](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms) | Yes | Yes |
| [SQL Server PowerShell](https://docs.microsoft.com/sql/relational-databases/scripting/sql-server-powershell) | Yes | Yes |
| [SQL Server Profiler](https://docs.microsoft.com/sql/tools/sql-server-profiler/sql-server-profiler) | No. Vedere [Eventi estesi](sql-database-xevent-db-diff-from-svr.md) | Yes |
| [Replica di SQL Server](https://docs.microsoft.com/sql/relational-databases/replication/sql-server-replication) | [Solo per iscritti alla replica transazionale e snapshot](sql-database-cloud-migrate.md) | Sì, [replica con Istanza gestita di database SQL - anteprima pubblica](http://docs.microsoft.com/sql/relational-databases/replication/replication-with-sql-database-managed-instance) |
| [SQL Server Reporting Services (SSRS)](https://docs.microsoft.com/sql/reporting-services/create-deploy-and-manage-mobile-and-paginated-reports) | No, vedere [Power BI](https://docs.microsoft.com/power-bi/) | No, vedere [Power BI](https://docs.microsoft.com/power-bi/) |
| [Stored procedure](https://docs.microsoft.com/sql/relational-databases/stored-procedures/stored-procedures-database-engine) | Yes | Yes |
| [Funzioni archiviate nel sistema](https://docs.microsoft.com/sql/relational-databases/system-functions/system-functions-for-transact-sql) | Supportate per la maggior parte. Vedere le singole funzioni | Sì, vedere le [differenze relative a stored procedure, funzioni e trigger](sql-database-managed-instance-transact-sql-information.md#stored-procedures-functions-triggers) |
| [Stored procedure di sistema](https://docs.microsoft.com/sql/relational-databases/system-stored-procedures/system-stored-procedures-transact-sql) | Supportate in alcuni casi. Vedere le singole stored procedure | Sì, vedere le [differenze relative a stored procedure, funzioni e trigger](sql-database-managed-instance-transact-sql-information.md#stored-procedures-functions-triggers) |
| [Tabelle di sistema](https://docs.microsoft.com/sql/relational-databases/system-tables/system-tables-transact-sql) | Supportate in alcuni casi. Vedere le singole tabelle | Sì, vedere le [differenze relative a T-SQL](sql-database-managed-instance-transact-sql-information.md) |
| [Viste del catalogo di sistema](https://docs.microsoft.com/sql/relational-databases/system-catalog-views/catalog-views-transact-sql) | Supportate in alcuni casi. Vedere le singole viste | Sì, vedere le [differenze relative a T-SQL](sql-database-managed-instance-transact-sql-information.md) |
| [Tabelle temporanee](https://docs.microsoft.com/sql/t-sql/statements/create-table-transact-sql#database-scoped-global-temporary-tables-azure-sql-database) | Tabelle temporanee locali e globali in ambito database | Tabelle temporanee locali e globali in ambito istanza |
| [Tabelle temporali](https://docs.microsoft.com/sql/relational-databases/tables/temporal-tables) | [Sì](https://docs.microsoft.com/azure/sql-database/sql-database-temporal-tables) | [Sì](https://docs.microsoft.com/azure/sql-database/sql-database-temporal-tables) |
|Introduzione al rilevamento delle minacce|  [Sì](sql-database-threat-detection.md)|[Sì](sql-database-managed-instance-threat-detection.md)|
| [Flag di traccia](https://docs.microsoft.com/sql/t-sql/database-console-commands/dbcc-traceon-trace-flags-transact-sql) | No  | No  |
| [Variabili](https://docs.microsoft.com/sql/t-sql/language-elements/variables-transact-sql) | Yes | Yes |
| [Transparent Data Encryption (TDE)](https://docs.microsoft.com/sql/relational-databases/security/encryption/transparent-data-encryption-tde) | Sì, solo livelli di servizio Utilizzo generico e Business Critical| Parziale, solo con crittografia gestita dal servizio |
[Rete virtuale](../virtual-network/virtual-networks-overview.md) | Parziale, vedere [Endpoint della rete virtuale](sql-database-vnet-service-endpoint-rule-overview.md) | Sì, solo modello Resource Manager |
| [Windows Server Failover Clustering](https://docs.microsoft.com/sql/sql-server/failover-clusters/windows/windows-server-failover-clustering-wsfc-with-sql-server) | La [disponibilità elevata](sql-database-high-availability.md) è inclusa in ogni database. Il ripristino di emergenza è trattato in [Panoramica della continuità aziendale del database SQL di Azure](sql-database-business-continuity.md) | La [disponibilità elevata](sql-database-high-availability.md) è inclusa in ogni database. Il ripristino di emergenza è trattato in [Panoramica della continuità aziendale del database SQL di Azure](sql-database-business-continuity.md) |
| [Indici XML](https://docs.microsoft.com/sql/t-sql/statements/create-xml-index-transact-sql) | Yes | Yes |

## <a name="next-steps"></a>Passaggi successivi

- Per informazioni sul servizio di Database SQL di Azure, vedere [Informazioni sul database SQL](sql-database-technical-overview.md)
- Per altre informazioni in proposito, vedere l'articolo di [informazioni su Istanza gestita](sql-database-managed-instance.md).
