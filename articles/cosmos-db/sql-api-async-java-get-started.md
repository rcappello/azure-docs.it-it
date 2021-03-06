---
title: Creare un'applicazione Java tramite Azure Cosmos DB Async Java SDK | Microsoft Docs
description: Questa esercitazione illustra come usare gli account API SQL di Azure Cosmos DB per archiviare e accedere ai dati tramite un'applicazione Async Java.
keywords: esercitazione su nosql, database online, applicazione console java
services: cosmos-db
author: SnehaGunda
manager: kfile
ms.service: cosmos-db
ms.component: cosmosdb-sql
ms.devlang: java
ms.topic: tutorial
ms.date: 06/29/2018
ms.author: sngun
ms.openlocfilehash: aa2613f7cb73c2c338189aaaa48587c49a3093f5
ms.sourcegitcommit: 32d218f5bd74f1cd106f4248115985df631d0a8c
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 09/24/2018
ms.locfileid: "46962205"
---
# <a name="build-a-java-application-by-using-azure-cosmos-db-async-java-sdk"></a>Creare un'applicazione Java tramite Azure Cosmos DB Async Java SDK 

> [!div class="op_single_selector"]
> * [.NET](sql-api-get-started.md)
> * [.NET Core](sql-api-dotnetcore-get-started.md)
> * [Java](sql-api-java-get-started.md)
> * [Async Java](sql-api-async-java-get-started.md)
> * [Node.JS](sql-api-nodejs-get-started.md)
> 

Azure Cosmos DB è un database multimodello distribuito a livello globale. Questa esercitazione illustra come usare gli account API SQL di Azure Cosmos DB per archiviare e accedere ai dati tramite un'applicazione Async Java. 

Argomenti trattati:

* Creazione e connessione a un account Azure Cosmos DB
* Configurazione della soluzione
* Creare una raccolta
* Creazione di documenti JSON
* Esecuzione di query sulla raccolta

Ecco come procedere.

## <a name="prerequisites"></a>Prerequisiti
Assicurarsi che sia disponibile quanto segue:

