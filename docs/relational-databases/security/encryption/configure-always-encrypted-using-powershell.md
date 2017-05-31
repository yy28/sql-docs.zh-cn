---
title: "使用 PowerShell 配置 Always Encrypted | Microsoft Docs"
ms.custom: 
ms.date: 09/29/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- dbe-security
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 12f2bde5-e100-41fa-b474-2d2332fc7650
caps.latest.revision: 15
author: stevestein
ms.author: sstein
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: 7e3971933bb32cc47f761d18ba8c0dd57b139636
ms.contentlocale: zh-cn
ms.lasthandoff: 04/11/2017

---
# <a name="configure-always-encrypted-using-powershell"></a>使用 PowerShell 配置 Always Encrypted
[!INCLUDE[tsql-appliesto-ss2016-asdb-xxxx-xxx_md](../../../includes/tsql-appliesto-ss2016-asdb-xxxx-xxx-md.md)]

SqlServer PowerShell 模块提供用于在 Azure SQL 数据库和 SQL Server 2016 中配置 [Always Encrypted](../../../relational-databases/security/encryption/always-encrypted-database-engine.md) 的 cmdlet。

SqlServer 模块中用于 Always Encrypted 的大部分 cmdlet 均适用于加密列中存储的 Always Encrypted 密钥或敏感数据，因此，必须在安全的计算机上运行这些 cmdlet。 管理 Always Encrypted 时，请不要在托管 SQL Server 实例的计算机上执行 cmdlet，而是在另一台计算机上执行。 

由于 Always Encrypted 的主要目的是确保加密的敏感数据的安全（即使数据库系统遭到入侵），因此执行用于处理 SQL Server 计算机上密钥或敏感数据的 PowerShell 脚本可减少或抵消该功能带来的益处。 有关其他安全相关的建议，请参阅 [Security Considerations for Key Management](../../../relational-databases/security/encryption/overview-of-key-management-for-always-encrypted.md#SecurityForKeyManagement)（密钥管理的安全注意事项）。

单个 cmdlet 文章的链接位于 [此页底部](#aecmdletreference)。

## <a name="prerequisites"></a>先决条件

在一台安全计算机（并非托管 SQL Server 实例的计算机）上安装 [SqlServer module](https://msdn.microsoft.com/library/mt740629.aspx) （SqlServer 模块）。 

通过安装 [SQL Server Management Studio](https://msdn.microsoft.com/library/mt238290.aspx)的最新版本来安装 SqlServer 模块。
请注意， *SqlServer* 模块不同于 *sqlps* 模块，后者不支持 Always Encrypted。 有关详细信息，请参阅团队的 [SQL PowerShell - July 2016 Update](https://blogs.technet.microsoft.com/dataplatforminsider/2016/06/30/sql-powershell-july-2016-update) （SQL PowerShell - 2016 年 7 月更新）博客文章。

## <a name="importsqlservermodule"></a> 导入 SqlServer 模块 

加载 SqlServer 模块：

1.    使用 **Set-ExecutionPolicy** cmdlet 设置相应的脚本执行策略。
2.    使用 **Import-Module** cmdlet 导入 SqlServer 模块。

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

通过 SQL Server PowerShell，你可以使用与你通常用于导航文件系统路径的命令相似的 Windows PowerShell 别名来导航路径。 导航到目标实例和数据库后，后续 cmdlet 将会面向该数据库，如下面的示例所示：

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

|CMDLET    |说明
|:---|:---
|**[Add-SqlAzureAuthenticationContext](https://msdn.microsoft.com/library/mt759815.aspx)**    |执行 Azure 身份验证，获取身份验证令牌。
|**[Add-SqlColumnEncryptionKeyValue](https://msdn.microsoft.com/library/mt759817.aspx)**    |为数据库中的现有列加密密钥对象添加新的加密值。
|**[Complete-SqlColumnMasterKeyRotation](https://msdn.microsoft.com/library/mt759791.aspx)**    |完成列主密钥的轮换
|**[Get-SqlColumnEncryptionKey](https://msdn.microsoft.com/library/mt759814.aspx)**    |返回数据库中定义的所有列加密密钥对象，或返回一个具有指定名称的列加密密钥对象。
|**[Get-SqlColumnMasterKey](https://msdn.microsoft.com/library/mt759782.aspx)**    |返回数据库中定义的列主密钥对象，或返回一个具有指定名称的列主密钥对象。
|**[Invoke-SqlColumnMasterKeyRotation](https://msdn.microsoft.com/library/mt759810.aspx)**    |启动列主密钥的轮换。
|**[New-SqlAzureKeyVaultColumnMasterKeySettings](https://msdn.microsoft.com/library/mt759795.aspx)**    |创建一个 SqlColumnMasterKeySettings 对象，该对象描述存储在 Azure 密钥保管库中的非对称密钥。
|**[New-SqlCngColumnMasterKeySettings](https://msdn.microsoft.com/library/mt759818.aspx)**    |创建一个 SqlColumnMasterKeySettings 对象，该对象描述存储在支持下一代加密技术 (CNG) API 的密钥存储中的非对称密钥。
|**[New-SqlColumnEncryptionKey](https://msdn.microsoft.com/library/mt759808.aspx)**    |在数据库中创建新的列加密密钥对象。
|**[New-SqlColumnEncryptionKeyEncryptedValue](https://msdn.microsoft.com/library/mt759794.aspx)**    |生成列加密密钥的加密值。
|**[New-SqlColumnEncryptionSettings](https://msdn.microsoft.com/library/mt759825.aspx)**    |创建一个新的 SqlColumnEncryptionSettings 对象，该对象封装有关单个列的加密的信息（包括 CEK 和加密类型）。
|**[New-SqlColumnMasterKey](https://msdn.microsoft.com/library/mt759813.aspx)**    |在数据库中创建新的列主密钥对象。
|**New-SqlColumnMasterKeySettings**|使用指定的提供程序和密钥路径为列主密钥创建 SqlColumnMasterKeySettings 对象。
|**[New-SqlCspColumnMasterKeySettings](https://msdn.microsoft.com/library/mt759784.aspx)**    |创建一个 SqlColumnMasterKeySettings 对象，该对象描述存储在带有加密服务提供程序 (CSP)（支持加密 API (CAPI)）的密钥存储中的非对称密钥。
|**[Remove-SqlColumnEncryptionKey](https://msdn.microsoft.com/library/mt759786.aspx)**    |从数据库删除列加密密钥对象。
|**[Remove-SqlColumnEncryptionKeyValue](https://msdn.microsoft.com/library/mt759783.aspx)**    |从数据库的现有列加密对象中删除加密值。
|**[Remove-SqlColumnMasterKey](https://msdn.microsoft.com/library/mt759800.aspx)**    |从数据库删除列主密钥对象。
|**[Set-SqlColumnEncryption](https://msdn.microsoft.com/library/mt759790.aspx)**    |加密、解密或重新加密数据库中的指定列。



## <a name="additional-resources"></a>其他资源

- [始终加密（数据库引擎）](../../../relational-databases/security/encryption/always-encrypted-database-engine.md)
- [Always Encrypted 密钥管理概述](../../../relational-databases/security/encryption/overview-of-key-management-for-always-encrypted.md)
- [对用于 SQL Server 的 .NET Framework 数据提供程序使用 Always Encrypted](../../../relational-databases/security/encryption/always-encrypted-client-development.md)
- [使用 SQL Server Management Studio 配置 Always Encrypted](../../../relational-databases/security/encryption/configure-always-encrypted-using-sql-server-management-studio.md)



