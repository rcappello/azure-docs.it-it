---
title: Panoramica dell'account di archiviazione di Azure | Microsoft Docs
description: Informazioni sulle opzioni per la creazione e l'uso di un account di archiviazione di Azure.
services: storage
author: tamram
ms.service: storage
ms.topic: article
ms.date: 09/13/2018
ms.author: tamram
ms.component: common
ms.openlocfilehash: 0b2bf8cdb1af85e5ddbd3b18dd6dfa47bcb835b4
ms.sourcegitcommit: 7c4fd6fe267f79e760dc9aa8b432caa03d34615d
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 09/28/2018
ms.locfileid: "47432886"
---
# <a name="azure-storage-account-overview"></a>Panoramica dell'account di archiviazione di Azure

Un account di archiviazione di Azure contiene tutti gli oggetti dati di Archiviazione di Azure: BLOB, file, code, tabelle e dischi. I dati nell'account di archiviazione di Azure sono permanenti e a disponibilità elevata, sicuri, altamente scalabili e accessibili da qualsiasi posizione tramite HTTP o HTTPS. 

Per informazioni su come creare un account di archiviazione di Azure, vedere [Creare un account di archiviazione](storage-quickstart-create-account.md).

## <a name="types-of-storage-accounts"></a>Tipi di account di archiviazione

Archiviazione di Azure offre tre tipi di account di archiviazione. Ogni tipo supporta caratteristiche diverse e ha uno specifico modello di prezzi. È importante tenere in considerazione tali differenze prima di creare un account di archiviazione per determinare il tipo di account ottimale per le proprie applicazioni. I tipi di account di archiviazione sono i seguenti:

* Account per **utilizzo generico v2** (scelta consigliata per la maggior parte degli scenari)
* Account per **utilizzo generico v1**
* Account di **archiviazione BLOB**

Nella tabella seguente sono descritti i tipi di account di archiviazione e le relative funzionalità:

| Tipo di account di archiviazione | Servizi supportati                       | Livelli di prestazioni supportati | Livelli di accesso supportati               | Opzioni di replica                                                | Modello di distribuzione<sup>1</sup>  | Crittografia<sup>2</sup> |
|----------------------|------------------------------------------|-----------------------------|--------------------------------------|--------------------------------------------------------------------|-------------------|------------|
| Utilizzo generico v2   | BLOB, file, coda, tabella e disco       | Standard, Premium           | Accesso frequente, accesso sporadico, archivio<sup>3</sup> | LRS, ZRS<sup>4</sup>, GRS, RA-GRS | Gestione risorse | Crittografato  |
| Utilizzo generico v1   | BLOB, file, coda, tabella e disco       | Standard, Premium           | N/D                                  | LRS, GRS, RA-GRS                                                   | Resource Manager, classica  | Crittografato  |
| Archiviazione BLOB         | BLOB (solo BLOB in blocchi e BLOB di accodamento) | Standard                    | Accesso frequente, accesso sporadico, archivio<sup>3</sup>                            | LRS, GRS, RA-GRS                                                   | Gestione risorse  | Crittografato  |

<sup>1</sup>È consigliabile usare il modello di distribuzione Azure Resource Manager. Gli account di archiviazione che usano il modello di distribuzione classico possono comunque essere creati in alcune posizioni e gli account classici esistenti continuano a essere supportati. Per altre informazioni, vedere [Confronto tra distribuzione di Azure Resource Manager e classica: comprensione dei modelli di implementazione e dello stato delle risorse](../../azure-resource-manager/resource-manager-deployment-model.md).

<sup>2</sup>Tutti gli account di archiviazione sono crittografati tramite Crittografia del servizio di archiviazione per i dati inattivi. Per altre informazioni, vedere [Crittografia del servizio di archiviazione di Azure per dati inattivi](storage-service-encryption.md).

<sup>3</sup>Il livello archivio è disponibile solo a livello di singolo BLOB, non a livello di account di archiviazione. Possono essere archiviati solo i BLOB in blocchi e i BLOB di accodamento. Per altre informazioni, vedere [Archivio BLOB di Azure: livelli di archiviazione ad accesso frequente, ad accesso sporadico e archivio](../blobs/storage-blob-storage-tiers.md).

<sup>4</sup>L'archiviazione con ridondanza della zona (ZRS) è disponibile solo per gli account di archiviazione standard per utilizzo generico v2. Per altre informazioni sull'archiviazione con ridondanza della zona, vedere [Archiviazione con ridondanza della zona: applicazioni di Archiviazione Azure a disponibilità elevata](storage-redundancy-zrs.md). Per altre informazioni sulle altre opzioni di replica, vedere [Replica di Archiviazione di Azure](storage-redundancy.md).

