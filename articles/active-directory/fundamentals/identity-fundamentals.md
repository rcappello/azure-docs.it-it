---
title: Concetti fondamentali sulla gestione delle identità di Azure | Microsoft Docs
description: Le identità basate sul cloud rappresentano il modo migliore per mantenere il controllo e la visibilità sulle modalità e sui tempi di accesso ai dati e alle applicazioni aziendali da parte degli utenti.
keywords: ''
author: eross-msft
manager: mtillman
ms.reviewer: jsnow
ms.author: lizross
ms.date: 08/07/2018
ms.topic: overview
ms.prod: ''
ms.service: active-directory
ms.component: fundamentals
ms.technology: ''
ms.assetid: ''
ms.custom: it-pro
ms.openlocfilehash: 797c35bad03c063203e3616740af633b71835a9c
ms.sourcegitcommit: 4de6a8671c445fae31f760385710f17d504228f8
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 08/08/2018
ms.locfileid: "39640217"
---
# <a name="fundamentals-of-azure-identity-management"></a>Concetti fondamentali sulla gestione delle identità di Azure

Un numero crescente di risorse digitali aziendali si trova oggi all'esterno delle reti aziendali, nel cloud e nei dispositivi. Per questo motivo, una soluzione efficace di gestione degli accessi e delle identità, basata sul cloud è diventata imprescindibile. Le identità basate sul cloud rappresentano il modo migliore per mantenere il controllo e la visibilità sulle modalità e sui tempi di accesso ai dati e alle applicazioni aziendali da parte degli utenti.

Microsoft protegge le identità basate sul cloud da oltre dieci anni. Con [Azure Active Directory (AD)](active-directory-whatis.md), questi stessi sistemi di protezione sono ora a disposizione dei clienti aziendali. Azure AD permette agli amministratori dell'organizzazione di assicurare facilmente la responsabilità di utenti e amministratori, migliorando notevolmente la sicurezza e la governance.

Azure AD Premium è una soluzione di gestione degli accessi e delle identità basata sul cloud con funzionalità di protezione avanzate che offre un'unica identità sicura per tutte le applicazioni, protezione delle identità migliorata dal [Graph di security intelligence di Microsoft](https://www.microsoft.com/en-us/security/intelligence) e Privileged Identity Management. Non si tratta di un semplice strumento di monitoraggio o reporting. Azure AD Premium può proteggere le identità degli utenti in tempo reale e permette di creare criteri di accesso adattivi basati sui rischi per proteggere i dati dell'organizzazione.

