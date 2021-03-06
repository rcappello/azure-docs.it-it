---
title: 'Esercitazione: Integrazione di Azure Active Directory con Dropbox for Business | Microsoft Docs'
description: Informazioni su come configurare l'accesso Single Sign-On tra Azure Active Directory e Dropbox for Business.
services: active-directory
documentationCenter: na
author: jeevansd
manager: mtillman
ms.reviewer: joflore
ms.assetid: 63502412-758b-4b46-a580-0e8e130791a1
ms.service: active-directory
ms.component: saas-app-tutorial
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/20/2018
ms.author: jeedes
ms.openlocfilehash: eadf6724891d348c2ea3654bcf19ef0d74078049
ms.sourcegitcommit: 3f8f973f095f6f878aa3e2383db0d296365a4b18
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 08/20/2018
ms.locfileid: "42143368"
---
# <a name="tutorial-azure-active-directory-integration-with-dropbox-for-business"></a>Esercitazione: Integrazione di Azure Active Directory con Dropbox for Business

Questa esercitazione descrive come integrare Dropbox for Business con Azure Active Directory (Azure AD).

L'integrazione di Dropbox for Business con Azure AD offre i vantaggi seguenti:

- È possibile controllare in Azure AD quali utenti possono accedere a Dropbox for Business.
- È possibile abilitare per gli utenti l'accesso automatico a Dropbox for Business (Single Sign-On) con i rispettivi account Azure AD.
- È possibile gestire gli account in un'unica posizione centrale: il portale di Azure.

Per altre informazioni sull'integrazione di app SaaS con Azure AD, vedere [Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory](../manage-apps/what-is-single-sign-on.md).

## <a name="prerequisites"></a>Prerequisiti

Per configurare l'integrazione di Azure AD con Dropbox for Business, sono necessari gli elementi seguenti:

- Sottoscrizione di Azure AD
- Sottoscrizione di Dropbox for Business abilitata per l'accesso Single Sign-On

> [!NOTE]
> Non è consigliabile usare un ambiente di produzione per testare i passaggi di questa esercitazione.

A questo scopo, è consigliabile seguire le indicazioni seguenti:

