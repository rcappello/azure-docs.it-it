---
title: Usare un SDK di Azure per configurare una macchina virtuale con identità gestite per le risorse di Azure
description: Istruzioni dettagliate per la configurazione e l'uso di identità gestite per le risorse di Azure in una macchina virtuale di Azure mediante un SDK di Azure.
services: active-directory
documentationcenter: ''
author: daveba
manager: mtillman
editor: ''
ms.service: active-directory
ms.component: msi
ms.devlang: na
ms.topic: conceptual
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 09/28/2017
ms.author: daveba
ms.openlocfilehash: 3b485fd0f655588ec5ae7941bcb6a43ca7728134
ms.sourcegitcommit: cc4fdd6f0f12b44c244abc7f6bc4b181a2d05302
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 09/25/2018
ms.locfileid: "47106700"
---
# <a name="configure-a-vm-with-managed-identities-for-azure-resources-using-an-azure-sdk"></a>Configurare una macchina virtuale con identità gestite per le risorse di Azure mediante un SDK di Azure

[!INCLUDE [preview-notice](../../../includes/active-directory-msi-preview-notice.md)]

Le identità gestite per le risorse Azure forniscono ai servizi di Azure un'identità gestita automaticamente in Azure Active Directory (AD). È possibile usare questa identità per l'autenticazione a qualsiasi servizio che supporti l'autenticazione di Azure AD senza dover inserire le credenziali nel codice. 

Questo articolo illustra come abilitare e rimuovere identità gestite per le risorse di Azure per una macchina virtuale di Azure mediante un SDK di Azure.

## <a name="prerequisites"></a>Prerequisiti

[!INCLUDE [msi-qs-configure-prereqs](../../../includes/active-directory-msi-qs-configure-prereqs.md)]

## <a name="azure-sdks-with-managed-identities-for-azure-resources-support"></a>SDK di Azure che supportano le identità gestite per le risorse di Azure 

Azure supporta più piattaforme di programmazione tramite una serie di [Azure SDK](https://azure.microsoft.com/downloads). Alcuni SDK sono stati aggiornati per supportare le identità gestite per le risorse di Azure e forniscono esempi che ne illustrano l'utilizzo. L'elenco viene aggiornato quando è disponibile supporto aggiuntivo:

| SDK | Esempio |
| --- | ------ | 
| .NET   | [Gestire risorse da una macchina virtuale abilitata con le identità gestite per le risorse di Azure abilitate](https://azure.microsoft.com/resources/samples/aad-dotnet-manage-resources-from-vm-with-msi/) |
| Java   | [Gestire risorse di archiviazione da una macchina virtuale abilitata con le identità gestite per le risorse di Azure](https://azure.microsoft.com/resources/samples/compute-java-manage-resources-from-vm-with-msi-in-aad-group/)|
| Node.js| [Creare una macchina virtuale con un'identità gestita assegnata dal sistema abilitata](https://azure.microsoft.com/resources/samples/compute-node-msi-vm/) |
| Python | [Creare una macchina virtuale con un'identità gestita assegnata dal sistema abilitata](https://azure.microsoft.com/resources/samples/compute-python-msi-vm/) |
| Ruby   | [Creare una macchina virtuale di Azure con un'identità gestita assegnata dal sistema abilitata](https://azure.microsoft.com/resources/samples/compute-ruby-msi-vm/) |

## <a name="next-steps"></a>Passaggi successivi

- Per imparare a usare anche il portale di Azure, PowerShell, l'interfaccia della riga di comando e i modelli di risorse, vedere gli articoli in **Configurare l'identità per una VM di Azure**.
