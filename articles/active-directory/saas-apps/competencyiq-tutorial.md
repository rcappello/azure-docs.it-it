---
title: 'Esercitazione: Integrazione di Azure Active Directory con CompetencyIQ | Microsoft Docs'
description: Informazioni su come configurare l'accesso Single Sign-On tra Azure Active Directory e CompetencyIQ.
services: active-directory
documentationCenter: na
author: jeevansd
manager: mtillman
ms.assetid: e262bf7e-cc7d-4d0e-aea7-861f00d8837d
ms.service: active-directory
ms.component: saas-app-tutorial
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/21/2017
ms.author: jeedes
ms.openlocfilehash: 8cb474c56e1802ccfe828f0040ae231f0748551e
ms.sourcegitcommit: 1d850f6cae47261eacdb7604a9f17edc6626ae4b
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 08/02/2018
ms.locfileid: "39437006"
---
# <a name="tutorial-azure-active-directory-integration-with-competencyiq"></a>Esercitazione: Integrazione di Azure Active Directory con CompetencyIQ

Questa esercitazione descrive come integrare CompetencyIQ con Azure Active Directory (Azure AD).

L'integrazione di CompetencyIQ con Azure AD offre i vantaggi seguenti:

- È possibile controllare in Azure AD chi può accedere a CompetencyIQ
- È possibile abilitare gli utenti per l'accesso automatico a CompetencyIQ (Single Sign-On) con gli account Azure AD personali
- È possibile gestire gli account in un'unica posizione centrale: il portale di Azure.

Per altre informazioni sull'integrazione di app SaaS con Azure AD, vedere [Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory](../manage-apps/what-is-single-sign-on.md).

## <a name="prerequisites"></a>Prerequisiti

Per configurare l'integrazione di Azure AD con CompetencyIQ, sono necessari gli elementi seguenti:

- Sottoscrizione di Azure AD
- Sottoscrizione di CompetencyIQ abilitata per l'accesso Single Sign-On

> [!NOTE]
> Non è consigliabile usare un ambiente di produzione per testare i passaggi di questa esercitazione.

A questo scopo, è consigliabile seguire le indicazioni seguenti:

