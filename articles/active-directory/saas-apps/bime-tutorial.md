---
title: 'Esercitazione: Integrazione di Azure Active Directory con Bime | Microsoft Docs'
description: Informazioni su come configurare l'accesso Single Sign-On tra Azure Active Directory e Bime.
services: active-directory
documentationCenter: na
author: jeevansd
manager: mtillman
ms.assetid: bdcf0729-c880-4c95-b739-0f6345b17dd8
ms.service: active-directory
ms.component: saas-app-tutorial
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/13/2017
ms.author: jeedes
ms.openlocfilehash: 966c5dcb6f45590fe1b6a8bb2d8b53c37aeed6b2
ms.sourcegitcommit: 1d850f6cae47261eacdb7604a9f17edc6626ae4b
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 08/02/2018
ms.locfileid: "39446596"
---
# <a name="tutorial-azure-active-directory-integration-with-bime"></a>Esercitazione: Integrazione di Azure Active Directory con Bime

Questa esercitazione descrive come integrare Bime con Azure Active Directory (Azure AD).

L'integrazione di Bime con Azure AD offre i vantaggi seguenti:

- È possibile controllare in Azure AD chi può accedere a Bime
- È possibile abilitare gli utenti per l'accesso automatico a Bime (Single Sign-On) con i propri account Azure AD
- È possibile gestire gli account in un'unica posizione centrale: il portale di Azure.

Per altre informazioni sull'integrazione di app SaaS con Azure AD, vedere [Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory](../manage-apps/what-is-single-sign-on.md).

## <a name="prerequisites"></a>Prerequisiti

Per configurare l'integrazione di Azure AD con Bime, sono necessari gli elementi seguenti:

- Sottoscrizione di Azure AD
- Sottoscrizione di Bime abilitata per l'accesso Single Sign-On

> [!NOTE]
> Non è consigliabile usare un ambiente di produzione per testare i passaggi di questa esercitazione.

A questo scopo, è consigliabile seguire le indicazioni seguenti:

- Non usare l'ambiente di produzione a meno che non sia necessario.
- Se non si dispone di un ambiente di prova di Azure AD, è possibile ottenere una versione di valutazione di un mese: [offerta prova](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Descrizione dello scenario
In questa esercitazione viene eseguito il test dell'accesso Single Sign-On di Azure AD in un ambiente di test. Lo scenario descritto in questa esercitazione prevede le due fasi fondamentali seguenti:

1. Aggiunta di Bime dalla raccolta
1. Configurazione e test dell'accesso Single Sign-On di Azure AD

## <a name="adding-bime-from-the-gallery"></a>Aggiunta di Bime dalla raccolta
Per configurare l'integrazione di Bime in Azure AD, è necessario aggiungere Bime dalla raccolta al proprio elenco di app SaaS gestite.

**Per aggiungere Bime dalla raccolta, seguire questa procedura:**

1. Nel **[portale di Azure](https://portal.azure.com)** fare clic sull'icona di **Azure Active Directory** nel riquadro di spostamento sinistro. 

    ![Active Directory][1]

1. Passare ad **Applicazioni aziendali**. Andare quindi a **Tutte le applicazioni**.

    ![APPLICAZIONI][2]
    
1. Fare clic sul pulsante **Nuova applicazione** nella parte superiore della finestra di dialogo per aggiungere una nuova applicazione.

    ![APPLICAZIONI][3]

1. Nella casella di ricerca digitare **Bime**.

    ![Creazione di un utente test di Azure AD](./media/bime-tutorial/tutorial_bime_search.png)

1. Nel pannello dei risultati selezionare **Bime** e quindi fare clic sul pulsante **Aggiungi** per aggiungere l'applicazione.

    ![Creazione di un utente test di Azure AD](./media/bime-tutorial/tutorial_bime_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Configurazione e test dell'accesso Single Sign-On di Azure AD
In questa sezione viene configurato e testato l'accesso Single Sign-On di Azure AD con Bime in base a un utente test di nome "Britta Simon".

Per il funzionamento dell'accesso Single Sign-On, Azure AD deve conoscere qual è l'utente di Bime che corrisponde a un utente di Azure AD. In altre parole, deve essere stabilita una relazione di collegamento tra un utente di Azure AD e l'utente correlato in Bime.

Per stabilire la relazione di collegamento, in Bime assegnare il valore di **nome utente** in Azure AD come valore di **Username** (Nome utente).

Per configurare e testare l'accesso Single Sign-On di Azure AD con Bime, è necessario completare i blocchi predefiniti seguenti:

1. **[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** : per abilitare gli utenti all'utilizzo di questa funzionalità.
1. **[Creazione di un utente test di Azure AD](#creating-an-azure-ad-test-user)** : per testare l'accesso Single Sign-On di Azure AD con l'utente Britta Simon.
1. **[Creazione di un utente di test di Bime](#creating-a-bime-test-user)**: per avere una controparte di Britta Simon in Bime collegata alla rappresentazione dell'utente in Azure AD.
1. **[Assegnazione dell'utente test di Azure AD](#assigning-the-azure-ad-test-user)** : per abilitare Britta Simon all'uso dell'accesso Single Sign-On di Azure AD.
1. **[Testing Single Sign-On](#testing-single-sign-on)** : per verificare se la configurazione funziona.

### <a name="configuring-azure-ad-single-sign-on"></a>Configurazione dell'accesso Single Sign-On di Azure AD

In questa sezione viene abilitato l'accesso Single Sign-On di Azure AD nel portale di Azure e viene configurato l'accesso Single Sign-On nell'applicazione Bime.

**Per configurare l'accesso Single Sign-On di Azure AD con Bime, seguire questa procedura:**

1. Nella pagina di integrazione dell'applicazione **Bime** del portale di Azure fare clic su **Single Sign-On**.

    ![Configure Single Sign-On][4]

1. Nella finestra di dialogo **Single Sign-On** selezionare **Accesso basato su SAML** per **Modalità** per abilitare l'accesso Single Sign-On.
 
    ![Configure Single Sign-On](./media/bime-tutorial/tutorial_bime_samlbase.png)

1. Nella sezione **URL e dominio Bime** seguire questa procedura:

    ![Configure Single Sign-On](./media/bime-tutorial/tutorial_bime_url.png)

    a. Nella casella di testo **URL di accesso** digitare l'URL usando il modello seguente: `https://<tenant-name>.Bimeapp.com`

    b. Nella casella di testo **Identificatore** digitare l'URL adottando il modello seguente: `https://<tenant-name>.Bimeapp.com`

    > [!NOTE] 
    > Poiché questi non sono i valori reali, Aggiornare questi valori con l'identificatore e l'URL di accesso effettivi. Per ottenere questi valori contattare il [team di supporto clienti di Bime](https://bime.zendesk.com/hc/categories/202604307-Support-tech-notes-and-tips-). 
 
1. Nella sezione **Certificato di firma SAML** copiare il valore **IDENTIFICAZIONE PERSONALE** dal certificato.

    ![Configure Single Sign-On](./media/bime-tutorial/tutorial_bime_certificate.png) 

1. Fare clic sul pulsante **Salva** .

    ![Configure Single Sign-On](./media/bime-tutorial/tutorial_general_400.png)

1. Nella sezione **Configurazione di Bime** fare clic su **Configura Bime** per aprire la finestra **Configura accesso**. Copiare l'**URL servizio Single Sign-On SAML** dalla **sezione Riferimento rapido.**

    ![Configure Single Sign-On](./media/bime-tutorial/tutorial_bime_configure.png) 

1. In un'altra finestra del Web browser accedere al sito aziendale di Bime come amministratore.

1. Nella barra degli strumenti fare clic su **Admin** e quindi su **Account**.
   
    ![Amministratore](./media/bime-tutorial/ic775558.png "Amministratore")

1. Nella pagina di configurazione dell’account, eseguire la procedura seguente:
   
    ![Configurare l'accesso Single Sign-On](./media/bime-tutorial/ic775559.png "Configurare l'accesso Single Sign-On")
   
    a. Selezionare **Enable SAML authentication**.

    b. Nella casella di testo **Remote login URL** (URL di accesso remoto) incollare il valore dell'**URL del servizio Single Sign-On SAML** copiato dal portale di Azure.

    c.  Incollare il valore **Identificazione personale** dal portale di Azure nella casella di testo **Certificate Fingerprint** (Impronta digitale certificato).       
   
    d. Fare clic su **Save**.

> [!TIP]
> Un riepilogo delle istruzioni è disponibile all'interno del [portale di Azure](https://portal.azure.com) durante la configurazione dell'app.  Dopo aver aggiunto l'app dalla sezione **Active Directory > Applicazioni aziendali** è sufficiente fare clic sulla scheda **Single Sign-On** e accedere alla documentazione incorporata tramite la sezione **Configurazione** nella parte inferiore. Altre informazioni sulla funzione di documentazione incorporata sono disponibili in [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985) (Documentazione incorporata di Azure AD).
> 

### <a name="creating-an-azure-ad-test-user"></a>Creazione di un utente test di Azure AD
Questa sezione descrive come creare un utente test denominato Britta Simon nel portale di Azure.

![Creare un utente di Azure AD][100]

**Per creare un utente test in Azure AD, eseguire la procedura seguente:**

1. Nel **portale di Azure** fare clic sull'icona di **Azure Active Directory** nel riquadro di spostamento sinistro.

    ![Creazione di un utente test di Azure AD](./media/bime-tutorial/create_aaduser_01.png) 

1. Passare a **Utenti e gruppi** e fare clic su **Tutti gli utenti** per visualizzare l'elenco di utenti.
    
    ![Creazione di un utente test di Azure AD](./media/bime-tutorial/create_aaduser_02.png) 

1. Nella parte superiore della finestra di dialogo fare clic su **Aggiungi** per aprire la finestra di dialogo **Utente**.
 
    ![Creazione di un utente test di Azure AD](./media/bime-tutorial/create_aaduser_03.png) 

1. Nella pagina della finestra di dialogo **Utente** seguire questa procedura:
 
    ![Creazione di un utente test di Azure AD](./media/bime-tutorial/create_aaduser_04.png) 

    a. Nella casella di testo **Nome** digitare **BrittaSimon**.

    b. Nella casella di testo **Nome utente** digitare l'**indirizzo di posta elettronica** di BrittaSimon.

    c. Selezionare **Mostra password** e prendere nota del valore della **Password**.

    d. Fare clic su **Create**(Crea).
 
### <a name="creating-a-bime-test-user"></a>Creazione di un utente test di Bime

Per consentire agli utenti di Azure AD di accedere a Bime, è necessario eseguirne il provisioning in Bime. Nel caso di Bime, il provisioning è un'attività manuale.

**Per configurare il provisioning utenti, seguire questa procedura:**

1. Accedere al tenant di **Bime** .

1. Nella barra degli strumenti fare clic su **Admin** e quindi su **Users** (Utenti).
   
    ![Amministratore](./media/bime-tutorial/ic775561.png "Amministratore")

1. In **Users List** (Elenco utenti) fare clic su **"+"** per aggiungere un nuovo utente.
   
    ![Utenti](./media/bime-tutorial/ic775562.png "Utenti")

1. Nella finestra di dialogo **Dettagli utente** seguire questa procedura:
   
    ![Dettagli utente](./media/bime-tutorial/ic775563.png "Dettagli utente")
   
    a. Nella casella di testo **First name** (Nome) immettere il nome dell'utente, ad esempio **Britta**.

    b. Nella casella di testo **Last name** (Cognome) immettere il cognome dell'utente, ad esempio **Simon**.
 
    c. Nella casella di testo **Email** (Posta elettronica) immettere l'indirizzo di posta elettronica dell'utente, ad esempio **brittasimon@contoso.com**.

    d. Fare clic su **Save**.

>[!NOTE]
>È possibile usare qualsiasi altro strumento o API di creazione di account utente fornita da Bime per eseguire il provisioning degli account utente di AAD.
>  

### <a name="assigning-the-azure-ad-test-user"></a>Assegnazione dell'utente test di Azure AD

In questa sezione Britta Simon viene abilitata per l'uso dell'accesso Single Sign-On di Azure concedendole l'accesso a Bime.

![Assegna utente][200] 

**Per assegnare Britta Simon a Bime, seguire questa procedura:**

1. Nel portale di Azure aprire la visualizzazione delle applicazioni e quindi la visualizzazione delle directory e passare ad **Applicazioni aziendali**, quindi fare clic su **Tutte le applicazioni**.

    ![Assegna utente][201] 

1. Nell'elenco delle applicazioni selezionare **Bime**.

    ![Configure Single Sign-On](./media/bime-tutorial/tutorial_bime_app.png) 

1. Scegliere **Utenti e gruppi** dal menu a sinistra.

    ![Assegna utente][202] 

1. Fare clic sul pulsante **Aggiungi**. Selezionare quindi **Utenti e gruppi** nella finestra di dialogo **Aggiungi assegnazione**.

    ![Assegna utente][203]

1. Nella finestra di dialogo **Utenti e gruppi** selezionare **Britta Simon** nell'elenco Utenti.

1. Fare clic sul pulsante **Seleziona** nella finestra di dialogo **Utenti e gruppi**.

1. Fare clic sul pulsante **Assegna** nella finestra di dialogo **Aggiungi assegnazione**.
    
### <a name="testing-single-sign-on"></a>Test dell'accesso Single Sign-On

Questa sezione descrive come testare la configurazione dell'accesso Single Sign-On di Azure AD usando il pannello di accesso.

Quando si fa clic sul riquadro Bime nel pannello di accesso, si dovrebbe accedere automaticamente all'applicazione Bime.

## <a name="additional-resources"></a>Risorse aggiuntive

* [Elenco di esercitazioni sulla procedura di integrazione delle app SaaS con Azure Active Directory](tutorial-list.md)
* [Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory](../manage-apps/what-is-single-sign-on.md)



<!--Image references-->

[1]: ./media/bime-tutorial/tutorial_general_01.png
[2]: ./media/bime-tutorial/tutorial_general_02.png
[3]: ./media/bime-tutorial/tutorial_general_03.png
[4]: ./media/bime-tutorial/tutorial_general_04.png

[100]: ./media/bime-tutorial/tutorial_general_100.png

[200]: ./media/bime-tutorial/tutorial_general_200.png
[201]: ./media/bime-tutorial/tutorial_general_201.png
[202]: ./media/bime-tutorial/tutorial_general_202.png
[203]: ./media/bime-tutorial/tutorial_general_203.png

