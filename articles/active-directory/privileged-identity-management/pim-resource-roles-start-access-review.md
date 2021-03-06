---
title: Avviare una verifica di accesso per i ruoli delle risorse di Azure in PIM | Microsoft Docs
description: Informazioni su come avviare una verifica di accesso per i ruoli delle risorse di Azure in Azure AD Privileged Identity Management (PIM).
services: active-directory
documentationcenter: ''
author: rolyon
manager: mtillman
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: conceptual
ms.component: pim
ms.date: 04/02/2018
ms.author: rolyon
ms.custom: pim
ms.openlocfilehash: 9a35d32d89931a03b33f232ba4f79226fc3f57e5
ms.sourcegitcommit: 63613e4c7edf1b1875a2974a29ab2a8ce5d90e3b
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 08/29/2018
ms.locfileid: "43189175"
---
# <a name="start-an-access-review-for-azure-resource-roles-in-pim"></a>Avviare una verifica di accesso per i ruoli delle risorse di Azure in PIM
Le assegnazioni dei ruoli diventano "obsolete" quando gli utenti hanno accessi con privilegi di cui non necessitano più. Per ridurre il rischio associato alle assegnazioni dei ruoli obsolete, gli amministratori dei ruoli con privilegi devono verificare periodicamente i ruoli. Questo documento illustra i passaggi per l'avvio di una verifica di accesso in Privileged Identity Management (PIM) per risorse di Azure.

Dalla pagina principale dell'applicazione PIM, passare a:

* **Verifiche di accesso** > **Aggiungi**

![Aggiungere verifiche di accesso](media/azure-pim-resource-rbac/rbac-access-review-home.png)

Quando si seleziona il pulsante **Aggiungi** viene visualizzato il pannello **Crea una verifica di accesso**. In questo pannello configurare la verifica assegnando un nome e un limite temporale, scegliere un ruolo da verificare e decidere chi esegue la verifica.

![Creare una verifica di accesso](media/azure-pim-resource-rbac/rbac-create-access-review.png)

### <a name="configure-the-review"></a>Configurare la verifica
Per creare una verifica di accesso, assegnare prima di tutto un nome e poi impostare le date di inizio e di fine.

![Schermata di configurazione della verifica](media/azure-pim-resource-rbac/rbac-access-review-setting-1.png)

Definire una durata della verifica che consenta agli utenti di completare l'operazione. Se la verifica termina prima della data di fine, è sempre possibile arrestare la verifica in anticipo.

### <a name="choose-a-role-to-review"></a>Scegliere un ruolo da verificare
Ogni verifica è incentrata su un solo ruolo. A meno che la verifica di accesso non sia stata avviata dal pannello di un ruolo specifico, è ora necessario scegliere un ruolo.

1. Passare a **Verifica l'appartenenza ai ruoli**
   
    ![Schermata Verifica l'appartenenza ai ruoli](media/azure-pim-resource-rbac/rbac-access-review-setting-2.png)
2. Scegliere un ruolo dall'elenco.

### <a name="decide-who-will-perform-the-review"></a>Decidere chi eseguirà la verifica
Sono disponibili tre opzioni per l'esecuzione di una verifica. La revisione può essere assegnata a un altro utente, essere eseguita personalmente oppure ogni utente può verificare il proprio accesso.

1. Scegliere una delle opzioni disponibili:
   
   * **Utenti selezionati**: usare questa opzione quando non è noto chi abbia bisogno dell'accesso. Con questa opzione è possibile assegnare l'esecuzione della revisione a un proprietario delle risorse o a un gestore del gruppo.
   * **Assegnato (autonomo)**: usare questa opzione per fare in modo che gli utenti verifichino le proprie assegnazioni di ruolo.
   
2. Passare a **Selezionare i revisori**.
   
    ![Schermata Selezionare i revisori](media/azure-pim-resource-rbac/rbac-access-review-setting-3.png)

### <a name="start-the-review"></a>Avviare la verifica
Infine, è possibile richiedere che gli utenti forniscano un motivo per l'approvazione dell'accesso. Se si vuole, aggiungere una descrizione della verifica. Quindi selezionare **Avvia**.

È necessario informare gli utenti che è presente una verifica dell'accesso in attesa e indicare loro [come eseguire una verifica dell'accesso](pim-resource-roles-perform-access-review.md).

## <a name="manage-the-access-review"></a>Gestire la verifica di accesso
È possibile tenere traccia dello stato di avanzamento delle verifiche eseguite dai revisori nel dashboard delle risorse di Azure in PIM. Nessun diritto di accesso viene modificato nella directory fino al [completamento della verifica](pim-resource-roles-complete-access-review.md).

Fino al termine del periodo di verifica, è possibile ricordare agli utenti di completare la verifica o arrestare la verifica in anticipo nella sezione Verifiche di accesso.

## <a name="next-steps"></a>Passaggi successivi

- [Completare una verifica di accesso per i ruoli delle risorse di Azure in PIM](pim-resource-roles-complete-access-review.md)
- [Eseguire una verifica di accesso dei ruoli delle risorse di Azure in PIM](pim-resource-roles-perform-access-review.md)
- [Avviare una verifica di accesso per i ruoli della directory di Azure AD in PIM](pim-how-to-start-security-review.md)
