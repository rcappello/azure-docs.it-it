---
title: Schemi di rilevamento AS2 per i messaggi B2B - App per la logica di Azure | Microsoft Docs
description: Creare schemi di rilevamento AS2 che consentono di monitorare i messaggi B2B negli account di integrazione per App per la logica di Azure con Enterprise Integration Pack
services: logic-apps
ms.service: logic-apps
ms.suite: integration
author: divyaswarnkar
ms.author: divswa
ms.reviewer: jonfan, estfan, LADocs
ms.topic: article
ms.assetid: f169c411-1bd7-4554-80c1-84351247bf94
ms.date: 01/27/2017
ms.openlocfilehash: 6c4144d26042729684e507b1afaa5e3006d8a34e
ms.sourcegitcommit: 2ad510772e28f5eddd15ba265746c368356244ae
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 08/28/2018
ms.locfileid: "43125931"
---
# <a name="create-schemas-for-tracking-as2-messages-and-mdns-in-integration-accounts-for-azure-logic-apps"></a>Creare schemi per il rilevamento di messaggi AS2 e notifiche sulla ricezione del messaggio negli account di integrazione per App per la logica di Azure

Per monitorare più facilmente il completamento delle operazioni, gli errori e le proprietà dei messaggi per le transazioni business-to-business (B2B) è possibile usare questi schemi di rilevamento AS2 nell'account di integrazione:

* Schema di rilevamento messaggi AS2
* Schema di rilevamento MDN AS2

## <a name="as2-message-tracking-schema"></a>Schema di rilevamento messaggi AS2

```json
{
   "agreementProperties": {  
      "senderPartnerName": "",  
      "receiverPartnerName": "",  
      "as2To": "",  
      "as2From": "",  
      "agreementName": ""  
   },  
   "messageProperties": {
      "direction": "",
      "messageId": "",
      "dispositionType": "",
      "fileName": "",
      "isMessageFailed": "",
      "isMessageSigned": "",
      "isMessageEncrypted": "",
      "isMessageCompressed": "",
      "correlationMessageId": "",
      "incomingHeaders": {
       },
      "outgoingHeaders": {
       },
      "isNrrEnabled": "",
      "isMdnExpected": "",
      "mdnType": ""
    }
}
```

| Proprietà | Tipo | Descrizione |
| --- | --- | --- |
| senderPartnerName | string | Nome partner del mittente del messaggio AS2. Facoltativa |
| receiverPartnerName | string | Nome partner del destinatario del messaggio AS2. Facoltativa |
| as2To | string | Nome del destinatario del messaggio AS2, dalle intestazioni del messaggio AS2. Obbligatoria |
| as2From | string | Nome del mittente del messaggio AS2, dalle intestazioni del messaggio AS2. Obbligatoria |
| agreementName | string | Nome del contratto AS2 in base al quale vengono risolti i messaggi. Facoltativa |
| direction | string | Direzione del flusso dei messaggi, ricezione o invio. Obbligatoria |
| messageId | string | ID del messaggio AS2, dalle intestazioni del messaggio AS2. Facoltativa |
| dispositionType |string | Valore del tipo di notifica sulla ricezione del messaggio (MDN). Facoltativa |
| fileName | string | Nome di file, dall'intestazione del messaggio AS2. Facoltativa |
| isMessageFailed |boolean | Se il messaggio AS2 non è riuscito. Obbligatoria |
| isMessageSigned | boolean | Se il messaggio AS2 era firmato. Obbligatoria |
| isMessageEncrypted | boolean | Se il messaggio AS2 era crittografato. Obbligatoria |
| isMessageCompressed |boolean | Se il messaggio AS2 era compresso. Obbligatoria |
| correlationMessageId | string | ID del messaggio AS2 per la correlazione dei messaggi con le notifiche MDN. Facoltativa |
| incomingHeaders |Dizionario di JToken | Dettagli dell'intestazione del messaggio AS2 in arrivo. Facoltativa |
| outgoingHeaders |Dizionario di JToken | Dettagli dell'intestazione del messaggio AS2 in uscita. Facoltativa |
| isNrrEnabled | boolean | Usare il valore predefinito se questo valore è sconosciuto. Obbligatoria |
| isMdnExpected | Boolean | Usare il valore predefinito se questo valore è sconosciuto. Obbligatoria |
| mdnType | Enum | I valori consentiti sono **NotConfigured**, **Sync** e **Async**. Obbligatoria |
||||

