---
title: Asset in Servizi multimediali di Azure | Microsoft Docs
description: Questo articolo descrive le caratteristiche degli asset e come vengono usati da Servizi multimediali di Azure.
services: media-services
documentationcenter: ''
author: Juliako
manager: cfowler
editor: ''
ms.service: media-services
ms.workload: ''
ms.topic: article
ms.date: 03/19/2018
ms.author: juliako
ms.openlocfilehash: 61555eb6cca6995215ce43051abbda9aa43539ec
ms.sourcegitcommit: d8ffb4a8cef3c6df8ab049a4540fc5e0fa7476ba
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 06/20/2018
ms.locfileid: "36284839"
---
# <a name="assets"></a>Asset

Un'entità **Asset** contiene file digitali, tra cui video, audio, immagini, raccolte di anteprime, tracce di testo e file di sottotitoli codificati, con i relativi metadati. Una volta caricati in un asset, i file digitali possono essere usati nei flussi di lavoro di codifica e trasmissione di Servizi multimediali.

Un asset viene mappato a un contenitore BLOB nell'[account di archiviazione di Azure](storage-account-concept.md) e i file contenuti nell'asset vengono archiviati come BLOB in blocchi in tale contenitore. È possibile interagire con i file di un'entità Asset nei contenitori tramite i client dell'SDK di archiviazione.

Servizi multimediali di Azure supporta i livelli BLOB quando l'account usa l'archiviazione Utilizzo generico v2 (GPv2). Con GPv2, è possibile spostare i file in un'archiviazione offline sicura o ad accesso sporadico. L'archiviazione offline sicura è adatta all'archiviazione di file di origine quando non sono più necessari (ad esempio, dopo la codifica).

In Servizi multimediali v3, l'input del processo può essere creato a partire da asset o da URL HTTP(S). Per creare un asset che può essere usato come input per il processo, vedere [Create a job input from a local file](job-input-from-local-file-how-to.md) (Creare un input del processo da un file locale).

Inoltre, consultare gli articoli sugli [account di archiviazione in Servizi multimediali](storage-account-concept.md) e su [trasformazioni e processi](transform-concept.md).

## <a name="asset-definition"></a>Definizione di asset

Nella tabella seguente vengono illustrate le proprietà di un asset e le relative definizioni.

|NOME|type|DESCRIZIONE|
|---|---|---|
|ID|stringa|ID di risorsa completo per la risorsa.|
|name|stringa|Nome della risorsa.|
|properties.alternateId |stringa|ID alternativo dell'asset.|
|properties.assetId |stringa|ID dell'asset.|
|properties.container |stringa|Nome del contenitore BLOB dell'asset.|
|properties.created |stringa|Data di creazione dell'asset.|
|properties.description |stringa|Descrizione dell'asset.|
|properties.lastModified |stringa|Data dell'ultima modifica dell'asset.|
|properties.storageAccountName |stringa|Nome dell'account di archiviazione.|
|properties.storageEncryptionFormat |AssetStorageEncryptionFormat |Formato di crittografia dell'asset. None oppure MediaStorageEncryption.|
|type|stringa|Tipo di risorsa.|

Per la definizione completa, vedere [Assets](https://docs.microsoft.com/rest/api/media/assets) (Asset).

## <a name="filtering-ordering-paging"></a>Filtro, ordinamento, paging

Servizi multimediali supporta le opzioni di query OData seguenti per gli asset: 

* $filter 
* $orderby 
* $top 
* $skiptoken 

### <a name="filteringordering"></a>Filtri/Ordinamento

La tabella seguente illustra come queste opzioni possono essere applicate alle proprietà di un asset: 

|NOME|Filtro|Ordine|
|---|---|---|
|ID|Supporta:<br/>Uguale a<br/>Maggiore di<br/>Minore di|Supporta:<br/>Crescente<br/>Decrescente|
|name|||
|properties.alternateId |Supporta:<br/>Uguale a||
|properties.assetId |Supporta:<br/>Uguale a||
|properties.container |||
|properties.created|Supporta:<br/>Uguale a<br/>Maggiore di<br/>Minore di|Supporta:<br/>Crescente<br/>Decrescente|
|properties.description |||
|properties.lastModified |||
|properties.storageAccountName |||
|properties.storageEncryptionFormat | ||
|type|||

L'esempio C# seguente applica il filtro alla data di creazione:

```csharp
var odataQuery = new ODataQuery<Asset>("properties/created lt 2018-05-11T17:39:08.387Z");
var firstPage = await MediaServicesArmClient.Assets.ListAsync(CustomerResourceGroup, CustomerAccountName, odataQuery);
```

### <a name="pagination"></a>Paginazione

La paginazione è supportata per ognuno dei quattro ordinamenti abilitati. 

Se la risposta di una query contiene molti elementi (attualmente più di 1000), il servizio restituisce una proprietà "\@odata.nextLink" per ottenere la pagina di risultati successiva. Questa proprietà può essere usata per scorrere l'intero set di risultati. Le dimensioni della pagina non sono configurabili dall'utente. 

Se gli asset vengono creati o eliminati durante il paging della raccolta, le modifiche vengono riflesse nei risultati restituiti (se tali modifiche si trovano nella parte della raccolta che non è stata scaricata). 

L'esempio C# seguente illustra come enumerare tutti gli asset nell'account.

```csharp
var firstPage = await MediaServicesArmClient.Assets.ListAsync(CustomerResourceGroup, CustomerAccountName);

var currentPage = firstPage;
while (currentPage.NextPageLink != null)
{
    currentPage = await MediaServicesArmClient.Assets.ListNextAsync(currentPage.NextPageLink);
}
```

Per esempi REST, vedere [Assets - List](https://docs.microsoft.com/rest/api/media/assets/list) (Asset - Elenco)


## <a name="storage-side-encryption"></a>Crittografia lato archiviazione

Per proteggere gli asset inattivi, è necessario crittografarli tramite crittografia lato archiviazione. La tabella seguente illustra il funzionamento della crittografia lato archiviazione in Servizi multimediali:

|Opzione di crittografia|DESCRIZIONE|Servizi multimediali v2|Servizi multimediali v3|
|---|---|---|---|
|Crittografia di archiviazione di Servizi multimediali|Crittografia AES-256, chiave gestita da Servizi multimediali|Supportata<sup>(1)</sup>|Non supportata<sup>(2)</sup>|
|[Crittografia del servizio di archiviazione per dati inattivi](https://docs.microsoft.com/azure/storage/common/storage-service-encryption)|Crittografia lato server offerta da Archiviazione di Azure, chiave gestita da Azure o dal cliente|Supportato|Supportato|
|[Crittografia lato client di archiviazione](https://docs.microsoft.com/azure/storage/common/storage-client-side-encryption)|Crittografia lato client offerta da Archiviazione di Azure, chiave gestita dal cliente in Key Vault|Non supportate|Non supportate|

<sup>1</sup> Servizi multimediali supporta la gestione di contenuto non crittografato/senza alcuna forma di crittografia, ma tale modalità non è consigliata.

<sup>2</sup> In Servizi multimediali versione 3, la crittografia di archiviazione (crittografia AES-256) è supportata per la compatibilità con le versioni precedenti solo se gli asset sono stati creati con Servizi multimediali versione 2. In altre parole, la versione 3 funziona con asset con crittografia di archiviazione esistenti, ma non consente la creazione di nuovi asset di questo tipo.

## <a name="next-steps"></a>Passaggi successivi

> [!div class="nextstepaction"]
> [Eseguire lo streaming di un file](stream-files-dotnet-quickstart.md)