Questo breve video offre una rapida panoramica delle funzionalità di protezione e gestione delle identità di Azure AD:
>[!VIDEO https://www.youtube.com/embed/9LGIJ2-FKIM]

Microsoft non offre soltanto un'identità che permette di accedere ovunque, ma anche un set di strumenti per l'automazione, la protezione e la gestione dell'IT all'interno dell'organizzazione. Nonostante l'avvento del cloud computing, è ancora necessario gestire e controllare alcune attività IT, come le chiamate al supporto tecnico per la reimpostazione delle password utente, la gestione dei gruppi di utenti e le richieste di applicazioni. A complicare ulteriormente la situazione, i dipendenti portano al lavoro i loro dispositivi personali e usano immediatamente le applicazioni SaaS disponibili rendendo difficile il controllo delle loro applicazioni nei data center aziendali e nelle piattaforma cloud pubbliche.

[!INCLUDE [identity](../../../includes/azure-ad-licenses.md)]

## <a name="connect-on-premises-active-directory-with-azure-ad-and-office-365"></a>Connettere Active Directory locale con Azure AD e Office 365
Le organizzazioni che hanno effettuato grossi investimenti in Active Directory locale possono estendere tali investimenti al cloud, integrando le directory locali con Azure AD in una [soluzione ibrida di gestione delle identità](https://aka.ms/aadframework). In questo modo è possibile aumentare la produttività degli utenti grazie a un'identità comune per l'accesso alle risorse, indipendentemente dalla località. Utenti e organizzazioni possono quindi usare Single Sign-On (SSO) per accedere alle risorse locali e a servizi cloud quali Office 365.

[Azure AD Connect](https://docs.microsoft.com/azure/active-directory/connect/active-directory-aadconnect) è l'unico strumento necessario per eseguire l'integrazione. Azure AD Connect offre funzionalità a supporto delle esigenze di sincronizzazione delle identità e sostituisce le versioni precedenti di strumenti di integrazione delle identità, quali DirSync e Azure AD Sync. Con Azure AD Connect, la sincronizzazione e la gestione delle identità tra istanze locali e Azure AD è resa possibile da:

- Sincronizzazione: questo componente è responsabile della creazione di utenti, gruppi e altri oggetti. Deve anche garantire che le informazioni sulle identità per utenti e gruppi locali corrispondano a quelle nel cloud. È anche possibile abilitare il writeback delle password per mantenere la sincronizzazione delle directory locali quando un utente aggiorna la password in Azure AD.
- Autenticazione: quando Azure AD è il nuovo piano di controllo, l'autenticazione è alla base dell'accesso cloud. La scelta del metodo di autenticazione corretto è una decisione chiave nella configurazione di una soluzione ibrida di gestione delle identità di Azure AD. Per scegliere tra autenticazione cloud (sincronizzazione dell'hash delle password/autenticazione pass-through) e autenticazione federata (AD FS) per l'organizzazione, vedere [questa guida](https://aka.ms/auth-options).
- Monitoraggio dell'integrità: [Azure AD Connect Health](https://docs.microsoft.com/azure/active-directory/connect-health/active-directory-aadconnect-health) può offrire un monitoraggio affidabile e una posizione centralizzata nel portale di Azure per visualizzare questa attività.

## <a name="increase-productivity-and-reduce-helpdesk-costs-with-self-service-and-single-sign-on-experiences"></a>Aumentare la produttività e ridurre i costi di supporto tecnico con esperienze self-service e Single Sign-On

I dipendenti sono più produttivi quando hanno un solo nome utente e una password da ricordare e un'esperienza coerente in ogni dispositivo. Questo permette loro di risparmiare tempo quando eseguono attività self-service, come [reimpostare una password dimenticata](https://docs.microsoft.com/azure/active-directory/active-directory-passwords) o richiedere l'accesso a un'applicazione senza dover attendere l'assistenza del supporto tecnico.

Azure AD [estende Active Directory locale](https://docs.microsoft.com/azure/active-directory/connect/active-directory-aadconnect) nel cloud, consentendo agli utenti di usare il proprio account aziendale principale sia per i dispositivi aggiunti a un dominio che per le risorse aziendali e per tutte le applicazioni Web e SaaS necessarie per svolgere il proprio lavoro. Oltre a eliminare la necessità di ricordare diversi set di nomi utente e password, permette anche di effettuare automaticamente il provisioning o il deprovisioning dell'accesso alle applicazioni degli utenti in base all'appartenenza ai gruppi dell'organizzazione e al relativo stato come dipendenti. Permette poi di controllare l'accesso ad app della raccolta o app locali sviluppate e pubblicate tramite il [proxy di applicazione di Azure AD](https://docs.microsoft.com/azure/active-directory/active-directory-application-proxy-get-started).

## <a name="manage-and-control-access-to-corporate-resources"></a>Gestire e controllare l'accesso alle risorse aziendali
Le soluzioni Microsoft di gestione degli accessi e delle identità consentono all'IT di proteggere l'accesso ad applicazioni e risorse nel data center aziendale e nel cloud, abilitando livelli di convalida aggiuntivi, ad esempio l'[autenticazione a più fattori](https://docs.microsoft.com/azure/multi-factor-authentication/multi-factor-authentication-whats-next) e i [criteri di accesso condizionale](https://docs.microsoft.com/azure/active-directory/active-directory-conditional-access-azure-portal). Il monitoraggio delle attività sospette tramite funzioni avanzate di report di sicurezza, controllo e avvisi consente di attenuare i potenziali problemi di sicurezza.

Il sistema di accesso condizionale in Azure AD Premium offre agli amministratori dell'organizzazione la possibilità di creare regole di accesso basate sui criteri per qualsiasi applicazione connessa ad Azure AD, come app SaaS, applicazioni personalizzate in esecuzione nel cloud o applicazioni Web locali. Azure AD valuta tali criteri in tempo reale e li applica ogni volta che un utente tenta l'accesso a un'applicazione. I criteri di protezione delle identità di Azure consentono di agire automaticamente in caso di attività sospette, ad esempio bloccando l'accesso per gli utenti ad alto rischio, applicando l'autenticazione a più fattori e reimpostando le password utente se si ritiene che le credenziali siano state compromesse.


## <a name="azure-active-directory-privileged-identity-management"></a>Azure Active Directory Privileged Identity Management

[Privileged Identity Management](https://docs.microsoft.com/azure/active-directory/active-directory-privileged-identity-management-getting-started), incluso nell'offerta Azure Active Directory Premium P2, consente di identificare, limitare e monitorare gli account amministrativi e il relativo accesso alle risorse in Azure Active Directory e in altri servizi online di Microsoft. Permette anche di gestire l'accesso amministrativo su richiesta per l'esatto periodo di tempo necessario.

Privileged Identity Management può applicare diritti di amministratore su richiesta, permettendo agli amministratori di richiedere l'elevazione temporanea dei privilegi con autenticazione a più fattori per periodi di tempo preconfigurati, prima che l'account torni a uno stato di utente normale.

## <a name="benefits-of-azure-identity"></a>Vantaggi della gestione delle identità di Azure

La gestione delle identità di Azure permette di:

-   Creare e gestire un'identità unica per ogni utente in tutta l'azienda, mantenendo utenti, gruppi e dispositivi sincronizzati con [Azure Active Directory Connect](https://docs.microsoft.com/azure/active-directory/connect/active-directory-aadconnect).

-   Offrire l'accesso Single Sign-On alle applicazioni, incluse migliaia di app SaaS preintegrate, o l'accesso remoto sicuro alle applicazioni SaaS locali tramite il [proxy di applicazione di Azure AD](https://docs.microsoft.com/azure/active-directory/active-directory-application-proxy-get-started).

-   Abilitare la sicurezza dell'accesso alle applicazioni grazie all'[autenticazione a più fattori](https://docs.microsoft.com/azure/multi-factor-authentication/multi-factor-authentication-whats-next) basata su regole per applicazioni locali e cloud.

-   Migliorare la produttività degli utenti con la [reimpostazione delle password self-service](https://docs.microsoft.com/azure/active-directory/active-directory-passwords) e il [portale delle app personali](https://docs.microsoft.com/azure/active-directory/active-directory-saas-access-panel-user-help) per le richieste di accesso a gruppi e applicazioni.

-   Sfruttare [la disponibilità elevata e l'affidabilità](https://docs.microsoft.com/azure/architecture/resiliency/high-availability-azure-applications) di una soluzione internazionale di gestione degli accessi e delle identità basata sul cloud di livello aziendale.

## <a name="next-steps"></a>Passaggi successivi
[Altre informazioni sulle soluzioni per la gestione delle identità di Azure](https://docs.microsoft.com/azure/active-directory/understand-azure-identity-solutions)
