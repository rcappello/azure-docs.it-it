---
title: Scaricare elementi di marketplace di Azure | Microsoft Docs
description: L'operatore cloud può scaricare elementi di marketplace di Azure per la distribuzione di Azure Stack.
services: azure-stack
documentationcenter: ''
author: sethmanheim
manager: femila
editor: ''
ms.assetid: ''
ms.service: azure-stack
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 10/09/2018
ms.author: sethm
ms.reviewer: ''
ms.openlocfilehash: cf6bc980f6fd821056a987d0c830863bd15ba779
ms.sourcegitcommit: 7824e973908fa2edd37d666026dd7c03dc0bafd0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/10/2018
ms.locfileid: "48902009"
---
# <a name="download-marketplace-items-from-azure-to-azure-stack"></a>Scaricare elementi di marketplace di Azure ad Azure Stack

*Si applica a: Azure Stack Development Kit e i sistemi integrati di Azure Stack*

Come operatore di cloud, scaricare gli elementi da Azure Marketplace e renderle disponibili in Azure Stack. Gli elementi che è possibile scegliere provengono da un elenco curato di elementi del Marketplace di Azure che vengono pre-testato e supportato per l'uso con Azure Stack. Elementi aggiuntivi vengono spesso aggiunte a questo elenco, quindi continuare a ricontrollare in seguito per il nuovo contenuto. 

Esistono due scenari per la connessione ad Azure Marketplace: 

- **Uno scenario connesso** -che richiede l'ambiente Azure Stack per essere connesso a internet. Usare il portale di Azure Stack per individuare e scaricare gli elementi. 
- **Uno scenario parzialmente connesso o disconnesso** -che richiede l'accesso a Internet utilizzando lo strumento di diffusione di marketplace per scaricare elementi di marketplace. Quindi, visualizzare i download disponibili è trasferire all'installazione di Azure Stack disconnesso. Questo scenario Usa PowerShell.

Visualizzare [elementi di Azure Marketplace per Azure Stack](azure-stack-marketplace-azure-items.md) per un elenco degli elementi di marketplace, è possibile scaricare.


## <a name="connected-scenario"></a>Scenario connesso
Se Azure Stack si connette a internet, è possibile utilizzare il portale di amministrazione per scaricare elementi di marketplace.

### <a name="prerequisites"></a>Prerequisiti
Distribuzione di Azure Stack deve disporre della connettività internet e deve essere [registrata con Azure](azure-stack-register.md).

### <a name="use-the-portal-to-download-marketplace-items"></a>Usare il portale per scaricare elementi di marketplace  
1. Accedere al portale di amministrazione di Azure Stack.

