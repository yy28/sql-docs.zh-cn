---
title: "PowerShell - 轮换 TDE 保护程序 - Azure SQL | Microsoft Docs"
description: "了解如何轮换用于 Azure SQL 服务器的透明数据加密 (TDE) 保护程序。"
keywords: 
services: sql-database
documentationcenter: 
author: becczhang
manager: jhubbard
editor: 
ms.prod: 
ms.reviewer: 
ms.suite: sql
ms.prod_service: sql-database, sql-data-warehouse
ms.service: sql-database
ms.custom: 
ms.component: security
ms.workload: Inactive
ms.tgt_pltfrm: 
ms.devlang: na
ms.topic: article
ms.date: 08/07/2017
ms.author: ryzhang26
ms.openlocfilehash: 85a1d74907dc3e6b887a172247850b9bc4452b31
ms.sourcegitcommit: b603dcac7326bba387befe68544619e026e6a15e
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/21/2017
---
# <a name="rotate-the-transparent-data-encryption-tde-protector-using-powershell"></a>使用 PowerShell 轮换透明数据加密 (TDE) 保护程序 
[!INCLUDE[appliesto-xx-asdb-asdw-xxx-md](../../../includes/appliesto-xx-asdb-asdw-xxx-md.md)]

本操作指南介绍如何使用 Azure Key Vault 中的 TDE 保护程序对 Azure SQL 服务器的执行密钥轮换。 轮换 Azure SQL 服务器的 TDE 保护程序意味着切换到保护服务器上的数据库的新非对称密钥。 密钥轮换是一个联机操作，完成应只需几秒钟，因为该操作仅解密和重新加密数据库的数据加密密钥，而不是整个数据库。

本指南讨论轮换服务器上的 TDE 保护程序的两个选项。

> [!NOTE]
> 暂停的 SQL 数据仓库必须在密钥轮换前恢复。
>

> [!IMPORTANT]
> 在滚动更新后不要删除以前版本的密钥。  密钥完成滚动更新后，某些数据仍使用以前的密钥加密，例如较旧的数据库备份。 
>

## <a name="prerequisites"></a>必备条件

- 本操作指南假定已使用 Azure Key Vault 的密钥作为 Azure SQL 数据库或数据仓库的 TDE 保护程序。 请参阅[使用 BYOK 支持的透明数据加密](transparent-data-encryption-byok-azure-sql.md)。
- 必须安装和运行 Azure PowerShell 版本 3.7.0 或更高版本。 
- [建议但可选]首先在硬件安全模块 (HSM) 或本地密钥存储中创建用于 TDE 保护程序的密钥材料，并将密钥材料导入 Azure Key Vault。 若要了解详细信息，请参照[有关使用硬件安全模块 (HSM) 和 Key Vault 的说明](https://docs.microsoft.com/azure/key-vault/key-vault-get-started)。

## <a name="option-1-auto-rotation"></a>选项 1：自动轮换

在相同的密钥名称和密钥保管库下，为 Key Vault 中现有的 TDE 保护程序密钥创建新版本。 在 24 小时内使用此新版本开始 Azure SQL 服务。 

若要使用 [Add-AzureKeyVaultKey](/powershell/module/azurerm.keyvault/add-azurekeyvaultkey) cmdlet 创建新版本的 TDE 保护程序：

   ```powershell
   Add-AzureKeyVaultKey `
   -VaultName <KeyVaultName> `
   -Name <KeyVaultKeyName> `
   -Destination <HardwareOrSoftware>
   ```

## <a name="option-2-manual-rotation"></a>选项 2：手动轮换

此选项使用 [Add-AzureKeyVaultKey](/powershell/module/azurerm.keyvault/add-azurekeyvaultkey)[Add-AzureRmSqlServerKeyVaultKey](/powershell/module/azurerm.sql/add-azurermsqlserverkeyvaultkey) 和 [Set-AzureRmSqlServerTransparentDataEncryptionProtector](/powershell/module/azurerm.sql/set-azurermsqlservertransparentdataencryptionprotector) cmdlet 来添加全新的密钥，该密钥可以在新的密钥名称下，甚至在另一个密钥保管库下。 

>[!NOTE]
>密钥保管库名称和密钥名称的组合长度不能超过 94 个字符。
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
  
## <a name="other-useful-powershell-cmdlets"></a>其他有用的 PowerShell cmdlet

- 若要将 TDE 保护程序从 Microsoft 托管模式切换到 BYOK 模式，请使用 [Set-AzureRmSqlServerTransparentDataEncryptionProtector](/powershell/module/azurerm.sql/set-azurermsqlservertransparentdataencryptionprotector) cmdlet。

   ```powershell
   Set-AzureRmSqlServerTransparentDataEncryptionProtector `
   -Type AzureKeyVault `
   -KeyId <KeyVaultKeyId> `
   -ServerName <LogicalServerName> `
   -ResourceGroup <SQLDatabaseResourceGroupName>
   ```

- 若要将 TDE 保护程序从 BYOK 模式切换到 Microsoft 托管模式，请使用 [Set-AzureRmSqlServerTransparentDataEncryptionProtector](/powershell/module/azurerm.sql/set-azurermsqlservertransparentdataencryptionprotector) cmdlet。

   ```powershell
   Set-AzureRmSqlServerTransparentDataEncryptionProtector `
   -Type ServiceManaged `
   -ServerName <LogicalServerName> `
   -ResourceGroup <SQLDatabaseResourceGroupName> 
   ``` 

## <a name="next-steps"></a>后续步骤

- 如果存在安全风险，了解如何删除可能已泄露的 TDE 保护程序：[删除可能已泄露的密钥](transparent-data-encryption-byok-azure-sql-remove-tde-protector.md) 

- 开始使用 TDE 的自带密钥支持：[通过 PowerShell 使用 Key Vault 的自有密钥启用 TDE](transparent-data-encryption-byok-azure-sql-configure.md)
