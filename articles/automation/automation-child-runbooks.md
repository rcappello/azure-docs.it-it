---
title: Runbook figlio in Automazione di Azure
description: Descrive i diversi metodi per avviare un runbook in automazione di Azure da un altro runbook e condividere informazioni tra di essi.
services: automation
ms.service: automation
ms.component: process-automation
author: georgewallace
ms.author: gwallace
ms.date: 08/14/2018
ms.topic: conceptual
manager: carmonm
ms.openlocfilehash: 037c2714d146bd59b30573df874794342d743e03
ms.sourcegitcommit: e2348a7a40dc352677ae0d7e4096540b47704374
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 09/05/2018
ms.locfileid: "43782233"
---
# <a name="child-runbooks-in-azure-automation"></a>Runbook figlio in Automazione di Azure

È buona norma in automazione di Azure scrivere runbook riutilizzabili e modulari con una funzione discreta che può essere utilizzata da altri runbook. Un runbook padre chiama spesso uno o più runbook figlio per eseguire la funzionalità richiesta. Esistono due modi per chiamare un runbook figlio e ognuno presenta differenze che è necessario comprendere in modo che sia possibile determinare quale sarà migliore per i diversi scenari.

## <a name="invoking-a-child-runbook-using-inline-execution"></a>Richiamare un runbook figlio con esecuzione inline

Per richiamare un runbook inline da un altro runbook, utilizzare il nome del runbook e fornire valori per i relativi parametri, esattamente come si farebbe per un'attività o un cmdlet.  Tutti i runbook nello stesso account di automazione sono disponibili a tutti gli altri per essere utilizzati come quanto segue. Il runbook padre attenderà il completamento del runbook figlio prima di passare alla riga successiva e gli output vengono restituiti direttamente all'elemento padre.

Quando si richiama un runbook inline, esso viene eseguito nello stesso processo del runbook padre. Nella cronologia del processo non verrà indicato il runbook figlio eseguito. Eventuali eccezioni e flussi di output dal runbook figlio verranno associati all'elemento padre. In questo modo si ottiene un minor numero di processi che sono quindi più semplici da rilevare e risolvere poiché le eccezioni generate dal runbook figlio e i relativi output del flusso sono associati al processo padre.

Quando viene pubblicato un runbook, tutti i runbook figlio chiamati devono già essere pubblicati. Questo avviene perché l'automazione di Azure crea un'associazione con i runbook figlio quando viene compilato un runbook. In caso contrario, il runbook padre sembrerà pubblicato correttamente ma al suo avvio verrà generata un'eccezione. In questo caso, è possibile ripubblicare il runbook padre per fare riferimento in modo corretto ai runbook figlio. Non è necessario ripubblicare il runbook padre se alcuni runbook figlio sono stati modificati in quanto l'associazione sarà già stata creata.

