---
title: Progettazione interativa di app in Language Understanding (LUIS)
titleSuffix: Azure Cognitive Services
description: LUIS apprende meglio in un ciclo iterativo di modifiche ai modelli, esempi di espressioni, pubblicazione e raccolta di dati da query endpoint.  Le app LUIS richiedono iterazioni di progettazione per eseguire il training di LUIS e ottenere l'estrazione dei dati migliori.
services: cognitive-services
author: diberry
manager: cgronlun
ms.service: cognitive-services
ms.component: language-understanding
ms.topic: article
ms.date: 09/10/2018
ms.author: diberry
ms.openlocfilehash: 05f5ceb5a0f3529d7635f7aae0c3c41c19f0b1ad
ms.sourcegitcommit: 4ecc62198f299fc215c49e38bca81f7eb62cdef3
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 09/24/2018
ms.locfileid: "47031952"
---
# <a name="authoring-cycle"></a>Ciclo di creazione
LUIS apprende meglio in un ciclo iterativo di modifiche ai modelli, esempi di espressioni, pubblicazione e raccolta di dati da query endpoint. 

![Ciclo di creazione](./media/luis-concept-app-iteration/iteration.png)

## <a name="building-a-luis-model"></a>Creazione di un modello LUIS
Lo scopo del modello è capire ciò che l'utente sta chiedendo (finalità) e quali parti della domanda forniscono i dettagli (entità) necessari a determinare la risposta. 

Il modello deve essere specifico del dominio dell'app per determinare le parole e le frasi rilevanti, oltre all'ordine tipico delle parole. 

Il modello include finalità ed entità. 

## <a name="add-training-examples"></a>Aggiungere esempi di training
LUIS necessita di espressioni di esempio nelle finalità. Gli esempi richiedono un numero sufficiente di variazioni nella scelta e nell'ordine delle parole per poter determinare la finalità dell'espressione. Per ogni espressione di esempio tutti i dati necessari devono essere etichettati come entità. 

Indicare a LUIS di ignorare le espressioni non rilevanti per il dominio dell'app assegnando l'espressione alla finalità **None** (Nessuna). Eventuali parole o frasi che non è necessario estrarre da un'espressione non devono essere etichettate. Non è prevista alcuna etichetta per le parole o le frasi da ignorare. 

## <a name="train-and-publish-the-app"></a>Eseguire il training dell'app e pubblicarla
Quando si dispone di 10 - 15 diverse espressioni per ciascuna finalità, e le entità necessarie sono etichettate, eseguire il training, quindi pubblicare. Dalla notifica di esito positivo della pubblicazione, usare il collegamento per ottenere gli endpoint. Assicurarsi di creare l'app e di pubblicarla affinché sia disponibile nelle [regioni endpoint](luis-reference-regions.md) necessarie. 

## <a name="https-endpoint-testing"></a>Test dall'endpoint HTTPS
È possibile eseguire il test dell'app LUIS dall'endpoint HTTPS. Il test dall'endpoint consente a LUIS di scegliere qualsiasi espressione con bassa probabilità di revisione.  

## <a name="recycle"></a>Ripetere il ciclo
Dopo aver completato un ciclo di creazione, è possibile ricominciare. Rivedere innanzitutto le espressioni endpoint che LUIS ha contrassegnato con probabilità bassa. Controllare le espressioni a livello di finalità e di entità. Dopo aver rivisto le espressioni, l'elenco di revisione dovrebbe risultare vuoto.  

## <a name="batch-testing"></a>Test in batch
Il test in batch è un modo per stabilire a quante espressioni di esempio LUIS assegna un punteggio. Gli esempi devono essere nuovi per LUIS e devono essere etichettati correttamente con la finalità e le entità che LUIS deve trovare. I risultati del test indicano le prestazioni di LUIS relativamente a quel set di espressioni. 

## <a name="next-steps"></a>Passaggi successivi

Concetti di [collaborazione](luis-concept-collaborator.md).