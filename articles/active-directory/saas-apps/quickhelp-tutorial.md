---
title: 'Esercitazione: Integrazione di Azure Active Directory con QuickHelp | Microsoft Docs'
description: Informazioni su come configurare l'accesso Single Sign-On tra Azure Active Directory e QuickHelp.
services: active-directory
documentationCenter: na
author: jeevansd
manager: mtillman
ms.assetid: 655c9ad3-2076-4e2c-8e47-9ed3bf04be56
ms.service: active-directory
ms.component: saas-app-tutorial
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/27/2017
ms.author: jeedes
ms.openlocfilehash: c99be60301085dddfd5c658ee1eed81b88238e54
ms.sourcegitcommit: 1d850f6cae47261eacdb7604a9f17edc6626ae4b
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 08/02/2018
ms.locfileid: "39421592"
---
# <a name="tutorial-azure-active-directory-integration-with-quickhelp"></a>Esercitazione: Integrazione di Azure Active Directory con QuickHelp

Questa esercitazione descrive come integrare QuickHelp con Azure Active Directory (Azure AD).

L'integrazione di QuickHelp con Azure AD offre i vantaggi seguenti:

- È possibile controllare in Azure AD chi può accedere a QuickHelp.
- È possibile abilitare gli utenti per l'accesso automatico a QuickHelp (Single Sign-On) con i propri account Azure AD.
- È possibile gestire gli account in un'unica posizione centrale: il portale di Azure.

Per altre informazioni sull'integrazione di app SaaS con Azure AD, vedere [Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory](../manage-apps/what-is-single-sign-on.md).

## <a name="prerequisites"></a>Prerequisiti

Per configurare l'integrazione di Azure AD con QuickHelp, sono necessari gli elementi seguenti:

- Sottoscrizione di Azure AD
- Sottoscrizione di QuickHelp abilitata per l'accesso Single Sign-On

> [!NOTE]
> Non è consigliabile usare un ambiente di produzione per testare i passaggi di questa esercitazione.

A questo scopo, è consigliabile seguire le indicazioni seguenti:

- Non usare l'ambiente di produzione a meno che non sia necessario.
- Se non si dispone di un ambiente di prova di Azure AD, è possibile ottenere una versione di valutazione di un mese [qui](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Descrizione dello scenario
In questa esercitazione viene eseguito il test dell'accesso Single Sign-On di Azure AD in un ambiente di test. Lo scenario descritto in questa esercitazione prevede le due fasi fondamentali seguenti:

1. Aggiunta di QuickHelp dalla raccolta
1. Configurazione e test dell'accesso Single Sign-On di Azure AD

## <a name="adding-quickhelp-from-the-gallery"></a>Aggiunta di QuickHelp dalla raccolta
Per configurare l'integrazione di QuickHelp in Azure AD, è necessario aggiungere QuickHelp dalla raccolta al proprio elenco di app SaaS gestite.

**Per aggiungere QuickHelp dalla raccolta, seguire questa procedura:**

1. Nel **[portale di Azure](https://portal.azure.com)** fare clic sull'icona di **Azure Active Directory** nel riquadro di spostamento sinistro. 

    ![Active Directory][1]

1. Passare ad **Applicazioni aziendali**. Andare quindi a **Tutte le applicazioni**.

    ![APPLICAZIONI][2]
    
1. Fare clic sul pulsante **Nuova applicazione** nella parte superiore della finestra di dialogo per aggiungere una nuova applicazione.

    ![APPLICAZIONI][3]

1. Nella casella di ricerca digitare **QuickHelp**.

    ![Creazione di un utente test di Azure AD](./media/quickhelp-tutorial/tutorial_quickhelp_search.png)

1. Nel pannello dei risultati selezionare **QuickHelp** e quindi fare clic sul pulsante **Aggiungi** per aggiungere l'applicazione.

    ![Creazione di un utente test di Azure AD](./media/quickhelp-tutorial/tutorial_quickhelp_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Configurazione e test dell'accesso Single Sign-On di Azure AD
In questa sezione viene configurato e testato l'accesso Single Sign-On di Azure AD con QuickHelp in base a un utente di test di nome "Britta Simon".

Per il funzionamento dell'accesso Single Sign-On, Azure AD deve conoscere qual è l'utente di QuickHelp che corrisponde a un utente di Azure AD. In altre parole, deve essere stabilita una relazione di collegamento tra un utente di Azure AD e l'utente correlato in QuickHelp.

Per stabilire la relazione di collegamento, in QuickHelp assegnare il valore di **nome utente** in Azure AD come valore di **Username**.

Per configurare e testare l'accesso Single Sign-On di Azure AD con QuickHelp, è necessario completare i blocchi predefiniti seguenti:

1. **[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** : per abilitare gli utenti all'utilizzo di questa funzionalità.
1. **[Creazione di un utente test di Azure AD](#creating-an-azure-ad-test-user)** : per testare l'accesso Single Sign-On di Azure AD con l'utente Britta Simon.
1. **[Creazione di un utente di test di QuickHelp](#creating-a-quickhelp-test-user)**: per avere una controparte di Britta Simon in QuickHelp collegata alla rappresentazione dell'utente in Azure AD.
1. **[Assegnazione dell'utente test di Azure AD](#assigning-the-azure-ad-test-user)** : per abilitare Britta Simon all'uso dell'accesso Single Sign-On di Azure AD.
1. **[Testing Single Sign-On](#testing-single-sign-on)** : per verificare se la configurazione funziona.

### <a name="configuring-azure-ad-single-sign-on"></a>Configurazione dell'accesso Single Sign-On di Azure AD

In questa sezione viene abilitato l'accesso Single Sign-On di Azure AD nel portale di Azure e viene configurato l'accesso Single Sign-On nell'applicazione QuickHelp.

**Per configurare Single Sign-On di Azure AD con QuickHelp, seguire questa procedura:**

1. Nella pagina di integrazione dell'applicazione **QuickHelp** del portale di Azure fare clic su **Single Sign-On**.

    ![Configure Single Sign-On][4]

1. Nella finestra di dialogo **Single Sign-On** selezionare **Accesso basato su SAML** per **Modalità** per abilitare l'accesso Single Sign-On.
 
    ![Configure Single Sign-On](./media/quickhelp-tutorial/tutorial_quickhelp_samlbase.png)

1. Nella sezione **URL e dominio QuickHelp** seguire questa procedura:

    ![Configure Single Sign-On](./media/quickhelp-tutorial/tutorial_quickhelp_url.png)

    a. Nella casella di testo **URL di accesso** digitare l'URL usando il modello seguente: `https://quickhelp.com/<ROUTEURL>`

    b. Nella casella di testo **Identificatore** digitare un URL: `https://auth.quickhelp.com`

    > [!NOTE] 
    > Poiché il valore dell'URL di accesso non è reale, è necessario aggiornare questo valore con l'URL di accesso effettivo. Per ottenere il valore, contattare l'amministratore QuickHelp dell'organizzazione o il BrainStorm Client Success Manager.
 
1. Nella sezione **Certificato di firma SAML** fare clic su **XML di metadati** e quindi salvare il file dei metadati nel computer.

    ![Configure Single Sign-On](./media/quickhelp-tutorial/tutorial_quickhelp_certificate.png) 

1. Fare clic sul pulsante **Salva** .

    ![Configure Single Sign-On](./media/quickhelp-tutorial/tutorial_general_400.png) 

1. Accedere al sito aziendale di QuickHelp come amministratore.

1. Nel menu in alto fare clic su **Admin**.
   
    ![Configure Single Sign-On][21]

1. Nel menu **QuickHelp Admin** fare clic su **Settings**.
   
    ![Configure Single Sign-On][22]

1. Fare clic su **Authentication Settings**.

1. Nella pagina **Authentication Settings** seguire questa procedura:
   
    ![Configure Single Sign-On][23]
   
    a. Come **tipo SSO**, selezionare **WSFederation**.
   
    b. Per caricare il file dei metadati di Azure scaricato, fare clic su **Sfoglia**, passare al file e quindi fare clic su **Carica metadati**.
   
    c. Nella casella di testo **Email** (Posta elettronica) digitare `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress`.
   
    d. Nella casella di testo **Nome** digitare `type http://schemas.xmlsoap.org/ws/2005/05/identity/claims/givenname`.
   
    e. Nella casella di testo **Cognome** digitare `type http://schemas.xmlsoap.org/ws/2005/05/identity/claims/surname`.
   
    f. Nella **barra delle azioni**, fare clic su **Salva**.

### <a name="creating-an-azure-ad-test-user"></a>Creazione di un utente test di Azure AD
Questa sezione descrive come creare un utente test denominato Britta Simon nel portale di Azure.

![Creare un utente di Azure AD][100]

**Per creare un utente test in Azure AD, eseguire la procedura seguente:**

1. Nel **portale di Azure** fare clic sull'icona di **Azure Active Directory** nel riquadro di spostamento sinistro.

    ![Creazione di un utente test di Azure AD](./media/quickhelp-tutorial/create_aaduser_01.png) 

1. Passare a **Utenti e gruppi** e fare clic su **Tutti gli utenti** per visualizzare l'elenco di utenti.
    
    ![Creazione di un utente test di Azure AD](./media/quickhelp-tutorial/create_aaduser_02.png) 

1. Nella parte superiore della finestra di dialogo fare clic su **Aggiungi** per aprire la finestra di dialogo **Utente**.
 
    ![Creazione di un utente test di Azure AD](./media/quickhelp-tutorial/create_aaduser_03.png) 

1. Nella pagina della finestra di dialogo **Utente** seguire questa procedura:
 
    ![Creazione di un utente test di Azure AD](./media/quickhelp-tutorial/create_aaduser_04.png) 

    a. Nella casella di testo **Nome** digitare **BrittaSimon**.

    b. Nella casella di testo **Nome utente** digitare l'**indirizzo di posta elettronica** di BrittaSimon.

    c. Selezionare **Mostra password** e prendere nota del valore della **Password**.

    d. Fare clic su **Create**(Crea).
 
### <a name="creating-a-quickhelp-test-user"></a>Creazione di un utente test di QuickHelp

Questa sezione descrive come creare un utente chiamato Britta Simon in QuickHelp.
Per il funzionamento dell'accesso Single Sign-On, Azure AD deve conoscere qual è l'utente di QuickHelp che corrisponde a un utente di Azure AD. In altre parole, deve essere stabilita una relazione di collegamento tra un utente di Azure AD e l'utente correlato in QuickHelp.

QuickHelp supporta il provisioning just-in-time. Ciò significa che, se necessario, un account utente viene creato automaticamente in QuickHelp e che l'account è collegato all'account di Azure AD.

Non è necessario alcun intervento dell'utente in questa sezione.

### <a name="assigning-the-azure-ad-test-user"></a>Assegnazione dell'utente test di Azure AD

In questa sezione Britta Simon viene abilitata per l'uso dell'accesso Single Sign-On di Azure concedendo l'accesso a QuickHelp.

![Assegna utente][200] 

**Per assegnare Britta Simon a QuickHelp, seguire questa procedura:**

1. Nel portale di Azure aprire la visualizzazione delle applicazioni e quindi la visualizzazione delle directory e passare ad **Applicazioni aziendali**, quindi fare clic su **Tutte le applicazioni**.

    ![Assegna utente][201] 

1. Nell'elenco delle applicazioni selezionare **QuickHelp**.

    ![Configure Single Sign-On](./media/quickhelp-tutorial/tutorial_quickhelp_app.png) 

1. Scegliere **Utenti e gruppi** dal menu a sinistra.

    ![Assegna utente][202] 

1. Fare clic sul pulsante **Aggiungi**. Selezionare quindi **Utenti e gruppi** nella finestra di dialogo **Aggiungi assegnazione**.

    ![Assegna utente][203]

1. Nella finestra di dialogo **Utenti e gruppi** selezionare **Britta Simon** nell'elenco Utenti.

1. Fare clic sul pulsante **Seleziona** nella finestra di dialogo **Utenti e gruppi**.

1. Fare clic sul pulsante **Assegna** nella finestra di dialogo **Aggiungi assegnazione**.
    
### <a name="testing-single-sign-on"></a>Test dell'accesso Single Sign-On

Questa sezione descrive come testare la configurazione dell'accesso Single Sign-On di Azure AD usando il pannello di accesso.  

Quando si fa clic sul riquadro QuickHelp nel pannello di accesso, si dovrebbe accedere automaticamente all'applicazione QuickHelp.


## <a name="additional-resources"></a>Risorse aggiuntive

* [Elenco di esercitazioni sulla procedura di integrazione delle app SaaS con Azure Active Directory](tutorial-list.md)
* [Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory](../manage-apps/what-is-single-sign-on.md)



<!--Image references-->

[1]: ./media/quickhelp-tutorial/tutorial_general_01.png
[2]: ./media/quickhelp-tutorial/tutorial_general_02.png
[3]: ./media/quickhelp-tutorial/tutorial_general_03.png
[4]: ./media/quickhelp-tutorial/tutorial_general_04.png

[100]: ./media/quickhelp-tutorial/tutorial_general_100.png

[200]: ./media/quickhelp-tutorial/tutorial_general_200.png
[201]: ./media/quickhelp-tutorial/tutorial_general_201.png
[202]: ./media/quickhelp-tutorial/tutorial_general_202.png
[203]: ./media/quickhelp-tutorial/tutorial_general_203.png
[21]: ./media/quickhelp-tutorial/tutorial_quickhelp_05.png
[22]: ./media/quickhelp-tutorial/tutorial_quickhelp_06.png
[23]: ./media/quickhelp-tutorial/tutorial_quickhelp_07.png
