---
title: "PowerShell - 删除 TDE 保护程序 - Azure SQL | Microsoft Docs"
description: "通过使用自带密钥 (BYOK) 支持的 TDE 应对 Azure SQL 数据库和数据仓库中可能已泄露的 TDE 保护程序操作指南。"
keywords: 
services: sql-database
documentationcenter: 
author: becczhang
manager: craigg
editor: 
ms.assetid: 
ms.service: sql-database
ms.custom: security
ms.workload: Inactive
ms.tgt_pltfrm: 
ms.devlang: na
ms.topic: article
ms.date: 08/07/2017
ms.author: rebeccaz
ms.translationtype: HT
ms.sourcegitcommit: 46b16dcf147dbd863eec0330e87511b4ced6c4ce
ms.openlocfilehash: 861a24ef2f0bc26adece27b2612d4bf2d4640a63
ms.contentlocale: zh-cn
ms.lasthandoff: 09/05/2017

---
# <a name="remove-a-transparent-data-encryption-tde-protector-using-powershell"></a>使用 PowerShell 删除透明数据加密 (TDE) 保护程序
[!INCLUDE[appliesto-xx-asdb-xxxx-xxx-md](../../../includes/appliesto-xx-asdb-xxxx-xxx-md.md)]

## <a name="prerequisites"></a>先决条件
- 必须具有 Azure 订阅，并且是该订阅的管理员
- 必须安装和运行 Azure PowerShell 版本 4.2.0 或更高版本。 
- 本操作指南假定已使用 Azure Key Vault 的密钥作为 Azure SQL 数据库或数据仓库的 TDE 保护程序。 要了解详细信息，请参阅[使用 BYOK 支持的透明数据加密](transparent-data-encryption-byok-azure-sql.md)。

## <a name="overview"></a>概述
本操作指南描述了如果使用自带密钥 (BYOK) 支持进行 TDE 的 Azure SQL 数据库和数据仓库可能已经泄露 TDE 保护程序，应该如何应对。 若要了解有关用于 TDE 的 BYOK 支持的详细信息，请参阅[概述页](transparent-data-encryption-byok-azure-sql.md)。 

以下过程应该只有在极端情况或测试环境下才能完成。 请仔细查看操作指南，因为从 Azure Key Vault 中删除经常使用的 TDE 保护程序可能会导致数据丢失。 

如果怀疑密钥已泄露，导致服务或用户可未经授权访问密钥，最好删除该密钥。

请记住，如果删除了 Key Vault 中的 TDE 保护程序，服务器下的所有加密数据库的连接都会受到阻止，这些数据库会脱机并在 24 小时内删除。 使用已泄露密钥加密的旧备份无法再访问。

本操作指南根据事件响应后的期望结果采用两种方法：
- 若要保持 Azure SQL 数据库/数据仓库可访问
- 若要使 Azure SQL 数据库/数据仓库不可访问

## <a name="to-keep-the-encrypted-resources-accessible"></a>若要保持加密的资源可访问
1. 在 Key Vault 中创建[新密钥](https://docs.microsoft.com/powershell/module/azurerm.keyvault/add-azurekeyvaultkey?view=azurermps-4.1.0)。 请确保在不含可能已泄露的 TDE 保护程序的单独的密钥保管库中创建此新密钥，因为访问控制设置在保管库级别。 
2. 使用 [Add-AzureRmSqlServerKeyVaultKey](/powershell/module/azurerm.sql/add-azurermsqlserverkeyvaultkey) 和 [Set-AzureRmSqlServerTransparentDataEncryptionProtector](/powershell/module/azurerm.sql/set-azurermsqlservertransparentdataencryptionprotector) cmdlet 将新密钥添加到服务器，并将它作为服务器的新的 TDE 保护程序更新。

   ```powershell
   # Add the key from Key Vault to the server  
   Add-AzureRmSqlServerKeyVaultKey `
   -ResourceGroupName <SQLDatabaseResourceGroupName> `
   -ServerName <LogicalServerName> `
   -KeyId <KeyVaultKeyId>
   
   # Set the key as the TDE protector for all resources under the server
   Set-AzureRmSqlServerTransparentDataEncryptionProtector `
   -ResourceGroupName <SQLDatabaseResourceGroupName> `
   -ServerName <LogicalServerName> `
   -Type AzureKeyVault -KeyId <KeyVaultKeyId> 
   ```

3. 请确保使用 [Get-AzureRmSqlServerTransparentDataEncryptionProtector](/powershell/module/azurerm.sql/get-azurermsqlservertransparentdataencryptionprotector) cmdlet 将服务器和任何副本更新到新的 TDE 保护程序。 

   >[!NOTE]
   > 新的 TDE 保护程序可能需要几分钟时间来传播到服务器下的所有数据库和辅助数据库。
   >

   ```powershell
   Get-AzureRmSqlServerTransparentDataEncryptionProtector `
   -ServerName <LogicalServerName> `
   -ResourceGroupName <SQLDatabaseResourceGroupName>
   ```

4. 在 Key Vault 中[备份新密钥](/powershell/module/azurerm.keyvault/backup-azurekeyvaultkey)。

   ```powershell
   <# -OutputFile parameter is optional; 
   if removed, a file name is automatically generated. #>
   Backup-AzureKeyVaultKey `
   -VaultName <KeyVaultName> `
   -Name <KeyVaultKeyName> `
   -OutputFile <DesiredBackupFilePath>
   ```
 
5. 使用 [Remove-AzureKeyVaultKey](/powershell/module/azurerm.keyvault/remove-azurekeyvaultkey) cmdlet 删除 Key Vault 中已泄露的密钥。 

   ```powershell
   Remove-AzureKeyVaultKey `
   -VaultName <KeyVaultName> `
   -Name <KeyVaultKeyName>
   ```
 
6. 若要使用 [Restore-AzureKeyVaultKey](/powershell/module/azurerm.keyvault/restore-azurekeyvaultkey) cmdlet 将密钥存储到 Key Vault：
   ```powershell
   Restore-AzureKeyVaultKey `
   -VaultName <KeyVaultName> `
   -InputFile <BackupFilePath>
   ```
 
## <a name="to-make-the-encrypted-resources-inaccessible"></a>若要使加密的资源不可访问
1. 删除正在由可能已泄露的密钥加密的数据库。
数据库和日志文件会自动备份，因此（只要提供密钥）可以随时完成数据库的时点还原。 在删除活动的 TDE 保护程序之前必须删除数据库，可防止大部分最近事务最多 10 分钟的数据丢失。 
2. 备份 Key Vault 中 TDE 保护程序的密钥材料。
3. 从 Key Vault 中删除可能已泄漏的密钥

## <a name="next-steps"></a>后续步骤

- 了解如何轮换服务器的 TDE 保护程序以符合安全要求：[使用 PowerShell 轮换透明数据加密保护程序](transparent-data-encryption-byok-azure-sql-key-rotation.md)

- 开始使用 TDE 的自带密钥支持：[通过 PowerShell 使用 Key Vault 的自有密钥启用 TDE](transparent-data-encryption-byok-azure-sql-configure.md)

