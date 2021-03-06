---
title: 'Esercitazione: Integrazione di Azure Active Directory con Yodeck | Microsoft Docs'
description: Informazioni su come configurare l'accesso Single Sign-On tra Azure Active Directory e Yodeck.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: b2c8dccb-eeb0-4f4d-a24d-8320631ce819
ms.service: active-directory
ms.component: saas-app-tutorial
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/20/2018
ms.author: jeedes
ms.openlocfilehash: b017efd2c170f543041dcb35a3a3d040389d1dac
ms.sourcegitcommit: 1d850f6cae47261eacdb7604a9f17edc6626ae4b
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 08/02/2018
ms.locfileid: "39436795"
---
# <a name="tutorial-azure-active-directory-integration-with-yodeck"></a>Esercitazione: Integrazione di Azure Active Directory con Yodeck

Questa esercitazione descrive come integrare Yodeck con Azure Active Directory (Azure AD).

L'integrazione di Yodeck con Azure AD offre i vantaggi seguenti:

- È possibile controllare in Azure AD chi può accedere a Yodeck.
- È possibile abilitare gli utenti per l'accesso automatico a Yodeck (Single Sign-On) con i propri account Azure AD.
- È possibile gestire gli account in un'unica posizione centrale: il portale di Azure.

Per altre informazioni sull'integrazione di app SaaS con Azure AD, vedere [Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory](../manage-apps/what-is-single-sign-on.md).

## <a name="prerequisites"></a>Prerequisiti

Per configurare l'integrazione di Azure AD con Yodeck, sono necessari gli elementi seguenti:

- Sottoscrizione di Azure AD
- Sottoscrizione di Yodeck abilitata per l'accesso Single Sign-On

> [!NOTE]
> Non è consigliabile usare un ambiente di produzione per testare i passaggi di questa esercitazione.

A questo scopo, è consigliabile seguire le indicazioni seguenti:

