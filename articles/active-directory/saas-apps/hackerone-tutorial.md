---
title: 'Esercitazione: Integrazione di Azure Active Directory con HackerOne | Microsoft Docs'
description: Informazioni su come configurare l'accesso Single Sign-On tra Azure Active Directory e HackerOne.
services: active-directory
documentationCenter: na
author: jeevansd
manager: mtillman
ms.assetid: 229d1efb-b6a5-4df8-9839-5d551487db4e
ms.service: active-directory
ms.component: saas-app-tutorial
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/28/2017
ms.author: jeedes
ms.openlocfilehash: 4e33ad66fe0ced9a426a608f4193ff52dec4f7ee
ms.sourcegitcommit: 1d850f6cae47261eacdb7604a9f17edc6626ae4b
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 08/02/2018
ms.locfileid: "39441834"
---
# <a name="tutorial-azure-active-directory-integration-with-hackerone"></a>Esercitazione: Integrazione di Azure Active Directory con HackerOne

Questa esercitazione descrive come integrare HackerOne con Azure Active Directory (Azure AD).

L'integrazione di HackerOne con Azure AD offre i vantaggi seguenti:

- È possibile controllare in Azure AD chi può accedere a HackerOne
- È possibile abilitare gli utenti per l'accesso automatico a HackerOne (Single Sign-On) con l'account Azure AD.
- È possibile gestire gli account in un'unica posizione centrale: il portale di Azure.

Per altre informazioni sull'integrazione di app SaaS con Azure AD, vedere [Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory](../manage-apps/what-is-single-sign-on.md).

## <a name="prerequisites"></a>Prerequisiti

Per configurare l'integrazione di Azure AD con HackerOne, sono necessari gli elementi seguenti:

- Sottoscrizione di Azure AD
- Sottoscrizione di HackerOne abilitata per l'accesso Single Sign-On

> [!NOTE]
> Non è consigliabile usare un ambiente di produzione per testare i passaggi di questa esercitazione.

A questo scopo, è consigliabile seguire le indicazioni seguenti:

