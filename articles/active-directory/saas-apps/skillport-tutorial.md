---
title: 'Esercitazione: Integrazione di Azure Active Directory con Skillport | Microsoft Docs'
description: Informazioni su come configurare l'accesso Single Sign-On tra Azure Active Directory e Skillport.
services: active-directory
documentationCenter: na
author: jeevansd
manager: mtillman
ms.assetid: 4df349b2-a73f-4b88-a077-ec0fbfc26527
ms.service: active-directory
ms.component: saas-app-tutorial
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 10/24/2017
ms.author: jeedes
ms.openlocfilehash: 71a2b7186c77c6c1872870a594b287479c292472
ms.sourcegitcommit: 1d850f6cae47261eacdb7604a9f17edc6626ae4b
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 08/02/2018
ms.locfileid: "39448306"
---
# <a name="tutorial-azure-active-directory-integration-with-skillport"></a>Esercitazione: Integrazione di Azure Active Directory con Skillport

Questa esercitazione descrive come integrare Skillport con Azure Active Directory (Azure AD).

L'integrazione di Skillport con Azure AD offre i vantaggi seguenti:

- È possibile controllare in Azure AD chi può accedere a Skillport
- È possibile abilitare gli utenti per l'accesso automatico a Skillport (Single Sign-On) con gli account Azure AD personali
- È possibile gestire gli account in un'unica posizione centrale: il portale di Azure.

Per altre informazioni sull'integrazione di app SaaS con Azure AD, vedere [Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory](../manage-apps/what-is-single-sign-on.md).

## <a name="prerequisites"></a>Prerequisiti

Per configurare l'integrazione di Azure AD con Skillport, sono necessari gli elementi seguenti:

- Sottoscrizione di Azure AD
- Sottoscrizione di Skillport abilitata per l'accesso Single Sign-On

> [!NOTE]
> Non è consigliabile usare un ambiente di produzione per testare i passaggi di questa esercitazione.

A questo scopo, è consigliabile seguire le indicazioni seguenti:

