---
title: Guida alla pubblicazione di offerte di macchine virtuali per Azure Marketplace
description: Questo articolo descrive i requisiti per pubblicare una macchina virtuale e una versione di prova gratuita del software da distribuire dal Marketplace.
services: Azure, Marketplace, Compute, Storage, Networking, Blockchain, Security
documentationcenter: ''
author: ellacroi
manager: nunoc
editor: ''
ms.assetid: ''
ms.service: marketplace
ms.workload: ''
ms.tgt_pltfrm: ''
ms.devlang: ''
ms.topic: article
ms.date: 07/09/2018
ms.author: ellacroi
ms.openlocfilehash: b8caeab7f08ffeee81492b01750cbb255e172872
ms.sourcegitcommit: a1140e6b839ad79e454186ee95b01376233a1d1f
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 08/28/2018
ms.locfileid: "43144523"
---
# <a name="virtual-machine-offer-publishing-guide"></a>Guida alla pubblicazione di offerte di macchine virtuali

Le immagini delle macchine virtuali sono uno dei modi principali di pubblicare una soluzione nel Marketplace di Azure. Usare questa guida per comprendere i requisiti per questa offerta. 

Sono offerte di transazioni che vengono distribuite e fatturate attraverso il Marketplace. L'utente viene invitato all'azione tramite "Scarica adesso".

## <a name="free-trial"></a>Versione di valutazione gratuita 

È possibile fare in modo che gli utenti possano testare la propria offerta accedendo a licenze software per un periodo limitato quando usano il modello di fatturazione Bring Your Own License (BYOL). Di seguito sono riportati i requisiti per implementare questa offerta. 

|Requisiti  |Dettagli  |
|---------|---------|
|Periodo di valutazione gratuita ed esperienza di valutazione     |   Il cliente può provare l'app gratuitamente per un periodo di tempo limitato. Il cliente non deve pagare costi di licenza o di sottoscrizione per l'offerta. I clienti non devono pagare il prodotto o il servizio proprietario di Microsoft sottostante. Tutte le opzioni di valutazione sono distribuite nella sottoscrizione di Azure. L'utente ha il controllo esclusivo dell'ottimizzazione dei costi e della gestione. È possibile scegliere una versione di valutazione gratuita o una demo interattiva. Indipendentemente dall'opzione selezionata, per la prova gratuita è necessario concedere al cliente un periodo prestabilito di tempo per provare l'offerta senza costi aggiuntivi.|
|Soluzione pronta all'uso e facilmente configurabile    |  L'app deve essere semplice e rapida da configurare e installare.       |
|Disponibilità/Tempo di attività    |    L'app o la piattaforma SaaS deve avere un tempo di attività pari ad almeno il 99,9%.     |
|Azure Active Directory     |    L'offerta deve consentire l'accesso Single Sign-On (SSO) federato di Azure Active Directory (accesso SSO federato di Azure AD) con il consenso abilitato.     |

## <a name="test-drive"></a>Test drive

Vengono distribuite una o più macchine virtuali tramite le applicazioni IaaS (infrastructure-as-a-service) o SaaS. Un vantaggio dell'opzione di pubblicazione del test drive è il provisioning automatico di una macchina virtuale o dell'intera soluzione con una presentazione guidata ospitata da un partner. Un test drive fornisce al cliente una valutazione senza alcun costo aggiuntivo. Non è necessario che il cliente sia già un utente di Azure per partecipare all'esperienza di prova. 

Per iniziare, contattare Microsoft all'indirizzo [amp-testdrive](mailto:amp-testdrive@microsoft.com). 

|Requisiti  |Dettagli |
|---------|---------|
| Si dispone di un'app di Marketplace   |    Una o più macchine virtuali tramite IaaS o SaaS.      |

## <a name="interactive-demo"></a>Demo interattiva

Fornire ai clienti un'esperienza guidata della soluzione usando una demo interattiva. Il vantaggio dell'opzione di pubblicazione della demo interattiva è dato dalla possibilità di fornire un'esperienza di valutazione di una soluzione complessa senza dover eseguire complicate operazioni di provisioning. 

## <a name="virtual-machine-offer"></a>Offerta per le macchine virtuali

Usare il tipo di offerta per le macchine virtuali quando si distribuisce un'appliance virtuale all'abbonamento associato al cliente. Le macchine virtuali sono completamente abilitate per la commercializzazione tramite i modelli di licenza con pagamento in base al consumo o Bring Your Own License (BYOL). Microsoft gestisce la transazione commerciale e addebita il costo al cliente per conto dell'utente. Si ottiene il vantaggio di usare la relazione di pagamento preferita tra il cliente e Microsoft, compresi eventuali contratti Enterprise.

>[!NOTE]
>A questo punto, gli impegni monetari associati a un contratto Enterprise possono essere usati per l'utilizzo di Azure della macchina virtuale, ma non per i costi di licenza del software.  

>[!NOTE]
>È possibile limitare l'individuazione e la distribuzione della VM a un set specifico di clienti pubblicando l'immagine e i prezzi in un'inserzione privata. Le offerte private consentono agli utenti di creare offerte esclusive per i clienti principali e di proporre software e condizioni di utilizzo personalizzati. Tali condizioni personalizzate consentono di porre in evidenza numerosi scenari, con offerte contenenti condizioni e prezzi particolari, nonché l'accesso anticipato a versioni software limitate. Le offerte private consentono di offrire a un gruppo ristretto di clienti prezzi o prodotti specifici, creando un nuovo SKU con i dettagli selezionati.  
*   Per altre informazioni sulle offerte private, visitare la pagina relativa alle offerte private in Azure Marketplace all'indirizzo [azure.microsoft.com/blog/private-offers-on-azure-marketplace](https://azure.microsoft.com/blog/private-offers-on-azure-marketplace).  

| Requisito | Dettagli |  
|:--- |:--- | 
| Fatturazione e misurazione | La macchina virtuale deve supportare la fatturazione mensile BYOL o con pagamento in base al consumo. |  
| Disco rigido virtuale (VHD) compatibile con Azure | Le macchine virtuali devono essere compilate in Windows o Linux.<ul> <li>Per altre informazioni sulla creazione di un disco rigido virtuale Linux, visitare la sezione Creare un VHD compatibile con Azure (basato su Linux) all'indirizzo [docs.microsoft.com/azure/marketplace-publishing/marketplace-publishing-vm-image-creation#2-create-an-azure-compatible-vhd-linux-based](https://docs.microsoft.com/azure/marketplace-publishing/marketplace-publishing-vm-image-creation#2-create-an-azure-compatible-vhd-linux-based).</li> <li>Per altre informazioni sulla creazione di un disco rigido virtuale Windows, visitare la sezione Creare un VHD compatibile con Azure (basato su Windows) all'indirizzo [docs.microsoft.com/azure/marketplace-publishing/marketplace-publishing-vm-image-creation#3-create-an-azure-compatible-vhd-windows-based](https://docs.microsoft.com/azure/marketplace-publishing/marketplace-publishing-vm-image-creation#3-create-an-azure-compatible-vhd-windows-based).</li> </ul> |  

## <a name="next-steps"></a>Passaggi successivi

Se non è già stato fatto, 

- [Registrarsi](https://azuremarketplace.microsoft.com/sell) in Marketplace

Se la registrazione è già stata effettuata e si sta creando una nuova offerta o lavorando su una esistente,

- [Accedere al portale Cloud Partner](https://cloudpartner.azure.com) per creare e completare l'offerta