- Non usare l'ambiente di produzione a meno che non sia necessario.
- Se non si dispone di un ambiente di prova di Azure AD, è possibile ottenere una versione di valutazione di un mese [qui](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Descrizione dello scenario
In questa esercitazione viene eseguito il test dell'accesso Single Sign-On di Azure AD in un ambiente di test. Lo scenario descritto in questa esercitazione prevede le due fasi fondamentali seguenti:

1. Aggiunta di HackerOne dalla raccolta
1. Configurazione e test dell'accesso Single Sign-On di Azure AD

## <a name="adding-hackerone-from-the-gallery"></a>Aggiunta di HackerOne dalla raccolta
Per configurare l'integrazione di HackerOne in Azure AD, è necessario aggiungere HackerOne dalla raccolta all'elenco di app SaaS gestite.

**Per aggiungere HackerOne dalla raccolta, seguire questa procedura:**

1. Nel **[portale di Azure](https://portal.azure.com)** fare clic sull'icona di **Azure Active Directory** nel riquadro di spostamento sinistro. 

    ![Active Directory][1]

1. Passare ad **Applicazioni aziendali**. Andare quindi a **Tutte le applicazioni**.

    ![APPLICAZIONI][2]
    
1. Fare clic sul pulsante **Nuova applicazione** nella parte superiore della finestra di dialogo per aggiungere una nuova applicazione.

    ![APPLICAZIONI][3]

1. Nella casella di ricerca digitare **HackerOne**.

    ![Creazione di un utente test di Azure AD](./media/hackerone-tutorial/tutorial_hackerone_search.png)

1. Nel pannello dei risultati selezionare **HackerOne** e quindi fare clic sul pulsante **Aggiungi** per aggiungere l'applicazione.

    ![Creazione di un utente test di Azure AD](./media/hackerone-tutorial/tutorial_hackerone_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Configurazione e test dell'accesso Single Sign-On di Azure AD

In questa sezione viene configurato e testato l'accesso Single Sign-On di Azure AD con HackerOne usando un utente di test di nome "Britta Simon".

Per il funzionamento dell'accesso Single Sign-On, Azure AD deve conoscere l'utente controparte di HackerOne corrispondente a un utente di Azure AD. In altre parole, deve essere stabilita una relazione di collegamento tra un utente di Azure AD e l'utente correlato in HackerOne.

Per stabilire la relazione di collegamento, in HackerOne assegnare il valore del **nome utente** in Azure AD come valore di **Username** (Nome utente).

Per configurare e testare l'accesso Single Sign-On di Azure AD con HackerOne, è necessario completare i blocchi predefiniti seguenti:

1. **[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** : per abilitare gli utenti all'utilizzo di questa funzionalità.
1. **[Creazione di un utente test di Azure AD](#creating-an-azure-ad-test-user)** : per testare l'accesso Single Sign-On di Azure AD con l'utente Britta Simon.
1. **[Creazione di un utente di test di HackerOne](#creating-a-hackerone-test-user)**: per avere una controparte di Britta Simon in HackerOne collegata alla rappresentazione dell'utente in Azure AD.
1. **[Assegnazione dell'utente test di Azure AD](#assigning-the-azure-ad-test-user)** : per abilitare Britta Simon all'uso dell'accesso Single Sign-On di Azure AD.
1. **[Testing Single Sign-On](#testing-single-sign-on)** : per verificare se la configurazione funziona.

### <a name="configuring-azure-ad-single-sign-on"></a>Configurazione dell'accesso Single Sign-On di Azure AD

In questa sezione viene abilitato l'accesso Single Sign-On di Azure AD nel portale di Azure e viene configurato l'accesso Single Sign-On nell'applicazione HackerOne.

**Per configurare l'accesso Single Sign-On di Azure AD con HackerOne, seguire questa procedura:**

1. Nella pagina di integrazione dell'applicazione **HackerOne** del portale di Azure fare clic su **Single Sign-On**.

    ![Configure Single Sign-On][4]

1. Nella finestra di dialogo **Single Sign-On** selezionare **Accesso basato su SAML** per **Modalità** per abilitare l'accesso Single Sign-On.
 
    ![Configure Single Sign-On](./media/hackerone-tutorial/tutorial_hackerone_samlbase.png)

1. Nella sezione **HackerOne Single sign-on URL and Identifier** (Identificatore e URL Single Sign-On di HackerOne) seguire questa procedura:

    ![Configure Single Sign-On](./media/hackerone-tutorial/tutorial_hackerone_url.png)

    a. Nella casella di testo **URL di accesso** digitare l'URL usando il modello seguente: `https://hackerone.com/<company name>/authentication`

    b. Nella casella di testo **Identificatore** digitare un URL come indicato di seguito: `https://hackerone.com/users/saml/metadata`
    
    > [!NOTE] 
    > Poiché non è reale, è necessario aggiornare questo valore con l'URL di accesso Sign-On effettivo. Per ottenere questo valore, contattare il [team di supporto di HackerOne](mailto:support@hackerone.com). 
 
1. Nella sezione **Certificato di firma SAML** fare clic su **Certificato (Base64)** e quindi salvare il file del certificato nel computer.

    ![Configure Single Sign-On](./media/hackerone-tutorial/tutorial_hackerone_certificate.png) 

1. Fare clic sul pulsante **Salva** .

    ![Configure Single Sign-On](./media/hackerone-tutorial/tutorial_general_400.png)

1. Nella sezione **Configurazione di HackerOne** fare clic su **Configura HackerOne** per aprire la finestra **Configura accesso**. Copiare l'**URL servizio Single Sign-On SAML** dalla **sezione Riferimento rapido.**

    ![Configure Single Sign-On](./media/hackerone-tutorial/tutorial_hackerone_configure.png) 

1. Accedere al tenant di HackerOne come amministratore.

1. Nel menu in alto fare clic su **Settings** (Impostazioni).
   
    ![Configure Single Sign-On](./media/hackerone-tutorial/tutorial_hackerone_001.png) 

1. Passare all'opzione **Authentication** (Autenticazione) e fare clic su **Add SAML settings** (Aggiungi impostazioni SAML).
   
    ![Configure Single Sign-On](./media/hackerone-tutorial/tutorial_hackerone_003.png) 

1. Nella finestra di dialogo **SAML Settings** (Impostazioni SAML) seguire questa procedura:
   
    ![Configure Single Sign-On](./media/hackerone-tutorial/tutorial_hackerone_004.png) 

    a. Nella casella di testo **Email Domain** (Dominio di posta elettronica) digitare un dominio registrato.

    b. Nella casella di testo **Single Sign On URL** (URL Single Sign-On) incollare il valore dell'**URL del servizio Single Sign-On SAML** copiato dal portale di Azure.

    c. Aprire nel Blocco note il **file del certificato** scaricato dal portale di Azure, copiarne il contenuto negli Appunti e incollarlo nella casella di testo **X509 Certificate** (Certificato X.509).
    
    d. Fare clic su **Save**.

1. Nella finestra di dialogo relativa alle impostazioni di autenticazione seguire questa procedura:
   
    ![Configure Single Sign-On](./media/hackerone-tutorial/tutorial_hackerone_005.png) 

    a. Fare clic su **Run test**(Esegui test).

    b. Se il valore del campo **Status** (Stato) corrisponde a **Last test status: created** (Stato ultimo test: creato), contattare il [team di supporto di HackerOne](mailto:support@hackerone.com) per richiedere una verifica della configurazione.

> [!TIP]
> Un riepilogo delle istruzioni è disponibile all'interno del [portale di Azure](https://portal.azure.com) durante la configurazione dell'app.  Dopo aver aggiunto l'app dalla sezione **Active Directory > Applicazioni aziendali** è sufficiente fare clic sulla scheda **Single Sign-On** e accedere alla documentazione incorporata tramite la sezione **Configurazione** nella parte inferiore. Altre informazioni sulla funzione di documentazione incorporata sono disponibili in [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985) (Documentazione incorporata di Azure AD).
> 

### <a name="creating-an-azure-ad-test-user"></a>Creazione di un utente test di Azure AD
Questa sezione descrive come creare un utente test denominato Britta Simon nel portale di Azure.

![Creare un utente di Azure AD][100]

**Per creare un utente test in Azure AD, eseguire la procedura seguente:**

1. Nel **portale di Azure** fare clic sull'icona di **Azure Active Directory** nel riquadro di spostamento sinistro.

    ![Creazione di un utente test di Azure AD](./media/hackerone-tutorial/create_aaduser_01.png) 

1. Passare a **Utenti e gruppi** e fare clic su **Tutti gli utenti** per visualizzare l'elenco di utenti.
    
    ![Creazione di un utente test di Azure AD](./media/hackerone-tutorial/create_aaduser_02.png) 

1. Nella parte superiore della finestra di dialogo fare clic su **Aggiungi** per aprire la finestra di dialogo **Utente**.
 
    ![Creazione di un utente test di Azure AD](./media/hackerone-tutorial/create_aaduser_03.png) 

1. Nella pagina della finestra di dialogo **Utente** seguire questa procedura:
 
    ![Creazione di un utente test di Azure AD](./media/hackerone-tutorial/create_aaduser_04.png) 

    a. Nella casella di testo **Nome** digitare **BrittaSimon**.

    b. Nella casella di testo **Nome utente** digitare l'**indirizzo di posta elettronica** di BrittaSimon.

    c. Selezionare **Mostra password** e prendere nota del valore della **Password**.

    d. Fare clic su **Create**(Crea).
 
### <a name="creating-a-hackerone-test-user"></a>Creazione di un utente test di HackerOne

Successivamente, viene creato un utente chiamato Britta Simon in HackerOne. HackerOne supporta il provisioning JIT (Just-In-Time) che è abilitato per impostazione predefinita.

Non è necessario alcun intervento dell'utente in questa sezione. Quando si accede a HackerOne, viene creato un nuovo utente se non esiste ancora.

>[!NOTE]
>Per creare un utente manualmente, è necessario contattare il team di supporto di HackerOne. 
> 

### <a name="assigning-the-azure-ad-test-user"></a>Assegnazione dell'utente test di Azure AD

In questa sezione Britta Simon viene abilitata per l'uso dell'accesso Single Sign-On di Azure concedendole l'accesso a HackerOne.

![Assegna utente][200] 

**Per assegnare Britta Simon a HackerOne, seguire questa procedura:**

1. Nel portale di Azure aprire la visualizzazione delle applicazioni e quindi la visualizzazione delle directory e passare ad **Applicazioni aziendali**, quindi fare clic su **Tutte le applicazioni**.

    ![Assegna utente][201] 

1. Nell'elenco di applicazioni selezionare **HackerOne**.

    ![Configure Single Sign-On](./media/hackerone-tutorial/tutorial_hackerone_app.png) 

1. Scegliere **Utenti e gruppi** dal menu a sinistra.

    ![Assegna utente][202] 

1. Fare clic sul pulsante **Aggiungi**. Selezionare quindi **Utenti e gruppi** nella finestra di dialogo **Aggiungi assegnazione**.

    ![Assegna utente][203]

1. Nella finestra di dialogo **Utenti e gruppi** selezionare **Britta Simon** nell'elenco Utenti.

1. Fare clic sul pulsante **Seleziona** nella finestra di dialogo **Utenti e gruppi**.

1. Fare clic sul pulsante **Assegna** nella finestra di dialogo **Aggiungi assegnazione**.
    
### <a name="testing-single-sign-on"></a>Test dell'accesso Single Sign-On

Viene infine eseguito il test della configurazione dell'accesso Single Sign-On di Azure AD usando il pannello di accesso.  

Quando si fa clic sul riquadro HackerOne nel pannello di accesso, verrà eseguito automaticamente l'accesso all'applicazione HackerOne.

## <a name="additional-resources"></a>Risorse aggiuntive

* [Elenco di esercitazioni sulla procedura di integrazione delle app SaaS con Azure Active Directory](tutorial-list.md)
* [Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory](../manage-apps/what-is-single-sign-on.md)

<!--Image references-->

[1]: ./media/hackerone-tutorial/tutorial_general_01.png
[2]: ./media/hackerone-tutorial/tutorial_general_02.png
[3]: ./media/hackerone-tutorial/tutorial_general_03.png
[4]: ./media/hackerone-tutorial/tutorial_general_04.png

[100]: ./media/hackerone-tutorial/tutorial_general_100.png

[200]: ./media/hackerone-tutorial/tutorial_general_200.png
[201]: ./media/hackerone-tutorial/tutorial_general_201.png
[202]: ./media/hackerone-tutorial/tutorial_general_202.png
[203]: ./media/hackerone-tutorial/tutorial_general_203.png

