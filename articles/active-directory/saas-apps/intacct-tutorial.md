---
title: 'Esercitazione: Integrazione di Azure Active Directory con Intacct | Documentazione Microsoft'
description: Informazioni su come configurare l'accesso Single Sign-On tra Azure Active Directory e Intacct.
services: active-directory
documentationCenter: na
author: jeevansd
manager: mtillman
ms.assetid: 92518e02-a62c-4b1b-a8e9-2803eb2b49ac
ms.service: active-directory
ms.component: saas-app-tutorial
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/23/2017
ms.author: jeedes
ms.openlocfilehash: d834ca75085878350e257cc1c50e60fc1bf28484
ms.sourcegitcommit: 1d850f6cae47261eacdb7604a9f17edc6626ae4b
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 08/02/2018
ms.locfileid: "39447340"
---
# <a name="tutorial-azure-active-directory-integration-with-intacct"></a>Esercitazione: Integrazione di Azure Active Directory con Intacct

Questa esercitazione descrive come integrare Intacct con Azure Active Directory (Azure AD).

L'integrazione di Intacct con Azure AD offre i vantaggi seguenti:

- È possibile controllare in Azure AD chi può accedere a Intacct
- È possibile abilitare gli utenti per l'accesso automatico a Intacct (Single Sign-On) con i propri account Azure AD
- È possibile gestire gli account in un'unica posizione centrale: il portale di Azure.

Per altre informazioni sull'integrazione di app SaaS con Azure AD, vedere [Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory](../manage-apps/what-is-single-sign-on.md).

## <a name="prerequisites"></a>Prerequisiti

Per configurare l'integrazione di Azure AD con Intacct, sono necessari gli elementi seguenti:

- Sottoscrizione di Azure AD
- Sottoscrizione di Intacct abilitata per l'accesso Single Sign-On

> [!NOTE]
> Non è consigliabile usare un ambiente di produzione per testare i passaggi di questa esercitazione.

A questo scopo, è consigliabile seguire le indicazioni seguenti:

- Non usare l'ambiente di produzione a meno che non sia necessario.
- Se non si dispone di un ambiente di prova di Azure AD, è possibile ottenere una versione di valutazione di un mese [qui](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Descrizione dello scenario
In questa esercitazione viene eseguito il test dell'accesso Single Sign-On di Azure AD in un ambiente di test. Lo scenario descritto in questa esercitazione prevede le due fasi fondamentali seguenti:

1. Aggiunta di Intacct dalla raccolta
1. Configurazione e test dell'accesso Single Sign-On di Azure AD

## <a name="adding-intacct-from-the-gallery"></a>Aggiunta di Intacct dalla raccolta
Per configurare l'integrazione di Intacct in Azure AD, è necessario aggiungere Intacct dalla raccolta al proprio elenco di app SaaS gestite.

**Per aggiungere Intacct dalla raccolta, seguire questa procedura:**

1. Nel **[portale di Azure](https://portal.azure.com)** fare clic sull'icona di **Azure Active Directory** nel riquadro di spostamento sinistro. 

    ![Active Directory][1]

1. Passare ad **Applicazioni aziendali**. Andare quindi a **Tutte le applicazioni**.

    ![APPLICAZIONI][2]
    
1. Fare clic sul pulsante **Nuova applicazione** nella parte superiore della finestra di dialogo per aggiungere una nuova applicazione.

    ![APPLICAZIONI][3]

1. Nella casella di ricerca digitare **Intacct**.

    ![Creazione di un utente test di Azure AD](./media/intacct-tutorial/tutorial_intacct_search.png)

1. Nel pannello dei risultati selezionare **Intacct** e quindi fare clic sul pulsante **Aggiungi** per aggiungere l'applicazione.

    ![Creazione di un utente test di Azure AD](./media/intacct-tutorial/tutorial_intacct_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Configurazione e test dell'accesso Single Sign-On di Azure AD
In questa sezione viene configurato e testato l'accesso Single Sign-On di Azure AD con Intacct con un utente di test di nome "Britta Simon".

Per il funzionamento dell'accesso Single Sign-On, Azure AD deve conoscere qual è l'utente di Intacct che corrisponde a un utente di Azure AD. In altre parole, deve essere stabilita una relazione di collegamento tra un utente di Azure AD e l'utente correlato in Intacct.

Per stabilire la relazione di collegamento, in Intacct assegnare il valore di **nome utente** in Azure AD come valore di **Username** (Nome utente).

Per configurare e testare l'accesso Single Sign-On di Azure AD con Intacct, è necessario completare i blocchi predefiniti seguenti:

1. **[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** : per abilitare gli utenti all'utilizzo di questa funzionalità.
1. **[Creazione di un utente test di Azure AD](#creating-an-azure-ad-test-user)** : per testare l'accesso Single Sign-On di Azure AD con l'utente Britta Simon.
1. **[Creazione di un utente di test di Intacct](#creating-an-intacct-test-user)**: per avere una controparte di Britta Simon in Intacct collegata alla relativa rappresentazione in Azure AD.
1. **[Assegnazione dell'utente test di Azure AD](#assigning-the-azure-ad-test-user)** : per abilitare Britta Simon all'uso dell'accesso Single Sign-On di Azure AD.
1. **[Testing Single Sign-On](#testing-single-sign-on)** : per verificare se la configurazione funziona.

### <a name="configuring-azure-ad-single-sign-on"></a>Configurazione dell'accesso Single Sign-On di Azure AD

In questa sezione viene abilitato l'accesso Single Sign-On di Azure AD nel portale di Azure e viene configurato l'accesso Single Sign-On nell'applicazione Intacct.

**Per configurare l'accesso Single Sign-On di Azure AD con Intacct, seguire questa procedura:**

1. Nella pagina di integrazione dell'applicazione **Intacct** del portale di Azure fare clic su **Single Sign-On**.

    ![Configure Single Sign-On][4]

1. Nella finestra di dialogo **Single Sign-On** selezionare **Accesso basato su SAML** per **Modalità** per abilitare l'accesso Single Sign-On.
 
    ![Configure Single Sign-On](./media/intacct-tutorial/tutorial_intacct_samlbase.png)

1. Nella sezione **URL e dominio Intacct** seguire questa procedura:

    ![Configure Single Sign-On](./media/intacct-tutorial/tutorial_intacct_url.png)

    Nella casella di testo **URL di risposta** digitare l'URL usando il modello seguente:
    | |
    |--|
    | `https://<companyname>.intacct.com/ia/acct/sso_response.phtml`|
    | `https://www.intacct.com/ia/acct/sso_response.phtml` |

    > [!NOTE] 
    > Poiché non è reale, è necessario aggiornare questo valore con l'URL di risposta effettivo. Per ottenere questo valore, contattare il [team di supporto di Intacct](https://us.intacct.com/support).

1. Nella sezione **Certificato di firma SAML** fare clic su **Certificato (Base64)** e quindi salvare il file del certificato nel computer.

    ![Configure Single Sign-On](./media/intacct-tutorial/tutorial_intacct_certificate.png) 

1. Fare clic sul pulsante **Salva** .

    ![Configure Single Sign-On](./media/intacct-tutorial/tutorial_general_400.png)

1. Nella sezione **Configurazione di Intacct** fare clic su **Configura Intacct** per aprire la finestra **Configura accesso**. Copiare l'**ID di entità SAML e l'URL del servizio Single Sign-On SAML** dalla sezione **Riferimento rapido.**

    ![Configure Single Sign-On](./media/intacct-tutorial/tutorial_intacct_configure.png) 

1. In un'altra finestra del Web browser accedere al sito aziendale di Intacct come amministratore.

1. Fare clic sulla scheda **Company** (Azienda) e quindi su **Company Info** (Informazioni sull'azienda).

    ![Azienda](./media/intacct-tutorial/ic790037.png "Azienda")

1. Fare clic sulla scheda **Security** (Sicurezza) e quindi su **Edit** (Modifica).

    ![Sicurezza](./media/intacct-tutorial/ic790038.png "Sicurezza")

1. Nella sezione **Single sign on (SSO)** seguire questa procedura:

    ![Single sign on](./media/intacct-tutorial/ic790039.png "single sign on")

    a. Selezionare **Abilita Single Sign-On**.

    b. In **Identity provider type** (Tipo di provider di identità) selezionare **SAML 2.0**.

    c. Nella casella di testo **Issuer URL** (URL autorità emittente) incollare il valore dell'**ID entità SAML** copiato dal portale di Azure.
   
    d. Nella casella di testo **URL di accesso** incollare il valore dell'**URL del servizio Single Sign-On SAML** copiato dal portale di Azure.

    e. Aprire il certificato con codifica **Base 64** nel Blocco note, copiarne il contenuto negli Appunti e incollarlo nella casella **Certificato**.
   
    f. Fare clic su **Save**.

> [!TIP]
> Un riepilogo delle istruzioni è disponibile all'interno del [portale di Azure](https://portal.azure.com) durante la configurazione dell'app.  Dopo aver aggiunto l'app dalla sezione **Active Directory > Applicazioni aziendali** è sufficiente fare clic sulla scheda **Single Sign-On** e accedere alla documentazione incorporata tramite la sezione **Configurazione** nella parte inferiore. Altre informazioni sulla funzione di documentazione incorporata sono disponibili in [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985) (Documentazione incorporata di Azure AD).
> 

### <a name="creating-an-azure-ad-test-user"></a>Creazione di un utente test di Azure AD
Questa sezione descrive come creare un utente test denominato Britta Simon nel portale di Azure.

![Creare un utente di Azure AD][100]

**Per creare un utente test in Azure AD, eseguire la procedura seguente:**

1. Nel **portale di Azure** fare clic sull'icona di **Azure Active Directory** nel riquadro di spostamento sinistro.

    ![Creazione di un utente test di Azure AD](./media/intacct-tutorial/create_aaduser_01.png) 

1. Passare a **Utenti e gruppi** e fare clic su **Tutti gli utenti** per visualizzare l'elenco di utenti.
    
    ![Creazione di un utente test di Azure AD](./media/intacct-tutorial/create_aaduser_02.png) 

1. Nella parte superiore della finestra di dialogo fare clic su **Aggiungi** per aprire la finestra di dialogo **Utente**.
 
    ![Creazione di un utente test di Azure AD](./media/intacct-tutorial/create_aaduser_03.png) 

1. Nella pagina della finestra di dialogo **Utente** seguire questa procedura:
 
    ![Creazione di un utente test di Azure AD](./media/intacct-tutorial/create_aaduser_04.png) 

    a. Nella casella di testo **Nome** digitare **BrittaSimon**.

    b. Nella casella di testo **Nome utente** digitare l'**indirizzo di posta elettronica** di BrittaSimon.

    c. Selezionare **Mostra password** e prendere nota del valore della **Password**.

    d. Fare clic su **Create**(Crea).
 
### <a name="creating-an-intacct-test-user"></a>Creazione di un utente di test di Intacct

Per consentire agli utenti di Azure AD di accedere a Intacct, è necessario eseguirne il provisioning in Intacct. In Intacct il provisioning è un'attività manuale.

**Per eseguire il provisioning degli account utente, seguire questa procedura:**

1. Accedere al tenant di **Intacct**.

1. Fare clic sulla scheda **Company** (Azienda) e quindi su **Users** (Utenti).

    ![Utenti](./media/intacct-tutorial/ic790041.png "Utenti")
1. Fare clic sulla scheda **Add** (Aggiungi).

    ![Aggiungi](./media/intacct-tutorial/ic790042.png "Aggiungi")
1. Nella sezione **Informazioni utente** seguire questa procedura:

    ![Informazioni utente](./media/intacct-tutorial/ic790043.png "Informazioni utente")

    a. Nelle caselle di testo **User ID**, **Last name**, **First name**, **Email address**, **Title** e **Phone** immettere l'ID utente, il cognome, il nome, l'indirizzo di posta elettronica, la posizione e il numero di telefono di un account Azure AD di cui si vuole eseguire il provisioning nella sezione **Informazioni utente**.

    b. Selezionare i **privilegi di amministratore** di un account Azure AD di cui si vuole eseguire il provisioning.
   
    c. Fare clic su **Save**. Il titolare dell'account Azure AD riceve un messaggio di posta elettronica con un collegamento da selezionare per confermare l'account e attivarlo.

>[!NOTE]
>Per eseguire il provisioning degli account utente di Azure AD, è possibile usare altri strumenti o API per la creazione di account utente Intacct forniti da Intacct.
        
### <a name="assigning-the-azure-ad-test-user"></a>Assegnazione dell'utente test di Azure AD

In questa sezione si abilita Britta Simon all'uso dell'accesso Single Sign-On di Azure concedendole l'accesso a Intacct.

![Assegna utente][200] 

**Per assegnare Britta Simon a Intacct, seguire questa procedura:**

1. Nel portale di Azure aprire la visualizzazione delle applicazioni e quindi la visualizzazione delle directory e passare ad **Applicazioni aziendali**, quindi fare clic su **Tutte le applicazioni**.

    ![Assegna utente][201] 

1. Nell'elenco delle applicazioni selezionare **Intacct**.

    ![Configure Single Sign-On](./media/intacct-tutorial/tutorial_intacct_app.png) 

1. Scegliere **Utenti e gruppi** dal menu a sinistra.

    ![Assegna utente][202] 

1. Fare clic sul pulsante **Aggiungi**. Selezionare quindi **Utenti e gruppi** nella finestra di dialogo **Aggiungi assegnazione**.

    ![Assegna utente][203]

1. Nella finestra di dialogo **Utenti e gruppi** selezionare **Britta Simon** nell'elenco Utenti.

1. Fare clic sul pulsante **Seleziona** nella finestra di dialogo **Utenti e gruppi**.

1. Fare clic sul pulsante **Assegna** nella finestra di dialogo **Aggiungi assegnazione**.
    
### <a name="testing-single-sign-on"></a>Test dell'accesso Single Sign-On

In questa sezione viene testata la configurazione dell'accesso Single Sign-On di Azure AD usando il pannello di accesso.

Quando si fa clic sul riquadro Intacct nel pannello di accesso, si dovrebbe accedere automaticamente all'applicazione Intacct.

## <a name="additional-resources"></a>Risorse aggiuntive

* [Elenco di esercitazioni sulla procedura di integrazione delle app SaaS con Azure Active Directory](tutorial-list.md)
* [Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory](../manage-apps/what-is-single-sign-on.md)

<!--Image references-->

[1]: ./media/intacct-tutorial/tutorial_general_01.png
[2]: ./media/intacct-tutorial/tutorial_general_02.png
[3]: ./media/intacct-tutorial/tutorial_general_03.png
[4]: ./media/intacct-tutorial/tutorial_general_04.png

[100]: ./media/intacct-tutorial/tutorial_general_100.png

[200]: ./media/intacct-tutorial/tutorial_general_200.png
[201]: ./media/intacct-tutorial/tutorial_general_201.png
[202]: ./media/intacct-tutorial/tutorial_general_202.png
[203]: ./media/intacct-tutorial/tutorial_general_203.png

