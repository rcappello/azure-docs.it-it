---
title: 'Esercitazione: Integrazione di Azure Active Directory con BGS Online | Documentazione Microsoft'
description: Informazioni su come configurare l'accesso Single Sign-On tra Azure Active Directory e BGS Online.
services: active-directory
documentationCenter: na
author: jeevansd
manager: mtillman
ms.assetid: 4fd6b29b-1b46-4fd1-9f5e-16b1c9d892cd
ms.service: active-directory
ms.component: saas-app-tutorial
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/09/2017
ms.author: jeedes
ms.openlocfilehash: 3e0da76410c00b8ec0865b094d15237f4f932fb5
ms.sourcegitcommit: 1d850f6cae47261eacdb7604a9f17edc6626ae4b
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 08/02/2018
ms.locfileid: "39421391"
---
# <a name="tutorial-azure-active-directory-integration-with-bgs-online"></a>Esercitazione: Integrazione di Azure Active Directory con BGS Online

Questa esercitazione descrive come integrare BGS Online con Azure Active Directory (Azure AD).

L'integrazione di BGS Online con Azure AD offre i vantaggi seguenti:

- È possibile controllare in Azure AD chi può accedere a BGS Online
- È possibile abilitare gli utenti per l'accesso automatico a BGS Online (Single Sign-On) con i propri account Azure AD
- È possibile gestire gli account in un'unica posizione centrale: il portale di Azure.

Per altre informazioni sull'integrazione di app SaaS con Azure AD, vedere [Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory](../manage-apps/what-is-single-sign-on.md).

## <a name="prerequisites"></a>Prerequisiti

Per configurare l'integrazione di Azure AD con BGS Online, sono necessari gli elementi seguenti:

- Sottoscrizione di Azure AD
- Sottoscrizione di BGS Online abilitata per l'accesso Single Sign-On

> [!NOTE]
> Non è consigliabile usare un ambiente di produzione per testare i passaggi di questa esercitazione.

A questo scopo, è consigliabile seguire le indicazioni seguenti:

