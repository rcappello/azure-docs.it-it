---
title: Risoluzione dei problemi per la creazione di tenant in Azure Active Directory B2C | Microsoft Docs
description: Problemi e soluzioni per la creazione di un tenant di Azure Active Directory o di un tenant di Azure Active Directory B2C.
services: active-directory-b2c
author: davidmu1
manager: mtillman
ms.service: active-directory
ms.workload: identity
ms.topic: conceptual
ms.date: 12/06/2016
ms.author: davidmu
ms.component: B2C
ms.openlocfilehash: 009f7ac2f7e614b7e07623e41888973f1a2b254d
ms.sourcegitcommit: 86cb3855e1368e5a74f21fdd71684c78a1f907ac
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 07/03/2018
ms.locfileid: "37440981"
---
# <a name="troubleshoot-creating-an-azure-active-directory-or-azure-active-directory-b2c-tenant"></a>Risoluzione dei problemi per la creazione di un tenant di Azure Active Directory o di un tenant di Azure Active Directory B2C 

## <a name="create-an-azure-ad-tenant"></a>Come creare un tenant di Azure Active Directory
Se non è possibile creare un tenant Azure Active Directory (Azure AD) al primo tentativo, riprovare. Se il problema persiste, contattare il supporto di Azure.

## <a name="create-an-azure-ad-b2c-tenant"></a>Creare un tenant di Azure AD B2C
Se si verificano problemi quando si [crea un tenant di Azure Active Directory B2C (Azure AD B2C)](active-directory-b2c-get-started.md), provare le seguenti opzioni:

* Se il tenant di Azure AD B2C non viene visualizzato nell'elenco di tenant, riprovare a creare il tenant.
* Se il tenant di Azure Active Directory B2C viene visualizzato nell'elenco di tenant e compare il seguente messaggio di errore, eliminare il tenant e crearlo di nuovo:

    "Impossibile completare la creazione del tenant B2C 'contosob2c'. Fare clic su questo [collegamento](http://go.microsoft.com/fwlink/?LinkID=624192&clcid=0x409) per maggiori informazioni. "
* Si verificano problemi noti quando si elimina un tenant Azure AD B2C esistente e lo si crea nuovamente utilizzando lo stesso nome di dominio. Quando si crea un nuovo tenant di Azure AD B2C, è necessario utilizzare un nome di dominio diverso.
* Se nessuna di queste soluzioni risolve il problema, contattare il supporto di Azure. Per maggiori informazioni, vedere [Presentare richieste di supporto per Azure AD B2C](active-directory-b2c-support.md).

