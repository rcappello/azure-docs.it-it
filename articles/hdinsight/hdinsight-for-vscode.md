---
title: Strumenti di Azure HDInsight - Usare Visual Studio Code per Hive, LLAP o PySpark | Microsoft Docs
description: Informazioni su come usare gli strumenti di Azure HDInsight per Visual Studio Code per creare e inviare query e script.
Keywords: VS Code,Azure HDInsight Tools,Hive,Python,PySpark,Spark,HDInsight,Hadoop,LLAP,Interactive Hive,Interactive Query
services: HDInsight
documentationcenter: ''
author: jejiang
ms.author: jejiang
ms.reviewer: jasonh
ms.service: hdinsight
ms.topic: conceptual
ms.date: 10/27/2017
ms.openlocfilehash: 5cf3a18dc01ba5670e73aa93cb6c9aab2d5de660
ms.sourcegitcommit: 5a9be113868c29ec9e81fd3549c54a71db3cec31
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 09/11/2018
ms.locfileid: "44378620"
---
# <a name="use-azure-hdinsight-tools-for-visual-studio-code"></a>Usare gli strumenti di Azure HDInsight per Visual Studio Code

Informazioni su come usare gli strumenti di Azure HDInsight per Visual Studio Code (VS Code) per creare e inviare processi batch Hive, query Hive interattive e script PySpark. Gli strumenti di Azure HDInsight possono essere installati sulle piattaforme supportate da VS Code, tra cui Windows, Linux e macOS. Sono previsti prerequisiti specifici per le diverse piattaforme.


## <a name="prerequisites"></a>Prerequisiti

Per completare le procedure descritte in questo articolo, sono necessari gli elementi seguenti:

- Un cluster HDInsight. Per creare un cluster, vedere [Introduzione a HDInsight](hadoop/apache-hadoop-linux-tutorial-get-started.md).
- [Visual Studio Code](https://www.visualstudio.com/products/code-vs.aspx).
- [Mono](http://www.mono-project.com/docs/getting-started/install/). Mono è necessario solo per Linux e macOS.

## <a name="install-the-hdinsight-tools"></a>Installare gli strumenti di HDInsight
   
Dopo avere installato i prerequisiti, è possibile installare gli strumenti di Azure HDInsight per VS Code. 

### <a name="to-install-azure-hdinsight-tools"></a>Per installare gli strumenti di Azure HDInsight

1. Aprire Visual Studio Code.

2. Nel riquadro sinistro selezionare **Estensioni**. Nella casella di ricerca immettere **HDInsight**.

3. Accanto a **Strumenti di Azure HDInsight** selezionare **Installa**. Dopo alcuni secondi il pulsante **Installa** diventa **Ricarica**.

4. Selezionare **Ricarica** per attivare l'estensione degli **strumenti di Azure HDInsight**.

5. Selezionare **Ricarica finestra** per confermare. Gli **strumenti di Azure HDInsight** vengono visualizzati nel riquadro **Estensioni**.

   ![HDInsight per Visual Studio Code - Installazione di Python](./media/hdinsight-for-vscode/install-hdInsight-plugin.png)

## <a name="open-hdinsight-workspace"></a>Aprire l'area di lavoro HDInsight

Per potersi connettere ad Azure, è prima necessario creare un'area di lavoro in VS Code.

### <a name="to-open-a-workspace"></a>Per aprire un'area di lavoro

1. Nel menu **File** selezionare **Apri cartella**. Specificare quindi una cartella esistente come cartella di lavoro oppure crearne una nuova. La cartella viene visualizzata nel riquadro sinistro.

2. Nel riquadro sinistro selezionare l'icona **Nuovo file** accanto alla cartella di lavoro.

   ![Nuovo file](./media/hdinsight-for-vscode/new-file.png)

3. Assegnare al nuovo file l'estensione hql (query Hive) o py (script Spark). 

## <a name="connect-to-hdinsight-cluster"></a>Connettersi al cluster HDInsight

Prima di inviare script ai cluster HDInsight da Visual Studio Code, è necessario connettersi al proprio account Azure oppure collegare un cluster, usando un nome utente e una password Ambari o un account aggiunto al dominio.

### <a name="to-connect-to-azure"></a>Per connettersi ad Azure

1. Creare una nuova cartella di lavoro e un nuovo file di script, se non sono già disponibili.

2. Fare clic con il pulsante destro del mouse sull'editor di script e quindi scegliere **HDInsight: Login** (HDInsight: Accesso) dal menu di scelta rapida. È anche possibile premere **CTRL+MAIUSC+P** e quindi immettere **HDInsight: Login** (HDInsight: Accesso).

    ![Accesso agli strumenti HDInsight per Visual Studio Code](./media/hdinsight-for-vscode/hdinsight-for-vscode-extension-login.png)

3. Per accedere, seguire le istruzioni di accesso nel riquadro **OUTPUT**.
    + Per un ambiente globale, l'accesso ad HDInsight attiverà il processo di accesso ad Azure.

        ![Istruzioni di accesso ad Azure](./media/hdinsight-for-vscode/hdi-azure-hdinsight-azure-signin.png)

    + Per altri ambienti, seguire le istruzioni di accesso.

        ![Istruzioni di accesso per altri ambienti](./media/hdinsight-for-vscode/hdi-azure-hdinsight-hdinsight-signin.png)

    Dopo essersi connessi, il nome dell'account di Azure viene visualizzato sulla barra di stato nella parte inferiore sinistra della finestra di VS Code. 

    > [!NOTE]
    > A causa di un problema di autenticazione di Azure noto, è necessario aprire un browser in modalità privata o in incognito. Se per l'account è abilitata l'autenticazione a due fattori, è consigliabile usare l'autenticazione tramite telefono anziché mediante codice PIN.
  

4. Fare clic con il pulsante destro del mouse sull'editor di script per visualizzare il menu di scelta rapida. Da questo menu di scelta rapida è possibile eseguire le attività seguenti:

    - Effettuare la disconnessione
    - Elencare cluster
    - Impostare cluster predefiniti
    - Inviare query Interactive Hive
    - Inviare script batch Hive
    - Inviare query PySpark interattive
    - Inviare script batch PySpark
    - Impostare la configurazione

<h3 id="linkcluster">Per collegare un cluster</h3>

È possibile collegare un cluster normale usando un nome utente Ambari gestito e anche collegare un cluster Hadoop di sicurezza usando un nome utente di dominio (ad esempio: user1@contoso.com).
1. Aprire il riquadro comandi premendo la combinazione di tasti **CTRL+MAIUSC+P** e quindi immettere **HDInsight: Collega un cluster**.

   ![comando di collegamento di un cluster](./media/hdinsight-for-vscode/link-cluster-command.png)

2. Immettere l'URL del cluster HDInsight -> immettere il nome utente -> immettere la password -> selezionare il tipo di cluster -> se la verifica viene superata, vengono visualizzate le informazioni sull'esito positivo.
   
   ![finestra di dialogo di collegamento di un cluster](./media/hdinsight-for-vscode/link-cluster-process.png)

   > [!NOTE]
   > Vengono usati il nome utente e la password collegati se il cluster ha eseguito l'accesso alla sottoscrizione di Azure e ha collegato un cluster. 
   
3. È possibile visualizzare un cluster collegato usando il comando **Elenca cluster**. È ora possibile inviare uno script al cluster collegato.

   ![Cluster collegato](./media/hdinsight-for-vscode/linked-cluster.png)

4. È anche possibile scollegare un cluster immettendo **HDInsight: Scollega un cluster** nel riquadro comandi.


### <a name="to-link-a-generic-livy-endpoint"></a>Per collegare un endpoint livy generico

1. Aprire il riquadro comandi premendo la combinazione di tasti **CTRL+MAIUSC+P** e quindi immettere **HDInsight: Collega un cluster**.
2. Selezionare**Endpoint livy generico**.
3. Immettere l'endpoint livy generico, ad esempio: http://10.172.41.42:18080.
4. Selezionare **Base** quando è richiesta un'autorizzazione per l'endpoint livy generico, in caso contrario, selezionare **Nessuna**.
5. Immettere il nome utente quando si seleziona **Base** nel passaggio 4.
6. Immettere la password quando si seleziona **Base** nel passaggio 4.
7. Endpoint livy generico collegato correttamente.

   ![cluster livy generico collegato](./media/hdinsight-for-vscode/link-cluster-process-generic-livy.png)

## <a name="list-hdinsight-clusters"></a>Elencare i cluster HDInsight

Per testare la connessione, è possibile elencare i cluster HDInsight:

### <a name="to-list-hdinsight-clusters-under-your-azure-subscription"></a>Per elencare i cluster HDInsight nella sottoscrizione di Azure
1. Aprire un'area di lavoro e quindi connettersi ad Azure. Per altre informazioni, vedere [Aprire l'area di lavoro HDInsight](#open-hdinsight-workspace) e [Connettersi ad Azure](#connect-to-hdinsight-cluster).

2. Fare clic con il pulsante destro del mouse sull'editor di script e quindi scegliere **HDInsight: List Cluster** (HDInsight: Elenca cluster) dal menu di scelta rapida. 

3. I cluster Hive e Spark verranno visualizzati nel riquadro **Output**.

    ![Impostare una configurazione del cluster predefinito](./media/hdinsight-for-vscode/list-cluster-result.png)

## <a name="set-a-default-cluster"></a>Impostare un cluster predefinito
1. Aprire un'area di lavoro e connettersi ad Azure. Vedere [Aprire l'area di lavoro HDInsight](#open-hdinsight-workspace) e [Connettersi ad Azure](#connect-to-hdinsight-cluster).

2. Fare clic con il pulsante destro del mouse sull'editor di script e quindi selezionare **HDInsight: Set Default Cluster** (HDInsight: Imposta cluster predefinito). 

3. Selezionare un cluster come predefinito per il file di script corrente. Gli strumenti aggiornano automaticamente il file di configurazione **.VSCode\settings.json**. 

   ![Impostare la configurazione del cluster predefinito](./media/hdinsight-for-vscode/set-default-cluster-configuration.png)

## <a name="set-the-azure-environment"></a>Configurare l'ambiente di Azure
1. Aprire il riquadro comandi premendo la combinazione di tasti **CTRL+MAIUSC+P**.

2. Immettere **HDInsight: Set Azure Environment** (HDInsight: Imposta ambiente di Azure).

3. Scegliere la voce di accesso predefinita tra Azure e AzureChina.

4. Lo strumento, nel frattempo, ha già salvato la voce di accesso predefinita selezionata in **.VSCode\settings.json**. Aggiornare direttamente la voce anche nel file di configurazione. 

   ![Impostare la configurazione della voce di accesso predefinita](./media/hdinsight-for-vscode/set-default-login-entry-configuration.png)

## <a name="submit-interactive-hive-queries-hive-batch-scripts"></a>Inviare query Hive interattive e script batch Hive

Gli strumenti HDInsight per VS Code consentono di inviare query Hive interattive e script batch Hive ai cluster di HDInsight.

1. Creare una nuova cartella di lavoro e un nuovo file di script Hive, se non sono già disponibili.

2. Connettersi all'account di Azure o collegare i cluster.

3. Copiare e incollare il codice seguente nel file Hive e salvarlo.

    ```hiveql
    SELECT * FROM hivesampletable;
    ```
4. Fare clic con il pulsante destro del mouse sull'editor di script, selezionare **HDInsight: Hive Interactive** per inviare la query o usare la combinazione di tasti **Ctrl + Alt + I**. Selezionare **HDInsight: Hive Batch** per inviare lo script o usare la combinazione di tasti **Ctrl + Alt + H**. 

5. Selezionare il cluster quando necessario. Gli strumenti consentono anche di inviare un blocco di codice, anziché l'intero file di script, usando il menu di scelta rapida. Subito dopo, il risultato della query viene visualizzato in una nuova scheda.

   ![Risultato di Interactive Hive](./media/hdinsight-for-vscode/interactive-hive-result.png)

    - Pannello dei **risultati**: è possibile salvare i risultati completi come file CSV, JSON o file EXCEL in un percorso locale oppure selezionare più righe.

    - Pannello dei **messaggi**: se si seleziona il numero di **riga**, si passa alla prima riga dello script in esecuzione.

## <a name="submit-interactive-pyspark-queries"></a>Inviare query PySpark interattive

### <a name="to-submit-interactive-pyspark-queries-to-spark-clusters"></a>Per inviare query PySpark interattive ai cluster Spark.

1. Creare una nuova cartella di lavoro e un nuovo file di script con estensione py, se non sono già disponibili.

2. Connettersi all'account Azure personale, se non si è già connessi.

3. Copiare e incollare il codice seguente nel file di script:
   ```python
   from operator import add
   lines = spark.read.text("/HdiSamples/HdiSamples/FoodInspectionData/README").rdd.map(lambda r: r[0])
   counters = lines.flatMap(lambda x: x.split(' ')) \
                .map(lambda x: (x, 1)) \
                .reduceByKey(add)

   coll = counters.collect()
   sortedCollection = sorted(coll, key = lambda r: r[1], reverse = True)

   for i in range(0, 5):
        print(sortedCollection[i])
   ```
4. Evidenziare questi script, Fare clic con il pulsante destro del mouse sull'editor di script e selezionare **HDInsight: PySpark Interactive** o usare la combinazione di tasti **Ctrl + Alt + I**.

5. Se non è ancora stata installata l'estensione **Python** in VS Code, selezionare il pulsante **Installa** come illustrato nella figura seguente:

    ![HDInsight per Visual Studio Code - Installazione di Python](./media/hdinsight-for-vscode/hdinsight-vscode-install-python.png)

6. Installare l'ambiente Python nel sistema, se non è già stato installato. 
   - Per Windows, scaricare e installare [Python](https://www.python.org/downloads/). Assicurarsi quindi che `Python` e `pip` siano presenti nel percorso del sistema.

   - Per le istruzioni relative a macOS e Linux, vedere [Configurare l'ambiente PySpark interattivo per Visual Studio Code](set-up-pyspark-interactive-environment.md).

7. Selezionare un cluster a cui inviare la query PySpark. Il risultato della query viene visualizzato subito dopo in una nuova scheda a destra:

   ![Risultato dell'invio del processo Python](./media/hdinsight-for-vscode/pyspark-interactive-result.png) 
8. Lo strumento supporta anche l'esecuzione di query sulla **clausola SQL**.

   ![Risultato dell'invio del processo Python](./media/hdinsight-for-vscode/pyspark-ineteractive-select-result.png) Lo stato dell'invio viene visualizzato a sinistra della barra di stato inferiore durante l'esecuzione delle query. Non inviare altre query se lo stato è impostato su **PySpark Kernel (busy)** (Kernel PySpark - Occupato). 

>[!NOTE]
>I cluster possono gestire le informazioni contenute nella sessione, come la variabile definita, la funzione e i valori corrispondenti, in modo che sia possibile farvi riferimento da più chiamate di servizio relative allo stesso cluster. 

### <a name="to-disable-environment-check"></a>Per disabilitare il controllo di ambiente

Per impostazione predefinita quando si inviano query PySpark interattive, gli strumenti di HDInsight verificano l'ambiente e installano pacchetti dipendenti. Per disabilitare il controllo di ambiente impostare **hdinsight.disablePysparkEnvironmentValidation** su **yes** sotto **IMPOSTAZIONI UTENTE**.

   ![Impostare il controllo di ambiente dalle impostazioni](./media/hdinsight-for-vscode/hdi-azure-hdinsight-environment-check.png)

In alternativa, fare clic su **disabilitare la convalida** dopo che viene visualizzata la finestra di dialogo.

   ![Impostare il controllo di ambiente dalla finestra di dialogo](./media/hdinsight-for-vscode/hdi-azure-hdinsight-environment-check-dialog.png)

### <a name="pyspark3-is-not-supported-with-spark2223"></a>PySpark 3 non è supportato con Spark 2.2/2.3

PySpark 3 non è più supportato con cluster Spark 2.2 e cluster Spark 2.3, è supportato solo "PySpark" per Python. Il fatto che l'invio a spark 2.2/2.3 abbia esito negativo con Python 3 è un problema noto.

   ![L'invio a python 3 ha esito negativo](./media/hdinsight-for-vscode/hdi-azure-hdinsight-py3-error.png)

Seguire i passaggi per usare Python 2.x: 

1. Installare Python 2.7 sul computer locale e aggiungerlo al percorso di sistema.

2. Riavviare VSCode.

3. Passare a Python 2 facendo clic su **Python XXX** sulla barra di stato, quindi scegliere il Python di destinazione.

   ![Selezionare la versione di Python](./media/hdinsight-for-vscode/hdi-azure-hdinsight-select-python.png)

## <a name="submit-pyspark-batch-job"></a>Inviare un processo batch PySpark

1. Creare una nuova cartella di lavoro e un nuovo file di script con estensione py, se non sono già disponibili.

2. Connettersi all'account Azure personale, se non si è già connessi.

3. Copiare e incollare il codice seguente nel file di script:

    ```python
    from __future__ import print_function
    import sys
    from operator import add
    from pyspark.sql import SparkSession
    if __name__ == "__main__":
        spark = SparkSession\
            .builder\
            .appName("PythonWordCount")\
            .getOrCreate()
    
        lines = spark.read.text('/HdiSamples/HdiSamples/SensorSampleData/hvac/HVAC.csv').rdd.map(lambda r: r[0])
        counts = lines.flatMap(lambda x: x.split(' '))\
                    .map(lambda x: (x, 1))\
                    .reduceByKey(add)
        output = counts.collect()
        for (word, count) in output:
            print("%s: %i" % (word, count))
        spark.stop()
    ```
4. Fare clic con il pulsante destro del mouse sull'editor di script e quindi selezionare **HDInsight: PySpark Batch** o usare la combinazione di tasti **Ctrl + Alt + H**. 

5. Selezionare un cluster a cui inviare il processo PySpark. 

   ![Risultato dell'invio del processo Python](./media/hdinsight-for-vscode/submit-pythonjob-result.png) 

Dopo aver inviato un processo Python, i log di invio vengono visualizzati nella finestra **Output** in VS Code. Vengono visualizzati anche l'**URL dell'interfaccia utente di Spark** e l'**URL dell'interfaccia utente di Yarn**. È possibile aprire l'URL in un Web browser per tenere traccia dello stato del processo.

## <a name="livy-configuration"></a>Configurazione di Livy

La configurazione di Livy è supportata ed è possibile impostarla in **.VSCode\settings.json** nella cartella dell'area di lavoro. Attualmente la configurazione di livy supporta solo lo script Python. Per altre informazioni, vedere [Livy LEGGIMI](https://github.com/cloudera/livy/blob/master/README.rst ).

<a id="triggerlivyconf"></a>**Come attivare la configurazione di livy**
   
È disponibile nel menu **File**, selezionare **Preferenze** e scegliere **Impostazioni** nel menu di scelta rapida. Fare clic sulla scheda **IMPOSTAZIONI AREA DI LAVORO**, è possibile iniziare a impostare la configurazione di livy.

È anche possibile inviare un file, si noti che la cartella con estensione vscode viene aggiunta automaticamente alla cartella di lavoro. È possibile trovare la configurazione di livy facendo clic su **.vscode\settings.json**.

+ Impostazioni di progetto:

    ![Configurazione di Livy](./media/hdinsight-for-vscode/hdi-livyconfig.png)

>[!NOTE]
>Per le impostazioni **driverMomory** e **executorMomry**, impostare il valore unità, ad esempio 1 g o 1024 m. 

+ Configurazioni di Livy supportate:   

    **POST /batches**   
    Request Body

    | name | description | type | 
    | :- | :- | :- | 
    | file | File contenente l'applicazione da eseguire | percorso (obbligatorio) | 
    | proxyUser | Utente da rappresentare durante l'esecuzione del processo | stringa | 
    | className | Classe principale Java/Spark dell'applicazione | stringa |
    | args | Argomenti della riga di comando per l'applicazione | elenco di stringhe | 
    | file JAR | file JAR da usare in questa sessione | Elenco di stringhe | 
    | pyFiles | File di Python da usare in questa sessione | Elenco di stringhe |
    | input | file da usare in questa sessione | Elenco di stringhe |
    | driverMemory | Quantità di memoria da usare per il processo del driver | stringa |
    | driverCores | Numero di core da usare per il processo del driver | int |
    | executorMemory | Quantità di memoria da usare per ogni processo executor | stringa |
    | executorCores | Numero di core da usare per ogni executor | int |
    | numExecutors | Numero di executor da avviare per questa sessione | int |
    | archives | Archivi da usare in questa sessione | Elenco di stringhe |
    | coda | Nome della coda a cui YARN viene effettuato l'invio | stringa |
    | name | Nome della sessione | stringa |
    | conf | Proprietà di configurazione di Spark | Mapping della chiave = val |

    Contenuto risposta   
    Oggetto batch creato.

    | name | description | type | 
    | :- | :- | :- | 
    | id | ID sessione | int | 
    | appId | ID applicazione della sessione |  string |
    | appInfo | Informazioni dettagliate sull'applicazione | Mapping della chiave = val |
    | log | Righe di log | elenco di stringhe |
    | state |   Stato batch | stringa |

>[!NOTE]
>La configurazione di livy assegnata verrà visualizzata nel riquadro di output quando si invia lo script.

## <a name="integrate-with-azure-hdinsight-from-explorer"></a>Eseguire l'integrazione con Azure HDInsight da Explorer

Azure HDInsight è stato aggiunto al pannello di sinistra. È possibile esplorare e gestire direttamente il cluster.

1. Espandere **AZURE HDINSIGHT**, se l'accesso non è stato eseguito, verrà visualizzato il collegamento **Accedi ad Azure...** .

    ![Immagine del collegamento di accesso](./media/hdinsight-for-vscode/hid-azure-hdinsight-sign-in.png)

2. Fare clic su **Accedi ad Azure**, il collegamento e il codice di accesso vengono visualizzati nella parte inferiore destra.

    ![Istruzioni di accesso per altri ambienti](./media/hdinsight-for-vscode/hdi-azure-hdinsight-azure-signin-code.png)

3. Fare clic sul pulsante **Copia e apri** per aprire il browser, incollare il codice, fare clic sul pulsante **Continua**, verrà visualizzato il messaggio di accesso eseguito.

4. Dopo aver effettuato l'accesso, le sottoscrizioni disponibili e i cluster (sono supportati Spark, Hadoop e HBase) sono elencati in **AZURE HDINSIGHT**. 

   ![Sottoscrizione di Azure HDInsight](./media/hdinsight-for-vscode/hdi-azure-hdinsight-subscription.png)

5. Espandere il cluster per visualizzare lo schema di database e tabella dei metadati hive.

   ![Cluster Azure HDInsight](./media/hdinsight-for-vscode/hdi-azure-hdinsight-cluster.png)

## <a name="additional-features"></a>Funzionalità aggiuntive

HDInsight per VS Code supporta le funzionalità seguenti:

- **Completamento automatico di IntelliSense**. Vengono visualizzati suggerimenti per parole chiave, metodi, variabili e così via. Icone diverse rappresentano vari tipi di oggetti.

    ![Tipi di oggetto IntelliSense degli strumenti di HDInsight per Visual Studio Code](./media/hdinsight-for-vscode/hdinsight-for-vscode-auto-complete-objects.png)
- **Indicatore di errore di IntelliSense**. Il servizio di linguaggio sottolinea gli errori di modifica nello script Hive.     
- **Evidenziazioni della sintassi**. Il servizio di linguaggio usa colori diversi per differenziare variabili, parole chiave, tipi di dati, funzioni e così via. 

    ![Evidenziazioni della sintassi degli strumenti di HDInsight per Visual Studio Code](./media/hdinsight-for-vscode/hdinsight-for-vscode-syntax-highlights.png)

## <a name="next-steps"></a>Passaggi successivi

### <a name="demo"></a>Demo
* HDInsight per VS Code: [Video](https://go.microsoft.com/fwlink/?linkid=858706)

### <a name="tools-and-extensions"></a>Strumenti ed estensioni

* [Usare Azure Toolkit per IntelliJ per il debug remoto di applicazioni Spark tramite VPN](spark/apache-spark-intellij-tool-plugin-debug-jobs-remotely.md)
* [Usare Azure Toolkit per IntelliJ per il debug remoto di applicazioni Spark tramite SSH](spark/apache-spark-intellij-tool-debug-remotely-through-ssh.md)
* [Usare gli strumenti HDInsight per IntelliJ con Hortonworks Sandbox](hadoop/hdinsight-tools-for-intellij-with-hortonworks-sandbox.md)
* [Use HDInsight Tools in Azure Toolkit for Eclipse to create Spark applications (Usare gli strumenti HDInsight nel Toolkit di Azure per Eclipse per creare applicazioni Spark)](spark/apache-spark-eclipse-tool-plugin.md)
* [Usare i notebook di Zeppelin con un cluster Spark in HDInsight](spark/apache-spark-zeppelin-notebook.md)
* [Kernel disponibili per notebook di Jupyter nel cluster Spark per HDInsight](spark/apache-spark-jupyter-notebook-kernels.md)
* [Usare pacchetti esterni con i notebook Jupyter](spark/apache-spark-jupyter-notebook-use-external-packages.md)
* [Installare Jupyter Notebook nel computer e connetterlo a un cluster HDInsight Spark](spark/apache-spark-jupyter-notebook-install-locally.md)
* [Visualizzare i dati Hive con Microsoft Power BI in Azure HDInsight](hadoop/apache-hadoop-connect-hive-power-bi.md)
* [Visualize Interactive Query Hive data with Power BI in Azure HDInsight](./interactive-query/apache-hadoop-connect-hive-power-bi-directquery.md) (Visualizzare i dati Hive di Interactive Query con Power BI in Azure HDInsight).
* [Configurare l'ambiente PySpark interattivo per Visual Studio Code](set-up-pyspark-interactive-environment.md)
* [Usare Zeppelin per eseguire query Hive in Azure HDInsight](./hdinsight-connect-hive-zeppelin.md)

### <a name="scenarios"></a>Scenari
* [Spark con Business Intelligence: eseguire l'analisi interattiva dei dati con strumenti di Business Intelligence mediante Spark in HDInsight](spark/apache-spark-use-bi-tools.md)
* [Spark con Machine Learning: utilizzare Spark in HDInsight per l'analisi della temperatura di compilazione utilizzando dati HVAC](spark/apache-spark-ipython-notebook-machine-learning.md)
* [Spark con Machine Learning: utilizzare Spark in HDInsight per stimare i risultati dell'ispezione cibo](spark/apache-spark-machine-learning-mllib-ipython.md)
* [Analisi dei log del sito Web mediante Spark in HDInsight](spark/apache-spark-custom-library-website-log-analysis.md)

### <a name="create-and-running-applications"></a>Creazione ed esecuzione di applicazioni
* [Creare un'applicazione autonoma con Scala](spark/apache-spark-create-standalone-application.md)
* [Eseguire processi in modalità remota in un cluster Spark usando Livy](spark/apache-spark-livy-rest-interface.md)

### <a name="manage-resources"></a>Gestire risorse
* [Gestire le risorse del cluster Apache Spark in Azure HDInsight](spark/apache-spark-resource-manager.md)
* [Tenere traccia ed eseguire il debug di processi in esecuzione nel cluster Apache Spark in Azure HDInsight](spark/apache-spark-job-debugging.md)



