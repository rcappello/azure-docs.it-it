---
title: Assegnare ruoli della directory di Azure AD in PIM | Microsoft Docs
description: Informazioni su come assegnare i ruoli della directory di Azure AD in Azure AD Privileged Identity Management (PIM).
services: active-directory
documentationcenter: ''
author: rolyon
manager: mtillman
editor: ''
ms.service: active-directory
ms.topic: conceptual
ms.workload: identity
ms.component: pim
ms.date: 07/23/2018
ms.author: rolyon
ms.openlocfilehash: 33bfe28bf612c47c9f42345dabccc017337c3d45
ms.sourcegitcommit: 63613e4c7edf1b1875a2974a29ab2a8ce5d90e3b
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 08/29/2018
ms.locfileid: "43190157"
---
# <a name="assign-azure-ad-directory-roles-in-pim"></a>Assegnare ruoli della directory di Azure AD in PIM

Con Azure Active Directory (Azure AD) un amministratore globale può rendere le assegnazioni di ruoli di directory **permanenti**. Queste assegnazioni di ruolo possono essere create usando il [portale di Azure](../users-groups-roles/directory-assign-admin-roles.md) o i [ comandi di PowerShell](/powershell/module/azuread#directory_roles).

Il servizio Azure AD Privileged Identity Management (PIM) consente anche agli amministratori di ruoli con privilegi di effettuare assegnazioni di ruoli di directory permanenti. Inoltre, gli amministratori di ruoli con privilegi possono rendere gli utenti **idonei** ai ruoli di directory. Un amministratore idoneo può attivare il ruolo quando serve, con autorizzazioni che scadono al termine delle operazioni. Per informazioni sui ruoli che è possibile gestire usando PIM, vedere [Ruoli della directory di Azure AD che è possibile gestire in PIM](pim-roles.md).

## <a name="make-a-user-eligible-for-a-role"></a>Rendere un utente idoneo per un ruolo

Per rendere un utente idoneo per un ruolo di directory di Azure AD, eseguire la procedura seguente:

1. Accedere al [portale di Azure](https://portal.azure.com/) con un utente membro del ruolo [Amministratore dei ruoli con privilegi](../users-groups-roles/directory-assign-admin-roles.md#privileged-role-administrator).

    Per informazioni su come concedere a un altro accesso di amministratore per la gestione di PIM, vedere [Concedere l'accesso ad altri amministratori per gestire PIM](pim-how-to-give-access-to-pim.md).

1. Aprire **Azure AD Privileged Identity Management**.

    Se PIM non è stato ancora avviato nel portale di Azure, andare al [Iniziare a usare PIM](pim-getting-started.md).

1. Fare clic su **Ruoli della directory di Azure AD**.

1. Fare clic su **Ruoli** o **Membri**.

    ![Ruoli della directory di Azure AD](./media/pim-how-to-add-role-to-user/pim-directory-roles.png)

1. Fare clic su **Aggiungi membro** per aprire Aggiungi membri gestiti.

1. Fare clic su **Selezionare un ruolo**, su un ruolo da gestire e quindi su **Seleziona**.

    ![Selezionare un ruolo](./media/pim-how-to-add-role-to-user/pim-select-a-role.png)

1. Fare clic su **Selezione membri**, selezionare gli utenti da assegnare al ruolo, quindi fare clic su **Seleziona**.

    ![Selezionare un ruolo](./media/pim-how-to-add-role-to-user/pim-select-members.png)

1. Nella finestra Aggiungi membri gestiti fare clic su **OK** per aggiungere l'utente al ruolo.

1. Nell'elenco dei ruoli predefiniti fare clic sul ruolo assegnato per visualizzare l'elenco dei membri.

     Quando il ruolo è stato assegnato, l'utente selezionato verrà visualizzato nell'elenco dei membri con il valore **Idoneo** per il ruolo.

    ![Utente idoneo per un ruolo](./media/pim-how-to-add-role-to-user/pim-directory-role-eligible.png)

1. Ora che l'utente è idoneo per il ruolo, è necessario comunicargli che può attivarlo seguendo le istruzioni in [Activate my Azure AD directory roles in PIM](pim-how-to-activate-role.md) (Attivare i ruoli della directory di Azure AD in PIM).

    Gli amministratori idonei devono registrarsi ad Azure Multi-Factor Authentication (MFA) durante l'attivazione. Se un utente non riesce a registrarsi al servizio Multi-Factor Authentication o usa un account Microsoft, in genere @outlook.com, è necessario rendere l'utente permanente in tutti i relativi ruoli.

## <a name="make-a-role-assignment-permanent"></a>Rendere permanente un'assegnazione di ruolo

Per impostazione predefinita, i nuovi utenti sono idonei solo per un ruolo della directory. Per rendere permanente un'assegnazione di ruolo, eseguire la procedura seguente:

1. Aprire **Azure AD Privileged Identity Management**.

1. Fare clic su **Ruoli della directory di Azure AD**.

1. Fare clic su **Membri**.

    ![Elenco di membri](./media/pim-how-to-add-role-to-user/pim-directory-role-list-members.png)

1. Fare clic su un ruolo **idoneo** che si vuole rendere permanente.

1. Fare clic su **Altro**, quindi su **Rendi permanente**.

    ![Rendere permanente l'assegnazione di ruolo](./media/pim-how-to-add-role-to-user/pim-make-perm.png)

    Il ruolo viene elencato come **permanente**.

    ![Elenco di membri con modifica permanente](./media/pim-how-to-add-role-to-user/pim-directory-role-list-members-permanent.png)

## <a name="remove-a-user-from-a-role"></a>Rimuovere un utente da un ruolo

È possibile rimuovere gli utenti dalle assegnazioni di ruoli, ma è necessario assicurarsi che sia sempre presente almeno un utente con ruolo di amministratore globale permanente. Se non si è certi se gli utenti necessitano ancora di assegnazioni di ruoli, è possibile [avviare una verifica di accesso per il ruolo](pim-how-to-start-security-review.md).

Per rimuovere un utente specifico da un ruolo della directory, eseguire la procedura seguente:

1. Aprire **Azure AD Privileged Identity Management**.

1. Fare clic su **Ruoli della directory di Azure AD**.

1. Fare clic su **Membri**.

    ![Elenco di membri](./media/pim-how-to-add-role-to-user/pim-directory-role-list-members.png)

1. Fare clic su un'assegnazione di ruolo da rimuovere.

1. Fare clic su **Altro** e quindi su **Rimuovi**.

    ![Rimuovere un ruolo](./media/pim-how-to-add-role-to-user/pim-remove-role.png)

1. Nel messaggio di conferma fare clic su **Sì**.

    ![Rimuovere un ruolo](./media/pim-how-to-add-role-to-user/pim-remove-role-confirm.png)

    L'assegnazione di ruolo viene rimossa.

## <a name="next-steps"></a>Passaggi successivi

- [Configurare le impostazioni dei ruoli della directory di Azure AD in PIM](pim-how-to-change-default-settings.md)
- [Assegnare i ruoli delle risorse di Azure in PIM](pim-resource-roles-assign-roles.md)
