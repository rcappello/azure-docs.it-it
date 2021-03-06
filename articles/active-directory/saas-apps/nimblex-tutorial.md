---
title: 'Esercitazione: Integrazione di Azure Active Directory con Nimblex | Microsoft Docs'
description: Informazioni su come configurare l'accesso Single Sign-On tra Azure Active Directory e Nimblex.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: d3e165a5-f062-4b50-ac0b-b400838e99cd
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/05/2018
ms.author: jeedes
ms.openlocfilehash: 7b5dc6d892741f63596589a48ad5d45891b14c21
ms.sourcegitcommit: 7208bfe8878f83d5ec92e54e2f1222ffd41bf931
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 07/14/2018
ms.locfileid: "39040406"
---
# <a name="tutorial-azure-active-directory-integration-with-nimblex"></a>Esercitazione: Integrazione di Azure Active Directory con Nimblex

Questa esercitazione illustra come integrare Nimblex con Azure Active Directory (Azure AD).

L'integrazione di Nimblex con Azure AD offre i vantaggi seguenti:

- È possibile controllare in Azure AD chi può accedere a Nimblex.
- È possibile abilitare gli utenti per l'accesso automatico a Nimblex (Single Sign-On) con i propri account Azure AD.
- È possibile gestire gli account in un'unica posizione centrale: il portale di Azure.

Per altre informazioni sull'integrazione di app SaaS con Azure AD, vedere [Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory](../manage-apps/what-is-single-sign-on.md).

## <a name="prerequisites"></a>Prerequisiti

Per configurare l'integrazione di Azure AD con Nimblex, sono necessari gli elementi seguenti:

- Sottoscrizione di Azure AD
- Una sottoscrizione Nimblex abilitata per l'accesso Single Sign-On

> [!NOTE]
> Non è consigliabile usare un ambiente di produzione per testare i passaggi di questa esercitazione.

A questo scopo, è consigliabile seguire le indicazioni seguenti:

- Non usare l'ambiente di produzione a meno che non sia necessario.
- Se non è disponibile un ambiente di valutazione di Azure AD, è possibile [ottenere una versione di valutazione di un mese](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Descrizione dello scenario
In questa esercitazione viene eseguito il test dell'accesso Single Sign-On di Azure AD in un ambiente di test. Lo scenario descritto in questa esercitazione prevede le due fasi fondamentali seguenti:

1. Aggiunta di Nimblex dalla raccolta
2. Configurazione e test dell'accesso Single Sign-On di Azure AD

## <a name="adding-nimblex-from-the-gallery"></a>Aggiunta di Nimblex dalla raccolta
Per configurare l'integrazione di Nimblex in Azure AD, è necessario aggiungere Nimblex dalla raccolta al proprio elenco di app SaaS gestite.

**Per aggiungere Nimblex dalla raccolta, seguire questa procedura:**

1. Nel **[portale di Azure](https://portal.azure.com)** fare clic sull'icona di **Azure Active Directory** nel riquadro di spostamento sinistro. 

    ![Pulsante Azure Active Directory][1]

2. Passare ad **Applicazioni aziendali**. Andare quindi a **Tutte le applicazioni**.

    ![Pannello Applicazioni aziendali][2]

1. Fare clic sul pulsante **Nuova applicazione** nella parte superiore della finestra di dialogo per aggiungere una nuova applicazione.

    ![Pulsante Nuova applicazione][3]

4. Nella casella di ricerca digitare **Nimblex**, selezionare **Nimblex** dal pannello dei risultati e quindi fare clic sul pulsante **Aggiungi** per aggiungere l'applicazione.

    ![Nimblex nell'elenco risultati](./media/nimblex-tutorial/tutorial_nimblex_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a>Configurare e testare l'accesso Single Sign-On di Azure AD

In questa sezione viene configurato e testato l'accesso Single Sign-On di Azure AD con Nimblex usando un utente test di nome "Britta Simon".

Per il funzionamento dell'accesso Single Sign-On, Azure AD deve conoscere qual è l'utente di Nimblex che corrisponde a un utente di Azure AD. In altre parole, deve essere stabilita una relazione di collegamento tra un utente di Azure AD e l'utente correlato in Nimblex.

Per configurare e testare l'accesso Single Sign-On di Azure AD con Nimblex, è necessario completare i blocchi predefiniti seguenti:

1. **[Configurare l'accesso Single Sign-On di Azure AD](#configure-azure-ad-single-sign-on)**: per consentire agli utenti di usare questa funzionalità.
2. **[Creare un utente di test di Azure AD](#create-an-azure-ad-test-user)**: per testare l'accesso Single Sign-On di Azure AD con l'utente Britta Simon.
3. **[Creare un utente di test di Nimblex](#create-a-nimblex-test-user)**: per avere una controparte di Britta Simon in Nimblex collegata alla rappresentazione dell'utente in Azure AD.
4. **[Assegnare l'utente test di Azure AD](#assign-the-azure-ad-test-user)**: per abilitare Britta Simon all'uso dell'accesso Single Sign-On di Azure AD.
5. **[Testare l'accesso Single Sign-On](#test-single-sign-on)** per verificare se la configurazione funziona.

### <a name="configure-azure-ad-single-sign-on"></a>Configurare l'accesso Single Sign-On di Azure AD

In questa sezione viene abilitato l'accesso Single Sign-On di Azure AD nel portale di Azure e viene configurato l'accesso Single Sign-On nell'applicazione Nimblex.

**Per configurare l'accesso Single Sign-On di Azure AD con Nimblex, seguire questa procedura:**

1. Nella pagina di integrazione dell'applicazione **Nimblex** del portale di Azure fare clic su **Single Sign-On**.

    ![Collegamento Configura accesso Single Sign-On][4]

2. Nella finestra di dialogo **Single Sign-On** selezionare **Accesso basato su SAML** per **Modalità** per abilitare l'accesso Single Sign-On.

    ![Finestra di dialogo Single Sign-On](./media/nimblex-tutorial/tutorial_nimblex_samlbase.png)

3. Nella sezione **URL e dominio Nimblex** seguire questa procedura:

    ![Informazioni su URL e dominio per l'accesso Single Sign-On di Nimblex](./media/nimblex-tutorial/tutorial_nimblex_url.png)

    a. Nella casella di testo **URL di accesso** digitare l'URL usando il modello seguente: `https://<YOUR APPLICATION PATH>/Login.aspx`

    b. Nella casella di testo **Identificatore** digitare l'URL adottando il modello seguente: `https://<YOUR APPLICATION PATH>/`

    c. Nella casella di testo **URL di risposta** digitare l'URL usando il modello seguente: `https://<path-to-application>/SamlReply.aspx`

    > [!NOTE] 
    > Poiché questi non sono i valori reali, è necessario aggiornarli con l'URL di accesso, l'identificatore e l'URL di risposta effettivi. Per ottenere questi valori, contattare il [team di supporto clienti di Nimblex](mailto:support@ebms.com.au).

4. Nella sezione **Certificato di firma SAML** fare clic su **Certificato (Base64)** e quindi salvare il file del certificato nel computer.

    ![Collegamento di download del certificato](./media/nimblex-tutorial/tutorial_nimblex_certificate.png) 

5. Fare clic sul pulsante **Salva** .

    ![Pulsante Salva per la configurazione dell'accesso Single Sign-On](./media/nimblex-tutorial/tutorial_general_400.png)

6. Nella sezione **Configurazione di Nimblex** fare clic su **Configura Nimblex** per aprire la finestra **Configura accesso**. Copiare l'**URL servizio Single Sign-On SAML** dalla **sezione Riferimento rapido.**

    ![Configurazione Nimblex](./media/nimblex-tutorial/tutorial_nimblex_configure.png) 

7. In un'altra finestra del Web browser accedere a Nimblex come amministratore.

9. Fare clic sul logo delle **impostazioni** in alto a destra.

    ![Impostazioni Nimblex](./media/nimblex-tutorial/tutorial_nimblex_settings.png)

10. Dalla pagina del **Pannello di controllo**, nella sezione **Sicurezza**, fare clic su **Single Sign-on**.

    ![Impostazioni Nimblex](./media/nimblex-tutorial/tutorial_nimblex_single.png)

11. Nella pagina **Gestisci Single Sign-On**, selezionare il nome dell'istanza e fare clic su **Modifica**.

    ![Saml Nimblex](./media/nimblex-tutorial/tutorial_nimblex_saml.png)

12. Nella pagina della finestra di dialogo **Modifica provider SSO** seguire questa procedura:

    ![Saml Nimblex](./media/nimblex-tutorial/tutorial_nimblex_sso.png)

    a. Nella casella di testo **Descrizione**, digitare il nome dell'istanza.

    b. Nel Blocco note, aprire il certificato con codifica Base 64 scaricato dal portale di Azure, copiarne il contenuto e quindi incollarlo nella casella **Certificato**.

    c. Nella casella di testo **URL di destinazione Single Sign-On del provider di identità**, incollare il valore di **URL servizio Single Sign-On SAML** copiato dal portale di Azure.

    d. Fare clic su **Save**.

### <a name="create-an-azure-ad-test-user"></a>Creare un utente test di Azure AD

Questa sezione descrive come creare un utente test denominato Britta Simon nel portale di Azure.

   ![Creare un utente test di Azure AD][100]

**Per creare un utente test in Azure AD, eseguire la procedura seguente:**

1. Nel portale di Azure fare clic sul pulsante **Azure Active Directory** nel riquadro sinistro.

    ![Pulsante Azure Active Directory](./media/nimblex-tutorial/create_aaduser_01.png)

2. Per visualizzare l'elenco di utenti, passare a **Utenti e gruppi** e quindi fare clic su **Tutti gli utenti**.

    ![Collegamenti "Utenti e gruppi" e "Tutti gli utenti"](./media/nimblex-tutorial/create_aaduser_02.png)

3. Per aprire la finestra di dialogo **Utente** fare clic su **Aggiungi** nella parte superiore della finestra di dialogo **Tutti gli utenti**.

    ![Pulsante Aggiungi](./media/nimblex-tutorial/create_aaduser_03.png)

4. Nella finestra di dialogo **Utente** seguire questa procedura:

    ![Finestra di dialogo Utente](./media/nimblex-tutorial/create_aaduser_04.png)

    a. Nella casella **Nome** digitare **BrittaSimon**.

    b. Nella casella **Nome utente** digitare l'indirizzo di posta elettronica dell'utente Britta Simon.

    c. Selezionare la casella di controllo **Mostra password** e quindi prendere nota del valore visualizzato nella casella **Password**.

    d. Fare clic su **Crea**.
 
### <a name="create-a-nimblex-test-user"></a>Creare un utente test di Nimblex

Questa sezione descrive come creare un utente chiamato Britta Simon in Nimblex. Nimblex supporta il provisioning just-in-time, che è abilitato per impostazione predefinita. Non è necessario alcun intervento dell'utente in questa sezione. Durante un tentativo di accesso a Nimblex viene creato un nuovo utente, se non esiste già.

>[!Note]
>Per creare un utente manualmente, contattare il [team del supporto clienti di Nimblex](mailto:support@ebms.com.au).

### <a name="assign-the-azure-ad-test-user"></a>Assegnare l'utente test di Azure AD

In questa sezione Britta Simon viene autorizzata a usare l'accesso Single Sign-On di Azure tramite la concessione dell'accesso a Nimblex.

![Assegnare il ruolo utente][200] 

**Per assegnare Britta Simon a Nimblex, seguire questa procedura:**

1. Nel portale di Azure aprire la visualizzazione delle applicazioni e quindi la visualizzazione delle directory e passare ad **Applicazioni aziendali**, quindi fare clic su **Tutte le applicazioni**.

    ![Assegna utente][201] 

2. Nell'elenco di applicazioni selezionare **Nimblex**.

    ![Collegamento di Nimblex nell'elenco delle applicazioni](./media/nimblex-tutorial/tutorial_nimblex_app.png)  

3. Scegliere **Utenti e gruppi** dal menu a sinistra.

    ![Collegamento "Utenti e gruppi"][202]

4. Fare clic sul pulsante **Aggiungi**. Selezionare quindi **Utenti e gruppi** nella finestra di dialogo **Aggiungi assegnazione**.

    ![Riquadro Aggiungi assegnazione][203]

5. Nella finestra di dialogo **Utenti e gruppi** selezionare **Britta Simon** nell'elenco Utenti.

6. Fare clic sul pulsante **Seleziona** nella finestra di dialogo **Utenti e gruppi**.

7. Fare clic sul pulsante **Assegna** nella finestra di dialogo **Aggiungi assegnazione**.
    
### <a name="test-single-sign-on"></a>Testare l'accesso Single Sign-On

In questa sezione viene testata la configurazione dell'accesso Single Sign-On di Azure AD usando il pannello di accesso.

Quando si fa clic sul riquadro Nimblex nel pannello di accesso, dovrebbe essere possibile accedere automaticamente all'applicazione Nimblex.
Per altre informazioni sul pannello di accesso, vedere [Introduzione al Pannello di accesso](../user-help/active-directory-saas-access-panel-introduction.md). 

## <a name="additional-resources"></a>Risorse aggiuntive

* [Elenco di esercitazioni sulla procedura di integrazione delle app SaaS con Azure Active Directory](tutorial-list.md)
* [Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory](../manage-apps/what-is-single-sign-on.md)



<!--Image references-->

[1]: ./media/nimblex-tutorial/tutorial_general_01.png
[2]: ./media/nimblex-tutorial/tutorial_general_02.png
[3]: ./media/nimblex-tutorial/tutorial_general_03.png
[4]: ./media/nimblex-tutorial/tutorial_general_04.png

[100]: ./media/nimblex-tutorial/tutorial_general_100.png

[200]: ./media/nimblex-tutorial/tutorial_general_200.png
[201]: ./media/nimblex-tutorial/tutorial_general_201.png
[202]: ./media/nimblex-tutorial/tutorial_general_202.png
[203]: ./media/nimblex-tutorial/tutorial_general_203.png

