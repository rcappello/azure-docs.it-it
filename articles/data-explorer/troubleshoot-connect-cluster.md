---
title: Errore durante la connessione a un cluster in Esplora dati di Azure
description: Questo articolo descrive i passaggi per la risoluzione dei problemi relatici alla connessione a un cluster in Esplora dati di Azure.
author: orspod
ms.author: v-orspod
ms.reviewer: mblythe
ms.service: data-explorer
services: data-explorer
ms.topic: conceptual
ms.date: 09/24/2018
ms.openlocfilehash: f66dcc55b01b407c59c65ea300757ab4ee1002ac
ms.sourcegitcommit: 32d218f5bd74f1cd106f4248115985df631d0a8c
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 09/24/2018
ms.locfileid: "46965059"
---
# <a name="troubleshoot-failure-to-connect-to-a-cluster-in-azure-data-explorer"></a>Risoluzione dei problemi: Errore durante la connessione a un cluster in Esplora dati di Azure

Se non si riesce a connettersi a un cluster in Esplora dati di Azure, seguire questa procedura.

1. Assicurarsi che la stringa di connessione sia corretta. Deve essere nel formato: `https://<ClusterName>.<Region>.kusto.windows.net`, come nell'esempio seguente: `https://docscluster.westus.kusto.windows.net`.

1. Assicurarsi di disporre delle autorizzazioni appropriate. In caso contrario, si otterrà una risposta di tipo *non autorizzato*.

    Per altre informazioni sulle autorizzazioni, vedere [Gestire le autorizzazioni per i database](manage-database-permissions.md). Se necessario, rivolgersi all'amministratore del cluster per essere aggiunti al ruolo appropriato.

1. Assicurarsi che il cluster non sia stato eliminato: rivedere il log attività nella sottoscrizione.

1. Controllare il [dashboard di integrità dei servizi di Azure](https://azure.microsoft.com/status/>). Cercare lo stato di Esplora dati di Azure nell'area in cui si sta cercando di connettersi al cluster.

    Se lo stato è diverso da **Buono**, valore indicato dal segno di spunta verde, provare a connettersi al cluster dopo che lo stato è migliorato.

1. Per richiedere ulteriore assistenza per la risoluzione del problema, aprire una richiesta di supporto nel [portale di Azure](https://portal.azure.com).