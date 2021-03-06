# [Documentazione di Data Lake Storage Gen1](index.md)
# [Passare alla documentazione di Data Lake Storage Gen2 (anteprima)](https://docs.microsoft.com/azure/storage/data-lake-storage/introduction)

# Panoramica
## [Panoramica di Data Lake Storage Gen1](data-lake-store-overview.md)
## [Confronto con Archiviazione di Azure](data-lake-store-comparison-with-blob-storage.md)
## [Elaborazione di Big Data](data-lake-store-data-scenarios.md)
## [Uso di applicazioni open source](data-lake-store-compatible-oss-other-applications.md)
## [Procedure consigliate](data-lake-store-best-practices.md)

# Attività iniziali
## [Uso del portale di Azure](data-lake-store-get-started-portal.md)
## [Uso di Azure PowerShell](data-lake-store-get-started-powershell.md)
## [Uso dell'interfaccia della riga di comando di Azure](data-lake-store-get-started-cli-2.0.md)

# Procedure
## Caricare e spostare dati
### [Uso di Data factory di Azure](../data-factory/load-azure-data-lake-store.md)
### [Con Storage Explorer](data-lake-store-in-storage-explorer.md)
### [Con AdlCopy](data-lake-store-copy-data-azure-storage-blob.md)
### [Con DistCp](data-lake-store-copy-data-wasb-distcp.md)
### [Uso di Sqoop](data-lake-store-data-transfer-sql-sqoop.md)
### [Caricare dati da origini offline](data-lake-store-offline-bulk-data-upload.md)
### [Eseguire la migrazione di Data Lake Storage Gen1 tra aree](data-lake-store-migration-cross-region.md)

## Proteggere i dati
### [Panoramica della sicurezza](data-lake-store-security-overview.md)
### [Controllo di accesso](data-lake-store-access-control.md)
### [Protezione dei dati archiviati](data-lake-store-secure-data.md)
### [Crittografia](data-lake-store-encryption.md)

## Eseguire l'autenticazione con Data Lake Storage Gen1
### [Opzioni di autenticazione](data-lakes-store-authentication-using-azure-active-directory.md)
### [Autenticazione dell'utente finale](data-lake-store-end-user-authenticate-using-active-directory.md)
#### [Uso di Java](data-lake-store-end-user-authenticate-java-sdk.md)
#### [Uso di .NET SDK](data-lake-store-end-user-authenticate-net-sdk.md)
#### [Uso dell'API REST](data-lake-store-end-user-authenticate-rest-api.md)
#### [Uso di Python](data-lake-store-end-user-authenticate-python.md)
### [Autenticazione da servizio a servizio](data-lake-store-service-to-service-authenticate-using-active-directory.md)
#### [Uso di Java](data-lake-store-service-to-service-authenticate-java.md)
#### [Uso di .NET SDK](data-lake-store-service-to-service-authenticate-net-sdk.md)
#### [Uso dell'API REST](data-lake-store-service-to-service-authenticate-rest-api.md)
#### [Uso di Python](data-lake-store-service-to-service-authenticate-python.md)

## Usare Data Lake Storage Gen1
### Operazioni di gestione dell'account
#### [Uso di .NET SDK](data-lake-store-get-started-net-sdk.md)
#### [Uso dell'API REST](data-lake-store-get-started-rest-api.md)
#### [Uso di Python](data-lake-store-get-started-python.md)
### Operazioni per file system
#### [Uso di .NET SDK](data-lake-store-data-operations-net-sdk.md)
#### [Uso di Java SDK](data-lake-store-get-started-java-sdk.md)
#### [Uso dell'API REST](data-lake-store-data-operations-rest-api.md)
#### [Uso di Python](data-lake-store-data-operations-python.md)