2.  Esaminare lo spazio di archiviazione disponibile prima del download di elementi del marketplace. In un secondo momento, quando si selezionano elementi per il download, è possibile confrontare le dimensioni del download per la capacità di archiviazione disponibile. Se la capacità è limitata, prendere in considerazione le opzioni per [la gestione dello spazio disponibile](azure-stack-manage-storage-shares.md#manage-available-space). 

    Per esaminare lo spazio disponibile, nel **gestione delle aree** selezionare l'area in cui si desidera esplorare e quindi passare alla **provider di risorse** > **archiviazione**.

    ![Esaminare lo spazio di archiviazione](media/azure-stack-download-azure-marketplace-item/storage.png)  

    
3. Aprire il Marketplace di Azure Stack e connettersi ad Azure. A tale scopo, selezionare **gestione Marketplace**, quindi selezionare **Add da Azure**.

    ![Aggiunta di Azure](media/azure-stack-download-azure-marketplace-item/marketplace.png)

    Il portale Visualizza l'elenco di elementi disponibili per il download da Azure Marketplace. È possibile fare clic su ogni elemento per visualizzare la descrizione e informazioni aggiuntive, tra cui le dimensioni di download. 

    ![Elenco di Marketplace](media/azure-stack-download-azure-marketplace-item/image03.png)

4. Selezionare l'elemento desiderato e quindi selezionare **scaricare**. Tempi di download variare.

    ![Messaggio di download](media/azure-stack-download-azure-marketplace-item/image04.png)

    Al termine del download, è possibile distribuire il nuovo elemento del marketplace come operatore di Azure Stack o un'utente.

5. Per distribuire l'elemento scaricato, selezionare **+ crea una risorsa**e quindi eseguire una ricerca tra le categorie per il nuovo elemento del marketplace. Selezionare quindi l'elemento per avviare il processo di distribuzione. Il processo varia per gli elementi del marketplace diversi. 

## <a name="disconnected-or-a-partially-connected-scenario"></a>Disconnesso o uno scenario di connesso parziale

Se Azure Stack in modalità senza connessione e senza connettività internet, è possibile utilizzare PowerShell e il *dello strumento di diffusione di marketplace* per scaricare gli elementi del marketplace in un computer con connettività internet. È quindi possibile trasferire gli elementi nell'ambiente Azure Stack. In un ambiente disconnesso, è possibile scaricare elementi del marketplace tramite il portale di Azure Stack. 

Lo strumento di diffusione marketplace è anche utilizzabile in uno scenario connesso. 

Lo scenario è composto da due parti:
- **Parte 1:** scaricare da Azure Marketplace. Nel computer con accesso a internet configurare PowerShell, scaricare lo strumento di diffusione e quindi scaricare form degli elementi di Azure Marketplace.  
- **Parte 2:** caricare e pubblicare nel Marketplace di Azure Stack. Spostare i file scaricati all'ambiente Azure Stack, importarli in Azure Stack e quindi pubblicarli in Azure Stack Marketplace.  


### <a name="prerequisites"></a>Prerequisiti
- Distribuzione di Azure Stack deve essere [registrata con Azure](azure-stack-register.md).  

- Nel computer che abbia la connettività internet deve essere **modulo di PowerShell di Azure Stack versione 1.2.11** o versione successiva. Se non è già presente, [installa i moduli di PowerShell specifici di Azure Stack](azure-stack-powershell-install.md).  

- Per abilitare l'importazione di un elemento del marketplace scaricato, il [ambiente di PowerShell per l'operatore di Azure Stack](azure-stack-powershell-configure-admin.md) deve essere configurato.  

