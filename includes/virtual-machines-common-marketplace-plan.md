---
title: File di inclusione
description: File di inclusione
services: virtual-machines-windows, virtual-machines-linux
author: dlepow
ms.service: multiple
ms.topic: include
ms.date: 09/28/2018
ms.author: danlep
ms.custom: include file
ms.openlocfilehash: f9974aae1e5996ffeaa6cde690a5e10ccba4cc32
ms.sourcegitcommit: 7bc4a872c170e3416052c87287391bc7adbf84ff
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 10/02/2018
ms.locfileid: "48019013"
---
## <a name="deploy-an-image-with-marketplace-terms"></a>Distribuire un'immagine con le condizioni del Marketplace

Alcune immagini di macchine virtuali in Azure Marketplace hanno condizioni di licenza e di acquisto aggiuntive che è necessario accettare prima di procedere alla distribuzione a livello di codice.  

Per distribuire una macchina virtuale da tale immagine, è necessario accettarne le condizioni e abilitare la distribuzione a livello di codice. Questa operazione deve essere eseguita una sola volta nell'ambito della sottoscrizione. Quindi, ogni volta che si distribuisce una macchina virtuale a livello di codice dall'immagine, è anche necessario specificare i parametri del *piano di acquisto*.

Le sezioni seguenti mostrano come:

* Scoprire se un'immagine del Marketplace ha condizioni di licenza aggiuntive 
* Accettare le condizioni a livello di codice
* Specificare i parametri del piano di acquisto quando si distribuisce una macchina virtuale a livello di codice

