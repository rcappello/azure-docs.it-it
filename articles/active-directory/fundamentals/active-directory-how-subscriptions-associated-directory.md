---
title: Come aggiungere una sottoscrizione di Azure esistente alla directory di Azure AD | Microsoft Docs
description: Come aggiungere una sottoscrizione esistente alla directory di Azure AD
services: active-directory
documentationcenter: ''
author: eross-msft
manager: mtillman
editor: ''
ms.service: active-directory
ms.workload: identity
ms.component: fundamentals
ms.topic: conceptual
ms.date: 12/12/2017
ms.author: lizross
ms.reviewer: jeffsta
ms.custom: oldportal;it-pro;
ms.openlocfilehash: 6b0933e9aa732cb9a01a454764fb0425465ec078
ms.sourcegitcommit: 9222063a6a44d4414720560a1265ee935c73f49e
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 08/03/2018
ms.locfileid: "39503312"
---
# <a name="how-to-associate-or-add-an-azure-subscription-to-azure-active-directory"></a>Come associare o aggiungere una sottoscrizione di Azure ad Azure Active Directory

Questo articolo contiene informazioni sulla relazione tra una sottoscrizione di Azure e Azure Active Directory (Azure AD) e su come aggiungere una sottoscrizione esistente alla directory di Azure AD. La sottoscrizione di Azure ha una relazione di trust con Azure AD, ovvero considera attendibile la directory per autenticare gli utenti, i servizi e i dispositivi. Più sottoscrizioni possono considerare attendibile la stessa directory, ma ogni sottoscrizione considera attendibile una sola directory. 

La relazione di trust tra la sottoscrizione e la directory è diversa dalla relazione con le altre risorse in Azure, ad esempio siti Web, database e così via. Se la sottoscrizione scade, non sarà più possibile accedere alle altre risorse associate alla sottoscrizione. La directory di Azure AD rimane però in Azure, sarà quindi possibile associarla a una sottoscrizione diversa e continuare a gestire la directory con la nuova sottoscrizione.

Tutti gli utenti dispongono di una singola home directory che li autentica, ma poi possono essere utenti guest in altre directory. In Azure AD è possibile visualizzare solo le directory di cui l'account utente è membro o guest.

## <a name="before-you-begin"></a>Prima di iniziare

* È necessario accedere con l'account con accesso di proprietario di controllo degli accessi in base al ruolo alla sottoscrizione.
* È necessario eseguire l'accesso con un account che esiste sia nella directory corrente a cui è associata la sottoscrizione che nella directory a cui la si vuole aggiungere. Per altre informazioni su come ottenere l'accesso a un'altra directory, vedere [Procedura di aggiunta di utenti di Collaborazione B2B ad Azure Active Directory da parte degli amministratori](../b2b/add-users-administrator.md).
* Questa funzionalità non è disponibile per sottoscrizioni CSP (MS-AZR-0145P, MS-AZR-0146P e MS-AZR-159P) e Microsoft Imagine (MS-AZR-0144P).

## <a name="to-associate-an-existing-subscription-to-your-azure-ad-directory"></a>Per associare una sottoscrizione esistente alla directory di Azure AD

1. Eseguire l'accesso e selezionare una sottoscrizione dalla [pagina Sottoscrizioni del portale di Azure](https://portal.azure.com/#blade/Microsoft_Azure_Billing/SubscriptionsBlade).
2. Fare clic su **Cambia directory**.

    ![Screenshot che illustra il pulsante Cambia directory](./media/active-directory-how-subscriptions-associated-directory/edit-directory-button.PNG)
3. Esaminare gli avvisi. Tutti gli utenti con [controllo degli accessi in base al ruolo](../../role-based-access-control/role-assignments-portal.md) a cui è assegnato l'accesso e tutti gli amministratori della sottoscrizione perdono l'accesso quando la directory della sottoscrizione cambia.
4. Selezionare una directory.

    ![Screenshot che illustra l'interfaccia utente per cambiare la directory](./media/active-directory-how-subscriptions-associated-directory/edit-directory-ui.PNG)
5. Fare clic su **Modifica**.
6. Completamento della procedura Passare alla nuova directory usando l'apposito controllo. Per la visualizzazione corretta di tutti gli elementi potrebbero essere necessari fino a 10 minuti.

    ![Screenshot che illustra la notifica dell'avvenuto cambio di directory](./media/active-directory-how-subscriptions-associated-directory/edit-directory-success.PNG)

    ![Screenshot che illustra il controllo per cambiare directory](./media/active-directory-how-subscriptions-associated-directory/directory-switcher.PNG)


Gli insiemi di credenziali delle chiavi di Azure di cui si dispone sono inoltre influenzati dallo spostamento di una sottoscrizione, pertanto [modificare l'ID tenant dell'insieme di credenziali delle chiavi](../../key-vault/key-vault-subscription-move-fix.md) prima di riprendere le operazioni.

La modifica della directory della sottoscrizione è un'operazione a livello di servizio. Non ha effetto sulla proprietà della fatturazione della sottoscrizione e l'amministratore account può continuare a modificare l'amministratore del servizio usando il [Centro account](https://account.azure.com/subscriptions). Per eliminare la directory originale, è necessario trasferire la proprietà della fatturazione della sottoscrizione a un nuovo amministratore account. Per altre informazioni sul trasferimento della proprietà della fatturazione, vedere [Trasferire la proprietà di una sottoscrizione di Azure a un altro account](../../billing/billing-subscription-transfer.md). 

## <a name="next-steps"></a>Passaggi successivi

* Per altre informazioni sulla creazione di una nuova directory di Azure AD gratuita, vedere [Come ottenere un tenant di Azure Active Directory](../develop/quickstart-create-new-tenant.md)
* Per altre informazioni sul trasferimento della proprietà della fatturazione di una proprietario di Azure, vedere [Trasferire la proprietà di una sottoscrizione di Azure a un altro account](../../billing/billing-subscription-transfer.md)
* Per altre informazioni sul modo in cui l'accesso alle risorse viene controllato in Microsoft Azure, vedere [Informazioni sull'accesso alle risorse in Azure](../../role-based-access-control/rbac-and-directory-admin-roles.md)
* Per altre informazioni su come assegnare i ruoli in Azure AD, vedere [Assegnazione dei ruoli di amministratore in Azure Active Directory](../users-groups-roles/directory-assign-admin-roles.md)

<!--Image references-->
[1]: ./media/active-directory-how-subscriptions-associated-directory/WAAD_PassThruAuth.png
[2]: ./media/active-directory-how-subscriptions-associated-directory/WAAD_OrgAccountSubscription.png
[3]: ./media/active-directory-how-subscriptions-associated-directory/WAAD_SignInDisambiguation.PNG
