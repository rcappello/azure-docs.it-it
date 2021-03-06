---
title: Restituire i dischi di Microsoft Azure Data Box | Microsoft Docs
description: Usare questa esercitazione per scoprire come restituire i dischi di Azure Data Box a Microsoft
services: databox
author: alkohli
ms.service: databox
ms.subservice: disk
ms.topic: tutorial
ms.date: 07/10/2018
ms.author: alkohli
Customer intent: As an IT admin, I need to be able to order Data Box Disk to upload on-premises data from my server onto Azure.
ms.openlocfilehash: f971a1bed0391e809e19ff5bb0508d153319faf4
ms.sourcegitcommit: 4047b262cf2a1441a7ae82f8ac7a80ec148c40c4
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 10/11/2018
ms.locfileid: "49094004"
---
# <a name="tutorial-return-azure-data-box-disk-and-verify-data-upload-to-azure"></a>Esercitazione: Restituire i dischi di Azure Data Box e verificare il caricamento dei dati in Azure

Questa è l'ultima esercitazione della serie: Distribuire Azure Data Box Disk. In questa esercitazione si apprenderà come:

> [!div class="checklist"]
> * Spedire i dischi di Data Box a Microsoft
> * Verificare il caricamento dei dati in Azure
> * Cancellazione dei dati dai dischi di Data Box

## <a name="prerequisites"></a>Prerequisiti

Prima di iniziare, assicurarsi di aver completato l'[Esercitazione: Copiare i dati su Azure Data Box Disk ed eseguire la verifica](data-box-disk-deploy-copy-data.md).

## <a name="ship-data-box-disk-back"></a>Restituire i dischi di Data Box

1. Dopo aver completato la convalida dei dati, scollegare i dischi. Rimuovere i cavi di collegamento.
2. Avvolgere i dischi e i cavi di collegamento nel pluriball e inserirli nella scatola per la spedizione.
3. Usare l'etichetta per la spedizione di ritorno nella busta in plastica trasparente applicata sulla scatola. Se l'etichetta è danneggiata o è stata smarrita, scaricare una nuova etichetta di spedizione dal portale di Azure e applicarla sulla scatola. Passare a **Panoramica > Scarica etichetta di spedizione**. 

    ![Scaricare l'etichetta di spedizione](media/data-box-disk-deploy-picked-up/download-shipping-label.png)

    Questa azione scarica un'etichetta per la spedizione di ritorno, come illustrato di seguito.

    ![Etichetta di spedizione di esempio](media/data-box-disk-deploy-picked-up/exmple-shipping-label.png)

4. Sigillare la scatola e assicurarsi che l'etichetta per la spedizione di ritorno sia visibile.
5. Pianificare un ritiro con UPS per la restituzione negli Stati Uniti. Se i dischi vengono rispediti in Europa con DHL, richiedere un ritiro a DHL, visitando il sito Web e specificando il numero di lettera di vettura. Passare al sito Web di DHL Express del paese e scegliere **Prenota il ritiro di un reso > Richiedere ritiro**.

    ![Spedizione di reso DHL](media/data-box-disk-deploy-picked-up/dhl-ship-1.png)
    
    Specificare il numero di lettera di vettura e fare clic su **Schedule Pickup** (Pianifica ritiro) per organizzare il ritiro.

      ![Pianificare il ritiro](media/data-box-disk-deploy-picked-up/dhl-ship-2.png)

7. Dopo il ritiro dei dischi da parte del vettore, lo stato dell'ordine nel portale diventa **Ritirato**. Viene visualizzato anche un ID di traccia.

    ![Dischi prelevati](media/data-box-disk-deploy-picked-up/data-box-portal-pickedup.png)

## <a name="verify-data-upload-to-azure"></a>Verificare il caricamento dei dati in Azure

Quando Microsoft riceve e analizza i dischi, lo stato del processo diventa **Ricevuto**. 

![Dischi ricevuti](media/data-box-disk-deploy-picked-up/data-box-portal-received.png)

I dati vengono copiati automaticamente quando i dischi vengono collegati a un server nel data center di Azure. A seconda delle dimensioni dei dati, l'operazione di copia potrebbe richiedere da alcune ore a giorni per il completamento. È possibile monitorare lo stato di avanzamento del processo di copia nel portale.

Al termine della copia, lo stato dell'ordine diventa **Completato**.

![Copia dei dati completata](media/data-box-disk-deploy-picked-up/data-box-portal-completed.png)

Verificare la presenza dei dati negli account di archiviazione prima di eliminarli dall'origine. Per verificare che i dati siano stati caricati in Azure, seguire questa procedura:

1. Passare all'account di archiviazione associato all'ordine del disco.
2. Passare a **Servizio Blob > Esplora BLOB**. Viene presentato l'elenco di contenitori. In modo corrispondente alla sottocartella creata nelle cartelle *BlockBlob* e *PageBlob*, contenitori con lo stesso nome vengono creati nell'account di archiviazione.
    Se i nomi delle cartelle non sono conformi alle convenzioni di denominazione di Azure, il caricamento dei dati in Azure avrà esito negativo.

4. Per verificare che sia stato caricato l'intero set di dati, usare Microsoft Azure Storage Explorer. Collegare l'account di archiviazione corrispondente all'ordine di noleggio del disco e quindi esaminare l'elenco dei contenitori BLOB. Selezionare un contenitore, fare clic su **Altro** e quindi fare clic su **Statistiche cartella**. Nel riquadro **Attività** vengono visualizzate le statistiche per la cartella, inclusi il numero di BLOB e le dimensioni totali dei BLOB. Le dimensioni totali dei BLOB devono corrispondere alle dimensioni del set di dati.

    ![Statistiche delle cartelle in Storage Explorer](media/data-box-disk-deploy-picked-up/folder-statistics-storage-explorer.png)

## <a name="erasure-of-data-from-data-box-disk"></a>Cancellazione dei dati dai dischi di Data Box

Dopo aver completato la copia e aver verificato che i dati siano disponibili nell'account di archiviazione di Azure, i dischi vengono cancellati in modo sicuro come da standard NIST. 

## <a name="next-steps"></a>Passaggi successivi

In questa esercitazione sono stati illustrati argomenti relativi ad Azure Data Box, ad esempio:

> [!div class="checklist"]
> * Spedire i dischi di Data Box a Microsoft
> * Verificare il caricamento dei dati in Azure
> * Cancellazione dei dati dai dischi di Data Box


Passare alla guida pratica successiva per scoprire come gestire i dischi di Data Box tramite il portale di Azure.

> [!div class="nextstepaction"]
> [Usare il portale di Azure per amministrare Azure Data Box Disk](./data-box-portal-ui-admin.md)


