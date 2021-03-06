---
title: Abilitare l'integrazione delle connessioni di LinkedIn ad Azure Active Directory | Microsoft Docs
description: Illustra come abilitare o disabilitare le connessioni dell'account LinkedIn per le app Microsoft in Azure Active Directory
services: active-directory
author: curtand
manager: mtillman
ms.service: active-directory
ms.workload: identity
ms.component: users-groups-roles
ms.topic: article
ms.date: 09/11/2018
ms.author: curtand
ms.reviewer: beengen
ms.custom: it-pro
ms.openlocfilehash: 0eaa2656313ecd9b64503051265dc16285f0a1f3
ms.sourcegitcommit: 794bfae2ae34263772d1f214a5a62ac29dcec3d2
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 09/11/2018
ms.locfileid: "44492840"
---
# <a name="linkedin-account-connections"></a>Connessioni all'account LinkedIn

Questo articolo spiega come abilitare o disabilitare le connessioni all'account LinkedIn per il tenant nell'interfaccia di amministrazione di Azure Active Directory (Azure AD).

> [!IMPORTANT]
> L'impostazione delle connessioni all'account LinkedIn è attualmente in corso di distribuzione nei tenant di Azure AD. Quando viene distribuita nel tenant, questa funzionalità è abilitata per impostazione predefinita. 
> 
> Eccezioni:
> * L'impostazione non è disponibile per i clienti che usano Microsoft Cloud per il governo degli Stati Uniti, Microsoft Cloud per la Germania,oppure Azure e Office 365 gestito da 21Vianet in Cina.
> * L'impostazione è disattivata per impostazione predefinita per i tenant sottoposti a provisioning in Germania. L'impostazione non è disponibile per i clienti che usano Microsoft Cloud per la Germania.
> * L'impostazione è disattivata per impostazione predefinita per i tenant sottoposti a provisioning in Francia.

> L'integrazione funziona solo se è stato abilitato *e* se si consente agli utenti di dare il consenso all'accesso delle app ai dati aziendali per loro conto. Per informazioni sull'impostazione di consenso, vedere [Come eliminare l'accesso di un utente a un'applicazione](https://docs.microsoft.com/azure/active-directory/application-access-assignment-how-to-remove-assignment).

## <a name="enable-or-disable-linkedin-account-connections-for-your-tenant-in-the-azure-portal"></a>Abilitare o disabilitare le connessioni all'account LinkedIn per il tenant nel portale di Azure

È possibile scegliere di abilitare o disabilitare le connessioni all'account LinkedIn per l'intero tenant oppure solo per utenti selezionati nel tenant.

1. Accedere all'[interfaccia di amministrazione di Azure Active Directory](https://aad.portal.azure.com/) con un account amministratore globale per il tenant di Azure AD.
2. Selezionare **Utenti**.
3. Nel pannello **Utenti** selezionare **Impostazioni utente**.
4. In **LinkedIn account connections** (Connessioni account LinkedIn):
  * Selezionare **Sì** per abilitare le connessioni dell'account LinkedIn per tutti gli utenti nel tenant
  * Selezionare **Selezionati** per abilitare le connessioni dell'account LinkedIn solo per gli utenti del tenant selezionati
  * Selezionare **No** per disabilitare le connessioni dell'account LinkedIn per tutti gli utenti ![Abilitazione delle connessioni dell'account LinkedIn](./media/linkedin-integration/linkedin-integration.png)
5. Al termine salvare le impostazioni facendo clic su **Salva**.

## <a name="enable-or-disable-linkedin-account-connections-for-your-tenant-using-group-policy"></a>Abilitare o disabilitare le connessioni all'account LinkedIn per il tenant usando Criteri di gruppo

1. Scaricare i [file dei modelli amministrativi di Office 2016 (ADMX/ADML)](https://www.microsoft.com/download/details.aspx?id=49030)
2. Estrarre i file **ADMX** e copiarli nel repository centrale.
3. Aprire Gestione Criteri di gruppo.
4. Creare un oggetto Criteri di gruppo con le impostazioni seguenti: **Configurazione utente** > **Modelli amministrativi** > **Microsoft Office 2016** > **Varie** > **Show LinkedIn features in Office applications** (Mostra funzionalità di LinkedIn nelle applicazioni di Office).
5. Selezionare **Abilitato** o **Disabilitato**.
  
 Stato | Effetto
------ | ------
**Enabled** | L'impostazione **Visualizza funzionalità di LinkedIn nelle applicazioni di Office** è abilitata nelle Opzioni di Office 2016. Gli utenti dell'organizzazione possono usare le funzionalità di LinkedIn nelle applicazioni di Office.
 **Disabilitato** | L'impostazione **Visualizza funzionalità di LinkedIn nelle applicazioni di Office** è disabilitata nelle Opzioni di Office 2016 e gli utenti finali non possono modificare questa impostazione. Gli utenti dell'organizzazione non possono usare le funzionalità di LinkedIn nelle applicazioni di Office 2016.

Questi Criteri di gruppo influiscono solo sulle app di Office 2016 per il computer locale. Gli utenti possono visualizzare in Office 365 le funzionalità di LinkedIn nella scheda del profilo anche se disabilitano LinkedIn per le app di Office 2016.

## <a name="learn-more"></a>Altre informazioni

* [Integrare LinkedIn all'interno dell'organizzazione](linkedin-user-consent.md)

* [About LinkedIn information and features in Microsoft apps and services](https://go.microsoft.com/fwlink/?linkid=850740) (Informazioni e funzionalità di LinkedIn nelle app e nei servizi Microsoft)

* [Centro assistenza LinkedIn](https://www.linkedin.com/help/linkedin)

## <a name="next-steps"></a>Passaggi successivi
Usare il collegamento seguente per visualizzare le impostazioni correnti delle connessioni dell'account LinkedIn nel portale di Azure:

[Configurare le connessioni dell'account LinkedIn](https://aad.portal.azure.com/#blade/Microsoft_AAD_IAM/UserManagementMenuBlade/UserSettings) 