---
title: Configurare e accedere ai log del server per il Database di Azure per MariaDB nel portale di Azure
description: Questo articolo descrive come configurare e accedere ai log del server nel Database di Azure per MariaDB dal Portale di Azure.
author: rachel-msft
ms.author: raagyema
editor: jasonwhowell
services: mariadb
ms.service: mariadb
ms.topic: conceptual
ms.date: 09/24/2018
ms.openlocfilehash: 0784dffc48aeddc854aa540cba24f1834cd41827
ms.sourcegitcommit: 32d218f5bd74f1cd106f4248115985df631d0a8c
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 09/24/2018
ms.locfileid: "46952835"
---
# <a name="configure-and-access-server-logs-in-the-azure-portal"></a>Configurare e accedere ai log del server nel portale di Azure

È possibile configurare, elencare e scaricare i [log del server di Database di Azure per MariaDB](concepts-server-logs.md) dal portale di Azure.

## <a name="prerequisites"></a>Prerequisiti
Per proseguire con questa guida, si richiedono:
- [Database di Azure per il server MariaDB](quickstart-create-mariadb-server-database-using-azure-portal.md)

## <a name="configure-logging"></a>Configurare la registrazione
Configurare l'accesso al log di query lente. 

1. Accedere al [portale di Azure](http://portal.azure.com/).

2. Selezionare il server del Database di Azure per MariaDB.

3. Nella sezione **Monitoraggio** della barra laterale selezionare **Log del server**. 
   ![Selezionare i log del server e fare clic per configurare](./media/howto-configure-server-logs-portal/1-select-server-logs-configure.png)

4. Selezionare l'intestazione **Fare clic qui per abilitare i log e configurare i parametri dei log** per visualizzare i parametri del server.

5. Cambiare i parametri che si desidera modificare, inclusa l'impostazione di "slow_query_log" su "ON". Tutte le modifiche apportate in questa sessione vengono evidenziate in viola. 

   Dopo avere modificato i parametri, è possibile fare clic su **Salva**. In alternativa è possibile **annullare** le modifiche.

   ![Fare clic su Salva o Annulla](./media/howto-configure-server-logs-portal/3-save-discard.png)

6. Tornare all'elenco di log facendo clic sul **pulsante di chiusura** (icona X) nella pagina **Parametri del server**.

## <a name="view-list-and-download-logs"></a>Visualizzare l'elenco e scaricare i log
Quando inizia la registrazione, è possibile visualizzare un elenco di log disponibili e scaricare i singoli file di log nel riquadro Log del server. 

1. Aprire il Portale di Azure.

2. Selezionare il server del Database di Azure per MariaDB.

3. Nella sezione **Monitoraggio** della barra laterale selezionare **Log del server**. Nella pagina viene visualizzato un elenco di file di log, come illustrato:

   ![Elenco di log](./media/howto-configure-server-logs-portal/4-server-logs-list.png)

   > [!TIP]
   > La convenzione di denominazione del log è **mysql-slow-< nome server>-yyyymmddhh.log**. Data e ora usate nel nome del file indicano l'ora in cui è stato generato il log. I file di log vengono ruotati ogni 24 ore o 7,5 GB, a seconda del valore raggiunto per primo.

4. Se necessario, usare la **casella di ricerca** per restringere l'elenco a un log specifico in base a data/ora. La ricerca viene eseguita in base al nome del log.

5. Scaricare i singoli file di log usando il pulsante per **scaricare** (icona con la freccia giù) accanto a ogni file di log nella riga della tabella, come illustrato:

   ![Fare clic sull'icona per scaricare](./media/howto-configure-server-logs-portal/5-download.png)

## <a name="next-steps"></a>Passaggi successivi
- Altre informazioni sui [log del server](concepts-server-logs.md) nel Database di Azure per MariaDB.
- Per altre informazioni sulle definizioni di parametri e la registrazione MariaDB, vedere la documentazione sui [log](https://mariadb.com/kb/en/library/slow-query-log-overview/).

<!-- - See [Access Server Logs in CLI](howto-configure-server-logs-in-cli.md) to learn how to download logs programmatically. -->