---
title: 'Esercitazione: Integrazione di Azure Active Directory con Hosted Graphite | Documentazione Microsoft'
description: Informazioni su come configurare l'accesso Single Sign-On tra Azure Active Directory e Hosted Graphite.
services: active-directory
documentationCenter: na
author: jeevansd
manager: mtillman
ms.assetid: a1ac4d7f-d079-4f3c-b6da-0f520d427ceb
ms.service: active-directory
ms.component: saas-app-tutorial
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/22/2017
ms.author: jeedes
ms.openlocfilehash: c64e54b80b6295358036d054af14ebe85432d3f6
ms.sourcegitcommit: 1d850f6cae47261eacdb7604a9f17edc6626ae4b
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 08/02/2018
ms.locfileid: "39437380"
---
# <a name="tutorial-azure-active-directory-integration-with-hosted-graphite"></a>Esercitazione: Integrazione di Azure Active Directory con Hosted Graphite

Questa esercitazione descrive come integrare Hosted Graphite con Azure Active Directory (Azure AD).

L'integrazione di Hosted Graphite in Azure AD offre i vantaggi seguenti:

- È possibile controllare in Azure AD gli utenti che possono accedere a Hosted Graphite
- È possibile abilitare gli utenti per l'accesso automatico a Hosted Graphite (Single Sign-On) con il proprio account Azure AD
- È possibile gestire gli account in un'unica posizione centrale: il portale di Azure.

Per altre informazioni sull'integrazione di app SaaS con Azure AD, vedere [Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory](../manage-apps/what-is-single-sign-on.md).

## <a name="prerequisites"></a>Prerequisiti

Per configurare l'integrazione di Azure AD in Hosted Graphite, è necessario quanto segue:

- Sottoscrizione di Azure AD
- Sottoscrizione di Hosted Graphite abilitata per l'accesso Single Sign-On

> [!NOTE]
> Non è consigliabile usare un ambiente di produzione per testare i passaggi di questa esercitazione.

A questo scopo, è consigliabile seguire le indicazioni seguenti:

