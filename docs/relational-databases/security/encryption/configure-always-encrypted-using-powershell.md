---
title: "使用 PowerShell 配置 Always Encrypted | Microsoft Docs"
ms.custom: 
ms.date: 05/17/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: security
ms.reviewer: 
ms.suite: sql
ms.technology: dbe-security
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 12f2bde5-e100-41fa-b474-2d2332fc7650
caps.latest.revision: "15"
author: stevestein
ms.author: sstein
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: ac3904e6dff2383dac9bbaa09621095b9b2ec11f
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/17/2017
---
# <a name="configure-always-encrypted-using-powershell"></a>使用 PowerShell 配置 Always Encrypted
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]

SqlServer PowerShell 模块提供用于在 Azure SQL 数据库和 SQL Server 2016 中配置 [Always Encrypted](../../../relational-databases/security/encryption/always-encrypted-database-engine.md) 的 cmdlet。

SqlServer 模块中的 Always Encrypted cmdlet 适用于密钥或敏感数据，因此，必须在安全的计算机上运行这些 cmdlet。 管理 Always Encrypted 时，请不要在托管 SQL Server 实例的计算机上执行 cmdlet，而是在另一台计算机上执行。

由于 Always Encrypted 的主要目的是确保加密敏感数据的安全（即使数据库系统遭到入侵），因此在 SQL Server 计算机上执行处理密钥或敏感数据的 PowerShell 脚本可减少或抵消该功能带来的益处。 有关其他安全相关的建议，请参阅 [Security Considerations for Key Management](../../../relational-databases/security/encryption/overview-of-key-management-for-always-encrypted.md#SecurityForKeyManagement)（密钥管理的安全注意事项）。

单个 cmdlet 文章的链接位于 [此页底部](#aecmdletreference)。

## <a name="prerequisites"></a>先决条件

在一台安全计算机（并非托管 SQL Server 实例的计算机）上安装 [SqlServer module](https://docs.microsoft.com/powershell/sqlserver/sqlserver/vlatest/sqlserver) （SqlServer 模块）。 可通过 PowerShell 库直接安装该模块。  请参阅[下载说明](../../../ssms/download-sql-server-ps-module.md)了解详细信息。


## <a name="importsqlservermodule"></a> 导入 SqlServer 模块 

加载 SqlServer 模块：

1.  使用 **Set-ExecutionPolicy** cmdlet 设置相应的脚本执行策略。
2.  使用 **Import-Module** cmdlet 导入 SqlServer 模块。

此示例将加载 SqlServer 模块。

```
# Import the SQL Server Module.  
Import-Module "SqlServer" 
```

## <a name="connectingtodatabase"></a> 连接到数据库

一些 Always Encrypted cmdlet 适用于数据库中的数据或元数据，并要求你首先应连接到数据库。 使用 SqlServer 模块配置 Always Encrypted 时，建议使用两种方法来连接到数据库： 
1. 使用 SQL Server PowerShell 连接。
2. 使用 SQL Server 管理对象 (SMO) 连接。

### <a name="using-sql-server-powershell"></a>使用 SQL Server PowerShell

此方法仅适用于 SQL Server（Azure SQL 数据库中不支持此方法）。

通过 SQL Server PowerShell，你可以使用与你通常用于导航文件系统路径的命令相似的 Windows PowerShell 别名来导航路径。 导航到目标实例和数据库后，后续 cmdlet 将以该数据库为目标，如下面的示例所示：

```
# Import the SqlServer module.
Import-Module "SqlServer"
# Navigate to the database in the remote instance.
cd SQLSERVER:\SQL\servercomputer\DEFAULT\Databases\yourdatabase
# List column master keys in the above database.
Get-SqlColumnMasterKey
```

 
或者，你可使用泛型 **Path** 参数来指定数据库路径，而不是导航到该数据库。


```
# Import the SqlServer module.
Import-Module "SqlServer" 
# List column master keys for the specified database.
Get-SqlColumnMasterKey -Path SQLSERVER:\SQL\servercomputer\DEFAULT\Databases\yourdatabase
```
 
### <a name="using-smo"></a>使用 SMO

此方法同时适用于 Azure SQL 数据库和 SQL Server。
使用 SMO，你可创建 [Database 类](https://msdn.microsoft.com/library/microsoft.sqlserver.management.smo.database.aspx)的一个对象，然后使用用于连接到该数据库的 cmdlet 的 **InputObject** 参数传递此对象。


```
# Import the SqlServer module
Import-Module "SqlServer"  

# Connect to your database (Azure SQL database).
$serverName = "<Azure SQL server name>.database.windows.net"
$databaseName = "<database name>"
$connStr = "Server = " + $serverName + "; Database = " + $databaseName + "; Authentication = Active Directory Integrated"
$connection = New-Object Microsoft.SqlServer.Management.Common.ServerConnection
$connection.ConnectionString = $connStr
$connection.Connect()
$server = New-Object Microsoft.SqlServer.Management.Smo.Server($connection)
$database = $server.Databases[$databaseName] 

# List column master keys for the specified database.
Get-SqlColumnMasterKey -InputObject $database
```


或者，你可使用管道传送：


```
$database | Get-SqlColumnMasterKey
```

## <a name="always-encrypted-tasks-using-powershell"></a>使用 PowerShell 的 Always Encrypted 任务

- [使用 PowerShell 配置 Always Encrypted 密钥](../../../relational-databases/security/encryption/configure-always-encrypted-keys-using-powershell.md) 
- [使用 PowerShell 轮换 Always Encrypted 密钥](../../../relational-databases/security/encryption/rotate-always-encrypted-keys-using-powershell.md)
- [使用 PowerShell 配置列加密](../../../relational-databases/security/encryption/configure-column-encryption-using-powershell.md)


##  <a name="aecmdletreference"></a> Always Encrypted Cmdlet 参考

以下 PowerShell cmdlet 可供 Always Encrypted 使用：

|CMDLET |说明
|:---|:---
|**[Add-SqlAzureAuthenticationContext](https://docs.microsoft.com/powershell/sqlserver/sqlserver/vlatest/add-sqlazureauthenticationcontext)**   |执行 Azure 身份验证，获取身份验证令牌。
|**[Add-SqlColumnEncryptionKeyValue](https://docs.microsoft.com/powershell/sqlserver/sqlserver/vlatest/add-sqlcolumnencryptionkeyvalue)**   |为数据库中的现有列加密密钥对象添加新的加密值。
|**[Complete-SqlColumnMasterKeyRotation](https://docs.microsoft.com/powershell/sqlserver/sqlserver/vlatest/complete-sqlcolumnmasterkeyrotation)**   |完成列主密钥的轮换
|**[Get-SqlColumnEncryptionKey](https://docs.microsoft.com/powershell/sqlserver/sqlserver/vlatest/get-sqlcolumnencryptionkey)** |返回数据库中定义的所有列加密密钥对象，或返回一个具有指定名称的列加密密钥对象。
|**[Get-SqlColumnMasterKey](https://docs.microsoft.com/powershell/sqlserver/sqlserver/vlatest/get-sqlcolumnmasterkey)** |返回数据库中定义的列主密钥对象，或返回一个具有指定名称的列主密钥对象。
|**[Invoke-SqlColumnMasterKeyRotation](https://docs.microsoft.com/powershell/sqlserver/sqlserver/vlatest/invoke-sqlcolumnmasterkeyrotation)**   |启动列主密钥的轮换。
|**[New-SqlAzureKeyVaultColumnMasterKeySettings](https://docs.microsoft.com/powershell/sqlserver/sqlserver/vlatest/new-sqlazurekeyvaultcolumnmasterkeysettings)**   |创建一个 SqlColumnMasterKeySettings 对象，该对象描述存储在 Azure 密钥保管库中的非对称密钥。
|**[New-SqlCngColumnMasterKeySettings](https://docs.microsoft.com/powershell/sqlserver/sqlserver/vlatest/new-sqlcngcolumnmasterkeysettings)**   |创建一个 SqlColumnMasterKeySettings 对象，该对象描述存储在支持下一代加密技术 (CNG) API 的密钥存储中的非对称密钥。
|**[New-SqlColumnEncryptionKey](https://docs.microsoft.com/powershell/sqlserver/sqlserver/vlatest/new-sqlcolumnencryptionkey)** |在数据库中创建列加密密钥对象。
|**[New-SqlColumnEncryptionKeyEncryptedValue](https://docs.microsoft.com/powershell/sqlserver/sqlserver/vlatest/new-sqlcolumnencryptionkeyencryptedvalue)** |生成列加密密钥的加密值。
|**[New-SqlColumnEncryptionSettings](https://docs.microsoft.com/powershell/sqlserver/sqlserver/vlatest/new-sqlcolumnencryptionsettings)**   |创建一个 SqlColumnEncryptionSettings 对象，该对象封装有关单个列的加密的信息（包括 CEK 和加密类型）。
|**[New-SqlColumnMasterKey](https://docs.microsoft.com/powershell/sqlserver/sqlserver/vlatest/new-sqlcolumnmasterkey)** |在数据库中创建列主密钥对象。
|**[New-SqlColumnMasterKeySettings](https://docs.microsoft.com/powershell/sqlserver/sqlserver/vlatest/new-sqlcolumnmasterkeysettings)**|使用指定的提供程序和密钥路径为列主密钥创建 SqlColumnMasterKeySettings 对象。
|**[New-SqlCspColumnMasterKeySettings](https://docs.microsoft.com/powershell/sqlserver/sqlserver/vlatest/new-sqlcspcolumnmasterkeysettings)**   |创建一个 SqlColumnMasterKeySettings 对象，该对象描述存储在带有加密服务提供程序 (CSP)（支持加密 API (CAPI)）的密钥存储中的非对称密钥。
|**[Remove-SqlColumnEncryptionKey](https://docs.microsoft.com/powershell/sqlserver/sqlserver/vlatest/remove-sqlcolumnencryptionkey)**   |从数据库删除列加密密钥对象。
|**[Remove-SqlColumnEncryptionKeyValue](https://docs.microsoft.com/powershell/sqlserver/sqlserver/vlatest/remove-sqlcolumnencryptionkeyvalue)** |从数据库的现有列加密对象中删除加密值。
|**[Remove-SqlColumnMasterKey](https://docs.microsoft.com/powershell/sqlserver/sqlserver/vlatest/remove-sqlcolumnmasterkey)**   |从数据库删除列主密钥对象。
|**[Set-SqlColumnEncryption](https://docs.microsoft.com/powershell/sqlserver/sqlserver/vlatest/set-sqlcolumnencryption)**   |加密、解密或重新加密数据库中的指定列。



## <a name="additional-resources"></a>其他资源

- [始终加密（数据库引擎）](../../../relational-databases/security/encryption/always-encrypted-database-engine.md)
- [Always Encrypted 密钥管理概述](../../../relational-databases/security/encryption/overview-of-key-management-for-always-encrypted.md)
- [对用于 SQL Server 的 .NET Framework 数据提供程序使用 Always Encrypted](../../../relational-databases/security/encryption/always-encrypted-client-development.md)
- [使用 SQL Server Management Studio 配置 Always Encrypted](../../../relational-databases/security/encryption/configure-always-encrypted-using-sql-server-management-studio.md)


