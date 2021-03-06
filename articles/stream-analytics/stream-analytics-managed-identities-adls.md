---
title: Usare le identità gestite per l'autenticazione dei processi di Analisi di flusso di Azure per l'output in Azure Data Lake Storage Gen1 (anteprima)
description: ''
services: stream-analytics
author: mamccrea
ms.author: mamccrea
ms.service: stream-analytics
ms.topic: conceptual
ms.date: 09/27/2018
ms.openlocfilehash: 72bf467cc0f2ba195aa4f25228bc9e08605cd4ee
ms.sourcegitcommit: 7bc4a872c170e3416052c87287391bc7adbf84ff
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 10/02/2018
ms.locfileid: "48018594"
---
# <a name="use-managed-identities-to-authenticate-azure-stream-analytics-jobs-to-azure-data-lake-storage-gen1-output-preview"></a>Usare le identità gestite per l'autenticazione dei processi di Analisi di flusso di Azure per l'output in Azure Data Lake Storage Gen1 (anteprima)

Analisi di flusso di Azure supporta l'autenticazione con identità gestita con l'output di Azure Data Lake Storage (ADLS) Gen1. L'identità è un'applicazione gestita registrata in Azure Active Directory che rappresenta un determinato processo di Analisi di flusso e può essere usata per l'autenticazione in una risorsa di destinazione. Le identità gestite eliminano le limitazioni associate ai metodi di autenticazione basata sull'utente, ad esempio la necessità di ripetere l'autenticazione a causa di modifiche della password o le scadenze dei token utente ogni 90 giorni. Inoltre, le identità gestite semplificano l'automazione delle distribuzioni dei processi di Analisi di flusso che inviano l'output ad Azure Data Lake Storage Gen1.