- Non usare l'ambiente di produzione a meno che non sia necessario.
- Se non si dispone di un ambiente di prova di Azure AD, è possibile ottenere una versione di valutazione di un mese [qui](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Descrizione dello scenario
In questa esercitazione viene eseguito il test dell'accesso Single Sign-On di Azure AD in un ambiente di test. Lo scenario descritto in questa esercitazione prevede le due fasi fondamentali seguenti:

1. Aggiunta di Skillport dalla raccolta
1. Configurazione e test dell'accesso Single Sign-On di Azure AD

## <a name="adding-skillport-from-the-gallery"></a>Aggiunta di Skillport dalla raccolta
Per configurare l'integrazione di Skillport in Azure AD, è necessario aggiungere Skillport dalla raccolta all'elenco di app SaaS gestite.

**Per aggiungere Skillport dalla raccolta, seguire questa procedura:**

1. Nel **[portale di Azure](https://portal.azure.com)** fare clic sull'icona di **Azure Active Directory** nel riquadro di spostamento sinistro. 

    ![Active Directory][1]

1. Passare ad **Applicazioni aziendali**. Andare quindi a **Tutte le applicazioni**.

    ![APPLICAZIONI][2]
    
1. Fare clic sul pulsante **Nuova applicazione** nella parte superiore della finestra di dialogo.

    ![APPLICAZIONI][3]

1. Nella casella di ricerca digitare **Skillport**.

    ![Creazione di un utente test di Azure AD](./media/skillport-tutorial/tutorial_skillport_search.png)

1. Nel pannello dei risultati selezionare **Skillport** e quindi fare clic sul pulsante **Aggiungi** per aggiungere l'applicazione.

    ![Creazione di un utente test di Azure AD](./media/skillport-tutorial/tutorial_skillport_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Configurazione e test dell'accesso Single Sign-On di Azure AD
In questa sezione viene configurato e testato l'accesso Single Sign-On di Azure AD con Skillport usando un utente di test di nome "Britta Simon".

Per il funzionamento dell'accesso Single Sign-On, Azure AD deve conoscere l'utente controparte di Skillport corrispondente a un utente di Azure AD. In altre parole, deve essere stabilita una relazione di collegamento tra un utente di Azure AD e l'utente correlato in Skillport.

Per stabilire la relazione di collegamento, assegnare il valore del **nome utente** in Azure AD come valore di **Username** (Nome utente) in Skillport.

Per configurare e testare l'accesso Single Sign-On di Azure AD con Skillport, è necessario completare le procedure di base seguenti:

1. **[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** : per abilitare gli utenti all'utilizzo di questa funzionalità.
1. **[Creazione di un utente test di Azure AD](#creating-an-azure-ad-test-user)** : per testare l'accesso Single Sign-On di Azure AD con l'utente Britta Simon.
1. **[Creazione di un utente di test di Skillport](#creating-a-skillport-test-user)**: per avere una controparte di Britta Simon in Skillport collegata alla rappresentazione dell'utente in Azure AD.
1. **[Assegnazione dell'utente test di Azure AD](#assigning-the-azure-ad-test-user)** : per abilitare Britta Simon all'uso dell'accesso Single Sign-On di Azure AD.
1. **[Testing Single Sign-On](#testing-single-sign-on)** : per verificare se la configurazione funziona.

### <a name="configuring-azure-ad-single-sign-on"></a>Configurazione dell'accesso Single Sign-On di Azure AD

In questa sezione viene abilitato l'accesso Single Sign-On di Azure AD nel portale di Azure e viene configurato l'accesso Single Sign-On nell'applicazione Skillport.

**Per configurare l'accesso Single Sign-On di Azure AD con Skillport, seguire questa procedura:**

1. Nella pagina di integrazione dell'applicazione **Skillport** del portale di Azure fare clic su **Single Sign-On**.

    ![Configure Single Sign-On][4]

1. Nella finestra di dialogo **Single Sign-On** selezionare **Accesso basato su SAML** per **Modalità** per abilitare l'accesso Single Sign-On.
 
    ![Configure Single Sign-On](./media/skillport-tutorial/tutorial_skillport_samlbase.png)

1. Nella sezione **URL e dominio Skillport** seguire questa procedura:

    ![Configure Single Sign-On](./media/skillport-tutorial/tutorial_skillport_url.png)

    a. Nella casella di testo **URL accesso** digitare l'URL:
      
      Data center UE: `https://adfs.skillport.eu`
   
      Data center USA: `https://sso.skillport.com`

    b. Nella casella di testo **Identificatore** digitare l'URL:
      
      Data center UE: `http://adfs.skillport.eu/adfs/services/trust`
   
      Data center USA: `https://sso.skillport.com`
   
    c. Nella casella di testo **URL di risposta** digitare l'URL:
    
      Data center UE: ` https://adfs.skillport.eu/adfs/ls/`
    
      Data center USA: `https://sso.skillport.com/sp/ACS.saml2`
 
1. Nella sezione **Certificato di firma SAML** fare clic su **XML metadati** e quindi salvare il file XML nel computer.

    ![Configure Single Sign-On](./media/skillport-tutorial/tutorial_skillport_certificate.png) 

1. Fare clic sul pulsante **Salva** .

    ![Configure Single Sign-On](./media/skillport-tutorial/tutorial_general_400.png)

1. Per configurare l'accesso Single Sign-On sul lato **Skillport**, è necessario inviare il file **XML metadati** scaricato al [team di supporto di Skillport](https://www.skillsoft.com/contact.asp). La configurazione verrà eseguita in modo che la connessione SSO SAML sia impostata correttamente su entrambi i lati.

### <a name="creating-an-azure-ad-test-user"></a>Creazione di un utente test di Azure AD
Questa sezione descrive come creare un utente test denominato Britta Simon nel portale di Azure.

![Creare un utente di Azure AD][100]

**Per creare un utente test in Azure AD, eseguire la procedura seguente:**

1. Nel **portale di Azure** fare clic sull'icona di **Azure Active Directory** nel riquadro di spostamento sinistro.

    ![Creazione di un utente test di Azure AD](./media/skillport-tutorial/create_aaduser_01.png) 

1. Andare a **Utenti e gruppi** e fare clic su **Tutti gli utenti** per visualizzare l'elenco di utenti.
    
    ![Creazione di un utente test di Azure AD](./media/skillport-tutorial/create_aaduser_02.png) 

1. Nella parte superiore della finestra di dialogo fare clic su **Aggiungi** per aprire la finestra di dialogo **Utente**.
 
    ![Creazione di un utente test di Azure AD](./media/skillport-tutorial/create_aaduser_03.png) 

1. Nella pagina della finestra di dialogo **Utente** seguire questa procedura:
 
    ![Creazione di un utente test di Azure AD](./media/skillport-tutorial/create_aaduser_04.png) 

    a. Nella casella di testo **Nome** digitare **BrittaSimon**.

    b. Nella casella di testo **Nome utente** digitare l'**indirizzo di posta elettronica** di BrittaSimon.

    c. Selezionare **Mostra password** e prendere nota del valore della **Password**.

    d. Fare clic su **Create**(Crea).
 
### <a name="creating-a-skillport-test-user"></a>Creazione di un utente di test di Skillport

Per creare l'utente di test di Skillport, è necessario contattare il [team di supporto di Skillport](https://www.skillsoft.com/contact.asp) perché sono previsti diversi scenari aziendali in base ai requisiti dell'utente finale. La configurazione verrà eseguita dopo averne discusso con gli utenti.  

### <a name="assigning-the-azure-ad-test-user"></a>Assegnazione dell'utente test di Azure AD

In questa sezione Britta Simon viene abilitata per l'uso dell'accesso Single Sign-On di Azure concedendole l'accesso a Skillport.

![Assegna utente][200] 

**Per assegnare Britta Simon a Skillport, seguire questa procedura:**

1. Nel portale di Azure aprire la visualizzazione delle applicazioni e quindi la visualizzazione delle directory e passare ad **Applicazioni aziendali**, quindi fare clic su **Tutte le applicazioni**.

    ![Assegna utente][201] 

1. Nell'elenco delle applicazioni selezionare **Skillport**.

    ![Configure Single Sign-On](./media/skillport-tutorial/tutorial_skillport_app.png) 

1. Scegliere **Utenti e gruppi** dal menu a sinistra.

    ![Assegna utente][202] 

1. Fare clic sul pulsante **Aggiungi**. Selezionare quindi **Utenti e gruppi** nella finestra di dialogo **Aggiungi assegnazione**.

    ![Assegna utente][203]

1. Nella finestra di dialogo **Utenti e gruppi** selezionare **Britta Simon** nell'elenco Utenti.

1. Fare clic sul pulsante **Seleziona** nella finestra di dialogo **Utenti e gruppi**.

1. Fare clic sul pulsante **Assegna** nella finestra di dialogo **Aggiungi assegnazione**.
    
### <a name="testing-single-sign-on"></a>Test dell'accesso Single Sign-On

In questa sezione viene testata la configurazione dell'accesso Single Sign-On di Azure AD usando il pannello di accesso.

Quando si fa clic sul riquadro Skillport nel pannello di accesso, si dovrebbe accedere automaticamente all'applicazione Skillport.
Per altre informazioni sul pannello di accesso, vedere [Introduzione al Pannello di accesso](../user-help/active-directory-saas-access-panel-introduction.md). 

## <a name="additional-resources"></a>Risorse aggiuntive

* [Elenco di esercitazioni sulla procedura di integrazione delle app SaaS con Azure Active Directory](tutorial-list.md)
* [Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory](../manage-apps/what-is-single-sign-on.md)



<!--Image references-->

[1]: ./media/skillport-tutorial/tutorial_general_01.png
[2]: ./media/skillport-tutorial/tutorial_general_02.png
[3]: ./media/skillport-tutorial/tutorial_general_03.png
[4]: ./media/skillport-tutorial/tutorial_general_04.png

[100]: ./media/skillport-tutorial/tutorial_general_100.png

[200]: ./media/skillport-tutorial/tutorial_general_200.png
[201]: ./media/skillport-tutorial/tutorial_general_201.png
[202]: ./media/skillport-tutorial/tutorial_general_202.png
[203]: ./media/skillport-tutorial/tutorial_general_203.png

