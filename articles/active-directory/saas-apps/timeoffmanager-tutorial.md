---
title: 'Esercitazione: Integrazione di Azure Active Directory con TimeOffManager | Microsoft Docs'
description: Informazioni su come configurare l'accesso Single Sign-On tra Azure Active Directory e TimeOffManager.
services: active-directory
documentationCenter: na
author: jeevansd
manager: mtillman
ms.reviewer: joflore
ms.assetid: 3685912f-d5aa-4730-ab58-35a088fc1cc3
ms.service: active-directory
ms.component: saas-app-tutorial
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/27/2017
ms.author: jeedes
ms.openlocfilehash: e7f0f6bb778dedeea61b74b5ca0c2edbadd5279b
ms.sourcegitcommit: 1d850f6cae47261eacdb7604a9f17edc6626ae4b
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 08/02/2018
ms.locfileid: "39430288"
---
# <a name="tutorial-azure-active-directory-integration-with-timeoffmanager"></a>Esercitazione: Integrazione di Azure Active Directory con TimeOffManager

Questa esercitazione descrive come integrare TimeOffManager con Azure Active Directory (Azure AD).

L'integrazione di TimeOffManager con Azure AD offre i vantaggi seguenti:

- È possibile controllare in Azure AD chi può accedere a TimeOffManager
- È possibile abilitare gli utenti per l'accesso automatico a TimeOffManager (Single Sign-On) con gli account Azure AD personali
- È possibile gestire gli account in un'unica posizione centrale: il portale di Azure.

Per altre informazioni sull'integrazione di app SaaS con Azure AD, vedere [Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory](../manage-apps/what-is-single-sign-on.md).

## <a name="prerequisites"></a>Prerequisiti

Per configurare l'integrazione di Azure AD con TimeOffManager, sono necessari gli elementi seguenti:

- Sottoscrizione di Azure AD
- Sottoscrizione di TimeOffManager abilitata per l'accesso Single Sign-On

> [!NOTE]
> Non è consigliabile usare un ambiente di produzione per testare i passaggi di questa esercitazione.

A questo scopo, è consigliabile seguire le indicazioni seguenti:

