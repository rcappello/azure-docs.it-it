---
title: Copiare o spostare dati in Archiviazione di Microsoft Azure con AzCopy in Linux | Microsoft Docs
description: Usare l'utilità AzCopy in Linux per spostare o copiare dati da o verso BLOB e contenuto del file. Copiare i dati in archiviazione di Azure da file locali o copiare i dati all'interno o tra account di archiviazione. Migrare facilmente i dati in archiviazione di Azure.
services: storage
author: seguler
ms.service: storage
ms.topic: article
ms.date: 04/26/2018
ms.author: seguler
ms.component: common
ms.openlocfilehash: 1aff2ecdec83886d40d12b76e64a14a81451e89e
ms.sourcegitcommit: f20e43e436bfeafd333da75754cd32d405903b07
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 10/17/2018
ms.locfileid: "49386689"
---
# <a name="transfer-data-with-azcopy-on-linux"></a>Trasferire dati con AzCopy in Linux

AzCopy è un'utilità della riga di comando progettata per la copia dei dati in/dall'archiviazione di BLOB e file di Microsoft Azure usando semplici comandi progettati per garantire prestazioni ottimali. È possibile copiare dati tra un file system e un account di archiviazione o tra più account di archiviazione.  

Esistono due versioni di AzCopy che è possibile scaricare. AzCopy su Linux offre opzioni della riga di comando in stile POSIX per le piattaforme Linux. [AzCopy in Windows](../storage-use-azcopy.md) offre opzioni della riga di comando in stile Windows. Questo articolo descrive AzCopy in Linux. 

> [!NOTE]  
> A partire dalla versione 7.2 di AzCopy, le dipendenze di .NET Core vengono incluse nel pacchetto di AzCopy. Se si usa la versione 7.2 o successiva, non è più necessario installare .NET Core come prerequisito.

## <a name="download-and-install-azcopy"></a>Scaricare e installare AzCopy

### <a name="installation-on-linux"></a>Installazione in Linux

