---
title: Configurare l'iscrizione e l'accesso con un account LinkedIn tramite Azure Active Directory B2C | Microsoft Docs
description: Consentire l'iscrizione e l'accesso ai clienti con account LinkedIn alle applicazioni da Azure Active Directory B2C.
services: active-directory-b2c
author: davidmu1
manager: mtillman
ms.service: active-directory
ms.workload: identity
ms.topic: conceptual
ms.date: 07/06/2018
ms.author: davidmu
ms.component: B2C
ms.openlocfilehash: e1949c32833bb1d5e6603a6f5e36e22dc58e8cec
ms.sourcegitcommit: 0c64460a345c89a6b579b1d7e273435a5ab4157a
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 08/31/2018
ms.locfileid: "43336929"
---
# <a name="set-up-sign-up-and-sign-in-with-a-linkedin-account-using-azure-active-directory-b2c"></a>Configurare l'iscrizione e l'accesso con un account LinkedIn tramite Azure Active Directory B2C

## <a name="create-a-linkedin-application"></a>Creare un'applicazione su LinkedIn

Per usare un account LinkedIn come provider di identità in Azure Active Directory (Azure AD) B2C, è necessario creare nel tenant un'applicazione che lo rappresenti. Se non si possiede già un account LinkedIn, è possibile crearlo sul sito [https://www.linkedin.com/](https://www.linkedin.com/).

1. Accedere al [sito Web di sviluppatori LinkedIn](https://www.developer.linkedin.com/) con le credenziali dell'account LinkedIn.
2. Selezionare **My Apps** (App personali) e quindi **Crea applicazione**.
3. Immettere **Nome società**, **Nome applicazione**, **Descrizione applicazione**, **Logo applicazione**, **Uso applicazione** , **URL del sito Web**, **Indirizzo di posta elettronica aziendale** e **Telefono (uff.)**.
4. Accettare il documento **LinkedIn API Terms of Use** (Condizioni d'uso dell'API LinkedIn) e fare clic su **Submit** (Invia).
5. Copiare i valori **ID client** e **Segreto client**. Si trovano nella sezione **Authentication Keys** (Chiavi di autenticazione) Sono necessari entrambi per configurare LinkedIn come provider di identità nel tenant. **Client Segreto** è un'importante credenziale di sicurezza.
6. Immettere `https://{tenant}.b2clogin.com/te/{tenant}.onmicrosoft.com/oauth2/authresp` negli **URL di reindirizzamento autorizzati**. Sostituire **{tenant}** con il nome del tenant, ad esempio contosob2c. Fare clic su **Aggiungi** e quindi su **Aggiorna**.

## <a name="configure-a-linkedin-account-as-an-identity-provider"></a>Configurare un account LinkedIn come provider di identità

1. Accedere al [portale di Azure](https://portal.azure.com/) come amministratore globale del tenant di Azure AD B2C.
2. Assicurarsi di usare la directory contenente il tenant Azure AD B2C passando a tale directory nell'angolo in alto a destra del portale di Azure. Selezionare le informazioni sulla sottoscrizione e quindi selezionare **Cambia directory**. 

    ![Passare al tenant di Azure AD B2C](./media/active-directory-b2c-setup-li-app/switch-directories.png)

    Scegliere la directory contenente il tenant.

    ![Selezionare la directory](./media/active-directory-b2c-setup-li-app/select-directory.png)

3. Scegliere **Tutti i servizi** nell'angolo in alto a sinistra del portale di Azure, cercare **Azure AD B2C** e selezionarlo.
4. Selezionare **Provider di identità** e quindi selezionare **Aggiungi**.
5. Specificare un **Nome**. Immettere ad esempio *LinkedIn*.
6. Fare clic su **Tipo di provider di identità**, selezionare **LinkedIn** e fare clic su **OK**.
7. Selezionare **Set up this identity provider** (Configura provider di identità), immettere l'ID Client registrato in precedenza in **ID Client** e immettere il segreto Client registrato come **Segreto client** dell'applicazione dell'account LinkedIn creata in precedenza.
8. Fare clic su **OK** e quindi su **Create** (Crea) per salvare la configurazione dell'account LinkedIn.