- Non usare l'ambiente di produzione a meno che non sia necessario.
- Se non è disponibile un ambiente di valutazione di Azure AD, è possibile [ottenere una versione di valutazione di un mese](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Descrizione dello scenario
In questa esercitazione viene eseguito il test dell'accesso Single Sign-On di Azure AD in un ambiente di test. Lo scenario descritto in questa esercitazione prevede le due fasi fondamentali seguenti:

1. Aggiungere TimeOffManager dalla raccolta
1. Configurare e testare l'accesso Single Sign-On di Azure AD

## <a name="add-timeoffmanager-from-the-gallery"></a>Aggiungere TimeOffManager dalla raccolta
Per configurare l'integrazione di TimeOffManager in Azure AD, è necessario aggiungere TimeOffManager dalla raccolta all'elenco di app SaaS gestite.

**Per aggiungere TimeOffManager dalla raccolta, seguire questa procedura:**

1. Nel **[portale di Azure](https://portal.azure.com)** fare clic sull'icona di **Azure Active Directory** nel riquadro di spostamento sinistro. 

    ![Active Directory][1]

1. Passare ad **Applicazioni aziendali**. Andare quindi a **Tutte le applicazioni**.

    ![APPLICAZIONI][2]
    
1. Fare clic sul pulsante **Nuova applicazione** nella parte superiore della finestra di dialogo per aggiungere una nuova applicazione.

    ![APPLICAZIONI][3]

1. Nella casella di ricerca digitare **TimeOffManager**, selezionare **TimeOffManager** dal pannello dei risultati e quindi fare clic sul pulsante **Aggiungi** per aggiungere l'applicazione.

    ![Aggiungere dalla raccolta](./media/timeoffmanager-tutorial/tutorial_timeoffmanager_addfromgallery.png)

##  <a name="configure-and-test-azure-ad-single-sign-on"></a>Configurare e testare l'accesso Single Sign-On di Azure AD
In questa sezione viene configurato e testato l'accesso Single Sign-On di Azure AD con TimeOffManager usando un utente di test di nome "Britta Simon".

Per il funzionamento dell'accesso Single Sign-On, Azure AD deve conoscere l'utente controparte di TimeOffManager corrispondente a un utente di Azure AD. In altre parole, deve essere stabilita una relazione di collegamento tra un utente di Azure AD e l'utente correlato in TimeOffManager.

Per stabilire la relazione di collegamento, in TimeOffManager assegnare il valore del **nome utente** in Azure AD come valore di **Username** (Nome utente).

Per configurare e testare l'accesso Single Sign-On di Azure AD con TimeOffManager, è necessario completare le procedure di base seguenti:

1. **[Configurare l'accesso Single Sign-On di Azure AD](#configure-azure-ad-single-sign-on)**: per consentire agli utenti di usare questa funzionalità.
1. **[Creare un utente di test di Azure AD](#create-an-azure-ad-test-user)**: per testare l'accesso Single Sign-On di Azure AD con l'utente Britta Simon.
1. **[Creare un utente di test di TimeOffManager](#create-a-timeoffmanager-test-user)**: per avere una controparte di Britta Simon in TimeOffManager collegata alla rappresentazione dell'utente in Azure AD.
1. **[Assegnare l'utente test di Azure AD](#assign-the-azure-ad-test-user)**: per abilitare Britta Simon all'uso dell'accesso Single Sign-On di Azure AD.
1. **[Testare l'accesso Single Sign-On](#test-single-sign-on)**: per verificare se la configurazione funziona.

### <a name="configure-azure-ad-single-sign-on"></a>Configurare l'accesso Single Sign-On di Azure AD

In questa sezione viene abilitato l'accesso Single Sign-On di Azure AD nel portale di Azure e viene configurato l'accesso Single Sign-On nell'applicazione TimeOffManager.

**Per configurare l'accesso Single Sign-On di Azure AD con TimeOffManager, seguire questa procedura:**

1. Nella pagina di integrazione dell'applicazione **TimeOffManager** del portale di Azure fare clic su **Single Sign-On**.

    ![Configure Single Sign-On][4]

1. Nella finestra di dialogo **Single Sign-On** selezionare **Accesso basato su SAML** per **Modalità** per abilitare l'accesso Single Sign-On.
 
    ![Accesso basato su SAML](./media/timeoffmanager-tutorial/tutorial_timeoffmanager_samlbase.png)

1. Nella sezione **URL e dominio TimeOffManager** seguire questa procedura:

     ![Sezione URL e dominio TimeOffManager](./media/timeoffmanager-tutorial/tutorial_timeoffmanager_url.png)

    Nella casella di testo **URL di risposta** digitare l'URL usando il modello seguente: `https://www.timeoffmanager.com/cpanel/sso/consume.aspx?company_id=<companyid>`

    > [!NOTE] 
    > Poiché non è reale, è necessario aggiornare questo valore con l'URL di risposta effettivo. È possibile ottenere questo valore dalla **pagina delle impostazioni per l'accesso Single Sign-On**, illustrata più avanti nell'esercitazione, oppure contattando il [team di supporto di TimeOffManager](https://www.purelyhr.com/contact-us).
 
1. Nella sezione **Certificato di firma SAML** fare clic su **Certificato (Base64)** e quindi salvare il file del certificato nel computer.

    ![Sezione Certificato di firma SAML](./media/timeoffmanager-tutorial/tutorial_timeoffmanager_certificate.png) 

1. Questa sezione descrive come consentire agli utenti di eseguire l'autenticazione a TimeOffManger con il proprio account in Azure AD usando la federazione basata sul protocollo SAML.
    
    L'applicazione TimeOffManger si aspetta che le asserzioni SAML abbiano un formato specifico, quindi è necessario aggiungere mapping di attributi personalizzati alla configurazione degli attributi del token SAML. La schermata seguente illustra un esempio relativo a questa operazione.

    ![attributi token SAML](./media/timeoffmanager-tutorial/tutorial_timeoffmanager_attrb.png "attributi token SAML")
    
    | Nome attributo | Valore attributo |
    | --- | --- |
    | Firstname |User.givenname |
    | Lastname |User.surname |
    | Email |User.mail |
    
    a.  Per ogni riga di dati nella tabella precedente, fare clic su **aggiungi attributo utente**.
    
    ![attributi token SAML](./media/timeoffmanager-tutorial/tutorial_timeoffmanager_addattrb.png "attributi token SAML")
    
    ![attributi token SAML](./media/timeoffmanager-tutorial/tutorial_timeoffmanager_addattrb1.png "attributi token SAML")
    
    b.  Nella casella di testo **Nome attributo** , digitare il nome dell'attributo indicato per quella riga.
    
    c.  Nella casella di testo **Valore attributo** selezionare il valore dell'attributo indicato per la riga.
    
    d.  Fare clic su **OK**.
    
1. Fare clic sul pulsante **Salva** .

    ![Configure Single Sign-On](./media/timeoffmanager-tutorial/tutorial_general_400.png)

1. Nella sezione **Configurazione di TimeOffManager** fare clic su **Configura TimeOffManager** per aprire la finestra **Configura accesso**. Copiare l'**URL di disconnessione, l'ID di entità SAML e l'URL del servizio Single Sign-On SAML** dalla sezione **Riferimento rapido.**

    ![Sezione Configurazione di TimeOffManager](./media/timeoffmanager-tutorial/tutorial_timeoffmanager_configure.png) 

1. In un'altra finestra del Web browser accedere al sito aziendale di TimeOffManager come amministratore.

1. Andare a **Account \> Account Options \> Single Sign-On Settings** (Account > Opzioni account > Impostazioni Single Sign-On).
   
   ![Single Sign-On Settings](./media/timeoffmanager-tutorial/ic795917.png "Single Sign-On Settings")
1. Nella sezione **Single Sign-On Settings** , eseguire la procedura seguente:
   
   ![Single Sign-On Settings](./media/timeoffmanager-tutorial/ic795918.png "Single Sign-On Settings")
   
   a. Aprire il certificato con codifica Base 64 nel Blocco note, copiarne il contenuto negli Appunti e incollare l’intero certificato nella casella di testo **Certificate X.509** .
   
   b. Nella casella di testo **IdP Issuer** (Autorità emittente IdP) incollare il valore dell'**ID di entità SAML** copiato dal portale di Azure.
   
   c. Nella casella di testo **IdP Endpoint URL** (URL endpoint IdP) incollare il valore dell'**URL del servizio Single Sign-On SAML** copiato dal portale di Azure.
   
   d. Per **Enforce SAML** (Applica SAML), selezionare **No**.
   
   e. Per **Auto-Create Users** (Crea utenti in automatico), selezionare **Sì**.
   
   f. Nella casella di testo **Logout URL** (URL di disconnessione) incollare il valore dell'**URL di disconnessione** copiato dal portale di Azure.
   
   g. Fare clic su **Save Changes** (Salva modifiche).

1. Nella pagina **Single Sign on settings** (Impostazioni Single Sign-On) copiare il valore dell'**URL del servizio consumer di asserzione** e incollarlo nella casella di testo **URL di risposta** nella sezione **URL e dominio TimeOffManager** del portale di Azure. 

      ![Single Sign-On Settings](./media/timeoffmanager-tutorial/ic795915.png "Single Sign-On Settings")

> [!TIP]
> Un riepilogo delle istruzioni è disponibile all'interno del [portale di Azure](https://portal.azure.com) durante la configurazione dell'app.  Dopo aver aggiunto l'app dalla sezione **Active Directory > Applicazioni aziendali** è sufficiente fare clic sulla scheda **Single Sign-On** e accedere alla documentazione incorporata tramite la sezione **Configurazione** nella parte inferiore. Altre informazioni sulla funzione di documentazione incorporata sono disponibili in [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985) (Documentazione incorporata di Azure AD).
> 

### <a name="create-an-azure-ad-test-user"></a>Creare un utente test di Azure AD
Questa sezione descrive come creare un utente test denominato Britta Simon nel portale di Azure.

![Creare un utente di Azure AD][100]

**Per creare un utente test in Azure AD, eseguire la procedura seguente:**

1. Nel **portale di Azure** fare clic sull'icona di **Azure Active Directory** nel riquadro di spostamento sinistro.

    ![Creazione di un utente test di Azure AD](./media/timeoffmanager-tutorial/create_aaduser_01.png) 

1. Passare a **Utenti e gruppi** e fare clic su **Tutti gli utenti** per visualizzare l'elenco di utenti.
    
    ![Utenti e gruppi --> Tutti gli utenti](./media/timeoffmanager-tutorial/create_aaduser_02.png) 

1. Nella parte superiore della finestra di dialogo fare clic su **Aggiungi** per aprire la finestra di dialogo **Utente**.
 
    ![Pulsante Aggiungi](./media/timeoffmanager-tutorial/create_aaduser_03.png) 

1. Nella pagina della finestra di dialogo **Utente** seguire questa procedura:
 
    ![Finestra di dialogo Utente](./media/timeoffmanager-tutorial/create_aaduser_04.png) 

    a. Nella casella di testo **Nome** digitare **BrittaSimon**.

    b. Nella casella di testo **Nome utente** digitare l'**indirizzo di posta elettronica** di BrittaSimon.

    c. Selezionare **Mostra password** e prendere nota del valore della **Password**.

    d. Fare clic su **Create**(Crea).
 
### <a name="create-a-timeoffmanager-test-user"></a>Creare un utente di test di TimeOffManager

Per consentire agli utenti di Azure AD di accedere a TimeOffManager, è necessario eseguirne il provisioning in TimeOffManager.  

TimeOffManager supporta solo il provisioning just in time dell'utente. Non è necessario eseguire alcuna operazione.  

Gli utenti vengono aggiunti automaticamente durante l'utilizzo di Single Sign-on primo accesso.

>[!NOTE]
>È possibile usare qualsiasi altro strumento o API di creazione di account utente di TimeOffManager per effettuare il provisioning degli account utente di Azure AD.
> 

### <a name="assign-the-azure-ad-test-user"></a>Assegnare l'utente test di Azure AD

In questa sezione Britta Simon viene abilitata per l'uso dell'accesso Single Sign-On di Azure concedendole l'accesso a TimeOffManager.

![Assegna utente][200] 

**Per assegnare Britta Simon a TimeOffManager, seguire questa procedura:**

1. Nel portale di Azure aprire la visualizzazione delle applicazioni e quindi la visualizzazione delle directory e passare ad **Applicazioni aziendali**, quindi fare clic su **Tutte le applicazioni**.

    ![Assegna utente][201] 

1. Nell'elenco delle applicazioni selezionare **TimeOffManager**.

    ![TimeOffManager nell'elenco di app](./media/timeoffmanager-tutorial/tutorial_timeoffmanager_app.png) 

1. Scegliere **Utenti e gruppi** dal menu a sinistra.

    ![Assegna utente][202] 

1. Fare clic sul pulsante **Aggiungi**. Selezionare quindi **Utenti e gruppi** nella finestra di dialogo **Aggiungi assegnazione**.

    ![Assegna utente][203]

1. Nella finestra di dialogo **Utenti e gruppi** selezionare **Britta Simon** nell'elenco Utenti.

1. Fare clic sul pulsante **Seleziona** nella finestra di dialogo **Utenti e gruppi**.

1. Fare clic sul pulsante **Assegna** nella finestra di dialogo **Aggiungi assegnazione**.
    
### <a name="test-single-sign-on"></a>Testare l'accesso Single Sign-On

In questa sezione viene testata la configurazione dell'accesso Single Sign-On di Azure AD usando il pannello di accesso.

Quando si fa clic sul riquadro TimeOffManager nel pannello di accesso, si dovrebbe accedere automaticamente all'applicazione TimeOffManager. Per altre informazioni sul pannello di accesso, vedere [Introduzione al Pannello di accesso](../user-help/active-directory-saas-access-panel-introduction.md).

## <a name="additional-resources"></a>Risorse aggiuntive

* [Elenco di esercitazioni sulla procedura di integrazione delle app SaaS con Azure Active Directory](tutorial-list.md)
* [Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory](../manage-apps/what-is-single-sign-on.md)



<!--Image references-->

[1]: ./media/timeoffmanager-tutorial/tutorial_general_01.png
[2]: ./media/timeoffmanager-tutorial/tutorial_general_02.png
[3]: ./media/timeoffmanager-tutorial/tutorial_general_03.png
[4]: ./media/timeoffmanager-tutorial/tutorial_general_04.png

[100]: ./media/timeoffmanager-tutorial/tutorial_general_100.png

[200]: ./media/timeoffmanager-tutorial/tutorial_general_200.png
[201]: ./media/timeoffmanager-tutorial/tutorial_general_201.png
[202]: ./media/timeoffmanager-tutorial/tutorial_general_202.png
[203]: ./media/timeoffmanager-tutorial/tutorial_general_203.png

