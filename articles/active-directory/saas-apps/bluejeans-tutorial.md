---
title: 'Esercitazione: Integrazione di Azure Active Directory con BlueJeans | Documentazione Microsoft'
description: Informazioni su come configurare l'accesso Single Sign-On tra Azure Active Directory e BlueJeans.
services: active-directory
documentationCenter: na
author: jeevansd
manager: mtillman
ms.assetid: dfc634fd-1b55-4ba8-94a8-b8288429b6a9
ms.service: active-directory
ms.component: saas-app-tutorial
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/15/2018
ms.author: jeedes
ms.openlocfilehash: 2ec94217a8df2efaa23eb3cc2c9d5a80e8037615
ms.sourcegitcommit: 1d850f6cae47261eacdb7604a9f17edc6626ae4b
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 08/02/2018
ms.locfileid: "39425988"
---
# <a name="tutorial-azure-active-directory-integration-with-bluejeans"></a>Esercitazione: Integrazione di Azure Active Directory con BlueJeans

Questa esercitazione descrive come integrare BlueJeans con Azure Active Directory (Azure AD).

L'integrazione di BlueJeans con Azure AD offre i vantaggi seguenti:

- È possibile controllare in Azure AD chi può accedere a BlueJeans
- È possibile abilitare gli utenti per l'accesso automatico a BlueJeans (Single Sign-On) con gli account Azure AD personali
- È possibile gestire gli account in un'unica posizione centrale: il portale di Azure.

Per altre informazioni sull'integrazione di app SaaS con Azure AD, vedere [Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory](../manage-apps/what-is-single-sign-on.md).

## <a name="prerequisites"></a>Prerequisiti

Per configurare l'integrazione di Azure AD con BlueJeans, sono necessari gli elementi seguenti:

- Sottoscrizione di Azure AD
- Sottoscrizione di BlueJeans abilitata per l'accesso Single Sign-On

> [!NOTE]
> Non è consigliabile usare un ambiente di produzione per testare i passaggi di questa esercitazione.

A questo scopo, è consigliabile seguire le indicazioni seguenti:

- Non usare l'ambiente di produzione a meno che non sia necessario.
- Se non si dispone di un ambiente di prova di Azure AD, è possibile ottenere una versione di valutazione di un mese [qui](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Descrizione dello scenario
In questa esercitazione viene eseguito il test dell'accesso Single Sign-On di Azure AD in un ambiente di test. Lo scenario descritto in questa esercitazione prevede le due fasi fondamentali seguenti:

1. Aggiunta di BlueJeans dalla raccolta
1. Configurazione e test dell'accesso Single Sign-On di Azure AD

## <a name="adding-bluejeans-from-the-gallery"></a>Aggiunta di BlueJeans dalla raccolta
Per configurare l'integrazione di BlueJeans in Azure AD, è necessario aggiungere BlueJeans dalla raccolta all'elenco di app SaaS gestite.

**Per aggiungere BlueJeans dalla raccolta, seguire questa procedura:**

1. Nel **[portale di Azure](https://portal.azure.com)** fare clic sull'icona di **Azure Active Directory** nel riquadro di spostamento sinistro.

    ![Active Directory][1]

1. Passare ad **Applicazioni aziendali**. Andare quindi a **Tutte le applicazioni**.

    ![APPLICAZIONI][2]

1. Fare clic sul pulsante **Nuova applicazione** nella parte superiore della finestra di dialogo per aggiungere una nuova applicazione.

    ![APPLICAZIONI][3]

1. Nella casella di ricerca digitare **BlueJeans**.

    ![Creazione di un utente test di Azure AD](./media/bluejeans-tutorial/tutorial_bluejeans_search.png)

1. Nel pannello dei risultati selezionare **BlueJeans** e quindi fare clic sul pulsante **Aggiungi** per aggiungere l'applicazione.

    ![Creazione di un utente test di Azure AD](./media/bluejeans-tutorial/tutorial_bluejeans_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Configurazione e test dell'accesso Single Sign-On di Azure AD
In questa sezione viene configurato e testato l'accesso Single Sign-On di Azure AD con BlueJeans usando un utente di test di nome "Britta Simon".

Per il funzionamento dell'accesso Single Sign-On, Azure AD deve conoscere l'utente controparte di BlueJeans corrispondente a un utente di Azure AD. In altre parole, deve essere stabilita una relazione di collegamento tra un utente di Azure AD e l'utente correlato in BlueJeans.

Per stabilire la relazione di collegamento, in BlueJeans assegnare il valore del **nome utente** in Azure AD come valore di **Username** (Nome utente).

Per configurare e testare l'accesso Single Sign-On di Azure AD con BlueJeans, è necessario completare le procedure di base seguenti:

1. **[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** : per abilitare gli utenti all'utilizzo di questa funzionalità.
1. **[Creazione di un utente test di Azure AD](#creating-an-azure-ad-test-user)** : per testare l'accesso Single Sign-On di Azure AD con l'utente Britta Simon.
1. **[Creazione di un utente di test di BlueJeans](#creating-a-bluejeans-test-user)**: per avere una controparte di Britta Simon in BlueJeans collegata alla rappresentazione dell'utente in Azure AD.
1. **[Assegnazione dell'utente test di Azure AD](#assigning-the-azure-ad-test-user)** : per abilitare Britta Simon all'uso dell'accesso Single Sign-On di Azure AD.
1. **[Testing Single Sign-On](#testing-single-sign-on)** : per verificare se la configurazione funziona.

### <a name="configuring-azure-ad-single-sign-on"></a>Configurazione dell'accesso Single Sign-On di Azure AD

In questa sezione viene abilitato l'accesso Single Sign-On di Azure AD nel portale di Azure e viene configurato l'accesso Single Sign-On nell'applicazione BlueJeans.

**Per configurare l'accesso Single Sign-On di Azure AD con BlueJeans, seguire questa procedura:**

1. Nella pagina di integrazione dell'applicazione **BlueJeans** del portale di Azure fare clic su **Single Sign-On**.

    ![Configure Single Sign-On][4]

1. Nella finestra di dialogo **Single Sign-On** selezionare **Accesso basato su SAML** per **Modalità** per abilitare l'accesso Single Sign-On.

    ![Configure Single Sign-On](./media/bluejeans-tutorial/tutorial_bluejeans_samlbase.png)

1. Nella sezione **URL e dominio BlueJeans** seguire questa procedura:

    ![Configure Single Sign-On](./media/bluejeans-tutorial/tutorial_bluejeans_url.png)

    a. Nella casella di testo **URL di accesso** digitare l'URL usando il modello seguente: `https://<companyname>.BlueJeans.com`

    b. Nella casella di testo **Identificatore** digitare l'URL adottando il modello seguente: `https://<companyname>.BlueJeans.com`

    > [!NOTE]
    > Poiché questi non sono i valori reali, Aggiornare questi valori con l'identificatore e l'URL di accesso effettivi. Per ottenere questi valori, contattare il [team di supporto clienti di BlueJeans](https://support.bluejeans.com/contact).

1. Nella sezione **Certificato di firma SAML** fare clic su **Certificato (Base64)** e quindi salvare il file del certificato nel computer.

    ![Configure Single Sign-On](./media/bluejeans-tutorial/tutorial_bluejeans_certificate.png) 

1. Fare clic sul pulsante **Salva** .

    ![Configure Single Sign-On](./media/bluejeans-tutorial/tutorial_general_400.png)

1. Nella sezione **Configurazione di BlueJeans** fare clic su **Configura BlueJeans** per aprire la finestra **Configura accesso**. Copiare l'**URL di disconnessione, l'URL di modifica password e l'URL del servizio Single Sign-On SAML** dalla **sezione di riferimento rapido**.

    ![Configure Single Sign-On](./media/bluejeans-tutorial/tutorial_bluejeans_configure.png) 

1. In un'altra finestra del Web browser accedere al sito aziendale di **BlueJeans** come amministratore.

1. Passare ad **ADMIN \> Group Settings \> Security**.

   ![Amministratore](./media/bluejeans-tutorial/IC785868.png "Amministratore")

1. Nella sezione **Security** seguire questa procedura:

   ![Single Sign-On SAML](./media/bluejeans-tutorial/IC785869.png "Single Sign-On SAML")

   a. Selezionare **SAML Single Sign On**.

   b. Selezionare **Enable automatic provisioning**.

1. Continuare e seguire questa procedura:

    ![Percorso certificato](./media/bluejeans-tutorial/IC785870.png "Percorso certificato")

    a. Fare clic su **Choose File**e quindi caricare il certificato scaricato.

    b. Incollare il valore dell'**URL del servizio Single Sign-On SAML** nella casella di testo **Login Url** (URL di accesso).

    c. Incollare il valore dell'**URL di modifica password** nella casella di testo **Change Password URL** (URL di modifica password).

    d. Incollare il valore dell'**URL di disconnessione** nella casella di testo **Logout URL** (URL disconnessione).

1. Continuare e seguire questa procedura:

    ![Salvare le modifiche](./media/bluejeans-tutorial/IC785874.png "Salvare le modifiche")

    a. Nella casella di testo **User id** (ID utente) digitare `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/name`.

    b. Nella casella di testo **Email** (Posta elettronica) digitare `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/name`.

    c. Fare clic su **Salva modifiche**.

### <a name="creating-an-azure-ad-test-user"></a>Creazione di un utente test di Azure AD
Questa sezione descrive come creare un utente test denominato Britta Simon nel portale di Azure.

![Creare un utente di Azure AD][100]

**Per creare un utente test in Azure AD, eseguire la procedura seguente:**

1. Nel **portale di Azure** fare clic sull'icona di **Azure Active Directory** nel riquadro di spostamento sinistro.

    ![Creazione di un utente test di Azure AD](./media/bluejeans-tutorial/create_aaduser_01.png)

1. Passare a **Utenti e gruppi** e fare clic su **Tutti gli utenti** per visualizzare l'elenco di utenti.

    ![Creazione di un utente test di Azure AD](./media/bluejeans-tutorial/create_aaduser_02.png)

1. Nella parte superiore della finestra di dialogo fare clic su **Aggiungi** per aprire la finestra di dialogo **Utente**.

    ![Creazione di un utente test di Azure AD](./media/bluejeans-tutorial/create_aaduser_03.png)

1. Nella pagina della finestra di dialogo **Utente** seguire questa procedura:

    ![Creazione di un utente test di Azure AD](./media/bluejeans-tutorial/create_aaduser_04.png) 

    a. Nella casella di testo **Nome** digitare **BrittaSimon**.

    b. Nella casella di testo **Nome utente** digitare l'**indirizzo di posta elettronica** di BrittaSimon.

    c. Selezionare **Mostra password** e prendere nota del valore della **Password**.

    d. Fare clic su **Create**(Crea).

### <a name="creating-a-bluejeans-test-user"></a>Creazione di un utente di test di BlueJeans

L'obiettivo di questa sezione consiste nel creare un utente chiamato Britta Simon in BlueJeans. BlueJeans supporta il provisioning utenti automatico, che è abilitato per impostazione predefinita. È possibile scoprire più dettagli [qui](bluejeans-provisioning-tutorial.md) su come configurare il provisioning utenti automatico.

**Per creare un utente manualmente, seguire questa procedura:**

1. Accedere al sito aziendale di **BlueJeans** come amministratore.

1. Passare ad **ADMIN \> Manage Users \> Add User**.

   ![Amministratore](./media/bluejeans-tutorial/IC785877.png "Amministratore")

   >[!IMPORTANT]
   >La scheda **Add User** è disponibile solo se nella scheda **Security** l'opzione **Enable automatic provisioning** è deselezionata. 

1. Nella sezione **Add User** seguire questa procedura:

    ![Aggiungere un utente](./media/bluejeans-tutorial/IC785886.png "Aggiungere un utente")

    a. Nelle caselle di testo **BlueJeans Username**, **Email address**, **BlueJeans Meeting ID**, **Moderator Passcode**, **Full Name** e **Company** digitare il nome utente, l'indirizzo di posta elettronica, l'ID riunione, il passcode moderatore, il nome completo e la società BlueJeans di un account ADD valido di cui si vuole eseguire il provisioning.

    b. Fare clic su **Add User**.

>[!NOTE]
>È possibile usare qualsiasi altro strumento o API di creazione di account utente fornita da BlueJeans per eseguire il provisioning degli account utente di AAD.

### <a name="assigning-the-azure-ad-test-user"></a>Assegnazione dell'utente test di Azure AD

In questa sezione Britta Simon viene abilitata per l'uso dell'accesso Single Sign-On di Azure concedendole l'accesso a BlueJeans.

![Assegna utente][200]

**Per assegnare Britta Simon a BlueJeans, seguire questa procedura:**

1. Nel portale di Azure aprire la visualizzazione delle applicazioni e quindi la visualizzazione delle directory e passare ad **Applicazioni aziendali**, quindi fare clic su **Tutte le applicazioni**.

    ![Assegna utente][201]

1. Nell'elenco delle applicazioni selezionare **BlueJeans**.

    ![Configure Single Sign-On](./media/bluejeans-tutorial/tutorial_bluejeans_app.png)

1. Scegliere **Utenti e gruppi** dal menu a sinistra.

    ![Assegna utente][202]

1. Fare clic sul pulsante **Aggiungi**. Selezionare quindi **Utenti e gruppi** nella finestra di dialogo **Aggiungi assegnazione**.

    ![Assegna utente][203]

1. Nella finestra di dialogo **Utenti e gruppi** selezionare **Britta Simon** nell'elenco Utenti.

1. Fare clic sul pulsante **Seleziona** nella finestra di dialogo **Utenti e gruppi**.

1. Fare clic sul pulsante **Assegna** nella finestra di dialogo **Aggiungi assegnazione**.

### <a name="testing-single-sign-on"></a>Test dell'accesso Single Sign-On

In questa sezione viene testata la configurazione dell'accesso Single Sign-On di Azure AD usando il pannello di accesso.

Quando si fa clic sul riquadro BlueJeans nel pannello di accesso, dovrebbe essere visualizzata la pagina di accesso dell'applicazione BlueJeans.
Per altre informazioni sul pannello di accesso, vedere [Introduzione al Pannello di accesso](../user-help/active-directory-saas-access-panel-introduction.md). 

## <a name="additional-resources"></a>Risorse aggiuntive

* [Elenco di esercitazioni sulla procedura di integrazione delle app SaaS con Azure Active Directory](tutorial-list.md)
* [Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory](../manage-apps/what-is-single-sign-on.md)
* [Configura provisioning utenti](bluejeans-provisioning-tutorial.md)

<!--Image references-->

[1]: ./media/bluejeans-tutorial/tutorial_general_01.png
[2]: ./media/bluejeans-tutorial/tutorial_general_02.png
[3]: ./media/bluejeans-tutorial/tutorial_general_03.png
[4]: ./media/bluejeans-tutorial/tutorial_general_04.png

[100]: ./media/bluejeans-tutorial/tutorial_general_100.png

[200]: ./media/bluejeans-tutorial/tutorial_general_200.png
[201]: ./media/bluejeans-tutorial/tutorial_general_201.png
[202]: ./media/bluejeans-tutorial/tutorial_general_202.png
[203]: ./media/bluejeans-tutorial/tutorial_general_203.png
