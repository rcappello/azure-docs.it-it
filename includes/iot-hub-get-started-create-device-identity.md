---
title: File di inclusione
description: File di inclusione
services: iot-hub
author: dominicbetts
ms.service: iot-hub
ms.topic: include
ms.date: 09/07/2018
ms.author: dobett
ms.custom: include file
ms.openlocfilehash: e80033d696de1b83da43fc27e5be9eca3b3f8757
ms.sourcegitcommit: 2d961702f23e63ee63eddf52086e0c8573aec8dd
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 09/07/2018
ms.locfileid: "44169163"
---
## <a name="create-a-device-identity"></a>Creare un'identità del dispositivo

In questa sezione si usa l'interfaccia della riga di comando di Azure per creare un'identità del dispositivo per questa esercitazione. L'interfaccia della riga di comando di Azure è preinstallata in [Azure Cloud Shell](https://docs.microsoft.com/zure/cloud-shell/overview) oppure è possibile [installarla localmente](https://docs.microsoft.com/cli/azure/install-azure-cli?view=azure-cli-latest). Gli ID dispositivo fanno distinzione tra maiuscole e minuscole.

1. Eseguire il seguente comando nell'ambiente della riga di comando in cui si usa l'interfaccia della riga di comando di Azure per installare l'estensione IoT:

    ```cmd/sh
    az extension add --name azure-cli-iot-ext
    ```

1. Se si sta eseguendo l'interfaccia della riga di comando di Azure localmente, usare il seguente comando per accedere al proprio account Azure (se si usa Cloud Shell, è stato effettuato automaticamente l'accesso e non è necessario eseguire questo comando):

    ```cmd/sh
    az login
    ```

1. Infine, creare una nuova identità del dispositivo denominata `myDeviceId` e recuperare la stringa di connessione con questi comandi:

    ```cmd/sh
    az iot hub device-identity create --device-id myDeviceId --hub-name {Your IoT Hub name}
    az iot hub device-identity show-connection-string --device-id myDeviceId --hub-name {Your IoT Hub name} -o table
    ```

   [!INCLUDE [iot-hub-pii-note-naming-device](iot-hub-pii-note-naming-device.md)]

Annotare la stringa di connessione del dispositivo visualizzata nei risultati. Questa stringa di connessione del dispositivo viene usata dall'app del dispositivo per la connessione all'hub IoT come dispositivo.

<!-- images and links -->
