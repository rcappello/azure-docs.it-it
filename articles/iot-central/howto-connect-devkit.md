---
title: Connettere un dispositivo DevKit all'applicazione Azure IoT Central | Microsoft Docs
description: Informazioni su come connettere un dispositivo MXChip IoT DevKit all'applicazione Azure IoT Central nello sviluppo di dispositivi.
author: tbhagwat3
ms.author: tanmayb
ms.date: 04/16/2018
ms.topic: conceptual
ms.service: iot-central
services: iot-central
manager: peterpr
ms.openlocfilehash: ea9ff8f93ede3b9ec5e7eed83c6049b0c23de7e8
ms.sourcegitcommit: 30221e77dd199ffe0f2e86f6e762df5a32cdbe5f
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 07/23/2018
ms.locfileid: "39205460"
---
# <a name="connect-an-mxchip-iot-devkit-device-to-your-azure-iot-central-application"></a>Connettere un dispositivo MXChip IoT DevKit all'applicazione Azure IoT Central

Questo articolo descrive come connettere un dispositivo MXChip IoT DevKit (DevKit) all'applicazione Microsoft Azure IoT Central nello sviluppo di dispositivi.

## <a name="before-you-begin"></a>Prima di iniziare

Per seguire la procedura descritta in questo articolo, sono necessari gli elementi seguenti:

1. Un'applicazione Azure IoT Central creata dal modello di applicazione **Sample Devkits**. Per altre informazioni, vedere [Creare l'applicazione Azure IoT Central](howto-create-application.md).
1. Un dispositivo DevKit. Per acquistare un dispositivo DevKit, vedere [MXChip IoT DevKit](http://mxchip.com/az3166).


## <a name="sample-devkits-application"></a>Applicazione **Sample Devkits**

Un'applicazione creata dal modello di applicazione **Sample Devkits** include un modello di dispositivo **MXChip** con le caratteristiche seguenti: 

- I dati di telemetria contenenti le misure del dispositivo relative a **umidità**, **temperatura**, **pressione**, **magnetometro** (lungo gli assi X, Y e Z), **accelerometro** (lungo gli assi X, Y e Z) e **giroscopio** (lungo gli assi X, Y e Z).
- Lo stato contenente una misura di esempio per lo **stato del dispositivo**.
- La misura relativa a un evento di tipo **Pulsante B premuto**. 
- Le impostazioni di visualizzazione per **tensione**, **corrente** e **velocità della ventola** e un comando di attivazione/disattivazione del **controllo a infrarossi**.
- Le proprietà relative al **numero dello stampo** e alla **posizione del dispositivo** oltre alla proprietà cloud relativa al **luogo di produzione**. 


Per informazioni dettagliate sulla configurazione, vedere [Dettagli del modello di dispositivo MXChip](howto-connect-devkit.md#mxchip-device-template-details).


## <a name="add-a-real-device"></a>Aggiungere un dispositivo reale

Nell'applicazione Azure IoT Central aggiungere un dispositivo reale dal modello di dispositivo **MXChip** e prendere nota della stringa di connessione del dispositivo. Per altre informazioni, vedere [Aggiungere un dispositivo reale all'applicazione Azure IoT Central](tutorial-add-device.md).

### <a name="prepare-the-devkit-device"></a>Preparare il dispositivo DevKit

> [!NOTE]
> Se il dispositivo è stato usato in precedenza e le credenziali Wi-Fi sono state salvate, per riconfigurare il dispositivo in modo che usi una rete Wi-Fi, una stringa di connessione o una misura di telemetria differente, premere contemporaneamente i pulsanti **A** e **B** sulla lavagna. Se non funziona, premere il pulsante di **reimpostazione** e riprovare.

#### <a name="before-you-start-configuring-the-device"></a>Prima di iniziare a configurare il dispositivo:
1. In **Sample Devkits** in IoT Central passare a `Device Explorer`-> `select MXChip Template` -> `Click on +New and choose **Real** Device` -> `Connect this device` (in alto a destra) 
2. Copiare la stringa di connessione primaria
3. Assicurarsi di salvare la stringa di connessione, poiché durante la preparazione del dispositivo DevKit la connessione a Internet verrà temporaneamente interrotta. 


#### <a name="to-prepare-the-devkit-device"></a>Per preparare il dispositivo DevKit:


1. Scaricare la versione più recente del firmware predefinito di Azure IoT Central per MXChip dalla pagina dei [rilasci](https://github.com/Azure/iot-central-firmware/releases) GitHub. Il nome del file di download nella pagina dei rilasci è simile a `AZ3166-IoT-Central-X.X.X.bin`.

1. Connettere il dispositivo DevKit al computer di sviluppo usando un cavo USB. In Windows viene visualizzata una finestra di Esplora file per un'unità mappata all'archiviazione nel dispositivo DevKit. Ad esempio, l'unità potrebbe chiamarsi **AZ3166 (D:)**.

1. Trascinare il file **iotCentral.bin** nella finestra dell'unità. Al termine del processo di copia il dispositivo viene riavviato con il nuovo firmware.

1. Al riavvio del dispositivo DevKit viene visualizzata la schermata seguente:

    ```
    Connect HotSpot:
    AZ3166_??????
    go-> 192.168.0.1 
    PIN CODE xxxxx
    ```

    > [!NOTE]
    > Se viene visualizzata una schermata diversa, premere contemporaneamente i pulsanti **A** e **B** sul dispositivo per riavviarlo. 

1. Il dispositivo è ora in modalità punto di accesso (AP). È possibile connettersi a questo punto di accesso Wi-Fi dal computer o dal dispositivo mobile.

1. Nel computer, telefono o tablet connettersi al nome della rete Wi-Fi visualizzato sullo schermo del dispositivo. Quando ci si connette a questa rete, non si può accedere a Internet. Questo stato è previsto e si rimane connessi a questa rete solo per un breve periodo di tempo durante la configurazione del dispositivo.

1. Aprire un Web browser e passare a [http://192.168.0.1/start](http://192.168.0.1/start). Viene visualizzata la pagina Web seguente:

    ![Pagina di configurazione del dispositivo](media/howto-connect-devkit/configpage.png)

    Nella pagina Web: 
    - aggiungere il nome della rete Wi-Fi 
    - la password della rete Wi-Fi
    - CODICE PIN visualizzato sul display del dispositivo 
    - la stringa di connessione del dispositivo, che dovrebbe essere già stata salvata nel corso della procedura: è possibile trovare la stringa di connessione in `https://apps.iotcentral.com` -> `Device Explorer` -> `Device` -> `Select or Create a new Real Device` -> `Connect this device` (in alto a destra)
    - Selezionare tutte le misure di telemetria disponibili. 

1. Dopo aver scelto di **configurare il dispositivo**, viene visualizzata questa pagina:

    ![Dispositivo configurato](media/howto-connect-devkit/deviceconfigured.png)

1. Premere il pulsante di **reimpostazione** sul dispositivo.



## <a name="view-the-telemetry"></a>Visualizzare i dati di telemetria

Al riavvio del dispositivo DevKit sulla schermata appare quanto segue:

* Il numero di messaggi di telemetria inviati.
* Il numero di errori.
* Il numero di proprietà desiderate ricevute e il numero di proprietà segnalate inviate.

Scuotere il dispositivo aumenta il numero di proprietà segnalate inviate. Il dispositivo invia un numero casuale come proprietà **Numero stampo** del dispositivo.

È possibile visualizzare le misure di telemetria e i valori delle proprietà segnalate e configurare le impostazioni in Azure IoT Central:

1. Usare **Device Explorer** per passare alla pagina delle **misure** per il dispositivo MXChip reale aggiunto:

    ![Passare al dispositivo reale](media/howto-connect-devkit/realdevicenew.png)

1. Nella pagina delle **misure** è possibile visualizzare i dati di telemetria provenienti dal dispositivo MXChip:

    ![Visualizzare i dati di telemetria dal dispositivo reale](media/howto-connect-devkit/devicetelemetrynew.png)

1. Nella pagina delle **proprietà** è possibile visualizzare l'ultimo numero stampo e il percorso dispositivo segnalato dal dispositivo:

    ![Visualizzare le proprietà del dispositivo](media/howto-connect-devkit/devicepropertynew.png)

1. Nella pagina delle **impostazioni** è possibile aggiornare le impostazioni per il dispositivo MXChip:

    ![Visualizzare le impostazioni del dispositivo](media/howto-connect-devkit/devicesettingsnew.png)

1. Nella pagina **Dashboard** è possibile visualizzare la mappa della posizione

    ![Visualizzare il dashboard dispositivo](media/howto-connect-devkit/devicedashboardnew.png)


## <a name="download-the-source-code"></a>Scaricare il codice sorgente

Per esaminare e modificare il codice del dispositivo, è possibile scaricarlo da GitHub. Se si prevede di modificare il codice, è opportuno seguire queste istruzioni per [preparare l'ambiente di sviluppo](https://microsoft.github.io/azure-iot-developer-kit/docs/get-started/#step-5-prepare-the-development-environment) per il sistema operativo desktop.

Per scaricare il codice sorgente, eseguire il comando seguente nel computer desktop:

```cmd/sh
git clone https://github.com/Azure/iot-central-firmware
```

Il comando precedente scarica il codice sorgente in una cartella denominata `iot-central-firmware`. 

> [!NOTE]
> Se **git** non è installato nell'ambiente di sviluppo, è possibile scaricarlo da [https://git-scm.com/download](https://git-scm.com/download).

## <a name="review-the-code"></a>Esaminare il codice

Usare Visual Studio Code, che è stato installato durante la preparazione dell'ambiente di sviluppo, per aprire la cartella `AZ3166` nella cartella `iot-central-firmware`: 

![Visual Studio Code](media/howto-connect-devkit/vscodeview.png)

Per vedere in che modo i dati di telemetria vengono inviati all'applicazione Azure IoT Central, aprire il file **main_telemetry.cpp** nella cartella di origine.

La funzione `buildTelemetryPayload` crea il payload della telemetria JSON usando i dati dei sensori nel dispositivo.

La funzione `sendTelemetryPayload` chiama `sendTelemetry` in **iotHubClient.cpp** per inviare il payload JSON all'hub IoT usato dall'applicazione Azure IoT Central.

Per vedere in che modo i valori delle proprietà vengono segnalati all'applicazione Azure IoT Central, aprire il file **main_telemetry.cpp** nella cartella di origine.

La funzione `telemetryLoop` invia la proprietà segnalata **doubleTap** quando l'accelerometro rileva un doppio tocco. Usa la funzione `sendReportedProperty` nel file di origine **iotHubClient.cpp**.

Il codice nel file di origine **iotHubClient.cpp** usa le funzioni [degli SDK e delle librerie di Microsoft Azure IoT per C](https://github.com/Azure/azure-iot-sdk-c) per interagire con l'hub IoT.

Per informazioni su come modificare, compilare e caricare il codice di esempio nel dispositivo, vedere il file **readme.md** nella cartella `AZ3166`.

## <a name="mxchip-device-template-details"></a>Dettagli del modello di dispositivo MXChip 

Un'applicazione creata dal modello di applicazione Sample Devkits include un modello di dispositivo MXChip con le caratteristiche seguenti:

### <a name="measurements"></a>Misure

#### <a name="telemetry"></a>Telemetria 

| Nome campo     | Unità  | Minima | Massima | Cifre decimali |
| -------------- | ------ | ------- | ------- | -------------- |
| umidità       | %      | 0       | 100     | 0              |
| temp           | °C     | -40     | 120     | 0              |
| pressure       | hPa    | 260     | 1260    | 0              |
| magnetometerX  | mgauss | -1000   | 1000    | 0              |
| magnetometerY  | mgauss | -1000   | 1000    | 0              |
| magnetometerZ  | mgauss | -1000   | 1000    | 0              |
| accelerometerX | mg     | -2000   | 2000    | 0              |
| accelerometerY | mg     | -2000   | 2000    | 0              |
| accelerometerZ | mg     | -2000   | 2000    | 0              |
| gyroscopeX     | mdps   | -2000   | 2000    | 0              |
| gyroscopeY     | mdps   | -2000   | 2000    | 0              |
| gyroscopeZ     | mdps   | -2000   | 2000    | 0              |


#### <a name="states"></a>Stati 
| NOME          | Nome visualizzato   | NORMALE | ATTENZIONE | PERICOLO | 
| ------------- | -------------- | ------ | ------- | ------ | 
| DeviceState   | Stato del dispositivo   | Verde  | Arancione  | Rosso    | 

#### <a name="events"></a>Eventi 
| NOME             | Nome visualizzato      | 
| ---------------- | ----------------- | 
| ButtonBPressed   | Pulsante B premuto  | 

### <a name="settings"></a>Impostazioni

Impostazioni numeriche

| Nome visualizzato | Nome campo | Unità | Cifre decimali | Minima | Massima | Initial |
| ------------ | ---------- | ----- | -------------- | ------- | ------- | ------- |
| Tensione      | setVoltage | Volt | 0              | 0       | 240     | 0       |
| Current      | setCurrent | Amp  | 0              | 0       | 100     | 0       |
| Velocità della ventola    | fanSpeed   | RPM   | 0              | 0       | 1000    | 0       |

Impostazioni attivazione/disattivazione

| Nome visualizzato | Nome campo | Testo attivato | Testo disattivato | Initial |
| ------------ | ---------- | ------- | -------- | ------- |
| IR           | activateIR | ATTIVA      | DISATTIVA      | Off     |

### <a name="properties"></a>Properties

| type            | Nome visualizzato | Nome campo | Tipo di dati |
| --------------- | ------------ | ---------- | --------- |
| Proprietà dispositivo | Numero stampo   | dieNumber  | number    |
| Proprietà dispositivo | Percorso dispositivo   | location  | location    |
| Text            | Prodotto in     | manufacturedIn   | N/D       |



## <a name="next-steps"></a>Passaggi successivi

Ora che si conosce la procedura per collegare un dispositivo DevKit all'applicazione Azure IoT Central, ecco i passi successivi suggeriti:

* [Preparare e connettere un dispositivo Raspberry Pi](howto-connect-raspberry-pi-python.md)