* Un account Azure attivo. Se non si ha un account, è possibile iscriversi per ottenere un [account gratuito](https://azure.microsoft.com/free/). 

  [!INCLUDE [cosmos-db-emulator-docdb-api](../../includes/cosmos-db-emulator-docdb-api.md)]

* [Git](https://git-scm.com/downloads).
* [Java Development Kit (JDK) 8+](http://www.oracle.com/technetwork/java/javase/downloads/index.html).
* [Maven](http://maven.apache.org/download.cgi).

## <a name="step-1-create-an-azure-cosmos-db-account"></a>Passaggio 1: Creare un account di Azure Cosmos DB
Creare prima di tutto un account Azure Cosmos DB. Se è già disponibile un account da usare, è possibile andare direttamente al passaggio [Clonare il progetto GitHub](#GitClone). Se si usa l'emulatore Azure Cosmos DB, seguire la procedura illustrata nell'articolo relativo all'[emulatore Azure Cosmos DB](local-emulator.md) per configurare l'emulatore e proseguire con il passaggio [Clonare il progetto GitHub](#GitClone).

[!INCLUDE [cosmos-db-create-dbaccount](../../includes/cosmos-db-create-dbaccount.md)]

## <a id="GitClone"></a>Passaggio 2: Clonare il progetto GitHub
Per iniziare, è possibile clonare il repository GitHub per l'[introduzione ad Azure Cosmos DB e Java](https://github.com/Azure-Samples/azure-cosmos-db-sql-api-async-java-getting-started). Eseguire questo comando da una directory locale per recuperare il progetto di esempio in locale.

```bash
git clone https://github.com/Azure-Samples/azure-cosmos-db-sql-api-async-java-getting-started.git

cd azure-cosmos-db-sql-api-async-java-getting-started
cd azure-cosmosdb-get-started

```
La directory contiene un oggetto `pom.xml` per il progetto e una cartella `src/main/java/com/microsoft/azure/cosmosdb/sample` che contiene il codice sorgente Java incluso `Main.java`, che mostra come eseguire semplici operazioni con Azure Cosmos DB, come la creazione di documenti e l'esecuzione di query sui dati all'interno di una raccolta. L'oggetto `pom.xml` include una dipendenza per [Azure Cosmos DB Java SDK su Maven](https://mvnrepository.com/artifact/com.microsoft.azure/azure-documentdb).

```xml
<dependency>
  <groupId>com.microsoft.azure</groupId>
  <artifactId>azure-documentdb</artifactId>
  <version>2.0.0</version>
</dependency>
```

## <a id="Connect"></a>Passaggio 3: Connettersi a un account Azure Cosmos DB
Tornare al [portale di Azure](https://portal.azure.com) per recuperare l'endpoint e la chiave master primaria. L'endpoint e la chiave primaria di Azure Cosmos DB sono necessari all'applicazione per conoscere la destinazione della connessione e ad Azure Cosmos DB per considerare attendibile la connessione dell'applicazione. Il file `AccountSettings.java` contiene i valori relativi a chiave primaria e URI. 

Nel portale di Azure passare all'account Azure Cosmos DB e quindi fare clic su **Chiavi**. Copiare l'URI e la CHIAVE PRIMARIA dal portale e incollarli nel file `AccountSettings.java`. 

```java
public class AccountSettings 
{
  // Replace MASTER_KEY and HOST with values from your Azure Cosmos DB account.
    
  // <!--[SuppressMessage("Microsoft.Security", "CS002:SecretInNextLine")]-->
  public static String MASTER_KEY = System.getProperty("ACCOUNT_KEY", 
          StringUtils.defaultString(StringUtils.trimToNull(
          System.getenv().get("ACCOUNT_KEY")), "<Fill your Azure Cosmos DB account key>"));

  public static String HOST = System.getProperty("ACCOUNT_HOST",
           StringUtils.defaultString(StringUtils.trimToNull(
           System.getenv().get("ACCOUNT_HOST")),"<Fill your Azure Cosmos DB URI>"));
}
```

![Screenshot del portale di Azure usato nell'esercitazione su NoSQL per creare un'applicazione console Java. Mostra un account Azure Cosmos DB, con l'hub ACTIVE evidenziato, il pulsante CHIAVI evidenziato nel pannello dell'account Azure Cosmos DB e i valori di URI, CHIAVE PRIMARIA e CHIAVE SECONDARIA evidenziati nel pannello Chiavi][keys]

## <a name="step-4-initialize-the-client-object"></a>Passaggio 4: Inizializzare l'oggetto client
Inizializzare l'oggetto client tramite i valori relativi a chiave primaria e URI host definiti nel file "AccountSettings.java"

```java
client = new AsyncDocumentClient.Builder()
         .withServiceEndpoint(AccountSettings.HOST)
         .withMasterKey(AccountSettings.MASTER_KEY)
         .withConnectionPolicy(ConnectionPolicy.GetDefault())
         .withConsistencyLevel(ConsistencyLevel.Session)
         .build();
```

## <a id="CreateDatabase"></a>Passaggio 5: Creare un database

È possibile creare un [database](sql-api-resources.md#databases) di Azure Cosmos DB usando il metodo createDatabaseIfNotExists() della classe DocumentClient. Un database è il contenitore logico per l'archiviazione di documenti JSON partizionato nelle raccolte.

```java
private void createDatabaseIfNotExists() throws Exception 
{
    
    writeToConsoleAndPromptToContinue("Check if database " + databaseName + " exists.");

    String databaseLink = String.format("/dbs/%s", databaseName);

    Observable<ResourceResponse<Database>> databaseReadObs = client.readDatabase(databaseLink, null);

    Observable<ResourceResponse<Database>> databaseExistenceObs = databaseReadObs
                .doOnNext(x -> {System.out.println("database " + databaseName + " already exists.");}).onErrorResumeNext(e -> {
   // if the database doesn't already exists
   // readDatabase() will result in 404 error
   if (e instanceof DocumentClientException) 
   {
       DocumentClientException de = (DocumentClientException) e;
       // if database 
       if (de.getStatusCode() == 404) {
       // if the database doesn't exist, create it.
       System.out.println("database " + databaseName + " doesn't existed," + " creating it...");
       Database dbDefinition = new Database();
       dbDefinition.setId(databaseName);
       return client.createDatabase(dbDefinition, null);
     }
     }

    // some unexpected failure in reading database happened.
    // pass the error up.
    System.err.println("Reading database " + databaseName + " failed.");
        return Observable.error(e);     
    });

   // wait for completion
   databaseExistenceObs.toCompletable().await();

   System.out.println("Checking database " + databaseName + " completed!\n");
}
```

## <a id="CreateColl"></a>Passaggio 6: Creare una raccolta

> [!WARNING]
> **createCollection** crea una nuova raccolta con velocità effettiva riservata, che presenta implicazioni in termini di prezzi. Per altre informazioni, visitare la [pagina relativa ai prezzi](https://azure.microsoft.com/pricing/details/cosmos-db/).
> 
> 
È possibile creare una raccolta usando il metodo createDocumentCollectionIfNotExists() della classe DocumentClient. Una raccolta è un contenitore di documenti JSON e di logica dell'applicazione JavaScript associata.

```java
private void createDocumentCollectionIfNotExists() throws Exception 
{
    
    writeToConsoleAndPromptToContinue("Check if collection " + collectionName + " exists.");

    // query for a collection with a given id
    // if it exists nothing else to be done
    // if the collection doesn't exist, create it.

    String databaseLink = String.format("/dbs/%s", databaseName);

    // we know there is only single page of result (empty or with a match)
    client.queryCollections(databaseLink, new SqlQuerySpec("SELECT * FROM r where r.id = @id", 
            new SqlParameterCollection(new SqlParameter("@id", collectionName))), null).single() 
            .flatMap(page -> {
            if (page.getResults().isEmpty()) {
             // if there is no matching collection create the collection.
             DocumentCollection collection = new DocumentCollection();
             collection.setId(collectionName);
             System.out.println("Creating collection " + collectionName);

             return client.createCollection(databaseLink, collection, null);
            } 
            else {
              // collection already exists, nothing else to be done.
              System.out.println("Collection " + collectionName + "already exists");
              return Observable.empty();
            }
      }).toCompletable().await();

 System.out.println("Checking collection " + collectionName + " completed!\n");
    }
```

## <a id="CreateDoc"></a>Passaggio 7: Creare documenti JSON

È possibile creare un [documento](sql-api-resources.md#documents) usando il metodo createDocument della classe DocumentClient. I documenti sono contenuto JSON definito dall'utente (arbitrario). Ora è possibile inserire uno o più documenti. Il file "src/main/java/com/microsoft/azure/cosmosdb/sample/Families.java" definisce i documenti JSON della famiglia 

```java
public static Family getJohnsonFamilyDocument() {
     Family andersenFamily = new Family();
     andersenFamily.setId("Johnson" + System.currentTimeMillis());
     andersenFamily.setLastName("Johnson");

      Parent parent1 = new Parent();
      parent1.setFirstName("John");

      Parent parent2 = new Parent();
      parent2.setFirstName("Lili");

      return andersenFamily;
    }
```

## <a id="Query"></a>Passaggio 8: Eseguire query sulle risorse di Azure Cosmos DB

Azure Cosmos DB supporta [query complesse](sql-api-sql-query.md) sui documenti JSON archiviati in ogni raccolta. Il codice di esempio seguente mostra come eseguire query su documenti in Azure Cosmos DB usando la sintassi SQL con il metodo [queryDocuments](/java/api/com.microsoft.azure.cosmosdb.rx._async_document_client.querydocuments).

```java
private void executeSimpleQueryAsyncAndRegisterListenerForResult(CountDownLatch completionLatch) 
{
    // Set some common query options
    FeedOptions queryOptions = new FeedOptions();
    queryOptions.setMaxItemCount(100);
    queryOptions.setEnableCrossPartitionQuery(true);

    String collectionLink = String.format("/dbs/%s/colls/%s", databaseName, collectionName);
    Observable<FeedResponse<Document>> queryObservable = client.queryDocuments(collectionLink,
           "SELECT * FROM Family WHERE Family.lastName = 'Andersen'", queryOptions);

    queryObservable.subscribe(queryResultPage -> {
            System.out.println("Got a page of query result with " +
            queryResultPage.getResults().size() + " document(s)"
            + " and request charge of " + queryResultPage.getRequestCharge());
    },
   // terminal error signal
        e -> {
          e.printStackTrace();
          completionLatch.countDown();
        },

   // terminal completion signal
         () -> {
            completionLatch.countDown();
         });
}
```

## <a id="Run"></a>Passaggio 9: Eseguire l'intera applicazione console Java
Per eseguire l'applicazione dalla console, passare alla cartella del progetto e compilare usando Maven:

```bash
mvn package
```

L'esecuzione di `mvn package` scarica la libreria di Azure Cosmos DB più recente da Maven e produce `GetStarted-0.0.1-SNAPSHOT.jar`. Eseguire l'app usando quanto segue:

```bash
mvn exec:java -DACCOUNT_HOST=<YOUR_COSMOS_DB_HOSTNAME> -DACCOUNT_KEY= <YOUR_COSMOS_DB_MASTER_KEY>
```
Congratulazioni! L'esercitazione su NoSQL è stata completata ed è stata creata un'applicazione console Java funzionante.

## <a name="next-steps"></a>Passaggi successivi
* Per un'esercitazione su app Web Java, vedere [Creazione di un'applicazione Web Java con Azure Cosmos DB](sql-api-java-application.md).
* Informazioni su come [monitorare un account Azure Cosmos DB](monitor-accounts.md).
* Eseguire query sul set di dati di esempio illustrato nella pagina [Query Playground](https://www.documentdb.com/sql/demo).

[keys]: media/sql-api-get-started/nosql-tutorial-keys.png