Per registrarsi per questa anteprima e scoprire di più sulle nuove funzionalità, vedere il post di blog [Eight new features in Azure Stream Analytics](https://azure.microsoft.com/en-us/blog/eight-new-features-in-azure-stream-analytics/) (Otto nuove funzionalità in Analisi di flusso di Azure).

Questo articolo illustra due metodi per abilitare l'identità gestita per un processo di Analisi di flusso di Azure che invia l'output ad Azure Data Lake Storage Gen1: tramite il portale di Azure e tramite la distribuzione dei modelli di Azure Resource Manager.

## <a name="enable-managed-identity-with-azure-portal"></a>Abilitare l'identità gestita con il portale di Azure

1. Per iniziare, creare un nuovo processo di Analisi di flusso o aprire un processo esistente nel portale di Azure. Nella barra dei menu sul lato sinistro della schermata selezionare **Identità gestita (anteprima)** in **Configura**.

   ![Configurare l'identità gestita (anteprima) di Analisi di flusso](./media/stream-analytics-managed-identities-adls/stream-analytics-managed-identity-preview.png)

2. Selezionare **Use System-assigned Managed Identity (preview)** (Usa identità gestita assegnata dal sistema - anteprima) dalla finestra visualizzata sulla destra. Fare clic su **Salva** per creare un'entità servizio per l'identità del processo di Analisi di flusso in Azure Active Directory. Il ciclo di vita dell'identità creata sarà gestito da Azure. Quando si elimina il processo di Analisi di flusso, l'identità associata (ovvero, l'entità servizio) viene eliminata automaticamente da Azure.

   Al momento del salvataggio della configurazione, l'ID oggetto (OID) dell'entità servizio viene indicato come ID dell'entità, come illustrato di seguito:

   ![ID dell'entità di Analisi di flusso](./media/stream-analytics-managed-identities-adls/stream-analytics-principal-id.png)
 
   L'entità servizio ha lo stesso nome del processo di Analisi di flusso. Ad esempio, se il nome del processo è **MyASAJob**, anche il nome dell'entità servizio creata è **MyASAJob**.

3. Nella finestra delle proprietà di output del sink di output di ADLS Gen1, fare clic sull'elenco a discesa Modalità di autenticazione e selezionare **Identità gestita (anteprima)**.

4. Compilare le proprietà rimanenti. Per altre informazioni sulla creazione di un output di ADLS, vedere [Create a Data lake Store output with stream analytics](../data-lake-store/data-lake-store-stream-analytics.md) (Creare un output di Data Lake Store con Analisi di flusso). Al termine, fare clic su **Salva**.

   ![Configurare Azure Data Lake Storage](./media/stream-analytics-managed-identities-adls/stream-analytics-configure-adls.png)
 
5. Passare alla pagina Panoramica di ADLS Gen1 e fare clic su **Esplora dati**.

   ![Configurare Data Lake Storage - Panoramica](./media/stream-analytics-managed-identities-adls/stream-analytics-adls-overview.png)

6. Nel riquadro Esplora dati selezionare **Accesso** e fare clic su **Aggiungi** nel riquadro di accesso.

   ![Configurare l'accesso a Data Lake Storage](./media/stream-analytics-managed-identities-adls/stream-analytics-adls-access.png)

7. Nella casella di testo nel riquadro **Seleziona utente o gruppo** digitare il nome dell'entità servizio. Tenere presente che il nome dell'entità servizio è anche il nome del processo di Analisi di flusso corrispondente. Quando si inizia a digitare il nome dell'entità, questa viene visualizzata sotto la casella di testo. Scegliere il nome dell'entità servizio desiderata e fare clic su **Seleziona**.

   ![Selezionare il nome di un'entità servizio](./media/stream-analytics-managed-identities-adls/stream-analytics-service-principal-name.png)
 
8. Nel riquadro **Autorizzazioni** selezionare le autorizzazioni **Scrittura** ed **Esecuzione**, quindi assegnarle a **Questa cartella e tutti gli elementi figlio**. Fare quindi clic su **OK**.

   ![Selezionare un'autorizzazione](./media/stream-analytics-managed-identities-adls/stream-analytics-select-permissions.png)
 
9. L'entità servizio viene elencata in **Autorizzazioni assegnate** nel riquadro **Accesso** come illustrato di seguito. È ora possibile tornare indietro e avviare il processo di Analisi di flusso.

   ![Elenco Accesso](./media/stream-analytics-managed-identities-adls/stream-analytics-access-list.png)

   Per altre informazioni sulle autorizzazioni del file system di Data Lake Storage Gen1, vedere [Controllo di accesso in Azure Data Lake Storage Gen1](../data-lake-store/data-lake-store-access-control.md).

## <a name="resource-manager-template-deployment"></a>Distribuzione del modello di Resource Manager

1. È possibile creare una risorsa *Microsoft.StreamAnalytics/streamingjobs* con un'identità gestita, includendo la proprietà seguente nella sezione delle risorse del modello di Resource Manager:

   ```json
   "Identity": {
   "Type": "SystemAssigned",
   },
   ```

   Questa proprietà indica ad Azure Resource Manager di creare e gestire l'identità per il processo di Analisi di flusso di Azure.

   **Processo di esempio**

   ```json
   { 
   "Name": "AsaJobWithIdentity", 
   "Type": "Microsoft.StreamAnalytics/streamingjobs", 
   "Location": "West US",
   "Identity": {
     "Type": "SystemAssigned", 
     }, 
   "properties": {
      "sku": {
       "name": "standard"
       },
   "outputs": [
         {
           "name": "string",
           "properties":{
             "datasource": {        
               "type": "Microsoft.DataLake/Accounts",
               "properties": {
                 "accountName": “myDataLakeAccountName",
                 "filePathPrefix": “cluster1/logs/{date}/{time}",
                 "dateFormat": "YYYY/MM/DD",
                 "timeFormat": "HH",
                 "authenticationMode": "Msi"
                 }
                 
   }
   ```
  
   **Risposta del processo di esempio**

   ```json
   { 
   "Name": "mySAJob", 
   "Type": "Microsoft.StreamAnalytics/streamingjobs", 
   "Location": "West US",
   "Identity": {
   "Type": "SystemAssigned",
    "principalId": "GUID", 
    "tenantId": "GUID", 
   }, 
   "properties": {
           "sku": {
             "name": "standard"
           },
   }
   ```

   Prendere nota dell'ID entità della risposta del processo per concedere l'accesso alla risorsa di ADLS richiesta.

   **ID tenant** è l'ID del tenant di Azure Active Directory in cui creare l'entità servizio. L'entità servizio viene creata nel tenant di Azure considerato attendibile dalla sottoscrizione.

   **tipo** indica il tipo di identità gestita, come descritto nei tipi di identità gestite. È supportato solo il tipo Assegnata dal sistema.

2. Fornire l'accesso all'entità servizio tramite PowerShell. Per concedere l'accesso all'entità servizio tramite PowerShell, eseguire il comando seguente:

   ```powershell
   Set-AzureRmDataLakeStoreItemAclEntry -AccountName <accountName> -Path <Path> -AceType User -Id <PrinicpalId> -Permissions <Permissions>
   ```

   **PrincipalId** è l'ID oggetto dell'entità servizio ed è elencato nella schermata del portale dopo aver creato l'entità servizio. Se il processo è stato creato usando la distribuzione di un modello di Resource Manager, l'ID oggetto è elencato nella proprietà Identity della risposta del processo.

   **Esempio**

   ```powershell
   PS > Set-AzureRmDataLakeStoreItemAclEntry -AccountName "adlsmsidemo" -Path / -AceType
   User -Id 14c6fd67-d9f5-4680-a394-cd7df1f9bacf -Permissions WriteExecute
   ```

   Per altre informazioni sul precedente comando di PowerShell, vedere la documentazione di [Set-AzureRmDataLakeStoreItemAclEntry](https://docs.microsoft.com/powershell/module/azurerm.datalakestore/set-azurermdatalakestoreitemaclentry?view=azurermps-6.8.1&viewFallbackFrom=azurermps-4.2.0#optional-parameters).

## <a name="next-steps"></a>Passaggi successivi

* [Create a Data lake Store output with stream analytics](../data-lake-store/data-lake-store-stream-analytics.md) (Creare un output di Data Lake Store con Analisi di flusso)
