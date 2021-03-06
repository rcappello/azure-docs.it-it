---
title: Versioni supportate in Database di Azure per MariaDB
description: In questo articolo vengono descritte le versioni supportate in Database di Azure per MariaDB.
author: ajlam
ms.author: andrela
editor: jasonwhowell
services: mariadb
ms.service: mariadb
ms.topic: conceptual
ms.date: 09/24/2018
ms.openlocfilehash: aa83b9955839aaa03aa2ebf46c9e464dc75c8d3a
ms.sourcegitcommit: 32d218f5bd74f1cd106f4248115985df631d0a8c
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 09/24/2018
ms.locfileid: "46977503"
---
# <a name="supported-azure-database-for-mariadb-server-versions"></a>Versioni server supportate in Database di Azure per MariaDB
Database di Azure per MariaDB è stato sviluppato dal database [MariaDB Server](https://downloads.mariadb.org/) open source usando il motore InnoDB. Al momento Database di Azure per MariaDB supporta la versione seguente:

## <a name="mariadb-version-10217"></a>Versione di MariaDB 10.2.17
Per altre informazioni sui miglioramenti e sulle correzioni in MariaDB 10.2.17, vedere la [documentazione di MariaDB](https://downloads.mariadb.org/mariadb/10.2.17/).

> [!NOTE]
> Nel servizio viene usato un gateway per reindirizzare le connessioni alle istanze del server. Dopo che è stata stabilita la connessione, il client MySQL visualizza la versione di MariaDB impostata nel gateway e non la versione effettiva in esecuzione nell'istanza del server MariaDB. Per determinare la versione dell'istanza del server MariaDB, usare il comando `SELECT VERSION();` dal prompt di MySQL.

## <a name="managing-updates-and-upgrades"></a>Gestire gli aggiornamenti
Il servizio gestisce automaticamente l'applicazione di patch per gli aggiornamenti delle versioni secondarie.

## <a name="next-steps"></a>Passaggi successivi
Per informazioni sulle quote specifiche di risorse e sulle limitazioni in base al **livello di servizio**, vedere [Livelli di servizio](./concepts-pricing-tiers.md)