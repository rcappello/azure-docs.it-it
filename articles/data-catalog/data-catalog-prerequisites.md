---
title: Prerequisiti del Catalogo dati di Azure
description: Informazioni sui prerequisiti necessari per iniziare a usare Azure Data Catalog.
services: data-catalog
author: markingmyname
ms.author: maghan
ms.assetid: ef497a54-dc4d-4820-b5bf-c361b64b964d
ms.service: data-catalog
ms.topic: conceptual
ms.date: 01/18/2018
ms.openlocfilehash: 5d05371d9b948dc2f7d6f834eb9431af80fc6365
ms.sourcegitcommit: b7e5bbbabc21df9fe93b4c18cc825920a0ab6fab
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 09/27/2018
ms.locfileid: "47406873"
---
# <a name="azure-data-catalog-prerequisites"></a>Prerequisiti del Catalogo dati di Azure

Prima di poter configurare Azure Data Catalog, sono necessarie alcune operazioni preliminari che però non richiedono molto tempo.

## <a name="azure-subscription"></a>Sottoscrizione di Azure
Per configurare Data Catalog, l'utente deve essere proprietario o comproprietario di una sottoscrizione di Azure.

Le sottoscrizioni di Azure consentono di organizzare l'accesso alle risorse del servizio cloud, ad esempio Data Catalog. Le sottoscrizioni consentono anche di controllare come l'utilizzo delle risorse viene segnalato, fatturato e pagato. Ogni sottoscrizione può avere un metodo di fatturazione e pagamento distinto e avere così sottoscrizioni e piani diversi per reparto, progetto, ufficio locale e così via. Ogni servizio cloud appartiene a una sottoscrizione ed è necessario che la sottoscrizione sia disponibile prima di configurare Data Catalog. Per altre informazioni, vedere l'articolo su come [gestire gli account, le sottoscrizioni e i ruoli amministrativi](../active-directory/users-groups-roles/directory-assign-admin-roles.md).

## <a name="azure-active-directory"></a>Azure Active Directory
Per configurare Data Catalog, è necessario accedere con un account utente di Azure Active Directory (Azure AD).

Azure AD è un servizio che offre semplici e pratiche funzionalità di gestione delle identità e degli accessi, sia nel cloud sia in locale. Gli utenti possono usare un singolo account aziendale o dell'istituto di istruzione per eseguire l'accesso Single Sign-On a qualsiasi applicazione Web locale o nel cloud. Data Catalog usa Azure AD per autenticare l'accesso. Per altre informazioni, vedere [Informazioni su Azure Active Directory](../active-directory/fundamentals/active-directory-whatis.md).

> [!NOTE]
> Usando il [portale di Azure](http://portal.azure.com/) è possibile eseguire l'accesso con un account Microsoft personale oppure con un account aziendale o dell'istituto di istruzione di Azure Active Directory. Per configurare Data Catalog usando il portale di Azure o il [portale di Data Catalog](http://www.azuredatacatalog.com), è necessario eseguire l'accesso con un account di Azure Active Directory, non con un account personale.
>
>

## <a name="active-directory-policy-configuration"></a>Configurazione dei criteri di Azure Active Directory
In alcune situazioni è possibile accedere al portale di Data Catalog, ma, quando si prova ad accedere allo strumento di registrazione dell'origine dati, viene visualizzato un messaggio di errore che impedisce l'accesso. Questo errore si verifica solo quando si è nella rete aziendale o ci si connette dall'esterno della rete aziendale.

Lo strumento di registrazione dell'origine dati usa l'autenticazione basata su form per convalidare le credenziali degli utenti in Active Directory. Per eseguire correttamente l'accesso, un amministratore di Azure Active Directory deve abilitare l'autenticazione basata su form nei criteri di autenticazione globali.

Nei criteri di autenticazione globali possono essere abilitati metodi di autenticazione separati per connessioni Intranet ed Extranet, come illustrato nello screenshot seguente. Se l'autenticazione basata su form non è abilitata per la rete da cui ci si connette, è possibile che si verifichino errori di accesso.

 ![Criteri di autenticazione globali di Active Directory](./media/data-catalog-prerequisites/global-auth-policy.png)

## <a name="next-steps"></a>Passaggi successivi
Per altre informazioni, vedere [Configurare i criteri di autenticazione](https://technet.microsoft.com/library/dn486781.aspx).