- Non usare l'ambiente di produzione a meno che non sia necessario.
- Se non si dispone di un ambiente di prova di Azure AD, è possibile ottenere una versione di valutazione di un mese [qui](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Descrizione dello scenario
In questa esercitazione viene eseguito il test dell'accesso Single Sign-On di Azure AD in un ambiente di test. Lo scenario descritto in questa esercitazione prevede le due fasi fondamentali seguenti:

1. Aggiunta di Hosted Graphite dalla raccolta
1. Configurazione e test dell'accesso Single Sign-On di Azure AD

## <a name="adding-hosted-graphite-from-the-gallery"></a>Aggiunta di Hosted Graphite dalla raccolta
Per configurare l'integrazione di Hosted Graphite in Azure AD, è necessario aggiungere Hosted Graphite dalla raccolta all'elenco delle app SaaS gestite.

**Per aggiungere Hosted Graphite dalla raccolta, eseguire i passaggi seguenti:**

1. Nel **[portale di Azure](https://portal.azure.com)** fare clic sull'icona di **Azure Active Directory** nel riquadro di spostamento sinistro. 

    ![Active Directory][1]

1. Passare ad **Applicazioni aziendali**. Andare quindi a **Tutte le applicazioni**.

    ![APPLICAZIONI][2]
    
1. Fare clic sul pulsante **Nuova applicazione** nella parte superiore della finestra di dialogo per aggiungere una nuova applicazione.

    ![APPLICAZIONI][3]

1. Nella casella di ricerca digitare **Hosted Graphite**.

    ![Creazione di un utente test di Azure AD](./media/hostedgraphite-tutorial/tutorial_hostedgraphite_search.png)

1. Nel pannello dei risultati selezionare **Hosted Graphite** e quindi fare clic sul pulsante **Aggiungi** per aggiungere l'applicazione.

    ![Creazione di un utente test di Azure AD](./media/hostedgraphite-tutorial/tutorial_hostedgraphite_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Configurazione e test dell'accesso Single Sign-On di Azure AD
In questa sezione viene configurato e testato l'accesso Single Sign-On di Azure AD con Hosted Graphite mediante un utente test di nome "Britta Simon".

Per il funzionamento dell'accesso Single Sign-On, Azure AD deve sapere quale utente di Hosted Graphite corrisponde a un determinato utente di Azure AD. In altre parole, è necessario stabilire una relazione di collegamento fra un utente di AD Azure e l'utente correlato di Hosted Graphite.

Per stabilire la relazione di collegamento, in Hosted Graphite assegnare il valore di **nome utente** di Azure AD come valore dell'attributo **Username** (Nome utente).

Per configurare e testare l'accesso Single Sign-On in AD Azure con Hosted Graphite, è necessario completare le operazioni seguenti:

1. **[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** : per abilitare gli utenti all'utilizzo di questa funzionalità.
1. **[Creazione di un utente test di Azure AD](#creating-an-azure-ad-test-user)** : per testare l'accesso Single Sign-On di Azure AD con l'utente Britta Simon.
1. **[Creazione di un utente test di Hosted Graphite](#creating-a-hosted-graphite-test-user)**: per avere una controparte di Britta Simon in Hosted Graphite collegata alla rappresentazione dell'utente in Azure AD.
1. **[Assegnazione dell'utente test di Azure AD](#assigning-the-azure-ad-test-user)** : per abilitare Britta Simon all'uso dell'accesso Single Sign-On di Azure AD.
1. **[Testing Single Sign-On](#testing-single-sign-on)** : per verificare se la configurazione funziona.

### <a name="configuring-azure-ad-single-sign-on"></a>Configurazione dell'accesso Single Sign-On di Azure AD

In questa sezione viene abilitato l'accesso Single Sign-On di Azure AD nel portale di Azure e viene configurato l'accesso Single Sign-On nell'applicazione Hosted Graphite.

**Per configurare l'accesso Single Sign-On in Azure AD con Hosted Graphite, procedere come segue:**

1. Nella pagina di integrazione dell'applicazione **Hosted Graphite** del portale di Azure fare clic su **Single Sign-On**.

    ![Configure Single Sign-On][4]

1. Nella finestra di dialogo **Single Sign-On** selezionare **Accesso basato su SAML** per **Modalità** per abilitare l'accesso Single Sign-On.
 
    ![Configure Single Sign-On](./media/hostedgraphite-tutorial/tutorial_hostedgraphite_samlbase.png)

1. Nella sezione **URL e dominio Hosted Graphite** seguire questa procedura per configurare l'applicazione in **modalità avviata da IDP**:

    ![Configure Single Sign-On](./media/hostedgraphite-tutorial/tutorial_hostedgraphite_url.png)

    a. Nella casella di testo **Identificatore** digitare l'URL adottando il modello seguente: `https://www.hostedgraphite.com/metadata/<user id>`.

    b. Nella casella di testo **URL di risposta** digitare l'URL usando il modello seguente: `https://www.hostedgraphite.com/complete/saml/<user id>`

1. Nella sezione **URL e dominio Hosted Graphite** seguire questa procedura per configurare l'applicazione in **modalità avviata da SP**:
   
    ![Configure Single Sign-On](./media/hostedgraphite-tutorial/tutorial_hostedgraphite_10.png)
  
    a. Fare clic sull'opzione **Mostra impostazioni URL avanzate**

    b. Nella casella di testo **URL di accesso** digitare l'URL usando il modello seguente: `https://www.hostedgraphite.com/login/saml/<user id>/`   

    > [!NOTE] 
    > Si noti che questi non sono i valori reali. È necessario aggiornare questi valori con l'identificatore, l'URL di risposta e l'URL di accesso effettivi. Per ottenere questi valori passare a Access->SAML setup (Accesso -> Configurazione SAML) nell'applicazione oppure contattare il [team di supporto di Hosted Graphite](mailto:help@hostedgraphite.com).
    >
 
1. Nella sezione **Certificato di firma SAML** fare clic su **Certificato (Base64)** e quindi salvare il file del certificato nel computer.

    ![Configure Single Sign-On](./media/hostedgraphite-tutorial/tutorial_hostedgraphite_certificate.png) 

1. Fare clic sul pulsante **Salva** .

    ![Configure Single Sign-On](./media/hostedgraphite-tutorial/tutorial_general_400.png)

1. Nella sezione **Configurazione di Hosted Graphite** fare clic su **Configura Hosted Graphite** per aprire la finestra **Configura accesso**. Copiare i valori **SAML Entity ID (ID entità SAML) e SAML Single Sign-On Service URL (URL servizio Single Sign-On SAML)** dalla sezione **Quick Reference** (Riferimento rapido).

    ![Configure Single Sign-On](./media/hostedgraphite-tutorial/tutorial_hostedgraphite_configure.png) 

1. Accedere al tenant di Hosted Graphite come amministratore.

1. Accedere alla **pagina SAML Setup** (Configurazione SAML) dalla barra laterale, facendo clic su **Accesso -> SAML Setup (Configurazione SAML)**.
   
    ![Configurazione accesso Single Sign-On sul lato app](./media/hostedgraphite-tutorial/tutorial_hostedgraphite_000.png)

1. Verificare che gli URL corrispondano alla configurazione eseguita nella sezione **URL e Dominio Hosted Graphite** del portale di Azure.
   
    ![Configurazione accesso Single Sign-On sul lato app](./media/hostedgraphite-tutorial/tutorial_hostedgraphite_001.png)

1. Nelle caselle di testo **Entity or Issuer ID** (ID entità o emittente) e **SSO Login URL** (URL di accesso SSO) incollare i valori di **SAML Entity ID** (ID entità SAML) e **SAML Single Sign-On Service URL** (URL servizio Single Sign-On SAML) copiati dal portale di Azure. 
   
    ![Configurazione accesso Single Sign-On sul lato app](./media/hostedgraphite-tutorial/tutorial_hostedgraphite_002.png)
   

1. Selezionare "**Sola lettura**" come **ruolo utente predefinito**.
    
    ![Configurazione accesso Single Sign-On sul lato app](./media/hostedgraphite-tutorial/tutorial_hostedgraphite_004.png)

1. Aprire nel Blocco note il certificato con codifica Base 64 scaricato dal portale di Azure, copiarne il contenuto negli Appunti e incollarlo nella casella di testo **Certificato X.509**.
    
    ![Configurazione accesso Single Sign-On sul lato app](./media/hostedgraphite-tutorial/tutorial_hostedgraphite_005.png)

1. Fare clic sul pulsante **Salva** .

> [!TIP]
> Un riepilogo delle istruzioni è disponibile all'interno del [portale di Azure](https://portal.azure.com) durante la configurazione dell'app.  Dopo aver aggiunto l'app dalla sezione **Active Directory > Applicazioni aziendali** è sufficiente fare clic sulla scheda **Single Sign-On** e accedere alla documentazione incorporata tramite la sezione **Configurazione** nella parte inferiore. Altre informazioni sulla funzione di documentazione incorporata sono disponibili in [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985) (Documentazione incorporata di Azure AD).
> 

### <a name="creating-an-azure-ad-test-user"></a>Creazione di un utente test di Azure AD
Questa sezione descrive come creare un utente test denominato Britta Simon nel portale di Azure.

![Creare un utente di Azure AD][100]

**Per creare un utente test in Azure AD, eseguire la procedura seguente:**

1. Nel **portale di Azure** fare clic sull'icona di **Azure Active Directory** nel riquadro di spostamento sinistro.

    ![Creazione di un utente test di Azure AD](./media/hostedgraphite-tutorial/create_aaduser_01.png) 

1. Passare a **Utenti e gruppi** e fare clic su **Tutti gli utenti** per visualizzare l'elenco di utenti.
    
    ![Creazione di un utente test di Azure AD](./media/hostedgraphite-tutorial/create_aaduser_02.png) 

1. Nella parte superiore della finestra di dialogo fare clic su **Aggiungi** per aprire la finestra di dialogo **Utente**.
 
    ![Creazione di un utente test di Azure AD](./media/hostedgraphite-tutorial/create_aaduser_03.png) 

1. Nella pagina della finestra di dialogo **Utente** seguire questa procedura:
 
    ![Creazione di un utente test di Azure AD](./media/hostedgraphite-tutorial/create_aaduser_04.png) 

    a. Nella casella di testo **Nome** digitare **BrittaSimon**.

    b. Nella casella di testo **Nome utente** digitare l'**indirizzo di posta elettronica** di BrittaSimon.

    c. Selezionare **Mostra password** e prendere nota del valore della **Password**.

    d. Fare clic su **Create**(Crea).
 
### <a name="creating-a-hosted-graphite-test-user"></a>Creazione di un utente test di Hosted Graphite

Questa sezione descrive come creare un utente chiamato Britta Simon in Hosted Graphite. Hosted Graphite supporta il provisioning JIT, che è abilitato per impostazione predefinita.

Non è necessario alcun intervento dell'utente in questa sezione. Durante un tentativo di accesso a Hosted Graphite verrà creato un nuovo utente, se questo non esiste già.

>[!NOTE]
>Per creare un utente manualmente, contattare il team di supporto di Hosted Graphite all'indirizzo <mailto:help@hostedgraphite.com>. 

### <a name="assigning-the-azure-ad-test-user"></a>Assegnazione dell'utente test di Azure AD

In questa sezione Britta Simon viene abilitata per l'uso dell'accesso Single Sign-On di Azure concedendole l'accesso a Hosted Graphite.

![Assegna utente][200] 

**Per assegnare Britta Simon a Hosted Graphite, seguire questa procedura:**

1. Nel portale di Azure aprire la visualizzazione delle applicazioni e quindi la visualizzazione delle directory e passare ad **Applicazioni aziendali**, quindi fare clic su **Tutte le applicazioni**.

    ![Assegna utente][201] 

1. Nell'elenco delle applicazioni selezionare **Hosted Graphite**.

    ![Configure Single Sign-On](./media/hostedgraphite-tutorial/tutorial_hostedgraphite_app.png) 

1. Scegliere **Utenti e gruppi** dal menu a sinistra.

    ![Assegna utente][202] 

1. Fare clic sul pulsante **Aggiungi**. Selezionare quindi **Utenti e gruppi** nella finestra di dialogo **Aggiungi assegnazione**.

    ![Assegna utente][203]

1. Nella finestra di dialogo **Utenti e gruppi** selezionare **Britta Simon** nell'elenco Utenti.

1. Fare clic sul pulsante **Seleziona** nella finestra di dialogo **Utenti e gruppi**.

1. Fare clic sul pulsante **Assegna** nella finestra di dialogo **Aggiungi assegnazione**.
    
### <a name="testing-single-sign-on"></a>Test dell'accesso Single Sign-On

Questa sezione descrive come testare la configurazione dell'accesso Single Sign-On di Azure AD usando il pannello di accesso.

Quando si fa clic sul riquadro Hosted Graphite nel pannello di accesso, si dovrebbe accedere automaticamente all'applicazione Hosted Graphite.

## <a name="additional-resources"></a>Risorse aggiuntive

* [Elenco di esercitazioni sulla procedura di integrazione delle app SaaS con Azure Active Directory](tutorial-list.md)
* [Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory](../manage-apps/what-is-single-sign-on.md)



<!--Image references-->

[1]: ./media/hostedgraphite-tutorial/tutorial_general_01.png
[2]: ./media/hostedgraphite-tutorial/tutorial_general_02.png
[3]: ./media/hostedgraphite-tutorial/tutorial_general_03.png
[4]: ./media/hostedgraphite-tutorial/tutorial_general_04.png

[100]: ./media/hostedgraphite-tutorial/tutorial_general_100.png

[200]: ./media/hostedgraphite-tutorial/tutorial_general_200.png
[201]: ./media/hostedgraphite-tutorial/tutorial_general_201.png
[202]: ./media/hostedgraphite-tutorial/tutorial_general_202.png
[203]: ./media/hostedgraphite-tutorial/tutorial_general_203.png