- Non usare l'ambiente di produzione a meno che non sia necessario.
- Se non si dispone di un ambiente di prova di Azure AD, è possibile ottenere una versione di valutazione di un mese [qui](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Descrizione dello scenario
In questa esercitazione viene eseguito il test dell'accesso Single Sign-On di Azure AD in un ambiente di test. Lo scenario descritto in questa esercitazione prevede le due fasi fondamentali seguenti:

1. Aggiunta di BGS Online dalla raccolta
1. Configurazione e test dell'accesso Single Sign-On di Azure AD

## <a name="adding-bgs-online-from-the-gallery"></a>Aggiunta di BGS Online dalla raccolta
Per configurare l'integrazione di BGS Online in Azure AD, è necessario aggiungere BGS Online dalla raccolta al proprio elenco di app SaaS gestite.

**Per aggiungere BGS Online dalla raccolta, seguire questa procedura:**

1. Nel **[portale di Azure](https://portal.azure.com)** fare clic sull'icona di **Azure Active Directory** nel riquadro di spostamento sinistro. 

    ![Active Directory][1]

1. Passare ad **Applicazioni aziendali**. Andare quindi a **Tutte le applicazioni**.

    ![APPLICAZIONI][2]
    
1. Fare clic sul pulsante **Nuova applicazione** nella parte superiore della finestra di dialogo per aggiungere una nuova applicazione.

    ![APPLICAZIONI][3]

1. Nella casella di ricerca digitare **BGS Online**.

    ![Creazione di un utente test di Azure AD](./media/bgsonline-tutorial/tutorial_bgsonline_search.png)

1. Nel pannello dei risultati selezionare **BGS Online** e quindi fare clic sul pulsante **Aggiungi** per aggiungere l'applicazione.

    ![Creazione di un utente test di Azure AD](./media/bgsonline-tutorial/tutorial_bgsonline_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Configurazione e test dell'accesso Single Sign-On di Azure AD
In questa sezione viene configurato e testato l'accesso Single Sign-On di Azure AD con BGS Online usando un utente di test di nome "Britta Simon".

Per il funzionamento dell'accesso Single Sign-On, Azure AD deve conoscere l'utente controparte di BGS Online che corrisponde a un utente di Azure AD. In altre parole, deve essere stabilita una relazione di collegamento tra un utente di Azure AD e l'utente correlato in BGS Online.

Per stabilire la relazione di collegamento, in BGS Online assegnare il valore del **nome utente** in Azure AD come valore di **Username** (Nome utente).

Per configurare e testare l'accesso Single Sign-On di Azure AD con BGS Online, è necessario completare i passaggi predefiniti seguenti:

1. **[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** : per abilitare gli utenti all'utilizzo di questa funzionalità.
1. **[Creazione di un utente test di Azure AD](#creating-an-azure-ad-test-user)** : per testare l'accesso Single Sign-On di Azure AD con l'utente Britta Simon.
1. **[Creazione di un utente di test di BGS Online](#creating-a-bgs-online-test-user)**: per avere una controparte di Britta Simon in BGS Online collegata alla rappresentazione dell'utente in Azure AD.
1. **[Assegnazione dell'utente test di Azure AD](#assigning-the-azure-ad-test-user)** : per abilitare Britta Simon all'uso dell'accesso Single Sign-On di Azure AD.
1. **[Testing Single Sign-On](#testing-single-sign-on)** : per verificare se la configurazione funziona.

### <a name="configuring-azure-ad-single-sign-on"></a>Configurazione dell'accesso Single Sign-On di Azure AD

In questa sezione viene abilitato l'accesso Single Sign-On di Azure AD nel portale di Azure e viene configurato l'accesso Single Sign-On nell'applicazione BGS Online.

**Per configurare Single Sign-On di Azure AD con BGS Online, seguire questa procedura:**

1. Nella pagina di integrazione dell'applicazione **BGS Online** del portale di Azure fare clic su **Single Sign-On**.

    ![Configure Single Sign-On][4]

1. Nella finestra di dialogo **Single Sign-On** selezionare **Accesso basato su SAML** per **Modalità** per abilitare l'accesso Single Sign-On.
 
    ![Configure Single Sign-On](./media/bgsonline-tutorial/tutorial_bgsonline_samlbase.png)

1. Nella sezione **URL e dominio BGS Online** seguire questa procedura:

    ![Configure Single Sign-On](./media/bgsonline-tutorial/tutorial_bgsonline_url.png)

    a. Nella casella di testo **Identificatore** digitare l'URL adottando il modello seguente:

    Per un ambiente di produzione, usare questo modello `https://<company name>.millwardbrown.report` 

    Per un ambiente di test, usare questo modello `https://millwardbrown.marketingtracker.nl/mt5/`

    b. Nella casella di testo **URL di risposta** digitare l'URL usando il modello seguente:
    
    Per un ambiente di produzione, usare questo modello `https://<company name>.millwardbrown.report/sso/saml/AssertionConsumerService.aspx` 
      
    Per un ambiente di test, usare questo modello `https://millwardbrown.marketingtracker.nl/mt5/sso/saml/AssertionConsumerService.aspx`

    > [!NOTE] 
    > Poiché questi non sono i valori reali, è necessario aggiornarli con l'identificatore e l'URL di risposta effettivi. Per ottenere questi valori contattare il [team di supporto di BGS Online](mailTo:bgsdashboardteam@millwardbrown.com).
 

1. Nella sezione **Certificato di firma SAML** fare clic su **XML di metadati** e quindi salvare il file dei metadati nel computer.

    ![Configure Single Sign-On](./media/bgsonline-tutorial/tutorial_bgsonline_certificate.png) 

1. Fare clic sul pulsante **Salva** .

    ![Configure Single Sign-On](./media/bgsonline-tutorial/tutorial_general_400.png)

1. Nella sezione **Configurazione di BGS Online** fare clic su **Configura BGS Online** per aprire la finestra **Configura accesso**. Copiare l'**URL servizio Single Sign-On SAML** dalla **sezione Riferimento rapido.**

    ![Configure Single Sign-On](./media/bgsonline-tutorial/tutorial_bgsonline_configure.png) 

1. Per configurare l'accesso Single Sign-On sul lato **BGS Online**, è necessario inviare il file **XML metadati** scaricato e il valore dell'**URL del servizio Single Sign-On SAML** al [team di supporto di BGS Online](mailto:bgsdashboardteam@millwardbrown.com). 


> [!TIP]
> Un riepilogo delle istruzioni è disponibile all'interno del [portale di Azure](https://portal.azure.com) durante la configurazione dell'app.  Dopo aver aggiunto l'app dalla sezione **Active Directory > Applicazioni aziendali** è sufficiente fare clic sulla scheda **Single Sign-On** e accedere alla documentazione incorporata tramite la sezione **Configurazione** nella parte inferiore. Altre informazioni sulla funzione di documentazione incorporata sono disponibili in [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985) (Documentazione incorporata di Azure AD).

### <a name="creating-an-azure-ad-test-user"></a>Creazione di un utente test di Azure AD
Questa sezione descrive come creare un utente test denominato Britta Simon nel portale di Azure.

![Creare un utente di Azure AD][100]

**Per creare un utente test in Azure AD, eseguire la procedura seguente:**

1. Nel **portale di Azure** fare clic sull'icona di **Azure Active Directory** nel riquadro di spostamento sinistro.

    ![Creazione di un utente test di Azure AD](./media/bgsonline-tutorial/create_aaduser_01.png) 

1. Passare a **Utenti e gruppi** e fare clic su **Tutti gli utenti** per visualizzare l'elenco di utenti.
    
    ![Creazione di un utente test di Azure AD](./media/bgsonline-tutorial/create_aaduser_02.png) 

1. Nella parte superiore della finestra di dialogo fare clic su **Aggiungi** per aprire la finestra di dialogo **Utente**.
 
    ![Creazione di un utente test di Azure AD](./media/bgsonline-tutorial/create_aaduser_03.png) 

1. Nella pagina della finestra di dialogo **Utente** seguire questa procedura:
 
    ![Creazione di un utente test di Azure AD](./media/bgsonline-tutorial/create_aaduser_04.png) 

    a. Nella casella di testo **Nome** digitare **BrittaSimon**.

    b. Nella casella di testo **Nome utente** digitare l'**indirizzo di posta elettronica** di BrittaSimon.

    c. Selezionare **Mostra password** e prendere nota del valore della **Password**.

    d. Fare clic su **Create**(Crea).
 
### <a name="creating-a-bgs-online-test-user"></a>Creazione di un utente di test di BGS Online

In questa sezione viene creato un utente di nome Britta Simon in BGS Online. Collaborare con il [team di supporto di BGS Online](mailto:bgsdashboardteam@millwardbrown.com) per aggiungere gli utenti alla piattaforma BGS Online.

### <a name="assigning-the-azure-ad-test-user"></a>Assegnazione dell'utente test di Azure AD

In questa sezione Britta Simon viene abilitata per l'uso dell'accesso Single Sign-On di Azure concedendole l'accesso a BGS Online.

![Assegna utente][200] 

**Per assegnare Britta Simon a BGS Online, seguire questa procedura:**

1. Nel portale di Azure aprire la visualizzazione delle applicazioni e quindi la visualizzazione delle directory e passare ad **Applicazioni aziendali**, quindi fare clic su **Tutte le applicazioni**.

    ![Assegna utente][201] 

1. Nell'elenco delle applicazioni selezionare **BGS Online**.

    ![Configure Single Sign-On](./media/bgsonline-tutorial/tutorial_bgsonline_app.png) 

1. Scegliere **Utenti e gruppi** dal menu a sinistra.

    ![Assegna utente][202] 

1. Fare clic sul pulsante **Aggiungi**. Selezionare quindi **Utenti e gruppi** nella finestra di dialogo **Aggiungi assegnazione**.

    ![Assegna utente][203]

1. Nella finestra di dialogo **Utenti e gruppi** selezionare **Britta Simon** nell'elenco Utenti.

1. Fare clic sul pulsante **Seleziona** nella finestra di dialogo **Utenti e gruppi**.

1. Fare clic sul pulsante **Assegna** nella finestra di dialogo **Aggiungi assegnazione**.
    
### <a name="testing-single-sign-on"></a>Test dell'accesso Single Sign-On

In questa sezione viene testata la configurazione dell'accesso Single Sign-On di Azure AD usando il pannello di accesso.

Quando si fa clic sul riquadro BGS Online nel pannello di accesso, si dovrebbe accedere automaticamente all'applicazione BGS Online.

## <a name="additional-resources"></a>Risorse aggiuntive

* [Elenco di esercitazioni sulla procedura di integrazione delle app SaaS con Azure Active Directory](tutorial-list.md)
* [Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory](../manage-apps/what-is-single-sign-on.md)



<!--Image references-->

[1]: ./media/bgsonline-tutorial/tutorial_general_01.png
[2]: ./media/bgsonline-tutorial/tutorial_general_02.png
[3]: ./media/bgsonline-tutorial/tutorial_general_03.png
[4]: ./media/bgsonline-tutorial/tutorial_general_04.png

[100]: ./media/bgsonline-tutorial/tutorial_general_100.png

[200]: ./media/bgsonline-tutorial/tutorial_general_200.png
[201]: ./media/bgsonline-tutorial/tutorial_general_201.png
[202]: ./media/bgsonline-tutorial/tutorial_general_202.png
[203]: ./media/bgsonline-tutorial/tutorial_general_203.png

