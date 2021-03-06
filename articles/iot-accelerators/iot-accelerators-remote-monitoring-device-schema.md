---
title: Schema dei dispositivi nella soluzione di monitoraggio remoto - Azure | Microsoft Docs
description: Questo articolo descrive lo schema JSON che definisce un dispositivo simulato nella soluzione di monitoraggio remota.
author: dominicbetts
manager: timlt
ms.author: dobett
ms.service: iot-accelerators
services: iot-accelerators
ms.date: 01/29/2018
ms.topic: conceptual
ms.openlocfilehash: f312f29e14c371e7b500f3eee6471151e3544513
ms.sourcegitcommit: 0c64460a345c89a6b579b1d7e273435a5ab4157a
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 08/31/2018
ms.locfileid: "43338856"
---
# <a name="understand-the-device-model-schema"></a>Informazioni sullo schema del modello dei dispositivi

È possibile usare dispositivi simulati nella soluzione di monitoraggio remoto per testarne il comportamento. Quando si distribuisce la soluzione di monitoraggio remoto, viene eseguito automaticamente il provisioning di una raccolta di dispositivi simulati. È possibile personalizzare i dispositivi simulati esistenti o crearne di nuovi.

Questo articolo descrive lo schema del modello di dispositivo che specifica le funzionalità e il comportamento di un dispositivo simulato. Il modello del dispositivo viene archiviato in un file JSON.

Gli articoli seguenti sono correlati all'articolo corrente:

* [Implement the device model behavior](iot-accelerators-remote-monitoring-device-behavior.md) (Implementare il comportamento del modello di dispositivo) descrive i file JavaScript usati per implementare il comportamento di un dispositivo simulato.
* [Creare un nuovo dispositivo simulato](iot-accelerators-remote-monitoring-create-simulated-device.md) riunisce tutti gli aspetti e illustra come distribuire un nuovo tipo di dispositivo simulato nella soluzione.

In questo articolo viene spiegato come:

>[!div class="checklist"]
> * Usare un file JSON per definire un modello di dispositivo simulato
> * Specificare le proprietà del dispositivo simulato
> * Specificare i dati di telemetria inviati dal dispositivo simulato
> * Specificare i metodi da cloud a dispositivo a cui risponde il dispositivo

[!INCLUDE [iot-accelerators-device-schema](../../includes/iot-accelerators-device-schema.md)]

## <a name="next-steps"></a>Passaggi successivi

In questo articolo è stato descritto come creare un modello di dispositivo simulato personalizzato. In questo articolo sono state presentate le procedure per:

<!-- Repeat task list from intro -->
>[!div class="checklist"]
> * Usare un file JSON per definire un modello di dispositivo simulato
> * Specificare le proprietà del dispositivo simulato
> * Specificare i dati di telemetria inviati dal dispositivo simulato
> * Specificare i metodi da cloud a dispositivo a cui risponde il dispositivo

Dopo aver appreso alcune informazioni di base sullo schema JSON, il passaggio successivo consigliato consiste nello scoprire come [implementare il comportamento del dispositivo simulato](iot-accelerators-remote-monitoring-device-behavior.md).

Per altre informazioni per sviluppatori sulla soluzione di monitoraggio remoto, vedere:

* [Guida di riferimento per gli sviluppatori](https://github.com/Azure/azure-iot-pcs-remote-monitoring-dotnet/wiki/Developer-Reference-Guide)
* [Guida per la risoluzione dei problemi per gli sviluppatori](https://github.com/Azure/azure-iot-pcs-remote-monitoring-dotnet/wiki/Developer-Troubleshooting-Guide)