> [!NOTE]
> Potrebbe essere necessario installare le dipendenze di .NET Core 2.1 evidenziate in questo [articolo sui prerequisiti per .NET Core](https://docs.microsoft.com/dotnet/core/linux-prerequisites?tabs=netcore2x) a seconda della distribuzione. 
>
> Per le distribuzioni RHEL 7 installare le dipendenze ICU e libunwind: ```yum install -y libunwind icu```

Per installare AzCopy in Linux (versione 7.2 o successive) è sufficiente estrarre un pacchetto tar ed eseguire lo script di installazione. 

**Distribuzioni basate su RHEL 6**: [collegamento per il download](https://aka.ms/downloadazcopylinuxrhel6)
```bash
wget -O azcopy.tar.gz https://aka.ms/downloadazcopylinuxrhel6
tar -xf azcopy.tar.gz
sudo ./install.sh
```

**Tutte le altre distribuzioni Linux**: [collegamento per il download](https://aka.ms/downloadazcopylinux64)
```bash
wget -O azcopy.tar.gz https://aka.ms/downloadazcopylinux64
tar -xf azcopy.tar.gz
sudo ./install.sh
```

Dopo aver installato AzCopy in Linux, è possibile rimuovere i file estratti. In alternativa, se non si hanno privilegi di superuser, è anche possibile eseguire `azcopy` usando lo script della shell azcopy nella cartella estratta.

### <a name="alternative-installation-on-ubuntu"></a>Installazione alternativa in Ubuntu

**Ubuntu 14.04**

Aggiungere un'origine apt per il repository di prodotti Linux di Microsoft e installare AzCopy:

```bash
sudo echo "deb [arch=amd64] https://packages.microsoft.com/repos/microsoft-ubuntu-trusty-prod/ trusty main" > azure.list
sudo cp ./azure.list /etc/apt/sources.list.d/
sudo apt-key adv --keyserver packages.microsoft.com --recv-keys EB3E94ADBE1229CF
```

```bash
sudo apt-get update
sudo apt-get install azcopy
```

**Ubuntu 16.04**

Aggiungere un'origine apt per il repository di prodotti Linux di Microsoft e installare AzCopy:

```bash
echo "deb [arch=amd64] https://packages.microsoft.com/repos/microsoft-ubuntu-xenial-prod/ xenial main" > azure.list
sudo cp ./azure.list /etc/apt/sources.list.d/
sudo apt-key adv --keyserver packages.microsoft.com --recv-keys EB3E94ADBE1229CF
```

```bash
sudo apt-get update
sudo apt-get install azcopy
```

## <a name="writing-your-first-azcopy-command"></a>Scrittura del primo comando AzCopy 
La sintassi di base per i comandi di AzCopy è la seguente:

```azcopy
azcopy --source <source> --destination <destination> [Options]
```

Gli esempi seguenti illustrano vari scenari per la copia dei dati da e in BLOB e file di Microsoft Azure. Per una spiegazione dettagliata dei parametri usati in ogni esempio, fare riferimento al menu `azcopy --help`.

## <a name="blob-download"></a>BLOB: scaricare
### <a name="download-single-blob"></a>Scaricare un singolo BLOB

```azcopy
azcopy \
    --source https://myaccount.blob.core.windows.net/mycontainer/abc.txt \
    --destination /mnt/myfiles/abc.txt \
    --source-key <key> 
```

Se la cartella `/mnt/myfiles` non esiste ancora, AzCopy la crea e scarica `abc.txt ` nella nuova cartella. 

### <a name="download-single-blob-from-secondary-region"></a>Scaricare un singolo BLOB da un'area secondaria

```azcopy
azcopy \
    --source https://myaccount-secondary.blob.core.windows.net/mynewcontainer/abc.txt \
    --destination /mnt/myfiles/abc.txt \
    --source-key <key>
```

È necessario che sia abilitata l'archiviazione con ridondanza geografica con accesso in lettura.

### <a name="download-all-blobs"></a>Scaricare tutti BLOB

```azcopy
azcopy \
    --source https://myaccount.blob.core.windows.net/mycontainer \
    --destination /mnt/myfiles \
    --source-key <key> \
    --recursive
```

Si supponga che i BLOB seguenti risiedano nel contenitore specificato:  

```
abc.txt
abc1.txt
abc2.txt
vd1/a.txt
vd1/abcd.txt
```

Dopo l'operazione di download, la directory `/mnt/myfiles` include i file seguenti:

```
/mnt/myfiles/abc.txt
/mnt/myfiles/abc1.txt
/mnt/myfiles/abc2.txt
/mnt/myfiles/vd1/a.txt
/mnt/myfiles/vd1/abcd.txt
```

Se non si specifica l'opzione `--recursive`, non verrà scaricato alcun BLOB.

### <a name="download-blobs-with-specified-prefix"></a>Scaricare i BLOB con il prefisso specificato

```azcopy
azcopy \
    --source https://myaccount.blob.core.windows.net/mycontainer \
    --destination /mnt/myfiles \
    --source-key <key> \
    --include "a" \
    --recursive
```

Si supponga che i BLOB seguenti risiedano nel contenitore specificato. Vengono scaricati tutti i BLOB che iniziano con il prefisso `a`.

```
abc.txt
abc1.txt
abc2.txt
xyz.txt
vd1\a.txt
vd1\abcd.txt
```

Dopo l'operazione di download, la cartella `/mnt/myfiles` include i file seguenti:

```
/mnt/myfiles/abc.txt
/mnt/myfiles/abc1.txt
/mnt/myfiles/abc2.txt
```

Il prefisso si applica alla directory virtuale che forma la prima parte del nome del BLOB. Nell'esempio precedente, la directory virtuale non corrisponde al prefisso specificato, quindi non viene scaricato alcun BLOB. Se inoltre l'opzione `--recursive` non è specificata, AzCopy non scarica alcun BLOB.

### <a name="set-the-last-modified-time-of-exported-files-to-be-same-as-the-source-blobs"></a>Impostare l'ora dell'ultima modifica dei file esportati sulla stessa ora dei BLOB di origine

```azcopy
azcopy \
    --source https://myaccount.blob.core.windows.net/mycontainer \
    --destination "/mnt/myfiles" \
    --source-key <key> \
    --preserve-last-modified-time
```

È anche possibile escludere BLOB dall'operazione di download in base all'ora dell'ultima modifica. Se ad esempio si vogliono escludere i BLOB in cui l'ora dell'ultima modifica è uguale o successiva a quella del file di destinazione, aggiungere l'opzione `--exclude-newer` .

```azcopy
azcopy \
    --source https://myaccount.blob.core.windows.net/mycontainer \
    --destination /mnt/myfiles \
    --source-key <key> \
    --preserve-last-modified-time \
    --exclude-newer
```

In alternativa, se si vogliono escludere i BLOB in cui l'ora dell'ultima modifica è uguale o precedente a quella del file di destinazione, aggiungere l'opzione `--exclude-older` .

```azcopy
azcopy \
    --source https://myaccount.blob.core.windows.net/mycontainer \
    --destination /mnt/myfiles \
    --source-key <key> \
    --preserve-last-modified-time \
    --exclude-older
```

## <a name="blob-upload"></a>BLOB: caricare
### <a name="upload-single-file"></a>Caricare un singolo file

```azcopy
azcopy \
    --source /mnt/myfiles/abc.txt \
    --destination https://myaccount.blob.core.windows.net/mycontainer/abc.txt \
    --dest-key <key>
```

Se il contenitore di destinazione specificato non esiste, AzCopy ne crea uno e vi carica il file.

### <a name="upload-single-file-to-virtual-directory"></a>Caricare un singolo file nella directory virtuale

```azcopy
azcopy \
    --source /mnt/myfiles/abc.txt \
    --destination https://myaccount.blob.core.windows.net/mycontainer/vd/abc.txt \
    --dest-key <key>
```

Se la directory virtuale specificata non esiste, AzCopy carica il file in modo da includere la directory virtuale nel nome del BLOB, *ovvero* `vd/abc.txt` nell'esempio precedente.

### <a name="redirect-from-stdin"></a>Reindirizzare da stdin

```azcopy
gzip myarchive.tar -c | azcopy \
    --destination https://myaccount.blob.core.windows.net/mycontainer/mydir/myarchive.tar.gz \
    --dest-key <key>
```

### <a name="upload-all-files"></a>Caricare tutti i file

```azcopy
azcopy \
    --source /mnt/myfiles \
    --destination https://myaccount.blob.core.windows.net/mycontainer \
    --dest-key <key> \
    --recursive
```

Se si specifica l'opzione `--recursive`, il contenuto della directory specificata viene caricato nell'archiviazione BLOB in modo ricorsivo, ovvero vengono caricati anche tutte le sottocartelle e i relativi file. Si supponga ad esempio che i file seguenti risiedano nella cartella `/mnt/myfiles`:

```
/mnt/myfiles/abc.txt
/mnt/myfiles/abc1.txt
/mnt/myfiles/abc2.txt
/mnt/myfiles/subfolder/a.txt
/mnt/myfiles/subfolder/abcd.txt
```

Dopo l'operazione di caricamento, il contenitore include i file seguenti:

```
abc.txt
abc1.txt
abc2.txt
subfolder/a.txt
subfolder/abcd.txt
```

Quando l'opzione `--recursive` non viene specificata, vengono caricati solo i tre file seguenti:

```
abc.txt
abc1.txt
abc2.txt
```

### <a name="upload-files-matching-specified-pattern"></a>Caricare i file corrispondenti ai criteri specificati

```azcopy
azcopy \
    --source /mnt/myfiles \
    --destination https://myaccount.blob.core.windows.net/mycontainer \
    --dest-key <key> \
    --include "a*" \
    --recursive
```

Si supponga che i file seguenti risiedano nella cartella `/mnt/myfiles`:

```
/mnt/myfiles/abc.txt
/mnt/myfiles/abc1.txt
/mnt/myfiles/abc2.txt
/mnt/myfiles/xyz.txt
/mnt/myfiles/subfolder/a.txt
/mnt/myfiles/subfolder/abcd.txt
```

Dopo l'operazione di caricamento, il contenitore include i file seguenti:

```
abc.txt
abc1.txt
abc2.txt
subfolder/a.txt
subfolder/abcd.txt
```

Quando l'opzione `--recursive` non viene specificata, AzCopy ignora file presenti nelle sottodirectory:

```
abc.txt
abc1.txt
abc2.txt
```

### <a name="specify-the-mime-content-type-of-a-destination-blob"></a>Specificare il tipo di contenuto MIME di un BLOB di destinazione
Per impostazione predefinita, AzCopy imposta il tipo di contenuto di un BLOB di destinazione su `application/octet-stream`. È tuttavia possibile specificare il tipo di contenuto in modo esplicito tramite l'opzione `--set-content-type [content-type]`. Questa sintassi imposta il tipo di contenuto per tutti i BLOB in un'operazione di caricamento.

```azcopy
azcopy \
    --source /mnt/myfiles \
    --destination https://myaccount.blob.core.windows.net/myContainer/ \
    --dest-key <key> \
    --include "ab" \
    --set-content-type "video/mp4"
```

Se si specifica l'opzione `--set-content-type` senza fornire un valore, AzCopy imposta il tipo di contenuto di ogni BLOB o file in base all'estensione di ciascuno di questi elementi.

```azcopy
azcopy \
    --source /mnt/myfiles \
    --destination https://myaccount.blob.core.windows.net/myContainer/ \
    --dest-key <key> \
    --include "ab" \
    --set-content-type
```

### <a name="customizing-the-mime-content-type-mapping"></a>Personalizzazione del mapping del tipo di contenuto MIME
AzCopy usa un file di configurazione che contiene mapping di estensioni al tipo di contenuto corrispondente. È possibile personalizzare questo mapping e aggiungere nuove coppie in base alle proprie esigenze. Il mapping si trova in ```/usr/lib/azcopy/AzCopyConfig.json```

## <a name="blob-copy"></a>BLOB: copiare
### <a name="copy-single-blob-within-storage-account"></a>Copiare un BLOB all'interno di un account di archiviazione

```azcopy
azcopy \
    --source https://myaccount.blob.core.windows.net/mycontainer1/abc.txt \
    --destination https://myaccount.blob.core.windows.net/mycontainer2/abc.txt \
    --source-key <key> \
    --dest-key <key>
```

Quando si copia un BLOB senza l'opzione --sync-copy, viene eseguita un'operazione di [copia sul lato server](http://blogs.msdn.com/b/windowsazurestorage/archive/2012/06/12/introducing-asynchronous-cross-account-copy-blob.aspx).

### <a name="copy-single-blob-across-storage-accounts"></a>Copiare un singolo BLOB tra account di archiviazione

```azcopy
azcopy \
    --source https://sourceaccount.blob.core.windows.net/mycontainer1/abc.txt \
    --destination https://destaccount.blob.core.windows.net/mycontainer2/abc.txt \
    --source-key <key1> \
    --dest-key <key2>
```

Quando si copia un BLOB senza l'opzione --sync-copy, viene eseguita un'operazione di [copia sul lato server](http://blogs.msdn.com/b/windowsazurestorage/archive/2012/06/12/introducing-asynchronous-cross-account-copy-blob.aspx).

### <a name="copy-single-blob-from-secondary-region-to-primary-region"></a>Copiare in BLOB singolo da un'area secondaria all'area primaria

```azcopy
azcopy \
    --source https://myaccount1-secondary.blob.core.windows.net/mynewcontainer1/abc.txt \
    --destination https://myaccount2.blob.core.windows.net/mynewcontainer2/abc.txt \
    --source-key <key1> \
    --dest-key <key2>
```

È necessario che sia abilitata l'archiviazione con ridondanza geografica con accesso in lettura.

### <a name="copy-single-blob-and-its-snapshots-across-storage-accounts"></a>Copiare un singolo BLOB e i relativi snapshot tra account di archiviazione

```azcopy
azcopy \
    --source https://sourceaccount.blob.core.windows.net/mycontainer1/ \
    --destination https://destaccount.blob.core.windows.net/mycontainer2/ \
    --source-key <key1> \
    --dest-key <key2> \
    --include "abc.txt" \
    --include-snapshot
```

Dopo l'operazione di copia, il contenitore di destinazione include il BLOB e i relativi snapshot. Il contenitore include i BLOB seguenti e i relativi snapshot:

```
abc.txt
abc (2013-02-25 080757).txt
abc (2014-02-21 150331).txt
```

### <a name="synchronously-copy-blobs-across-storage-accounts"></a>Copiare in modo sincrono i BLOB tra account di archiviazione
Per impostazione predefinita, AzCopy copia i dati tra due endpoint di archiviazione in modo asincrono. L'operazione di copia viene pertanto eseguita in background sfruttando la capacità di larghezza di banda disponibile non limitata da alcun contratto di servizio relativo alla velocità di copia di un BLOB. 

L'opzione `--sync-copy` garantisce che l'operazione di copia avvenga a velocità costante. AzCopy esegue la copia sincrona scaricando i BLOB da copiare dall'origine specificata nella memoria locale, per poi caricarli nella destinazione dell'archiviazione BLOB.

```azcopy
azcopy \
    --source https://myaccount1.blob.core.windows.net/myContainer/ \
    --destination https://myaccount2.blob.core.windows.net/myContainer/ \
    --source-key <key1> \
    --dest-key <key2> \
    --include "ab" \
    --sync-copy
```

`--sync-copy`, tuttavia, può generare costi aggiuntivi in uscita rispetto alla copia asincrona. Per evitare costi in uscita, si consiglia quindi di usare questa opzione in una macchina virtuale di Azure che si trova nella stessa area dell'account di archiviazione di origine.

## <a name="file-download"></a>File: scaricare
### <a name="download-single-file"></a>Scaricare un singolo file

```azcopy
azcopy \
    --source https://myaccount.file.core.windows.net/myfileshare/myfolder1/abc.txt \
    --destination /mnt/myfiles/abc.txt \
    --source-key <key>
```

Se l'origine specificata è una condivisione file di Azure, è necessario specificare il nome file esatto, *ad esempio* `abc.txt`, per copiare un solo file oppure specificare l'opzione `--recursive` per copiare tutti i file nella condivisione in modo ricorsivo. Se si specificano sia il criterio del file che l'opzione `--recursive` contemporaneamente, verrà generato un errore.

### <a name="download-all-files"></a>Scaricare tutti i file

```azcopy
azcopy \
    --source https://myaccount.file.core.windows.net/myfileshare/ \
    --destination /mnt/myfiles \
    --source-key <key> \
    --recursive
```

Le cartelle vuote non vengono scaricate.

## <a name="file-upload"></a>File: caricare
### <a name="upload-single-file"></a>Caricare un singolo file

```azcopy
azcopy \
    --source /mnt/myfiles/abc.txt \
    --destination https://myaccount.file.core.windows.net/myfileshare/abc.txt \
    --dest-key <key>
```

### <a name="upload-all-files"></a>Caricare tutti i file

```azcopy
azcopy \
    --source /mnt/myfiles \
    --destination https://myaccount.file.core.windows.net/myfileshare/ \
    --dest-key <key> \
    --recursive
```

Le cartelle vuote non vengono caricate.

### <a name="upload-files-matching-specified-pattern"></a>Caricare i file corrispondenti ai criteri specificati

```azcopy
azcopy \
    --source /mnt/myfiles \
    --destination https://myaccount.file.core.windows.net/myfileshare/ \
    --dest-key <key> \
    --include "ab*" \
    --recursive
```

## <a name="file-copy"></a>File: copia
### <a name="copy-across-file-shares"></a>Copiare tra condivisioni file

```azcopy
azcopy \
    --source https://myaccount1.file.core.windows.net/myfileshare1/ \
    --destination https://myaccount2.file.core.windows.net/myfileshare2/ \
    --source-key <key1> \
    --dest-key <key2> \
    --recursive
```
Quando si copia un file tra condivisioni file, viene eseguita un'operazione di [copia sul lato server](http://blogs.msdn.com/b/windowsazurestorage/archive/2012/06/12/introducing-asynchronous-cross-account-copy-blob.aspx).

### <a name="copy-from-file-share-to-blob"></a>Copiare dalla condivisione file al BLOB

```azcopy
azcopy \ 
    --source https://myaccount1.file.core.windows.net/myfileshare/ \
    --destination https://myaccount2.blob.core.windows.net/mycontainer/ \
    --source-key <key1> \
    --dest-key <key2> \
    --recursive
```
Quando si copia un file dalla condivisione file al BLOB, viene eseguita un'operazione di [copia sul lato server](http://blogs.msdn.com/b/windowsazurestorage/archive/2012/06/12/introducing-asynchronous-cross-account-copy-blob.aspx).

### <a name="copy-from-blob-to-file-share"></a>Copy dal BLOB alla condivisione file

```azcopy
azcopy \
    --source https://myaccount1.blob.core.windows.net/mycontainer/ \
    --destination https://myaccount2.file.core.windows.net/myfileshare/ \
    --source-key <key1> \
    --dest-key <key2> \
    --recursive
```
Quando si copia un file dal BLOB alla condivisione file, viene eseguita un'operazione di [copia sul lato server](http://blogs.msdn.com/b/windowsazurestorage/archive/2012/06/12/introducing-asynchronous-cross-account-copy-blob.aspx).

### <a name="synchronously-copy-files"></a>Copiare file in modo sincrono
È possibile specificare l'opzione `--sync-copy` per copiare i dati da archiviazione file ad archiviazione file, da archiviazione file ad archiviazione BLOB e da archiviazione BLOB ad archiviazione file in modo sincrono. AzCopy esegue questa operazione scaricando i dati di origine nella memoria locale e caricandoli di nuovo nella destinazione. In questo caso, vengono applicati i costi in uscita standard.

```azcopy
azcopy \
    --source https://myaccount1.file.core.windows.net/myfileshare1/ \
    --destination https://myaccount2.file.core.windows.net/myfileshare2/ \
    --source-key <key1> \
    --dest-key <key2> \
    --recursive \
    --sync-copy
```

Durante la copia da Archiviazione file ad Archiviazione BLOB, il tipo di BLOB predefinito è il BLOB in blocchi. Per modificare il tipo di BLOB di destinazione, è possibile specificare l'opzione `--blob-type page`. I tipi disponibili sono `page | block | append`.

`--sync-copy` può generare costi aggiuntivi in uscita rispetto alla copia asincrona. Per evitare costi in uscita, si consiglia quindi di usare questa opzione in una macchina virtuale di Azure che si trova nella stessa area dell'account di archiviazione di origine.

## <a name="other-azcopy-features"></a>Altre funzionalità di AzCopy
### <a name="only-copy-data-that-doesnt-exist-in-the-destination"></a>Copiare solo i dati che non esistono nella destinazione
I parametri `--exclude-older` e `--exclude-newer` consentono di escludere dalla copia, rispettivamente, le risorse di origine precedenti o più recenti. Per copiare solo e risorse di origine che non esistono nella destinazione, è possibile specificare entrambi i parametri nel comando AzCopy:

    --source http://myaccount.blob.core.windows.net/mycontainer --destination /mnt/myfiles --source-key <sourcekey> --recursive --exclude-older --exclude-newer

    --source /mnt/myfiles --destination http://myaccount.file.core.windows.net/myfileshare --dest-key <destkey> --recursive --exclude-older --exclude-newer

    --source http://myaccount.blob.core.windows.net/mycontainer --destination http://myaccount.blob.core.windows.net/mycontainer1 --source-key <sourcekey> --dest-key <destkey> --recursive --exclude-older --exclude-newer

### <a name="use-a-configuration-file-to-specify-command-line-parameters"></a>Usare un file di configurazione per specificare i parametri della riga di comando

```azcopy
azcopy --config-file "azcopy-config.ini"
```

È possibile includere i parametri della riga di comando di AzCopy in un file di configurazione. AzCopy elabora i parametri nel file come se fossero stati specificati nella riga di comando, eseguendo una sostituzione diretta con i contenuti del file.

Si supponga che sia presente un file di configurazione denominato `copyoperation`, che contiene le righe seguenti. Ogni parametro di AzCopy può essere specificato su una singola riga

    --source http://myaccount.blob.core.windows.net/mycontainer --destination /mnt/myfiles --source-key <sourcekey> --recursive --quiet

o su righe separate:

    --source http://myaccount.blob.core.windows.net/mycontainer
    --destination /mnt/myfiles
    --source-key<sourcekey>
    --recursive
    --quiet

Se il parametro viene suddiviso su due righe, l'operazione di AzCopy ha esito negativo, come mostrato di seguito per il parametro `--source-key`:

    http://myaccount.blob.core.windows.net/mycontainer
    /mnt/myfiles
    --sourcekey
    <sourcekey>
    --recursive
    --quiet

### <a name="specify-a-shared-access-signature-sas"></a>Specificare una firma di accesso condiviso

```azcopy
azcopy \
    --source https://myaccount.blob.core.windows.net/mycontainer1/abc.txt \
    --destination https://myaccount.blob.core.windows.net/mycontainer2/abc.txt \
    --source-sas <SAS1> \
    --dest-sas <SAS2>
```

È anche possibile specificare una firma di accesso condiviso per il contenitore URI:

```azcopy
azcopy \
    --source https://myaccount.blob.core.windows.net/mycontainer1/?SourceSASToken \
    --destination /mnt/myfiles \
    --recursive
```

### <a name="journal-file-folder"></a>Cartella del file journal
Ogni volta che si invia un comando ad AzCopy, l'utilità verifica se il file journal è presente nella cartella predefinita o in una cartella specificata dall'utente tramite questa opzione. Se il file journal non viene trovato in tali percorsi, AzCopy considera l'operazione come nuova e quindi crea un nuovo file journal.

Se il file journal esiste, AzCopy verifica se la riga di comando di input corrisponde alla riga di comando nel file journal. Se le righe di comando corrispondono, AzCopy avvia la ripresa dell'operazione incompleta. Se non corrispondono, viene richiesto se si vuole sovrascrivere il file journal per avviare una nuova operazione o annullare l'operazione corrente.

Se si vuole usare il percorso predefinito per il file journal:

```azcopy
azcopy \
    --source /mnt/myfiles \
    --destination https://myaccount.blob.core.windows.net/mycontainer \
    --dest-key <key> \
    --resume
```

Se si omette l'opzione`--resume` o si specifica l'opzione `--resume` senza il percorso della cartella, come illustrato sopra, AzCopy creerà il file journal nel percorso predefinito, ovvero `~\Microsoft\Azure\AzCopy`. Se il file journal esiste già, AzCopy riprenderà l'operazione in base al file journal.

Se si vuole specificare un percorso personalizzato per il file journal:

```azcopy
azcopy \
    --source /mnt/myfiles \
    --destination https://myaccount.blob.core.windows.net/mycontainer \
    --dest-key key \
    --resume "/mnt/myjournal"
```

In questo esempio viene creato il file journal, nel caso in cui non esista già: Se esiste, AzCopy riprenderà l'operazione in base al file journal.

Se si vuole riprendere un'operazione di AzCopy, ripetere lo stesso comando. AzCopy in Linux richiederà la conferma:

```azcopy
Incomplete operation with same command line detected at the journal directory "/home/myaccount/Microsoft/Azure/AzCopy", do you want to resume the operation? Choose Yes to resume, choose No to overwrite the journal to start a new operation. (Yes/No)
```

### <a name="output-verbose-logs"></a>Output di log dettagliati

```azcopy
azcopy \
    --source /mnt/myfiles \
    --destination https://myaccount.blob.core.windows.net/mycontainer \
    --dest-key <key> \
    --verbose
```

### <a name="specify-the-number-of-concurrent-operations-to-start"></a>Specificare il numero di operazioni simultanee da avviare
L'opzione `--parallel-level` specifica il numero di operazioni di copia simultanee. Per impostazione predefinita, AzCopy avvia un determinato numero di operazioni simultanee per aumentare la velocità effettiva di trasferimento dei dati. Il numero di operazioni simultanee è uguale a 8 volte il numero di processori disponibili. Se AzCopy è in esecuzione in una rete con larghezza di banda ridotta, è possibile specificare un numero inferiore per --parallel-level in modo da evitare errori generati dalla competizione tra le risorse.

>[!TIP]
>Per visualizzare l'elenco completo dei parametri di AzCopy, vedere il menu 'azcopy - help'.

## <a name="installation-steps-for-azcopy-71-and-earlier-versions"></a>Passaggi di installazione per AzCopy 7.1 e versioni precedenti

AzCopy in Linux (versione 7.1 e precedenti) richiede il framework .NET Core. Le istruzioni di installazione sono disponibili nella pagina di [installazione di .NET Core](https://www.microsoft.com/net/core#linuxubuntu).

Ad esempio, iniziare installando .NET Core su Ubuntu 16.10. Per le istruzioni di installazione più recenti, vedere la pagina di installazione di [.NET Core in Linux](https://www.microsoft.com/net/core#linuxubuntu).


```bash
sudo sh -c 'echo "deb [arch=amd64] https://apt-mo.trafficmanager.net/repos/dotnet-release/ yakkety main" > /etc/apt/sources.list.d/dotnetdev.list' 
sudo apt-key adv --keyserver hkp://keyserver.ubuntu.com:80 --recv-keys 417A0893
sudo apt-get update
sudo apt-get install dotnet-sdk-2.0.0
```

Dopo aver installato .NET Core, scaricare e installare AzCopy.

```bash
wget -O azcopy.tar.gz https://aka.ms/downloadazcopyprlinux
tar -xf azcopy.tar.gz
sudo ./install.sh
```

Dopo aver installato AzCopy in Linux, è possibile rimuovere i file estratti. In alternativa, se non si hanno privilegi di superuser, è possibile eseguire `azcopy` usando lo script della shell azcopy nella cartella estratta.

## <a name="known-issues-and-best-practices"></a>Problemi noti e procedure consigliate
### <a name="error-installing-azcopy"></a>Errore durante l'installazione di AzCopy
Se si verificano problemi con l'installazione di AzCopy, si può provare a eseguire AzCopy usando lo script bash nella cartella `azcopy` estratta.

```bash
cd azcopy
./azcopy
```

### <a name="limit-concurrent-writes-while-copying-data"></a>Limitare le scritture simultanee durante la copia dei dati
Durante la copia di BLOB o file con AzCopy, tenere presente che altre applicazioni potrebbero modificare i dati mentre è in corso la copia. Se possibile, assicurarsi che i dati copiati non vengano modificati durante l'operazione di copia. Ad esempio, se si copia un file VHD associato a una macchina virtuale di Azure, verificare che altre applicazioni non stiano scrivendo nel file VHD durante la copia. Un buon metodo per eseguire questa operazione è tramite leasing della risorsa da copiare. In alternativa, è prima possibile creare uno snapshot del file VHD e quindi copiare lo snapshot.

Se non è possibile evitare che altre applicazioni scrivano nei BLOB o nei file durante l'operazione di copia, tenere presente che al termine del processo la parità delle risorse copiate con le risorse di origine potrebbe non essere completa.

### <a name="running-multiple-azcopy-processes"></a>Esecuzione di più processi AzCopy
È possibile eseguire più processi AzCopy su un singolo client a condizione di usare cartelle journal diverse. Non è supportato l'uso di una singola cartella journal per più processi AzCopy.

Primo processo:
```azcopy
azcopy \
    --source /mnt/myfiles1 \
    --destination https://myaccount.blob.core.windows.net/mycontainer/myfiles1 \
    --dest-key <key> \
    --resume "/mnt/myazcopyjournal1"
```

Secondo processo:
```azcopy
azcopy \
    --source /mnt/myfiles2 \
    --destination https://myaccount.blob.core.windows.net/mycontainer/myfiles2 \
    --dest-key <key> \
    --resume "/mnt/myazcopyjournal2"
```

## <a name="next-steps"></a>Passaggi successivi
Per altre informazioni su Archiviazione di Azure e AzCopy, vedere le risorse seguenti:

### <a name="azure-storage-documentation"></a>Documentazione di Archiviazione di Azure
* [Introduzione ad Archiviazione di Azure](../storage-introduction.md)
* [Creare un account di archiviazione](../storage-create-storage-account.md)
* [Gestire BLOB con Storage Explorer](https://docs.microsoft.com/azure/vs-azure-tools-storage-explorer-blobs)
* [Utilizzo dell'interfaccia della riga di comando di Azure con archiviazione di Azure](../storage-azure-cli.md)
* [Come usare l'archiviazione BLOB da C++](../blobs/storage-c-plus-plus-how-to-use-blobs.md)
* [Come usare l'archiviazione BLOB da Java](../blobs/storage-java-how-to-use-blob-storage.md)
* [Come usare l'archiviazione BLOB da Node.js](../blobs/storage-nodejs-how-to-use-blob-storage.md)
* [Come usare l'archiviazione BLOB da Python](../blobs/storage-python-how-to-use-blob-storage.md)

### <a name="azure-storage-blog-posts"></a>Post del blog di Archiviazione di Azure:
* [Annuncio della versione di anteprima di AzCopy in Linux](https://azure.microsoft.com/blog/announcing-azcopy-on-linux-preview/)
* [Introduzione alla versione di anteprima della libreria per lo spostamento dei dati di Archiviazione di Azure](https://azure.microsoft.com/blog/introducing-azure-storage-data-movement-library-preview-2/)
* [AzCopy: introduzione alla copia sincrona e al tipo di contenuto personalizzato](http://blogs.msdn.com/b/windowsazurestorage/archive/2015/01/13/azcopy-introducing-synchronous-copy-and-customized-content-type.aspx)
* [AzCopy: annuncio della disponibilità per tutti di AzCopy 3.0 oltre alla versione di anteprima di AzCopy 4.0 con il supporto di tabelle e file](http://blogs.msdn.com/b/windowsazurestorage/archive/2014/10/29/azcopy-announcing-general-availability-of-azcopy-3-0-plus-preview-release-of-azcopy-4-0-with-table-and-file-support.aspx)
* [AzCopy: ottimizzazione per gli scenari di copia su larga scala](http://go.microsoft.com/fwlink/?LinkId=507682)
* [AzCopy:supporto per l'archiviazione con ridondanza geografica e accesso in lettura](http://blogs.msdn.com/b/windowsazurestorage/archive/2014/04/07/azcopy-support-for-read-access-geo-redundant-account.aspx)
* [AzCopy:trasferimento di dati con modalità riavviabile e token di firma di accesso condiviso](http://blogs.msdn.com/b/windowsazurestorage/archive/2013/09/07/azcopy-transfer-data-with-re-startable-mode-and-sas-token.aspx)
* [AzCopy: uso del comando di copia dei BLOB tra account](http://blogs.msdn.com/b/windowsazurestorage/archive/2013/04/01/azcopy-using-cross-account-copy-blob.aspx)
* [AzCopy: Caricamento e download di file per BLOB di Microsoft Azure](http://blogs.msdn.com/b/windowsazurestorage/archive/2012/12/03/azcopy-uploading-downloading-files-for-windows-azure-blobs.aspx)
