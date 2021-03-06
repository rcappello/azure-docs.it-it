---
title: PowerShell - Ruotare la protezione TDE - Database SQL di Azure| Microsoft Docs
description: Informazioni su come ruotare la protezione di Transparent Data Encryption (TDE) per un server SQL di Azure.
services: sql-database
ms.service: sql-database
ms.subservice: security
ms.custom: ''
ms.devlang: ''
ms.topic: conceptual
author: aliceku
ms.author: aliceku
ms.reviewer: vanto
manager: jhubbard
ms.date: 08/07/2017
ms.openlocfilehash: fc8660b6fa6d9778a4eac9ce939181aa24d5097d
ms.sourcegitcommit: 3a02e0e8759ab3835d7c58479a05d7907a719d9c
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 10/13/2018
ms.locfileid: "49309639"
---
# <a name="rotate-the-transparent-data-encryption-tde-protector-using-powershell"></a>Ruotare la protezione Transparent Data Encryption (TDE) tramite PowerShell 

Questo articolo descrive la rotazione delle chiavi per un server SQL di Azure usando una protezione TDE di Azure Key Vault. Ruotare una protezione TDE di un server SQL di Azure significa passare a una nuova chiave asimmetrica che protegge i database nel server. La rotazione delle chiavi è un'operazione online e richiede solo pochi secondi, perché si limita a decrittografare e crittografare nuovamente la chiave di crittografia dei dati del database, ma non l'intero database.

In questa guida vengono illustrate due opzioni per ruotare la protezione TDE nel server.

> [!NOTE]
> È necessario riprendere un SQL Data Warehouse in pausa prima delle rotazioni delle chiavi.
>

> [!IMPORTANT]
> **Non eliminare** le versioni precedenti della chiave dopo l'effetto di rotazione.  Quando le chiavi vengono ruotate, alcuni dati vengono comunque crittografati con le chiavi precedenti, ad esempio, i backup meno recenti del database. 
>

## <a name="prerequisites"></a>Prerequisiti

- Questa guida pratica presuppone che una chiave di Azure Key Vault sia già in uso come protezione TDE per un database SQL di Azure o un data warehouse. Vedere [Transparent Data Encryption con supporto BYOK](transparent-data-encryption-byok-azure-sql.md).
- È necessario che sia installato e sia esecuzione Azure PowerShell 3.7.0 o una versione più recente. 
- [Consigliata ma facoltativa] Creare innanzitutto il materiale della chiave per la protezione TDE in un modulo di protezione hardware (HSM) o in un archivio chiavi locale e importare il materiale della chiave in Azure Key Vault. Seguire le [Istruzioni per l'uso di un modulo di protezione hardware (HSM) e di Key Vault](https://docs.microsoft.com/azure/key-vault/key-vault-get-started) per altre informazioni.

## <a name="option-1-auto-rotation"></a>Opzione 1: rotazione automatica

Generare una nuova versione della chiave di protezione TDE esistente in Key Vault, con lo stesso nome della chiave e insieme di credenziali delle chiavi. Il servizio SQL di Azure si avvia usando questa nuova versione entro 24 ore. 

Per creare una nuova versione della protezione TDE usare il cmdlet [Add-AzureKeyVaultKey](/powershell/module/azurerm.keyvault/add-azurekeyvaultkey):

   ```powershell
   Add-AzureKeyVaultKey `
   -VaultName <KeyVaultName> `
   -Name <KeyVaultKeyName> `
   -Destination <HardwareOrSoftware>
   ```

## <a name="option-2-manual-rotation"></a>Opzione 2: rotazione manuale

L'opzione usa i cmdlet [Add-AzureKeyVaultKey](/powershell/module/azurerm.keyvault/add-azurekeyvaultkey), [Add-AzureRmSqlServerKeyVaultKey](/powershell/module/azurerm.sql/add-azurermsqlserverkeyvaultkey) e [Set-AzureRmSqlServerTransparentDataEncryptionProtector](/powershell/module/azurerm.sql/set-azurermsqlservertransparentdataencryptionprotector) per aggiungere una chiave completamente nuova, che può avere un nuovo nome della chiave o un altro insieme di credenziali delle chiavi. 

>[!NOTE]
>La lunghezza combinata per il nome dell'insieme di credenziali delle chiavi non può superare 94 caratteri.
>

   ```powershell
   # Add a new key to Key Vault
   Add-AzureKeyVaultKey `
   -VaultName <KeyVaultName> `
   -Name <KeyVaultKeyName> `
   -Destination <HardwareOrSoftware>

   # Add the new key from Key Vault to the server
   Add-AzureRmSqlServerKeyVaultKey `
   -KeyId <KeyVaultKeyId> `
   -ServerName <LogicalServerName> `
   -ResourceGroup <SQLDatabaseResourceGroupName>   
  
   <# Set the key as the TDE protector for all resources 
   under the server #>
   Set-AzureRmSqlServerTransparentDataEncryptionProtector `
   -Type AzureKeyVault `
   -KeyId <KeyVaultKeyId> `
   -ServerName <LogicalServerName> `
   -ResourceGroup <SQLDatabaseResourceGroupName>
   ```
  
## <a name="other-useful-powershell-cmdlets"></a>Altri cmdlet PowerShell utili

- Per passare la protezione TDE dalla modalità gestita da Microsoft a BYOK, usare il cmdlet [Set-AzureRmSqlServerTransparentDataEncryptionProtector](/powershell/module/azurerm.sql/set-azurermsqlservertransparentdataencryptionprotector).

   ```powershell
   Set-AzureRmSqlServerTransparentDataEncryptionProtector `
   -Type AzureKeyVault `
   -KeyId <KeyVaultKeyId> `
   -ServerName <LogicalServerName> `
   -ResourceGroup <SQLDatabaseResourceGroupName>
   ```

- Per il passaggio della protezione TDE dalla modalità gestita da Microsoft a BYOK, usare il cmdlet [Set-AzureRmSqlServerTransparentDataEncryptionProtector](/powershell/module/azurerm.sql/set-azurermsqlservertransparentdataencryptionprotector).

   ```powershell
   Set-AzureRmSqlServerTransparentDataEncryptionProtector `
   -Type ServiceManaged `
   -ServerName <LogicalServerName> `
   -ResourceGroup <SQLDatabaseResourceGroupName> 
   ``` 

## <a name="next-steps"></a>Passaggi successivi

- In caso di rischio per la sicurezza, consultare [Rimuovere una chiave potenzialmente compromessa](transparent-data-encryption-byok-azure-sql-remove-tde-protector.md) per informazioni su come rimuovere una protezione TDE potenzialmente compromessa 

- Introduzione al supporto Bring Your Own Key per TDE: [Abilitare TDE tramite la propria chiave da Key Vault usando PowerShell](transparent-data-encryption-byok-azure-sql-configure.md)
