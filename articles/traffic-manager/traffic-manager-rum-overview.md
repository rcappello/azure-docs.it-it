---
title: Misurazioni utente reale in Gestione traffico di Azure | Microsoft Docs
description: Introduzione a Misurazioni utente reale in Gestione traffico
services: traffic-manager
documentationcenter: traffic-manager
author: KumudD
manager: timlt
editor: ''
tags: ''
ms.assetid: ''
ms.service: traffic-manager
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: ''
ms.workload: infrastructure
ms.date: 03/16/2018
ms.author: kumud
ms.custom: ''
ms.openlocfilehash: 4e8d808d65c9898d230455d128e3ffc50db303d6
ms.sourcegitcommit: 48ab1b6526ce290316b9da4d18de00c77526a541
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 03/23/2018
ms.locfileid: "30178114"
---
# <a name="traffic-manager-real-user-measurements-overview"></a>Panoramica di Misurazioni utente reale in Gestione traffico

Quando si configura un profilo di Gestione traffico per usare il metodo di routing delle prestazioni, il servizio esamina da dove provengono le richieste di query DNS e prende decisioni di routing per indirizzare tali richiedenti all'area di Azure che dia loro la latenza più bassa. Questa operazione viene eseguita usando l'intelligence della latenza di rete che Gestione traffico mantiene per reti di utenti finali diverse.

Misurazioni utente reale consente di misurare le misurazioni di latenza di rete per le aree di Azure, dalle applicazioni client che usano gli utenti finali, e a Gestione traffico di considerare anche tali informazioni per prendere decisioni di routing. Se si sceglie di usare Misurazioni utente reale, è possibile aumentare l'accuratezza del routing per le richieste provenienti dalle reti in cui si trovano gli utenti finali. 

## <a name="how-real-user-measurements-work"></a>Funzionamento di Misurazioni utente reale

Misurazioni utente reale fa in modo che le applicazioni client misurino la latenza per le aree di Azure come rilevata dalle reti degli utenti finali in cui vengono usate. Ad esempio, se si dispone di una pagina Web accessibile da utenti in posizioni diverse (ad esempio, le regioni nord americane), è possibile sfruttare la potenza di Misurazioni utente reale quando si usa il metodo di routing delle prestazioni per ottenerle nella migliore area di Azure in cui l'applicazione server è ospitata.

Inizia incorporando un JavaScript fornito da Azure (con una chiave univoca in esso) nelle pagine Web. Al termine dell'operazione, ogni volta che un utente visita la pagina Web, JavaScript esegue una query a Gestione traffico per ottenere informazioni sulle aree di Azure che deve misurare. Il servizio restituisce un set di endpoint allo script, che quindi misura tali aree consecutivamente scaricando un'immagine a un singolo pixel ospitata in tali aree di Azure e annotando la latenza tra il momento in cui la richiesta è stata inviata e l'ora di ricezione del primo byte. Queste misurazioni vengono quindi riferite al servizio di Gestione traffico.

Nel tempo, questo si verifica più volte e in molte reti facendo sì che Gestione traffico ottenga informazioni più accurate sulle caratteristiche di latenza delle reti in cui si trovano gli utenti finali. Queste informazioni iniziano ad essere incluse nelle decisioni di routing prese da Gestione traffico. Di conseguenza, tale operazione comporta una maggiore accuratezza in quelle decisioni basate sulle misurazioni utente reale inviate.

Quando si usa Misurazioni utente reale, la fatturazione viene eseguita in base al numero di misurazioni inviate a Gestione traffico. Per altri dettagli sui prezzi, visitare la [pagina dei prezzi di Gestione Traffico](https://azure.microsoft.com/pricing/details/traffic-manager/).

## <a name="next-steps"></a>Passaggi successivi
- Informazioni su come usare [Misurazioni utente reale con le pagine Web](traffic-manager-create-rum-web-pages.md)
- Informazioni sul [funzionamento di Gestione traffico](traffic-manager-overview.md)
- Altre informazioni su [Mobile Center](https://docs.microsoft.com/mobile-center/)
- Ulteriori informazioni sui [metodi di routing del traffico](traffic-manager-routing-methods.md) supportati da Gestione traffico
- Informazioni su come [creare un profilo di Gestione traffico](traffic-manager-create-profile.md)