- È necessario disporre di un [account di archiviazione](azure-stack-manage-storage-accounts.md) nello Stack di Azure che include un contenitore accessibile pubblicamente (ovvero un blob di archiviazione). Usare il contenitore come risorsa di archiviazione temporanea per i file di raccolta di elementi di marketplace. Se non ha familiarità con gli account di archiviazione e i contenitori, vedere [usare i BLOB - portale di Azure](https://docs.microsoft.com/azure/storage/blobs/storage-quickstart-blobs-portal) nella documentazione di Azure.

- Lo strumento di diffusione marketplace viene scaricato durante la prima procedura. 

### <a name="use-the-marketplace-syndication-tool-to-download-marketplace-items"></a>Usare lo strumento di diffusione di marketplace per scaricare elementi di marketplace

1. In un computer con connessione Internet, aprire una console PowerShell come amministratore.

2. Aggiungere l'account di Azure che è stata utilizzata per registrare Azure Stack. Per aggiungere l'account, in PowerShell eseguire `Add-AzureRmAccount` senza parametri. Viene chiesto di immettere le credenziali dell'account Azure e potrebbe essere necessario usare l'autenticazione a 2 fattori in base alla configurazione dell'account.

3. Se si hanno più sottoscrizioni, eseguire il comando seguente per selezionare il certificato che è stato usato per la registrazione:  

   ```PowerShell  
   Get-AzureRmSubscription -SubscriptionID '<Your Azure Subscription GUID>' | Select-AzureRmSubscription
   $AzureContext = Get-AzureRmContext
   ```

4. Scaricare la versione più recente dello strumento di diffusione di marketplace con lo script seguente:  

   ```PowerShell
   # Download the tools archive.
   [Net.ServicePointManager]::SecurityProtocol = [Net.SecurityProtocolType]::Tls12 
   invoke-webrequest https://github.com/Azure/AzureStack-Tools/archive/master.zip `
     -OutFile master.zip

   # Expand the downloaded files.
   expand-archive master.zip `
     -DestinationPath . `
     -Force

   # Change to the tools directory.
   cd .\AzureStack-Tools-master

   ```

5. Importare il modulo di diffusione, quindi avviare lo strumento eseguendo i comandi seguenti. Sostituire `Destination folder path` con un percorso per archiviare i file scaricati da Azure Marketplace.   

   ```PowerShell  
   Import-Module .\Syndication\AzureStack.MarketplaceSyndication.psm1

   Sync-AzSOfflineMarketplaceItem 
      -Destination "Destination folder path in quotes" `
      -AzureTenantID $AzureContext.Tenant.TenantId `
      -AzureSubscriptionId $AzureContext.Subscription.Id 
   ```

6. Quando viene eseguito lo strumento, viene chiesto di immettere le credenziali dell'account Azure. Accedere all'account di Azure che è stata utilizzata per registrare Azure Stack. Dopo che l'account di accesso ha esito positivo, si dovrebbe essere una schermata simile all'immagine seguente, con l'elenco degli elementi disponibili nel marketplace.  

   ![Controllo popup degli elementi di Azure Marketplace](media/azure-stack-download-azure-marketplace-item/image05.png)

7. Selezionare l'elemento che si desidera scaricare e annotare la *versione*. (È possibile tenere premuto il *Ctrl* chiave per selezionare più immagini.) Si farà riferimento al *versione* quando si importa l'elemento nella procedura successiva. 
   
   È anche possibile filtrare l'elenco delle immagini usando il **Aggiungi criteri** opzione.

8. Selezionare **OK**e quindi leggere e accettare le condizioni legali. 

9. Il tempo impiegato per il download dipende dalle dimensioni dell'elemento. Al termine del download, l'elemento è disponibile nella cartella specificata nello script. Il download include un file di disco rigido virtuale (per le macchine virtuali) o un oggetto. File ZIP (per estensioni di macchina virtuale). Include anche un pacchetto di raccolta nel *azpkg* formato. (Un *azpkg* pacchetto è un *zip* file.)
 

### <a name="import-the-download-and-publish-to-azure-stack-marketplace"></a>Importare il download e la pubblicazione in Marketplace Azure Stack
1. I file di immagini di macchine virtuali o modelli di soluzione che hai [scaricati in precedenza](#use-the-marketplace-syndication-tool-to-download-marketplace-items) devono essere rese disponibili in locale nell'ambiente Azure Stack.  

2. Usare il portale di amministrazione per caricare il pacchetto di elemento di marketplace (il file con estensione azpkg) e l'immagine di disco rigido virtuale (file con estensione vhd) in archiviazione Blob di Azure Stack. Caricamento del pacchetto e i file del disco li rende disponibili in Azure Stack in modo che è possibile pubblicare l'elemento in un secondo momento per il Marketplace di Azure Stack.

   Caricamento richiede di disporre di un account di archiviazione con un contenitore accessibile pubblicamente (vedere i prerequisiti per questo scenario).  
   1. Nel portale di amministrazione di Azure Stack, passare a **tutti i servizi** e quindi nel **dati e archiviazione** categoria, seleziona **account di archiviazione**.  
   
   2. Selezionare un account di archiviazione dalla sottoscrizione e quindi sotto **servizio BLOB**, selezionare **contenitori**.  
      ![Servizio BLOB](media/azure-stack-download-azure-marketplace-item/blob-service.png)  
   
   3. Selezionare il contenitore a cui si vuole usare e quindi selezionare **caricare** per aprire il **carica blob** riquadro.  
      ![Contenitore](media/azure-stack-download-azure-marketplace-item/container.png)  
   
   4. Nel riquadro blob Upload, individuare i file di pacchetto e il disco da caricare nell'archivio e quindi selezionare **caricare**.  
      ![upload](media/azure-stack-download-azure-marketplace-item/upload.png)  

   5. File caricati vengono visualizzati nel riquadro del contenitore. Selezionare un file e quindi copiare l'URL dal **proprietà Blob** riquadro. Si userà questo URL nel passaggio successivo quando si importa l'elemento del marketplace per Azure Stack.  Nell'immagine seguente, il contenitore è *test-blob-storage* e il file sia *Microsoft.WindowsServer2016DatacenterServerCore ARM.1.0.801.azpkg*.  Il file è di URL *https://testblobstorage1.blob.local.azurestack.external/blob-test-storage/Microsoft.WindowsServer2016DatacenterServerCore-ARM.1.0.801.azpkg*.  
      ![Proprietà BLOB](media/azure-stack-download-azure-marketplace-item/blob-storage.png)  

3. Importare l'immagine di disco rigido virtuale di Azure Stack usando il **Add-AzsPlatformimage** cmdlet. Quando si utilizza questo cmdlet, sostituire il *server di pubblicazione*, *offrono*e altri valori di parametro con i valori dell'immagine che si desidera importare. 

   È possibile ottenere il *server di pubblicazione*, *offrono*, e *sku* i valori dell'immagine dal file di testo che consente di scaricare il file con estensione AZPKG. Il file di testo viene archiviato nel percorso di destinazione. Il *versione* valore è la versione osservata durante il download dell'elemento da Azure nella procedura precedente. 
 
   Nello script di esempio seguente, vengono usati i valori per Windows Server 2016 Datacenter - macchina virtuale di base del Server. Il valore per *- Osuri* è un percorso di esempio per la posizione di archiviazione blob per l'elemento.

   ```PowerShell  
   Add-AzsPlatformimage `
    -publisher "MicrosoftWindowsServer" `
    -offer "WindowsServer" `
    -sku "2016-Datacenter-Server-Core" `
    -osType Windows `
    -Version "2016.127.20171215" `
    -OsUri "https://mystorageaccount.blob.local.azurestack.external/cont1/Microsoft.WindowsServer2016DatacenterServerCore-ARM.1.0.801.vhd"  
   ```
   **Informazioni sui modelli di soluzione:** alcuni modelli possono includere un piccolo 3 MB. File di disco rigido virtuale con il nome **fixed3.vhd**. Non è necessario importare il file di Azure Stack. Fixed3.vhd.  Questo file è incluso con alcuni modelli di soluzione per soddisfare i requisiti di pubblicazione per Azure Marketplace.

   Esaminare la descrizione di modelli e scaricare e importare requisiti aggiuntivi, ad esempio dischi rigidi virtuali che sono necessari per lavorare con il modello di soluzione.  
   
   **Informazioni sulle estensioni:** quando si lavora con le estensioni di immagine di macchina virtuale, usare i parametri seguenti:
   - *Autore*
   - *Tipo*
   - *Versione*  

   Non si usa *offrono* per le estensioni.   


4.  Usare PowerShell per pubblicare l'elemento del marketplace in Azure Stack usando il **Add-AzsGalleryItem** cmdlet. Ad esempio:   
    ```PowerShell  
    Add-AzsGalleryItem `
     -GalleryItemUri "https://mystorageaccount.blob.local.azurestack.external/cont1/Microsoft.WindowsServer2016DatacenterServerCore-ARM.1.0.801.azpkg" `
     –Verbose
    ```
5. Dopo aver pubblicato un elemento della raccolta, è ora disponibile per l'uso. Per verificare che l'elemento della raccolta viene pubblicato, passare a **tutti i servizi**, quindi nel **generali** categoria, seleziona **Marketplace**.  Se il download è un modello di soluzione, assicurarsi che si aggiunge un'immagine di disco rigido virtuale dipendenti per tale modello di soluzione.  
  ![Marketplace di visualizzazione](media/azure-stack-download-azure-marketplace-item/view-marketplace.png)  

> [!NOTE]
> Con la versione di PowerShell per Azure Stack 1.3.0 è ora possibile aggiungere estensioni della macchina virtuale.

Ad esempio: 

````PowerShell
Add-AzsVMExtension -Publisher "Microsoft" -Type "MicroExtension" -Version "0.1.0" -ComputeRole "IaaS" -SourceBlob "https://github.com/Microsoft/PowerShell-DSC-for-Linux/archive/v1.1.1-294.zip" -SupportMultipleExtensions -VmOsType "Linux"
````

## <a name="next-steps"></a>Passaggi successivi
[Creare e pubblicare un elemento del Marketplace](azure-stack-create-and-publish-marketplace-item.md)