- Non usare l'ambiente di produzione a meno che non sia necessario.
- Se non è disponibile un ambiente di valutazione di Azure AD, è possibile [ottenere una versione di valutazione di un mese](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Descrizione dello scenario
In questa esercitazione viene eseguito il test dell'accesso Single Sign-On di Azure AD in un ambiente di test. Lo scenario descritto in questa esercitazione prevede le due fasi fondamentali seguenti:

1. Aggiunta di Yodeck dalla raccolta
1. Configurazione e test dell'accesso Single Sign-On di Azure AD

## <a name="adding-yodeck-from-the-gallery"></a>Aggiunta di Yodeck dalla raccolta
Per configurare l'integrazione di Yodeck in Azure AD, è necessario aggiungere Yodeck dalla raccolta al proprio elenco di app SaaS gestite.

**Per aggiungere Yodeck dalla raccolta, seguire questa procedura:**

1. Nel **[portale di Azure](https://portal.azure.com)** fare clic sull'icona di **Azure Active Directory** nel riquadro di spostamento sinistro. 

    ![Pulsante Azure Active Directory][1]

1. Passare ad **Applicazioni aziendali**. Andare quindi a **Tutte le applicazioni**.

    ![Pannello Applicazioni aziendali][2]
    
1. Fare clic sul pulsante **Nuova applicazione** nella parte superiore della finestra di dialogo per aggiungere una nuova applicazione.

    ![Pulsante Nuova applicazione][3]

1. Nella casella di ricerca digitare **Yodeck**, selezionare **Yodeck** nel pannello dei risultati e quindi fare clic sul pulsante **Aggiungi** per aggiungere l'applicazione.

    ![Yodeck nell'elenco risultati](./media/yodeck-tutorial/tutorial_yodeck_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a>Configurare e testare l'accesso Single Sign-On di Azure AD

In questa sezione viene configurato e testato l'accesso Single Sign-On di Azure AD con Yodeck usando un utente di test di nome "Britta Simon".

Per il funzionamento dell'accesso Single Sign-On, Azure AD deve conoscere qual è l'utente di Yodeck che corrisponde a un utente di Azure AD. In altre parole, deve essere stabilita una relazione di collegamento tra un utente di Azure AD e l'utente correlato in Yodeck.

Per configurare e testare l'accesso Single Sign-On di Azure AD con Yodeck, è necessario completare i blocchi predefiniti seguenti:

1. **[Configurare l'accesso Single Sign-On di Azure AD](#configure-azure-ad-single-sign-on)**: per consentire agli utenti di usare questa funzionalità.
1. **[Creare un utente di test di Azure AD](#create-an-azure-ad-test-user)**: per testare l'accesso Single Sign-On di Azure AD con l'utente Britta Simon.
1. **[Creare un utente di test di Yodeck](#create-a-yodeck-test-user)**: per avere una controparte di Britta Simon in Yodeck collegata alla rappresentazione dell'utente in Azure AD.
1. **[Assegnare l'utente test di Azure AD](#assign-the-azure-ad-test-user)**: per abilitare Britta Simon all'uso dell'accesso Single Sign-On di Azure AD.
1. **[Testare l'accesso Single Sign-On](#test-single-sign-on)** per verificare se la configurazione funziona.

### <a name="configure-azure-ad-single-sign-on"></a>Configurare l'accesso Single Sign-On di Azure AD

In questa sezione viene abilitato l'accesso Single Sign-On di Azure AD nel portale di Azure e viene configurato l'accesso Single Sign-On nell'applicazione Yodeck.

**Per configurare l'accesso Single Sign-On di Azure AD con Yodeck, seguire questa procedura:**

1. Nella pagina di integrazione dell'applicazione **Yodeck** del portale di Azure fare clic su **Single Sign-On**.

    ![Collegamento Configura accesso Single Sign-On][4]

1. Nella finestra di dialogo **Single Sign-On** selezionare **Accesso basato su SAML** per **Modalità** per abilitare l'accesso Single Sign-On.

    ![Finestra di dialogo Single Sign-On](./media/yodeck-tutorial/tutorial_yodeck_samlbase.png)

1. Nella sezione **URL e dominio Yodeck** seguire questa procedura se si vuole configurare l'applicazione in modalità avviata da **IDP**:

    ![Informazioni su URL e dominio per l'accesso Single Sign-On di Yodeck](./media/yodeck-tutorial/tutorial_yodeck_url.png)

    Nella casella di testo **Identificatore (ID entità)** digitare l'URL: `https://app.yodeck.com/api/v1/account/metadata/`

1. Selezionare **Mostra impostazioni URL avanzate** e seguire questa procedura se si vuole configurare l'applicazione in modalità avviata da **SP**:

    ![Informazioni su URL e dominio per l'accesso Single Sign-On di Yodeck](./media/yodeck-tutorial/tutorial_yodeck_url1.png)

    Nella casella di testo **URL accesso** digitare l'URL: `https://app.yodeck.com/login`

1. Nella sezione **Certificato di firma SAML** fare clic sul pulsante Copia per copiare l'**URL dei metadati di federazione dell'app** e incollarlo nel Blocco note.

    ![Collegamento di download del certificato](./media/yodeck-tutorial/tutorial_yodeck_certificate.png)

1. Fare clic sul pulsante **Salva** .

    ![Pulsante Salva per la configurazione dell'accesso Single Sign-On](./media/yodeck-tutorial/tutorial_general_400.png)
    
1. In un'altra finestra del Web browser accedere al sito aziendale di Yodeck come amministratore.

1. Fare clic sull'opzione **User Settings** (Impostazioni utente) nell'angolo in alto a destra della pagina e selezionare **Account Settings** (Impostazioni account).

    ![Configurazione di Yodeck](./media/yodeck-tutorial/configure1.png)

1. Selezionare **SAML** e seguire questa procedura:

    ![Configurazione di Yodeck](./media/yodeck-tutorial/configure2.png)

    a. Selezionare **Import from URL** (Importa dall'URL).

    b. Nella casella di testo **URL** incollare il valore dell'**URL dei metadati di federazione dell'app** copiato dal portale di Azure e fare clic su **Import** (Importa).
    
    c. Dopo l'importazione dell'**URL dei metadati di federazione dell'app**, gli altri campi vengono automaticamente popolati.

    d. Fare clic su **Save**.

### <a name="create-an-azure-ad-test-user"></a>Creare un utente test di Azure AD

Questa sezione descrive come creare un utente test denominato Britta Simon nel portale di Azure.

   ![Creare un utente test di Azure AD][100]

**Per creare un utente test in Azure AD, eseguire la procedura seguente:**

1. Nel portale di Azure fare clic sul pulsante **Azure Active Directory** nel riquadro sinistro.

    ![Pulsante Azure Active Directory](./media/yodeck-tutorial/create_aaduser_01.png)

1. Per visualizzare l'elenco di utenti, passare a **Utenti e gruppi** e quindi fare clic su **Tutti gli utenti**.

    ![Collegamenti "Utenti e gruppi" e "Tutti gli utenti"](./media/yodeck-tutorial/create_aaduser_02.png)

1. Per aprire la finestra di dialogo **Utente** fare clic su **Aggiungi** nella parte superiore della finestra di dialogo **Tutti gli utenti**.

    ![Pulsante Aggiungi](./media/yodeck-tutorial/create_aaduser_03.png)

1. Nella finestra di dialogo **Utente** seguire questa procedura:

    ![Finestra di dialogo Utente](./media/yodeck-tutorial/create_aaduser_04.png)

    a. Nella casella **Nome** digitare **BrittaSimon**.

    b. Nella casella **Nome utente** digitare l'indirizzo di posta elettronica dell'utente Britta Simon.

    c. Selezionare la casella di controllo **Mostra password** e quindi prendere nota del valore visualizzato nella casella **Password**.

    d. Fare clic su **Create**(Crea).
 
### <a name="create-a-yodeck-test-user"></a>Creare un utente di test di Yodeck

Per consentire agli utenti di Azure AD di accedere a Yodeck, è necessario effettuarne il provisioning in Yodeck.
Nel caso di Yodeck, il provisioning è un'attività manuale.

**Per eseguire il provisioning di un account utente, seguire questa procedura:**

1. Accedere al sito aziendale di Yodeck come amministratore.

1. Fare clic sull'opzione **User Settings** (Impostazioni utente) nell'angolo in alto a destra della pagina e selezionare **Users** (Utenti).

    ![Aggiungere un dipendente](./media/yodeck-tutorial/user1.png)

1. Fare clic su **+User** (+Utenti) per aprire la scheda **User Details** (Dettagli utente).

    ![Aggiungere un dipendente](./media/yodeck-tutorial/user2.png)

1. Nella finestra di dialogo **Dettagli utente** seguire questa procedura:

    ![Aggiungere un dipendente](./media/yodeck-tutorial/user3.png)

    a. Digitare il nome dell'utente, ad esempio **Britta**, nella casella di testo **First Name** (Nome).

    b. Nella casella di testo **Last name** (Cognome) digitare il cognome dell'utente, ad esempio **Simon**.

    c. Nella casella di testo **Email** digitare l'indirizzo di posta elettronica dell'utente, ad esempio **brittasimon@contoso.com**.

    d. Selezionare l'opzione **Account Permissions** (Autorizzazioni account) appropriata in base ai requisiti aziendali.
    
    e. Fare clic su **Save**.

### <a name="assign-the-azure-ad-test-user"></a>Assegnare l'utente test di Azure AD

In questa sezione Britta Simon viene abilitata per l'uso dell'accesso Single Sign-On di Azure concedendole l'accesso a Yodeck.

![Assegnare il ruolo utente][200]

**Per assegnare Britta Simon a Yodeck, seguire questa procedura:**

1. Nel portale di Azure aprire la visualizzazione delle applicazioni e quindi la visualizzazione delle directory e passare ad **Applicazioni aziendali**, quindi fare clic su **Tutte le applicazioni**.

    ![Assegna utente][201]

1. Nell'elenco delle applicazioni selezionare **Yodeck**.

    ![Collegamento di Yodeck nell'elenco delle applicazioni](./media/yodeck-tutorial/tutorial_yodeck_app.png)  

1. Scegliere **Utenti e gruppi** dal menu a sinistra.

    ![Collegamento "Utenti e gruppi"][202]

1. Fare clic sul pulsante **Aggiungi**. Selezionare quindi **Utenti e gruppi** nella finestra di dialogo **Aggiungi assegnazione**.

    ![Riquadro Aggiungi assegnazione][203]

1. Nella finestra di dialogo **Utenti e gruppi** selezionare **Britta Simon** nell'elenco Utenti.

1. Fare clic sul pulsante **Seleziona** nella finestra di dialogo **Utenti e gruppi**.

1. Fare clic sul pulsante **Assegna** nella finestra di dialogo **Aggiungi assegnazione**.
    
### <a name="test-single-sign-on"></a>Testare l'accesso Single Sign-On

In questa sezione viene testata la configurazione dell'accesso Single Sign-On di Azure AD usando il pannello di accesso.

Quando si fa clic sul riquadro Yodeck nel pannello di accesso, si dovrebbe accedere automaticamente all'applicazione Yodeck.
Per altre informazioni sul pannello di accesso, vedere [Introduzione al Pannello di accesso](../user-help/active-directory-saas-access-panel-introduction.md). 

## <a name="additional-resources"></a>Risorse aggiuntive

* [Elenco di esercitazioni sulla procedura di integrazione delle app SaaS con Azure Active Directory](tutorial-list.md)
* [Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory](../manage-apps/what-is-single-sign-on.md)



<!--Image references-->

[1]: ./media/yodeck-tutorial/tutorial_general_01.png
[2]: ./media/yodeck-tutorial/tutorial_general_02.png
[3]: ./media/yodeck-tutorial/tutorial_general_03.png
[4]: ./media/yodeck-tutorial/tutorial_general_04.png

[100]: ./media/yodeck-tutorial/tutorial_general_100.png

[200]: ./media/yodeck-tutorial/tutorial_general_200.png
[201]: ./media/yodeck-tutorial/tutorial_general_201.png
[202]: ./media/yodeck-tutorial/tutorial_general_202.png
[203]: ./media/yodeck-tutorial/tutorial_general_203.png

