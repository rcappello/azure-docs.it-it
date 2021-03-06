---
title: 'Esercitazione: Integrazione di Azure Active Directory con GitHub | Microsoft Docs'
description: Informazioni su come configurare l'accesso Single Sign-On tra Azure Active Directory e GitHub.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 8761f5ca-c57c-4a7e-bf14-ac0421bd3b5e
ms.service: active-directory
ms.component: saas-app-tutorial
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/23/2018
ms.author: jeedes
ms.openlocfilehash: b2a90a4599e5d07baba721d5649b72422dc5cb4d
ms.sourcegitcommit: 58c5cd866ade5aac4354ea1fe8705cee2b50ba9f
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 08/24/2018
ms.locfileid: "42818746"
---
# <a name="tutorial-azure-active-directory-integration-with-github"></a>Esercitazione: Integrazione di Azure Active Directory con GitHub

Questa esercitazione descrive come integrare GitHub con Azure Active Directory (Azure AD).

L'integrazione di GitHub con Azure AD offre i vantaggi seguenti:

- È possibile controllare in Azure AD chi può accedere a GitHub.
- È possibile abilitare gli utenti per l'accesso automatico a GitHub (Single Sign-On) con i propri account Azure AD.
- È possibile gestire gli account in un'unica posizione centrale: il portale di Azure.

Per altre informazioni sull'integrazione di app SaaS con Azure AD, vedere [Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory](../manage-apps/what-is-single-sign-on.md).

## <a name="prerequisites"></a>Prerequisiti

Per configurare l'integrazione di Azure AD con GitHub, sono necessari gli elementi seguenti:

- Sottoscrizione di Azure AD
- Una sottoscrizione abilitata GitHub per l'accesso Single Sign-On

> [!NOTE]
> Non è consigliabile usare un ambiente di produzione per testare i passaggi di questa esercitazione.

A questo scopo, è consigliabile seguire le indicazioni seguenti:

- Non usare l'ambiente di produzione a meno che non sia necessario.
- Se non è disponibile un ambiente di valutazione di Azure AD, è possibile [ottenere una versione di valutazione di un mese](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Descrizione dello scenario

In questa esercitazione viene eseguito il test dell'accesso Single Sign-On di Azure AD in un ambiente di test. Lo scenario descritto in questa esercitazione prevede le due fasi fondamentali seguenti:

1. Aggiunta di GitHub dalla raccolta
2. Configurazione e test dell'accesso Single Sign-On di Azure AD

## <a name="adding-github-from-the-gallery"></a>Aggiunta di GitHub dalla raccolta

Per configurare l'integrazione di GitHub in Azure AD, è necessario aggiungere GitHub dalla raccolta al proprio elenco di app SaaS gestite.

**Per aggiungere GitHub dalla raccolta, seguire questa procedura:**

1. Nel **[portale di Azure](https://portal.azure.com)** fare clic sull'icona di **Azure Active Directory** nel riquadro di spostamento sinistro. 

    ![Pulsante Azure Active Directory][1]

2. Passare ad **Applicazioni aziendali**. Andare quindi a **Tutte le applicazioni**.

    ![Pannello Applicazioni aziendali][2]

3. Fare clic sul pulsante **Nuova applicazione** nella parte superiore della finestra di dialogo per aggiungere una nuova applicazione.

    ![Pulsante Nuova applicazione][3]

4. Nella casella di ricerca digitare **GitHub**, selezionare **GitHub** nel pannello dei risultati e quindi fare clic sul pulsante **Aggiungi** per aggiungere l'applicazione.

    ![GitHub nell'elenco risultati](./media/github-tutorial/tutorial_github_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a>Configurare e testare l'accesso Single Sign-On di Azure AD

In questa sezione viene configurato e testato l'accesso Single Sign-On di Azure AD con GitHub in base a un utente test di nome "Britta Simon".

Per il funzionamento dell'accesso Single Sign-On, Azure AD deve conoscere qual è l'utente di GitHub che corrisponde a un utente di Azure AD. In altre parole, deve essere stabilita una relazione di collegamento tra un utente di Azure AD e l'utente correlato in GitHub.

Per configurare e testare l'accesso Single Sign-On di Azure AD con GitHub, è necessario completare i blocchi predefiniti seguenti:

1. **[Configurare l'accesso Single Sign-On di Azure AD](#configure-azure-ad-single-sign-on)**: per consentire agli utenti di usare questa funzionalità.
2. **[Creare un utente di test di Azure AD](#create-an-azure-ad-test-user)**: per testare l'accesso Single Sign-On di Azure AD con l'utente Britta Simon.
3. **[Creare un utente test di GitHub](#create-a-github-test-user)**: per avere una controparte di Britta Simon in GitHub collegata alla rappresentazione dell'utente in Azure AD.
4. **[Assegnare l'utente test di Azure AD](#assign-the-azure-ad-test-user)**: per abilitare Britta Simon all'uso dell'accesso Single Sign-On di Azure AD.
5. **[Testare l'accesso Single Sign-On](#test-single-sign-on)** per verificare se la configurazione funziona.

### <a name="configure-azure-ad-single-sign-on"></a>Configurare l'accesso Single Sign-On di Azure AD

In questa sezione viene abilitato l'accesso Single Sign-On di Azure AD nel portale di Azure e viene configurato l'accesso Single Sign-On nell'applicazione GitHub.

**Per configurare Single Sign-On di Azure AD con GitHub, seguire questa procedura:**

1. Nella pagina di integrazione dell'applicazione **GitHub** del portale di Azure fare clic su **Single Sign-On**.

    ![Collegamento Configura accesso Single Sign-On][4]

2. Nella finestra di dialogo **Single Sign-On** selezionare **Accesso basato su SAML** per **Modalità** per abilitare l'accesso Single Sign-On.

    ![Finestra di dialogo Single Sign-On](./media/github-tutorial/tutorial_github_samlbase.png)

3. Nella sezione **URL e dominio GitHub** seguire questa procedura:

    ![Informazioni su URL e dominio per l'accesso Single Sign-On di GitHub](./media/github-tutorial/tutorial_github_url.png)

    a. Nella casella di testo **URL di accesso** digitare l'URL usando il modello seguente: `https://github.com/orgs/<entity-id>/sso`

    b. Nella casella di testo **Identificatore (ID entità)** digitare un URL usando il criterio seguente: `https://github.com/orgs/<entity-id>`

    > [!NOTE]
    > Si noti che questi non sono i valori reali. È necessario aggiornare questi valori con l'identificatore e l'URL di accesso effettivi. In questo caso, è consigliabile di usare il valore univoco della stringa nell'identificatore. Passare alla sezione Admin di GitHub per recuperare questi valori.

4. Nella sezione **User Attributes** (Attributi utente) selezionare **User Identifier** (Identificatore utente) come user.mail.

    ![Configure Single Sign-On](./media/github-tutorial/tutorial_github_attribute_new01.png)

5. Nella sezione **Certificato di firma SAML** fare clic su **Certificato (Base64)** e quindi salvare il file del certificato nel computer.

    ![Collegamento di download del certificato](./media/github-tutorial/tutorial_github_certificate.png) 

6. Fare clic sul pulsante **Salva** .

    ![Pulsante Salva per la configurazione dell'accesso Single Sign-On](./media/github-tutorial/tutorial_general_400.png)

7. Nella sezione **GitHub Configuration** (Configurazione GitHub) fare clic su **Configure GitHub** (Configura GitHub) per aprire la finestra **Configura accesso**. Copiare l'**URL di disconnessione, l'ID di entità SAML e l'URL del servizio Single Sign-On SAML** dalla sezione **Riferimento rapido.**

    ![Configurazione GitHub](./media/github-tutorial/tutorial_github_configure.png) 

8. In un'altra finestra del Web browser accedere al sito aziendale di GitHub come amministratore.

9. Passare a **Settings** (Impostazioni) e fare clic su **Security** (Sicurezza).

    ![Impostazioni](./media/github-tutorial/tutorial_github_config_github_03.png)

10. Selezionare la casella **Enable SAML authentication** (Abilita autenticazione SAML) mostrando i campi di configurazione dell'accesso Single Sign-On. Usare quindi il valore URL di Single Sign-On per aggiornare l'URL di Single Sign-On nella configurazione di Azure AD.

    ![Impostazioni](./media/github-tutorial/tutorial_github_config_github_13.png)

11. Configurare i campi seguenti:

    a. Nella casella di testo **URL di accesso**, incollare il valore di **URL servizio Single Sign-On SAML** copiato dal portale di Azure.

    b. Nella casella di testo **autorità di certificazione** incollare il valore di **ID entità SAML** copiato dal portale di Azure.

    c. Aprire il certificato scaricato nel Blocco note dal portale di Azure e incollarne il contenuto nella casella di testo **Certificato pubblico**.

    ![Impostazioni](./media/github-tutorial/tutorial_github_config_github_051.png)

12. Fare clic su **Test SAML configuration** (Test configurazione SAML) per confermare l'assenza di errori di convalida o errori durante l'accesso SSO.

    ![Impostazioni](./media/github-tutorial/tutorial_github_config_github_06.png)

13. Fare clic su **Save**

> [!NOTE]
> L'accesso Single Sign-On in GitHub esegue l'autenticazione in un'organizzazione specifica in GitHub e non sostituisce l'autenticazione di GitHub. Pertanto, se la sessione GitHub.com dell'utente è scaduta, potrebbe venire richiesto di eseguire l'autenticazione con l'ID/la password GitHub durante il processo di accesso Single Sign-On.

### <a name="create-an-azure-ad-test-user"></a>Creare un utente test di Azure AD

Questa sezione descrive come creare un utente test denominato Britta Simon nel portale di Azure.

   ![Creare un utente test di Azure AD][100]

**Per creare un utente test in Azure AD, eseguire la procedura seguente:**

1. Nel portale di Azure fare clic sul pulsante **Azure Active Directory** nel riquadro sinistro.

    ![Pulsante Azure Active Directory](./media/github-tutorial/create_aaduser_01.png)

2. Per visualizzare l'elenco di utenti, passare a **Utenti e gruppi** e quindi fare clic su **Tutti gli utenti**.

    ![Collegamenti "Utenti e gruppi" e "Tutti gli utenti"](./media/github-tutorial/create_aaduser_02.png)

3. Per aprire la finestra di dialogo **Utente** fare clic su **Aggiungi** nella parte superiore della finestra di dialogo **Tutti gli utenti**.

    ![Pulsante Aggiungi](./media/github-tutorial/create_aaduser_03.png)

4. Nella finestra di dialogo **Utente** seguire questa procedura:

    ![Finestra di dialogo Utente](./media/github-tutorial/create_aaduser_04.png)

    a. Nella casella **Nome** digitare **BrittaSimon**.

    b. Nella casella **Nome utente** digitare l'indirizzo di posta elettronica dell'utente Britta Simon.

    c. Selezionare la casella di controllo **Mostra password** e quindi prendere nota del valore visualizzato nella casella **Password**.

    d. Fare clic su **Create**(Crea).

### <a name="create-a-github-test-user"></a>Creare un utente test GitHub

Questa sezione descrive come creare un utente chiamato Britta Simon in GitHub. GitHub supporta il provisioning utenti automatico, che è abilitato per impostazione predefinita. È possibile scoprire più dettagli [qui](github-provisioning-tutorial.md) su come configurare il provisioning utenti automatico.

**Per creare un utente manualmente, seguire questa procedura:**

1. Accedere al sito aziendale di GitHub come amministratore.

2. Fare clic su **Persone**.

    ![Persone](./media/github-tutorial/tutorial_github_config_github_08.png "Persone")

3. Fare clic su **Invite member** (Invita membro).

    ![Invitare utenti](./media/github-tutorial/tutorial_github_config_github_09.png "Invitare utenti")

4. Nella finestra di dialogo **Invite member** (Invita membro) seguire questa procedura:

    a. Nella casella di testo **Email** (Posta elettronica) digitare l'indirizzo di posta elettronica dell'account di Britta Simon.

    ![Invitare persone](./media/github-tutorial/tutorial_github_config_github_10.png "Invitare persone")

    b. Fare clic su **Send Invitation** (Invia invito).

    ![Invitare persone](./media/github-tutorial/tutorial_github_config_github_11.png "Invitare persone")

    > [!NOTE]
    > Il titolare dell'account Azure Active Directory riceverà un messaggio di posta elettronica con un collegamento da selezionare per confermare l'account e attivarlo.

### <a name="assign-the-azure-ad-test-user"></a>Assegnare l'utente test di Azure AD

In questa sezione Britta Simon viene abilitata all'uso di Single Sign-On di Azure con accesso a GitHub.

![Assegnare il ruolo utente][200] 

**Per assegnare Britta Simon a GitHub, seguire questa procedura:**

1. Nel portale di Azure aprire la visualizzazione delle applicazioni e quindi la visualizzazione delle directory e passare ad **Applicazioni aziendali**, quindi fare clic su **Tutte le applicazioni**.

    ![Assegna utente][201]

2. Nell'elenco di applicazioni selezionare **GitHub**.

    ![Collegamento di GitHub nell'elenco delle applicazioni](./media/github-tutorial/tutorial_github_app.png)  

3. Scegliere **Utenti e gruppi** dal menu a sinistra.

    ![Collegamento "Utenti e gruppi"][202]

4. Fare clic sul pulsante **Aggiungi**. Selezionare quindi **Utenti e gruppi** nella finestra di dialogo **Aggiungi assegnazione**.

    ![Riquadro Aggiungi assegnazione][203]

5. Nella finestra di dialogo **Utenti e gruppi** selezionare **Britta Simon** nell'elenco Utenti.

6. Fare clic sul pulsante **Seleziona** nella finestra di dialogo **Utenti e gruppi**.

7. Fare clic sul pulsante **Assegna** nella finestra di dialogo **Aggiungi assegnazione**.

### <a name="test-single-sign-on"></a>Testare l'accesso Single Sign-On

In questa sezione viene testata la configurazione dell'accesso Single Sign-On di Azure AD usando il pannello di accesso.

Quando si fa clic sul riquadro GitHub nel pannello di accesso, si dovrebbe accedere automaticamente all'applicazione GitHub.
Per altre informazioni sul pannello di accesso, vedere [Introduzione al Pannello di accesso](../user-help/active-directory-saas-access-panel-introduction.md).

## <a name="additional-resources"></a>Risorse aggiuntive

* [Elenco di esercitazioni sulla procedura di integrazione delle app SaaS con Azure Active Directory](tutorial-list.md)
* [Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory](../manage-apps/what-is-single-sign-on.md)

<!--Image references-->

[1]: ./media/github-tutorial/tutorial_general_01.png
[2]: ./media/github-tutorial/tutorial_general_02.png
[3]: ./media/github-tutorial/tutorial_general_03.png
[4]: ./media/github-tutorial/tutorial_general_04.png

[100]: ./media/github-tutorial/tutorial_general_100.png

[200]: ./media/github-tutorial/tutorial_general_200.png
[201]: ./media/github-tutorial/tutorial_general_201.png
[202]: ./media/github-tutorial/tutorial_general_202.png
[203]: ./media/github-tutorial/tutorial_general_203.png