- Non usare l'ambiente di produzione a meno che non sia necessario.
- Se non si dispone di un ambiente di prova di Azure AD, è possibile ottenere una versione di valutazione di un mese [qui](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Descrizione dello scenario
In questa esercitazione viene eseguito il test dell'accesso Single Sign-On di Azure AD in un ambiente di test. Lo scenario descritto in questa esercitazione prevede le due fasi fondamentali seguenti:

1. Aggiunta di CompetencyIQ dalla raccolta
1. Configurazione e test dell'accesso Single Sign-On di Azure AD

## <a name="adding-competencyiq-from-the-gallery"></a>Aggiunta di CompetencyIQ dalla raccolta
Per configurare l'integrazione di CompetencyIQ in Azure AD, è necessario aggiungere CompetencyIQ dalla raccolta all'elenco di app SaaS gestite.

**Per aggiungere CompetencyIQ dalla raccolta, seguire questa procedura:**

1. Nel **[portale di Azure](https://portal.azure.com)** fare clic sull'icona di **Azure Active Directory** nel riquadro di spostamento sinistro. 

    ![Active Directory][1]

1. Passare ad **Applicazioni aziendali**. Andare quindi a **Tutte le applicazioni**.

    ![APPLICAZIONI][2]
    
1. Fare clic sul pulsante **Nuova applicazione** nella parte superiore della finestra di dialogo per aggiungere una nuova applicazione.

    ![APPLICAZIONI][3]

1. Nella casella di ricerca digitare **CompetencyIQ**.

    ![Creazione di un utente test di Azure AD](./media/competencyiq-tutorial/tutorial_competencyiq_search.png)

1. Nel pannello dei risultati selezionare **CompetencyIQ** e quindi fare clic sul pulsante **Aggiungi** per aggiungere l'applicazione.

    ![Creazione di un utente test di Azure AD](./media/competencyiq-tutorial/tutorial_competencyiq_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Configurazione e test dell'accesso Single Sign-On di Azure AD
In questa sezione viene configurato e testato l'accesso Single Sign-On di Azure AD con CompetencyIQ usando un utente di test di nome "Britta Simon".

Per il funzionamento dell'accesso Single Sign-On, Azure AD deve conoscere l'utente controparte di CompetencyIQ corrispondente a un utente di Azure AD. In altre parole, deve essere stabilita una relazione di collegamento tra un utente di Azure AD e l'utente correlato in CompetencyIQ.

Per stabilire la relazione di collegamento, in CompetencyIQ assegnare il valore del **nome utente** in Azure AD come valore di **Username** (Nome utente).

Per configurare e testare l'accesso Single Sign-On di Azure AD con CompetencyIQ, è necessario completare le procedure di base seguenti:

1. **[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** : per abilitare gli utenti all'utilizzo di questa funzionalità.
1. **[Creazione di un utente test di Azure AD](#creating-an-azure-ad-test-user)** : per testare l'accesso Single Sign-On di Azure AD con l'utente Britta Simon.
1. **[Creazione di un utente di test di CompetencyIQ](#creating-a-competencyiq-test-user)**: per avere una controparte di Britta Simon in CompetencyIQ collegata alla rappresentazione dell'utente in Azure AD.
1. **[Assegnazione dell'utente test di Azure AD](#assigning-the-azure-ad-test-user)** : per abilitare Britta Simon all'uso dell'accesso Single Sign-On di Azure AD.
1. **[Testing Single Sign-On](#testing-single-sign-on)** : per verificare se la configurazione funziona.

### <a name="configuring-azure-ad-single-sign-on"></a>Configurazione dell'accesso Single Sign-On di Azure AD

In questa sezione viene abilitato l'accesso Single Sign-On di Azure AD nel nuovo portale di Azure e viene configurato l'accesso Single Sign-On nell'applicazione CompetencyIQ.

**Per configurare l'accesso Single Sign-On di Azure AD con CompetencyIQ, seguire questa procedura:**

1. Nella pagina di integrazione dell'applicazione **CompetencyIQ** del portale di Azure fare clic su **Single Sign-On**.

    ![Configure Single Sign-On][4]

1. Nella finestra di dialogo **Single Sign-On** selezionare **Accesso basato su SAML** per **Modalità** per abilitare l'accesso Single Sign-On.
 
    ![Configure Single Sign-On](./media/competencyiq-tutorial/tutorial_competencyiq_samlbase.png)

1. Nella sezione **URL e dominio CompetencyIQ** seguire questa procedura:

    ![Configure Single Sign-On](./media/competencyiq-tutorial/tutorial_competencyiq_url1.png)

    a. Nella casella di testo **URL di accesso** digitare l'URL usando il modello seguente: `https://<customer>.competencyiq.com/`
    
    b. Nella casella di testo **Identificatore** digitare l'URL: `https://www.competencyiq.com/`

    > [!NOTE] 
    > Poiché non è reale, è necessario aggiornare questo valore con l'URL di disconnessione effettivo. Per ottenere il valore, contattare il [team di supporto clienti di CompetencyIQ](https://www.competencyiq.com/). 
 
1. Nella sezione **Certificato di firma SAML** fare clic su **XML di metadati** e quindi salvare il file dei metadati nel computer.

    ![Configure Single Sign-On](./media/competencyiq-tutorial/tutorial_competencyiq_certificate.png) 

1. Fare clic sul pulsante **Salva** .

    ![Configure Single Sign-On](./media/competencyiq-tutorial/tutorial_general_400.png)

1. Nella sezione **Configurazione di CompetencyIQ** fare clic su **Configura CompetencyIQ** per aprire la finestra **Configura accesso**. Copiare l'**ID di entità SAML** e l'**URL del servizio Single Sign-On SAML** dalla sezione **Riferimento rapido**.

    ![Configure Single Sign-On](./media/competencyiq-tutorial/tutorial_competencyiq_configure.png) 

1. Per configurare l'accesso Single Sign-On sul lato **CompetencyIQ**, è necessario inviare il file **XML metadati** scaricato, l'**ID di entità SAML** e l'**URL del servizio Single Sign-On SAML** al [team di supporto di CompetencyIQ](https://www.competencyiq.com/). La configurazione viene eseguita in modo che la connessione SSO SAML sia impostata correttamente su entrambi i lati.

> [!TIP]
> Un riepilogo delle istruzioni è disponibile all'interno del [portale di Azure](https://portal.azure.com) durante la configurazione dell'app.  Dopo aver aggiunto l'app dalla sezione **Active Directory > Applicazioni aziendali** è sufficiente fare clic sulla scheda **Single Sign-On** e accedere alla documentazione incorporata tramite la sezione **Configurazione** nella parte inferiore. Altre informazioni sulla funzione di documentazione incorporata sono disponibili in [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985) (Documentazione incorporata di Azure AD).
> 

### <a name="creating-an-azure-ad-test-user"></a>Creazione di un utente test di Azure AD
Questa sezione descrive come creare un utente test denominato Britta Simon nel portale di Azure.

![Creare un utente di Azure AD][100]

**Per creare un utente test in Azure AD, eseguire la procedura seguente:**

1. Nel **portale di Azure** fare clic sull'icona di **Azure Active Directory** nel riquadro di spostamento sinistro.

    ![Creazione di un utente test di Azure AD](./media/competencyiq-tutorial/create_aaduser_01.png) 

1. Passare a **Utenti e gruppi** e fare clic su **Tutti gli utenti** per visualizzare l'elenco di utenti.
    
    ![Creazione di un utente test di Azure AD](./media/competencyiq-tutorial/create_aaduser_02.png) 

1. Nella parte superiore della finestra di dialogo fare clic su **Aggiungi** per aprire la finestra di dialogo **Utente**.
 
    ![Creazione di un utente test di Azure AD](./media/competencyiq-tutorial/create_aaduser_03.png) 

1. Nella pagina della finestra di dialogo **Utente** seguire questa procedura:
 
    ![Creazione di un utente test di Azure AD](./media/competencyiq-tutorial/create_aaduser_04.png) 

    a. Nella casella di testo **Nome** digitare **BrittaSimon**.

    b. Nella casella di testo **Nome utente** digitare l'**indirizzo di posta elettronica** di BrittaSimon.

    c. Selezionare **Mostra password** e prendere nota del valore della **Password**.

    d. Fare clic su **Create**(Crea).
 
### <a name="creating-a-competencyiq-test-user"></a>Creazione di un utente di test di CompetencyIQ

Per consentire agli utenti di Azure AD di accedere a CompetencyIQ, è necessario effettuarne il provisioning in CompetencyIQ. Contattare il [team di supporto di CompetencyIQ](https://www.competencyiq.com/) per creare gli utenti nell'applicazione.

### <a name="assigning-the-azure-ad-test-user"></a>Assegnazione dell'utente test di Azure AD

In questa sezione Britta Simon viene abilitata per l'uso dell'accesso Single Sign-On di Azure concedendole l'accesso a CompetencyIQ.

![Assegna utente][200] 

**Per assegnare Britta Simon a CompetencyIQ, seguire questa procedura:**

1. Nel portale di Azure aprire la visualizzazione delle applicazioni e quindi la visualizzazione delle directory e passare ad **Applicazioni aziendali**, quindi fare clic su **Tutte le applicazioni**.

    ![Assegna utente][201] 

1. Nell'elenco delle applicazioni selezionare **CompetencyIQ**.

    ![Configure Single Sign-On](./media/competencyiq-tutorial/tutorial_competencyiq_app.png) 

1. Scegliere **Utenti e gruppi** dal menu a sinistra.

    ![Assegna utente][202] 

1. Fare clic sul pulsante **Aggiungi**. Selezionare quindi **Utenti e gruppi** nella finestra di dialogo **Aggiungi assegnazione**.

    ![Assegna utente][203]

1. Nella finestra di dialogo **Utenti e gruppi** selezionare **Britta Simon** nell'elenco Utenti.

1. Fare clic sul pulsante **Seleziona** nella finestra di dialogo **Utenti e gruppi**.

1. Fare clic sul pulsante **Assegna** nella finestra di dialogo **Aggiungi assegnazione**.
    
### <a name="testing-single-sign-on"></a>Test dell'accesso Single Sign-On

In questa sezione viene testata la configurazione dell'accesso Single Sign-On di Azure AD usando il pannello di accesso.

Quando si fa clic sul riquadro CompetencyIQ nel pannello di accesso, si dovrebbe accedere automaticamente all'applicazione CompetencyIQ.
Per altre informazioni sul pannello di accesso, vedere [Introduzione al Pannello di accesso](../user-help/active-directory-saas-access-panel-introduction.md). 

## <a name="additional-resources"></a>Risorse aggiuntive

* [Elenco di esercitazioni sulla procedura di integrazione delle app SaaS con Azure Active Directory](tutorial-list.md)
* [Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory](../manage-apps/what-is-single-sign-on.md)



<!--Image references-->

[1]: ./media/competencyiq-tutorial/tutorial_general_01.png
[2]: ./media/competencyiq-tutorial/tutorial_general_02.png
[3]: ./media/competencyiq-tutorial/tutorial_general_03.png
[4]: ./media/competencyiq-tutorial/tutorial_general_04.png

[100]: ./media/competencyiq-tutorial/tutorial_general_100.png

[200]: ./media/competencyiq-tutorial/tutorial_general_200.png
[201]: ./media/competencyiq-tutorial/tutorial_general_201.png
[202]: ./media/competencyiq-tutorial/tutorial_general_202.png
[203]: ./media/competencyiq-tutorial/tutorial_general_203.png