## <a name="as2-mdn-tracking-schema"></a>Schema di rilevamento MDN AS2

```json
{
   "agreementProperties": {
      "senderPartnerName": "",
      "receiverPartnerName": "",
      "as2To": "",
      "as2From": "",
      "agreementName": "g"
   },
   "messageProperties": {
      "direction": "",
      "messageId": "",
      "originalMessageId": "",
      "dispositionType": "",
      "isMessageFailed": "",
      "isMessageSigned": "",
      "isNrrEnabled": "",
      "statusCode": "",
      "micVerificationStatus": "",
      "correlationMessageId": "",
      "incomingHeaders": {
      },
      "outgoingHeaders": {
      }
   }
}
```

| Proprietà | type | Descrizione |
| --- | --- | --- |
| senderPartnerName | string | Nome partner del mittente del messaggio AS2. Facoltativa |
| receiverPartnerName | string | Nome partner del destinatario del messaggio AS2. Facoltativa |
| as2To | string | Nome partner che riceve il messaggio AS2. Obbligatoria |
| as2From | string | Nome partner che invia il messaggio AS2. Obbligatoria |
| agreementName | string | Nome del contratto AS2 in base al quale vengono risolti i messaggi. Facoltativa |
| direction |string | Direzione del flusso dei messaggi, ricezione o invio. Obbligatoria |
| messageId | string | ID del messaggio AS2. Facoltativa |
| originalMessageId |string | ID del messaggio originale AS2. Facoltativa |
| dispositionType | string | Valore del tipo di gestione MDN. Facoltativa |
| isMessageFailed |boolean | Se il messaggio AS2 non è riuscito. Obbligatoria |
| isMessageSigned |boolean | Se il messaggio AS2 era firmato. Obbligatoria |
| isNrrEnabled | boolean | Usare il valore predefinito se questo valore è sconosciuto. Obbligatoria |
| statusCode | Enum | I valori consentiti sono **Accepted**, **Rejected** e **AcceptedWithErrors**. Obbligatoria |
| micVerificationStatus | Enum | I valori consentiti sono **NotApplicable**, **Succeeded** e **Failed**. Obbligatoria |
| correlationMessageId | string | ID correlazione. ID del messaggio originale, ovvero ID del messaggio per cui è configurata la notifica MDN. Facoltativa |
| incomingHeaders | Dizionario di JToken | Indica i dettagli dell'intestazione del messaggio in arrivo. Facoltativa |
| outgoingHeaders |Dizionario di JToken | Indica i dettagli dell'intestazione del messaggio in uscita. Facoltativa |
||||

## <a name="b2b-protocol-tracking-schemas"></a>Schemi di rilevamento per il protocollo B2B

Per informazioni sugli schemi di rilevamento per il protocollo B2B, vedere:

* [Schemi di rilevamento X12](logic-apps-track-integration-account-x12-tracking-schema.md)
* [Schemi di rilevamento personalizzati B2B](logic-apps-track-integration-account-custom-tracking-schema.md)

## <a name="next-steps"></a>Passaggi successivi

* Informazioni sul [monitoraggio dei messaggi B2B](logic-apps-monitor-b2b-message.md)
* Informazioni sul [rilevamento dei messaggi B2B in Log Analytics](../logic-apps/logic-apps-track-b2b-messages-omsportal.md)