## Prestazioni
### [Overview](data-lake-store-performance-tuning-guidance.md)
### [Uso di Azure PowerShell](data-lake-store-performance-tuning-powershell.md)
### [Uso di Spark in HDInsight](data-lake-store-performance-tuning-spark.md)
### [Uso di Hive in HDInsight](data-lake-store-performance-tuning-hive.md)
### [Uso di MapReduce in HDInsight](data-lake-store-performance-tuning-mapreduce.md)
### [Uso di Storm in HDInsight](data-lake-store-performance-tuning-storm.md)

## Eseguire l'integrazione con i servizi di Azure
### Con HDInsight
#### [Uso del portale di Azure](data-lake-store-hdinsight-hadoop-use-portal.md)
#### [Uso di Azure PowerShell (archiviazione predefinita)](data-lake-store-hdinsight-hadoop-use-powershell-for-default-storage.md)
#### [Uso di Azure PowerShell (archiviazione aggiuntiva)](data-lake-store-hdinsight-hadoop-use-powershell.md)
#### [Uso del modello di Azure](data-lake-store-hdinsight-hadoop-use-resource-manager-template.md)
### [Accesso alla rete virtuale di Azure dalle macchine virtuali](data-lake-store-connectivity-from-vnets.md)
### [Uso con Data Lake Analytics](../data-lake-analytics/data-lake-analytics-get-started-portal.md)
### [Uso con Hub eventi di Azure](data-lake-store-archive-eventhub-capture.md)
### [Uso con Data Factory](../data-factory/load-azure-data-lake-store.md)
### [Uso con l'analisi di flusso](data-lake-store-stream-analytics.md)
### [Uso con Power BI](data-lake-store-power-bi.md)
### [Uso con Data Catalog](data-lake-store-with-data-catalog.md)
### [Uso con PolyBase in SQL Data Warehouse](../sql-data-warehouse/sql-data-warehouse-load-from-azure-data-lake-store.md)
### [Uso con SQL Server Integration Services](https://docs.microsoft.com/sql/integration-services/connection-manager/azure-data-lake-store-connection-manager)
### [Altre opzioni di integrazione di Azure](data-lake-store-integrate-with-other-services.md)

## Gestisci
### [Accedere ai log di diagnostica](data-lake-store-diagnostic-logs.md)
### [Pianificare la disponibilità elevata](data-lake-store-disaster-recovery-guidance.md)

# riferimento
## [Esempi di codice](https://azure.microsoft.com/resources/samples/?service=data-lake-store)
## [Azure PowerShell](/powershell/module/azurerm.datalakestore)
## [.NET](https://docs.microsoft.com/dotnet/api/overview/azure/data-lake-store?view=azure-dotnet)
## [Java](/java/api/com.microsoft.azure.datalake.store)
## [Node.JS](https://www.npmjs.com/package/azure-arm-datalake-store)
## [Python (gestione di account)](https://docs.microsoft.com/python/api/azure.mgmt.datalake.store?view=azure-python)
## [Python (gestione del file system)](http://azure-datalake-store.readthedocs.io/en/latest)
## [REST](/rest/api/datalakestore)
## [Interfaccia della riga di comando di Azure](https://docs.microsoft.com/cli/azure/dls)

# Risorse
## [Roadmap per Azure](https://azure.microsoft.com/roadmap/)
## [Blog di Data Lake Store](https://blogs.msdn.microsoft.com/azuredatalake/)
## [Commenti e suggerimenti su UserVoice](https://feedback.azure.com/forums/327234-data-lake)
## [Forum di MSDN](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureDataLake)
## [Prezzi](https://azure.microsoft.com/pricing/details/data-lake-store/)
## [Calcolatore prezzi](https://azure.microsoft.com/pricing/calculator/)
## [Aggiornamenti del servizio](https://azure.microsoft.com/updates/?product=data-lake-store)
## [Forum di Stack Overflow](http://stackoverflow.com/questions/tagged/azure-data-lake)
## [Video](https://azure.microsoft.com/documentation/videos/index/?services=data-lake-store)