### <a name="general-purpose-v2-accounts"></a>Account per utilizzo generico v2

Gli account di archiviazione per utilizzo generico v2 supportano le funzionalità di archiviazione di Azure più recenti e incorporano tutte le funzionalità degli account di archiviazione BLOB e per utilizzo generico v1. Gli account per utilizzo generico v2 offrono i prezzi per gigabyte più bassi per Archiviazione di Azure, oltre a prezzi per transazione competitivi a livello di settore. Gli account di archiviazione per utilizzo generico v2 supportano i servizi di archiviazione di Azure seguenti:

- BLOB (tutti i tipi)
- File
- Dischi
- Queues
- Tabelle

Per la maggior parte degli scenari è consigliabile usare un account di archiviazione per utilizzo generico v2. È possibile eseguire facilmente l'aggiornamento di un account di archiviazione per utilizzo generico v1 o un account di archiviazione BLOB a un account per utilizzo generico v2, senza tempi di inattività e senza la necessità di riscrivere le applicazioni o copiare i dati. Per altre informazioni sull'aggiornamento a un account per utilizzo generico v2, vedere [Eseguire l'aggiornamento a un account di archiviazione per utilizzo generico v2](storage-account-upgrade.md). 

Gli account di archiviazione per utilizzo generico v2 offrono più livelli di accesso per l'archiviazione dei dati in base ai modelli di utilizzo. Per altre informazioni, vedere [Livelli di accesso per i dati BLOB in blocchi](#access-tiers-for-block-blob-data).

### <a name="general-purpose-v1-accounts"></a>Account per utilizzo generico v1

Gli account per utilizzo generico v1 consentono di accedere a tutti i servizi di archiviazione di Azure, ma potrebbero non offrire le funzionalità più recenti o i prezzi più bassi per gigabyte. Gli account di archiviazione per utilizzo generico v1 supportano i servizi di archiviazione di Azure seguenti:

- BLOB (tutti i tipi)
- File
- Dischi
- Queues
- Tabelle

Mentre gli account per utilizzo generico v2 rappresentano la scelta consigliata nella maggior parte dei casi, gli account per utilizzo generico v1 sono particolarmente indicati per questi scenari: 

* Le applicazioni richiedono il modello di distribuzione classica di Azure. Gli account per utilizzo generico v2 e gli account di archiviazione BLOB supportano solo il modello di distribuzione Azure Resource Manager.

* Le applicazioni sono a elevato utilizzo di transazioni o comportano un uso significativo della larghezza di banda per la replica geografica, ma non richiedono una capacità di grandi dimensioni. In questo caso, un account per utilizzo generico v1 può essere la scelta più economica.

* Si usa una versione dell'[API REST dei servizi di archiviazione](https://msdn.microsoft.com/library/azure/dd894041.aspx) precedente alla 2014-02-14 o una libreria client con una versione precedente alla 4.x e non è possibile aggiornare l'applicazione.

### <a name="blob-storage-accounts"></a>Account di archiviazione BLOB

Gli account di archiviazione BLOB sono account specializzati per l'archiviazione di oggetti dati non strutturati come BLOB in blocchi. Gli account di archiviazione BLOB offrono lo stesso livello di durabilità, disponibilità, scalabilità e prestazioni disponibile con gli account di archiviazione per utilizzo generico v2. Gli account di archiviazione BLOB supportano l'archiviazione dei BLOB in blocchi e dei BLOB di accodamento, ma non dei BLOB di pagine.

Gli account di archiviazione BLOB offrono più livelli di accesso per l'archiviazione dei dati in base ai modelli di utilizzo. Per altre informazioni, vedere [Livelli di accesso per i dati BLOB in blocchi](#access-tiers-for-block-blob-data).

## <a name="naming-storage-accounts"></a>Denominazione degli account di archiviazione

Quando si assegna un nome all'account di archiviazione, tenere presenti queste regole:

- I nomi degli account di archiviazione devono avere una lunghezza compresa tra 3 e 24 caratteri e possono contenere solo numeri e lettere minuscole.
- Nome dell'account di archiviazione deve essere univoco all'interno di Azure. Due account di archiviazione non possono avere lo stesso nome.

## <a name="performance-tiers"></a>Livelli di prestazioni

Gli account di archiviazione per utilizzo generico possono essere configurati per uno dei livelli di prestazioni seguenti:

* Un livello di prestazioni standard per l'archiviazione di BLOB, file, tabelle, code e dischi delle macchine virtuali di Azure.
* Un livello di prestazioni Premium per l'archiviazione solo dei dischi delle macchine virtuali di Azure. Per una panoramica approfondita del servizio di archiviazione Premium, vedere [Archiviazione Premium: archiviazione ad alte prestazioni per carichi di lavoro delle macchine virtuali di Azure](../../virtual-machines/windows/premium-storage.md) .

## <a name="access-tiers-for-block-blob-data"></a>Livelli di accesso per i dati BLOB in blocchi

Archiviazione di Azure offre diverse opzioni per l'accesso ai dati BLOB in blocchi in base ai modelli di utilizzo. Ogni livello di accesso in Archiviazione di Azure è ottimizzato per un determinato modello di utilizzo dei dati. Selezionando il livello di accesso corretto per le proprie esigenze, è possibile archiviare i dati BLOB in blocchi nel modo economicamente più conveniente.

I livelli di accesso disponibili sono i seguenti:

* Il livello ad **accesso frequente**, che è ottimizzato per l'accesso frequente degli oggetti nell'account di archiviazione. L'accesso ai dati nel livello ad accesso frequente è il più conveniente, mentre i costi di archiviazione sono leggermente superiori. I nuovi account di archiviazione vengono creati nel livello ad accesso frequente per impostazione predefinita.
* Il livello ad **accesso sporadico**, che è ottimizzato per l'archiviazione di grandi quantità di dati a cui si accede poco frequentemente e che vengono archiviati per almeno 30 giorni. L'archiviazione dei dati nel livello ad accesso sporadico è più conveniente, ma l'accesso ai dati può risultare leggermente più costoso rispetto al livello ad accesso frequente.
* Il livello **archivio**, che è disponibile solo per singoli BLOB in blocchi. Il livello archivio è ottimizzato per i dati che possono tollerare alcune ore di latenza di recupero e rimarranno nel livello archivio per almeno 180 giorni. Il livello archivio è l'opzione più conveniente per l'archiviazione dei dati, ma l'accesso ai dati è più costoso rispetto ai livelli ad accesso frequente o ad accesso sporadico. 

> [!NOTE]
> Il [livello di accesso Premium](../blobs/storage-blob-storage-tiers.md#premium-access-tier) è disponibile in anteprima limitata come un account di archiviazione con ridondanza locale nelle aree Europa settentrionale, Stati Uniti orientali 2, Stati Uniti centrali e Stati Uniti occidentali. Per informazioni su come registrarsi per l'anteprima, vedere [Introducing Azure Premium Blob Storage](http://aka.ms/premiumblob) (Presentazione dell'archiviazione BLOB Premium di Azure).

Se il modello di utilizzo dei dati cambia, è possibile passare da uno di questi livelli di accesso all'altro in qualsiasi momento. 

> [!IMPORTANT]
> La modifica del livello di accesso per un account di archiviazione o un BLOB esistente può comportare costi aggiuntivi.

Per altre informazioni sui livelli di accesso, vedere [Archivio BLOB di Azure: livelli di archiviazione Premium (anteprima), ad accesso frequente, ad accesso sporadico e archivio](../blobs/storage-blob-storage-tiers.md).

## <a name="replication"></a>Replica

[!INCLUDE [storage-common-redundancy-options](../../../includes/storage-common-redundancy-options.md)]

Per altre informazioni sulla replica dell'archiviazione, vedere [Replica di Archiviazione di Azure](storage-redundancy.md).

## <a name="encryption"></a>Crittografia

Tutti i dati nell'account di archiviazione vengono crittografati sul lato del servizio. Per altre informazioni sulla crittografia, vedere [Crittografia del servizio di archiviazione di Azure per dati inattivi](storage-service-encryption.md).

## <a name="storage-account-endpoints"></a>Endpoint dell'account di archiviazione

Un account di archiviazione offre uno spazio dei nomi univoco in Azure per i dati. Tutti gli oggetti archiviati in Archiviazione di Azure hanno un indirizzo che include il nome univoco dell'account. La combinazione del nome dell'account e dell'endpoint di servizio di Archiviazione di Azure costituisce gli endpoint per l'account di archiviazione.

Ad esempio, se l'account di archiviazione per utilizzo generico si chiama *mystorageaccount*, gli endpoint predefiniti per tale account sono:

* Archiviazione BLOB: http://*mystorageaccount*.blob.core.windows.net
* Archiviazione tabelle: http://*mystorageaccount*.table.core.windows.net
* Archiviazione code: http://*mystorageaccount*.queue.core.windows.net
* File di Azure: http://*mystorageaccount*.file.core.windows.net

> [!NOTE]
> Un account di archiviazione BLOB espone solo l'endpoint di servizio BLOB.

L'URL per accedere a un oggetto in un account di archiviazione viene formato aggiungendo la posizione dell'oggetto nell'account di archiviazione all'endpoint. Ad esempio, il formato di un indirizzo è simile al seguente: http://*mystorageaccount*.blob.core.windows.net/*mycontainer*/*myblob*.

È anche possibile configurare l'account di archiviazione per l'uso di un dominio personalizzato per i BLOB. Per altre informazioni, vedere [Configurare un nome di dominio personalizzato per l'account di Archiviazione di Azure](../blobs/storage-custom-domain-name.md).  

## <a name="control-access-to-account-data"></a>Controllare l'accesso ai dati dell'account

Per impostazione predefinita, i dati nel proprio account sono accessibili solo all'utente, ovvero al proprietario dell'account. È possibile controllare chi può accedere ai dati e quali autorizzazioni assegnare.

Ogni richiesta effettuata all'account di archiviazione deve essere autorizzata. Al livello del servizio, la richiesta deve includere un'intestazione *Autorizzazione* valida, che include tutte le informazioni necessarie al servizio per la convalida della richiesta prima dell'esecuzione.

È possibile concedere l'accesso ai dati nell'account di archiviazione usando uno degli approcci seguenti:

- **Azure Active Directory:** usare le credenziali di Azure Active Directory (Azure AD) per autenticare un utente, gruppo o un'altra identità per l'accesso ai dati BLOB e della coda (anteprima). Se l'autenticazione di un'identità ha esito positivo, Azure AD restituisce un token da usare per l'autorizzazione della richiesta con l'archiviazione BLOB di Azure o con l'archiviazione code. Per altre informazioni, vedere [Autenticare l'accesso ad Archiviazione di Azure tramite Azure Active Directory (anteprima)](storage-auth-aad.md).
- **Autorizzazione con chiave condivisa:** usare la chiave di accesso dell'account di archiviazione per creare una stringa di connessione usata dall'applicazione in fase di esecuzione per accedere ad Archiviazione di Azure. I valori nella stringa di connessione vengono usati per creare l'intestazione *Autorizzazione* che viene passata ad Archiviazione di Azure. Per altre informazioni, vedere [Configurare le stringhe di connessione di Archiviazione di Azure](storage-configure-connection-string.md).
- **Firma di accesso condiviso:** usare una firma di accesso condiviso per delegare l'accesso alle risorse nell'account di archiviazione, se non si usa l'autenticazione di Azure AD. Una firma di accesso condiviso è un token che incapsula nell'URL tutte le informazioni necessarie per autorizzare una richiesta ad Archiviazione di Azure. È possibile specificare la risorsa di archiviazione, le autorizzazioni concesse e l'intervallo per cui sono valide le autorizzazioni come parte della firma di accesso condiviso. Per altre informazioni, vedere [Uso delle firme di accesso condiviso](storage-dotnet-shared-access-signature-part-1.md).

> [!NOTE]
> L'autenticazione degli utenti o delle applicazioni tramite le credenziali di Azure AD offre un livello superiore di sicurezza e facilità d'uso rispetto ad altri metodi di autorizzazione. Mentre con le applicazioni è possibile continuare a usare l'autorizzazione con chiave condivisa, l'uso di Azure AD consente di evitare la necessità di archiviare la chiave di accesso dell'account con il codice. È anche possibile continuare a usare le firme di accesso condiviso (SAS) per concedere accesso specifico alle risorse dell'account di archiviazione, ma Azure AD offre funzionalità simili senza la necessità di gestire i token SAS o di occuparsi della revoca di una SAS compromessa. 
>
> Microsoft consiglia di usare l'autenticazione di Azure AD per le applicazioni BLOB e di accodamento di Archiviazione di Azure, quando possibile.

## <a name="copying-data-into-a-storage-account"></a>Copia dei dati in un account di archiviazione

Microsoft fornisce utilità e librerie per l'importazione dei dati da dispositivi di archiviazione locali o provider di archiviazione cloud di terze parti. La soluzione da usare dipende dalla quantità di dati da trasferire. 

Quando effettua l'aggiornamento a un account per utilizzo generico v2 da un account per utilizzo generico v1 o un account di archiviazione BLOB, la migrazione dei dati viene eseguita automaticamente. Microsoft consiglia questo percorso per l'aggiornamento dell'account. Se tuttavia si decide di spostare i dati da un account per utilizzo generico v1 a un account di archiviazione BLOB, sarà necessario eseguire manualmente la migrazione dei dati, usando gli strumenti e le librerie descritti di seguito. 

### <a name="azcopy"></a>AzCopy

AzCopy è un'utilità da riga di comando Windows progettata per offrire prestazioni elevate di copia dei dati da e verso Archiviazione di Azure. È possibile usare AzCopy per copiare i dati in un account di archiviazione BLOB da un account di archiviazione per utilizzo generico esistente o per caricare i dati da dispositivi di archiviazione locali. Per altre informazioni, vedere [Trasferire dati con l'utilità da riga di comando AzCopy](../common/storage-use-azcopy.md?toc=%2fazure%2fstorage%2fblobs%2ftoc.json).

### <a name="data-movement-library"></a>Libreria di spostamento dei dati

La libreria di spostamento dei dati di Archiviazione di Azure per .NET si basa sul framework di spostamento dei dati principali alla base di AzCopy. La libreria è progettata per operazioni di trasferimento dei dati affidabili, semplici e a prestazioni elevate simili a quelle di AzCopy. È possibile usarla per sfruttare tutti i vantaggi delle funzionalità fornite da AzCopy nell'applicazione in modo nativo senza dover eseguire e monitorare istanze esterne di AzCopy. Per altre informazioni, vedere [Azure Storage Data Movement Library for .Net](https://github.com/Azure/azure-storage-net-data-movement) (Libreria per lo spostamento dei dati di Archiviazione di Azure per .NET)

### <a name="rest-api-or-client-library"></a>API REST o libreria client

È possibile creare un'applicazione personalizzata per eseguire la migrazione dei dati all'account di archiviazione BLOB usando una delle librerie client di Azure o l'API REST dei servizi di archiviazione di Azure. Archiviazione di Azure fornisce librerie client avanzate per più linguaggi e piattaforme, ad esempio .NET, Java, C++, Node.js, PHP, Ruby e Python. Le librerie client offrono funzionalità avanzate, ad esempio la logica di ripetizione dei tentativi, la registrazione e i caricamenti paralleli. È possibile sviluppare usando direttamente l'API REST, che può essere chiamata da qualsiasi linguaggio in grado di eseguire richieste HTTP/HTTPS.

Per altre informazioni sull'API REST di Archiviazione di Azure, vedere [Informazioni di riferimento sulle API REST dei servizi di archiviazione di Azure](https://docs.microsoft.com/rest/api/storageservices/). 

> [!IMPORTANT]
> I BLOB crittografati con la crittografia lato client archiviano i metadati correlati alla crittografia con il BLOB. Se si copia un BLOB crittografato con la crittografia lato client, verificare che l'operazione di copia mantenga i metadati del BLOB e soprattutto quelli correlati alla crittografia. Se si copia un BLOB senza i metadati di crittografia, il contenuto del BLOB non sarà più recuperabile. Per altre informazioni sui metadati correlati alla crittografia, vedere [Crittografia lato client e Insieme di credenziali chiave Azure per Archiviazione di Microsoft Azure](../common/storage-client-side-encryption.md?toc=%2fazure%2fstorage%2fblobs%2ftoc.json).

### <a name="azure-importexport-service"></a>Servizio Importazione/Esportazione di Azure

Se si dispone di una grande quantità di dati da importare nell'account di archiviazione, prendere in considerazione il servizio Importazione/Esportazione di Azure. Il servizio Importazione/Esportazione di Azure viene usato per importare in modo sicuro grandi quantità di dati nell'archivio BLOB di Azure e in File di Azure tramite la spedizione delle unità disco a un data center di Azure. 

È anche possibile usare il servizio Importazione/Esportazione per trasferire i dati dall'archivio BLOB di Azure a unità disco per la spedizione al sito locale. È possibile importare dati da uno o più dischi nell'Archivio Blob di Azure o in File di Azure. Per altre informazioni, vedere [Che cos'è il servizio Importazione/Esportazione di Azure?](https://docs.microsoft.com/azure/storage/common/storage-import-export-service).

## <a name="storage-account-billing"></a>Fatturazione dell'account di archiviazione

[!INCLUDE [storage-account-billing-include](../../../includes/storage-account-billing-include.md)]

## <a name="next-steps"></a>Passaggi successivi

* Per informazioni su come creare un account di archiviazione di Azure, vedere [Creare un account di archiviazione](storage-quickstart-create-account.md).
* Per gestire o eliminare un account di archiviazione esistente, vedere [Gestire gli account di archiviazione di Azure](storage-account-manage.md).