- Non usare l'ambiente di produzione a meno che non sia necessario.
- Se non è disponibile un ambiente di valutazione di Azure AD, è possibile [ottenere una versione di valutazione di un mese](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Descrizione dello scenario

In questa esercitazione viene eseguito il test dell'accesso Single Sign-On di Azure AD in un ambiente di test.
Lo scenario descritto in questa esercitazione prevede le due fasi fondamentali seguenti:

1. Aggiunta di Dropbox for Business dalla raccolta
2. Configurazione e test dell'accesso Single Sign-On di Azure AD

## <a name="adding-dropbox-for-business-from-the-gallery"></a>Aggiunta di Dropbox for Business dalla raccolta

Per configurare l'integrazione di Dropbox for Business in Azure AD, è necessario aggiungere Dropbox for Business dalla raccolta al proprio elenco di app SaaS gestite.

**Per aggiungere Dropbox for Business dalla raccolta, seguire questa procedura:**

1. Nel **[portale di Azure](https://portal.azure.com)** fare clic sull'icona di **Azure Active Directory** nel riquadro di spostamento sinistro.

    ![Pulsante Azure Active Directory][1]

2. Passare ad **Applicazioni aziendali**. Andare quindi a **Tutte le applicazioni**.

    ![Pannello Applicazioni aziendali][2]

3. Fare clic sul pulsante **Nuova applicazione** nella parte superiore della finestra di dialogo per aggiungere una nuova applicazione.

    ![Pulsante Nuova applicazione][3]

4. Nella casella di ricerca digitare **Dropbox for Business**, selezionare **Dropbox for Business** nel pannello dei risultati e quindi fare clic sul pulsante **Aggiungi** per aggiungere l'applicazione.

    ![Dropbox for Business nell'elenco dei risultati](./media/dropboxforbusiness-tutorial/tutorial_dropboxforbusiness_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a>Configurare e testare l'accesso Single Sign-On di Azure AD

In questa sezione viene configurato e testato l'accesso Single Sign-On di Azure AD a Dropbox for Business con l'utente di test "Britta Simon".

Per il funzionamento dell'accesso Single Sign-On, Azure AD deve conoscere l'utente di Dropbox for Business che corrisponde a un utente di Azure AD. In altre parole, deve essere stabilita una relazione di collegamento tra un utente di Azure AD e l'utente correlato in Dropbox for Business.

Per stabilire la relazione di collegamento, in Dropbox for Business assegnare il valore del **nome utente** in Azure AD come valore di **Username** (Nome utente).

Per configurare e testare l'accesso Single Sign-On di Azure AD con Dropbox for Business, è necessario completare i blocchi predefiniti seguenti:

1. **[Configurare l'accesso Single Sign-On di Azure AD](#configure-azure-ad-single-sign-on)**: per consentire agli utenti di usare questa funzionalità.
2. **[Creare un utente di test di Azure AD](#create-an-azure-ad-test-user)**: per testare l'accesso Single Sign-On di Azure AD con l'utente Britta Simon.
3. **[Creare un utente di test di Dropbox for Business](#create-a-dropbox-for-business-test-user)**: per avere una controparte di Britta Simon in Dropbox for Business collegata alla relativa rappresentazione dell'utente in Azure AD.
4. **[Assegnare l'utente test di Azure AD](#assign-the-azure-ad-test-user)**: per abilitare Britta Simon all'uso dell'accesso Single Sign-On di Azure AD.
5. **[Testare l'accesso Single Sign-On](#test-single-sign-on)** per verificare se la configurazione funziona.

### <a name="configure-azure-ad-single-sign-on"></a>Configurare l'accesso Single Sign-On di Azure AD

In questa sezione viene abilitato l'accesso Single Sign-On di Azure AD nel portale di Azure e viene configurato l'accesso Single Sign-On nell'applicazione Dropbox for Business.

**Per configurare l'accesso Single Sign-On di Azure AD con Dropbox for Business, seguire questa procedura:**

1. Nella pagina di integrazione dell'applicazione **Dropbox for Business** del portale di Azure fare clic su **Single Sign-On**.

    ![Collegamento Configura accesso Single Sign-On][4]

2. Nella finestra di dialogo **Single Sign-On** selezionare **Accesso basato su SAML** per **Modalità** per abilitare l'accesso Single Sign-On.
 
    ![Finestra di dialogo Single Sign-On](./media/dropboxforbusiness-tutorial/tutorial_dropboxforbusiness_samlbase.png)

3. Nella sezione **URL e dominio Dropbox for Business** seguire questa procedura:

    ![Informazioni su URL e dominio per l'accesso Single Sign-On in Dropbox for Business](./media/dropboxforbusiness-tutorial/tutorial_dropboxforbusiness_url1.png)

    a. Nella casella di testo **URL di accesso** digitare l'URL usando il modello seguente: `https://www.dropbox.com/sso/<id>`

    b. Nella casella di testo **Identificatore** digitare un valore: `Dropbox`

    > [!NOTE]
    > Il valore precedente non è un valore reale. È necessario aggiornarlo con l'URL di accesso effettivo, descritto più avanti nell'esercitazione.

4. Nella sezione **Certificato di firma SAML** fare clic su **Certificato (Base64)** e quindi salvare il file del certificato nel computer.

    ![Collegamento di download del certificato](./media/dropboxforbusiness-tutorial/tutorial_dropboxforbusiness_certificate.png) 

5. Fare clic sul pulsante **Salva** .

    ![Pulsante Salva per la configurazione dell'accesso Single Sign-On](./media/dropboxforbusiness-tutorial/tutorial_general_400.png)

6. Nella sezione **Configurazione di Dropbox for Business** fare clic su **Configura Dropbox for Business** per aprire la finestra **Configura accesso**. Copiare l'**URL servizio Single Sign-On SAML** dalla **sezione Riferimento rapido.**

    ![Configurazione di Dropbox for Business](./media/dropboxforbusiness-tutorial/tutorial_dropboxforbusiness_configure.png) 

7. Per configurare l'accesso Single Sign-On sul lato **Dropbox for Business**, passare al tenant di Dropbox for Business e accedere al proprio tenant di Dropbox for business.

    ![Configurare l'accesso Single Sign-On](./media/dropboxforbusiness-tutorial/ic769509.png "Configurare l'accesso Single Sign-On")

8. Fare clic su **Icona utente** e selezionare la scheda **Impostazioni**.

    ![Configurare l'accesso Single Sign-On](./media/dropboxforbusiness-tutorial/configure1.png "Configurare l'accesso Single Sign-On")

9. Nel riquadro di spostamento a sinistra fare clic su **Console di amministrazione**.

    ![Configurare l'accesso Single Sign-On](./media/dropboxforbusiness-tutorial/configure2.png "Configurare l'accesso Single Sign-On")

10. In **Console di amministrazione** fare clic su **Impostazioni** nel riquadro di spostamento a sinistra.

    ![Configurare l'accesso Single Sign-On](./media/dropboxforbusiness-tutorial/configure3.png "Configurare l'accesso Single Sign-On")

11. Selezionare l’opzione **Single sign-on** sotto la sezione **Autenticazione**.

    ![Configurare l'accesso Single Sign-On](./media/dropboxforbusiness-tutorial/configure4.png "Configurare l'accesso Single Sign-On")

12. Nella sezione **Single sign-on**seguire questa procedura:  

    ![Configurare l'accesso Single Sign-On](./media/dropboxforbusiness-tutorial/configure5.png "Configurare l'accesso Single Sign-On")

    a. Selezionare **necessari** come opzione nell'elenco a discesa per il **Single sign-on**.

    b. Fare clic su **Aggiungi URL di accesso** e nella casella di testo **URL di accesso del provider di identità** incollare il valore di **URL servizio Single Sign-On SAML** copiato dal portale di Azure e quindi selezionare **Completato**.

    ![Configurare l'accesso Single Sign-On](./media/dropboxforbusiness-tutorial/configure6.png "Configurare l'accesso Single Sign-On")

    c. Fare clic su **Carica certificato**e quindi andare al **file di certificato oBase64** scaricato dal portale di Azure.

    d. Fare clic su **Copia il link** e incollare il valore copiato nella casella di testo **URL Sign-on** delle sezioni **dominio e URL di Dropbox for Business** nel portale di Azure.

    e. Fare clic su **Save**.

### <a name="create-an-azure-ad-test-user"></a>Creare un utente test di Azure AD

Questa sezione descrive come creare un utente test denominato Britta Simon nel portale di Azure.

   ![Creare un utente test di Azure AD][100]

**Per creare un utente test in Azure AD, eseguire la procedura seguente:**

1. Nel portale di Azure fare clic sul pulsante **Azure Active Directory** nel riquadro sinistro.

    ![Pulsante Azure Active Directory](./media/dropboxforbusiness-tutorial/create_aaduser_01.png)

1. Per visualizzare l'elenco di utenti, passare a **Utenti e gruppi** e quindi fare clic su **Tutti gli utenti**.

    ![Collegamenti "Utenti e gruppi" e "Tutti gli utenti"](./media/dropboxforbusiness-tutorial/create_aaduser_02.png)

1. Per aprire la finestra di dialogo **Utente** fare clic su **Aggiungi** nella parte superiore della finestra di dialogo **Tutti gli utenti**.

    ![Pulsante Aggiungi](./media/dropboxforbusiness-tutorial/create_aaduser_03.png)

1. Nella finestra di dialogo **Utente** seguire questa procedura:

    ![Finestra di dialogo Utente](./media/dropboxforbusiness-tutorial/create_aaduser_04.png)

    a. Nella casella **Nome** digitare **BrittaSimon**.

    b. Nella casella **Nome utente** digitare l'indirizzo di posta elettronica dell'utente Britta Simon.

    c. Selezionare la casella di controllo **Mostra password** e quindi prendere nota del valore visualizzato nella casella **Password**.

    d. Fare clic su **Create**(Crea).
 
### <a name="create-a-dropbox-for-business-test-user"></a>Creare un utente di test di Dropbox for Business

In questa sezione viene creato un utente di nome Britta Simon in Dropbox for Business. Dropbox for Business supporta il provisioning JIT (Just-In-Time) che è abilitato per impostazione predefinita.

Non è necessario alcun intervento dell'utente in questa sezione. Se un utente non esiste in Dropbox for Business, ne viene creato uno nuovo quando si tenta di accedere a Dropbox for Business.

>[!Note]
>Se è necessario creare un utente manualmente, contattare il [team di supporto clienti di Dropbox for Business](https://www.dropbox.com/business/contact) 

### <a name="assign-the-azure-ad-test-user"></a>Assegnare l'utente test di Azure AD

In questa sezione si abilita Britta Simon all'uso dell'accesso Single Sign-On di Azure concedendole l'accesso a Dropbox for Business.

![Assegnare il ruolo utente][200] 

**Per assegnare Britta Simon a Dropbox for Business, seguire questa procedura:**

1. Nel portale di Azure aprire la visualizzazione delle applicazioni e quindi la visualizzazione delle directory e passare ad **Applicazioni aziendali**, quindi fare clic su **Tutte le applicazioni**.

    ![Assegna utente][201] 

1. Nell'elenco delle applicazioni selezionare **Dropbox for Business**.

    ![Collegamento di Dropbox for Business nell'elenco delle applicazioni](./media/dropboxforbusiness-tutorial/tutorial_dropboxforbusiness_app.png)  

1. Scegliere **Utenti e gruppi** dal menu a sinistra.

    ![Collegamento "Utenti e gruppi"][202]

1. Fare clic sul pulsante **Aggiungi**. Selezionare quindi **Utenti e gruppi** nella finestra di dialogo **Aggiungi assegnazione**.

    ![Riquadro Aggiungi assegnazione][203]

1. Nella finestra di dialogo **Utenti e gruppi** selezionare **Britta Simon** nell'elenco Utenti.

1. Fare clic sul pulsante **Seleziona** nella finestra di dialogo **Utenti e gruppi**.

1. Fare clic sul pulsante **Assegna** nella finestra di dialogo **Aggiungi assegnazione**.
    
### <a name="test-single-sign-on"></a>Testare l'accesso Single Sign-On

In questa sezione viene testata la configurazione dell'accesso Single Sign-On di Azure AD usando il pannello di accesso.

Quando si fa clic sul riquadro di Dropbox for Business nel pannello di accesso dovrebbe essere visualizzata la pagina di accesso dell'applicazione Dropbox for Business.
 

## <a name="additional-resources"></a>Risorse aggiuntive

* [Elenco di esercitazioni sulla procedura di integrazione delle app SaaS con Azure Active Directory](tutorial-list.md)
* [Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory](../manage-apps/what-is-single-sign-on.md)



<!--Image references-->

[1]: ./media/dropboxforbusiness-tutorial/tutorial_general_01.png
[2]: ./media/dropboxforbusiness-tutorial/tutorial_general_02.png
[3]: ./media/dropboxforbusiness-tutorial/tutorial_general_03.png
[4]: ./media/dropboxforbusiness-tutorial/tutorial_general_04.png

[100]: ./media/dropboxforbusiness-tutorial/tutorial_general_100.png

[200]: ./media/dropboxforbusiness-tutorial/tutorial_general_200.png
[201]: ./media/dropboxforbusiness-tutorial/tutorial_general_201.png
[202]: ./media/dropboxforbusiness-tutorial/tutorial_general_202.png
[203]: ./media/dropboxforbusiness-tutorial/tutorial_general_203.png