I parametri di un runbook figlio chiamato inline possono essere costituiti da qualsiasi tipo di dati, inclusi gli oggetti complessi, e non esiste alcuna [serializzazione JSON](automation-starting-a-runbook.md#runbook-parameters) come quando si avvia il runbook usando il portale di Azure o il cmdlet Start-AzureRmAutomationRunbook.

### <a name="runbook-types"></a>Tipi di runbook

Tipi che possono richiamarsi a vicenda:

* Un [runbook di PowerShell](automation-runbook-types.md#powershell-runbooks) e i [runbook grafici](automation-runbook-types.md#graphical-runbooks) possono chiamarsi reciprocamente inline (entrambi i tipi sono basati su PowerShell).
* Un [runbook del flusso di lavoro PowerShell](automation-runbook-types.md#powershell-workflow-runbooks) e i runbook grafici del flusso di lavoro PowerShell possono richiamarsi a vicenda inline (entrambi i tipi si basano su PowerShell).
* I tipi PowerShell e i tipi di flusso di lavoro PowerShell non possono richiamarsi a vicenda online e devono utilizzare Start-AzureRmAutomationRunbook.

Quando è importante l’ordine di pubblicazione:

* L'ordine di pubblicazione dei runbook è rilevante solo per i runbook del flusso di lavoro PowerShell e i runbook grafici del flusso di lavoro PowerShell.

Quando si richiama un runbook figlio grafico o del flusso di lavoro PowerShell tramite l’esecuzione inline, è sufficiente utilizzare il nome del runbook.  Quando si chiama un runbook figlio di PowerShell, è necessario anteporre al nome *.\\* per specificare che lo script si trova nella directory locale.

### <a name="example"></a>Esempio

Nell'esempio seguente viene richiamato un runbook figlio di test che accetta tre parametri, un oggetto complesso, un numero intero e un valore booleano. L'output del runbook figlio viene assegnato a una variabile.  In questo caso, il runbook figlio è un runbook del flusso di lavoro PowerShell.

```azurepowershell-interactive
$vm = Get-AzureRmVM –ResourceGroupName "LabRG" –Name "MyVM"
$output = PSWF-ChildRunbook –VM $vm –RepeatCount 2 –Restart $true
```

Di seguito si trova lo stesso esempio con un runbook di PowerShell come elemento figlio.

```azurepowershell-interactive
$vm = Get-AzureRmVM –ResourceGroupName "LabRG" –Name "MyVM"
$output = .\PS-ChildRunbook.ps1 –VM $vm –RepeatCount 2 –Restart $true
```

## <a name="starting-a-child-runbook-using-cmdlet"></a>Avvio di un runbook figlio utilizzando cmdlet

È possibile usare il cmdlet [Start-AzureRmAutomationRunbook](/powershell/module/AzureRM.Automation/Start-AzureRmAutomationRunbook) per avviare un runbook come descritto nella sezione relativa all'[avvio di un runbook con Windows PowerShell](automation-starting-a-runbook.md#starting-a-runbook-with-windows-powershell). Sono disponibili due modalità di utilizzo di questo cmdlet.  In una modalità, il cmdlet restituisce l'ID del processo non appena viene creato il processo figlio per il runbook figlio.  Nell'altra modalità, che consente di specificare il parametro **-wait** , il cmdlet attende che l'elemento figlio finisca il processo e restituisce l'output dal runbook figlio.

Verrà eseguito il processo da un runbook figlio avviato con un cmdlet in un processo separato dal runbook padre. Questo comporta più processi rispetto al richiamo del runbook inline e li rende più difficili da rilevare. L'elemento padre può avviare diversi runbook figli in modo asincrono senza attendere che ognuno di essi sia terminato. Per questa stessa tipologia di esecuzione parallela che chiama l’inline del runbook figlio, il runbook padre dovrà usare la [parola chiave parallela](automation-powershell-workflow.md#parallel-processing).

L'output dei runbook figlio non viene restituito ai runbook padre in modo affidabile a causa dei tempi. È anche possibile che alcune variabili come $VerbosePreference, $WarningPreference e altre variabili non vengano propagate ai runbook figlio. Per evitare questi problemi, è possibile richiamare i runbook figlio come processi di automazione separati usando il cmdlet `Start-AzureRmAutomationRunbook` con l'opzione `-Wait`. In questo modo viene bloccato il runbook padre fino al completamento del runbook figlio.

Se non si vuole bloccare il runbook padre in attesa, è possibile richiamare il runbook figlio usando il cmdlet `Start-AzureRmAutomationRunbook` senza l'opzione `-Wait`. Sarà quindi necessario usare `Get-AzureRmAutomationJob` per attendere il completamento del processo e `Get-AzureRmAutomationJobOutput` e `Get-AzureRmAutomationJobOutputRecord` per recuperare i risultati.

I parametri per un runbook figlio avviato con un cmdlet vengono forniti come una tabella hash, come descritto in [Parametri di Runbook](automation-starting-a-runbook.md#runbook-parameters). Possono essere utilizzati solo tipi di dati semplici. Se il runbook dispone di un parametro con un tipo di dati complessi, deve essere chiamato inline.

Il contesto della sottoscrizione potrebbe andare perso quando si richiamano i runbook figli per processi separati. Affinché il runbook figlio possa richiamare i cmdlet di Azure Resource Manager con una sottoscrizione di Azure desiderata, il runbook figlio deve autenticarsi presso tale sottoscrizione indipendentemente dal runbook padre.

Se i processi nello stesso account di Automazione di Azure usano più sottoscrizioni, selezionare una sottoscrizione in un processo può cambiare il contesto della sottoscrizione attualmente selezionata anche per altri processi, che non è in genere consigliabile. Per evitare questo problema, salvare il risultato della chiamata cmdlet `Select-AzureRmSubscription` chiamata e passare questo oggetto al parametro `DefaultProfile` di tutte le chiamate cmdlet successive di Azure Resource Manager. Questo modello deve essere applicato in modo coerente a tutti i runbook in esecuzione nell'account di Automazione di Azure.

### <a name="example"></a>Esempio

Nell'esempio seguente viene avviato un runbook figlio con parametri e si attende il suo completamento con il parametro Start-AzureRmAutomationRunbook -wait. Una volta completato, l'output viene raccolto dal runbook figlio. Per usare `Start-AzureRmAutomationRunbook` è necessario eseguire l'autenticazione alla sottoscrizione di Azure.

```azurepowershell-interactive
# Connect to Azure with RunAs account
$ServicePrincipalConnection = Get-AutomationConnection -Name 'AzureRunAsConnection'

Add-AzureRmAccount `
    -ServicePrincipal `
    -TenantId $ServicePrincipalConnection.TenantId `
    -ApplicationId $ServicePrincipalConnection.ApplicationId `
    -CertificateThumbprint $ServicePrincipalConnection.CertificateThumbprint

$AzureContext = Select-AzureRmSubscription -SubscriptionId $ServicePrincipalConnection.SubscriptionID

$params = @{"VMName"="MyVM";"RepeatCount"=2;"Restart"=$true}

Start-AzureRmAutomationRunbook `
    –AutomationAccountName 'MyAutomationAccount' `
    –Name 'Test-ChildRunbook' `
    -ResourceGroupName 'LabRG' `
    -DefaultProfile $AzureContext `
    –Parameters $params –wait
```

## <a name="comparison-of-methods-for-calling-a-child-runbook"></a>Confronto di metodi per chiamare un runbook figlio

Nella tabella seguente vengono riepilogate le differenze tra i due metodi per chiamare un runbook da un altro runbook.

|  | Inline | Cmdlet |
|:--- |:--- |:--- |
| Processo |I runbook figlio vengono eseguiti nello stesso processo dell’elemento padre. |Viene creato un processo separato per il runbook figlio. |
| Esecuzione |Il runbook padre attende il completamento del runbook figlio prima di continuare. |Il runbook padre continua subito dopo l'avvio del runbook figlio *o* attende il completamento del processo figlio. |
| Output |Il runbook padre può ottenere output direttamente dal runbook figlio. |Il runbook padre deve recuperare l'output dal processo del runbook figlio *o* può ottenere direttamente l'output dal runbook figlio. |
| Parametri |I valori per i parametri di runbook figlio vengono specificati separatamente e possono utilizzare qualsiasi tipo di dati. |I valori per i parametri di runbook figlio devono essere combinati in una singola tabella di hash e possono includere solo tipi di dati semplici, matrice e oggetto che sfruttano la serializzazione JSON. |
| Account di automazione |Il runbook padre può utilizzare solo runbook figlio nello stesso account di automazione. |Il runbook padre può usare runbook figlio di qualsiasi account di automazione della stessa sottoscrizione di Azure e anche di una sottoscrizione diversa a cui si ha una connessione. |
| Pubblicazione |Il runbook figlio deve essere pubblicato prima della pubblicazione del runbook padre. |Il runbook figlio deve essere pubblicato prima che il runbook padre venga avviato. |

## <a name="next-steps"></a>Passaggi successivi

* [Avvio di un runbook in Automazione di Azure](automation-starting-a-runbook.md)
* [Output di runbook e messaggi in automazione di Azure](automation-runbook-output-and-messages.md)
