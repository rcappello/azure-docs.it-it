---
title: Registrare un nuovo dispositivo Azure IoT Edge (portale) | Microsoft Docs
description: Usare il portale di Azure per registrare un nuovo dispositivo IoT Edge
author: kgremban
manager: timlt
ms.author: kgremban
ms.date: 06/05/2018
ms.topic: conceptual
ms.service: iot-edge
services: iot-edge
ms.openlocfilehash: b61594469df33e11c23c9cbe0b9542da374fefa3
ms.sourcegitcommit: 150a40d8ba2beaf9e22b6feff414f8298a8ef868
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 06/27/2018
ms.locfileid: "37034736"
---
# <a name="register-a-new-azure-iot-edge-device-from-the-azure-portal"></a>Registrare un nuovo dispositivo Azure IoT Edge dal portale di Azure

Per poter usare i dispositivi IoT con Azure IoT Edge, è necessario registrarli nell'hub IoT. Dopo la registrazione di un dispositivo, si riceve una stringa di connessione che può essere usata per configurare il dispositivo per i carichi di lavoro Edge. 

Questo articolo illustra come registrare un nuovo dispositivo IoT Edge usando il portale di Azure.

## <a name="prerequisites"></a>Prerequisiti

* Un [hub IoT](../iot-hub/iot-hub-create-through-portal.md) nella sottoscrizione di Azure. 

## <a name="create-a-device"></a>Creare un dispositivo

Nel portale di Azure i dispositivi IoT Edge vengono creati e gestiti separatamente da quelli che si connettono all'hub IoT ma non sono abilitati per Edge. 

1. Accedere al [portale di Azure](https://portal.azure.com) e passare all'hub IoT. 
2. Selezionare **IoT Edge** dal menu.
3. Selezionare **Aggiungi dispositivo IoT Edge**. 
4. Specificare un ID descrittivo del dispositivo. 
5. Selezionare **Salva**. 

## <a name="view-all-devices"></a>Visualizzare tutti i dispositivi

Tutti i dispositivi abilitati per Edge che si connettono all'hub IoT sono elencati nella pagina **IoT Edge**. 

## <a name="retrieve-the-connection-string"></a>Recuperare la stringa di connessione

Quando si è pronti per configurare il dispositivo, è necessaria la stringa di connessione che collega il dispositivo fisico alla relativa identità nell'hub IoT.

1. Dalla pagina **IoT Edge** nel portale fare clic sull'ID del dispositivo nell'elenco dei dispositivi Edge. 
2. Copiare il valore di **Stringa di connessione - chiave primaria** o **Stringa di connessione - chiave secondaria**. 

## <a name="next-steps"></a>Passaggi successivi

Informazioni su come [distribuire moduli in un dispositivo con il portale di Azure](how-to-deploy-modules-portal.md)