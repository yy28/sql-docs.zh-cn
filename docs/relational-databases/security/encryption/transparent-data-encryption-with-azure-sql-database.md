---
title: "借助 Azure SQL 数据库实现透明数据加密 | Microsoft Docs"
ms.custom:
- SQL2016_New_Updated
- MSDN content
- MSDN - SQL DB
ms.date: 09/02/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.service: sql-database
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- TDE, SQL Database
- encryption (SQL Database), TDE
- Transparent Data Encryption, SQL Database
ms.assetid: 0bf7e8ff-1416-4923-9c4c-49341e208c62
caps.latest.revision: 21
author: BYHAM
ms.author: rickbyh
manager: jhubbard
translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 1c607015f1ead5b19d4c32c5bac62eb624b0578b
ms.lasthandoff: 04/11/2017

---
# <a name="transparent-data-encryption-with-azure-sql-database"></a>借助 Azure SQL 数据库实现透明数据加密
[!INCLUDE[tsql-appliesto-xxxxxx-asdb-asdw-xxx_md](../../../includes/tsql-appliesto-xxxxxx-asdb-asdw-xxx-md.md)]

  [!INCLUDE[ssSDSFull](../../../includes/sssdsfull-md.md)] 透明数据加密对数据库、关联的备份和事务日志文件执行实时加密和解密，而无需更改应用程序，从而帮助保护用户免受恶意活动的威胁。  
  
 TDE 使用称为数据库加密密钥的对称密钥加密整个数据库的存储。 在 [!INCLUDE[ssSDS](../../../includes/sssds-md.md)] 中，数据库加密密钥通过内置的服务器证书进行保护。 内置服务器证书对每个 [!INCLUDE[ssSDS](../../../includes/sssds-md.md)] 服务器而言是唯一的。 如果数据库是 GeoDR 关系，则将它受每个服务器上不同的密钥保护。 如果 2 个数据库连接到同一台服务器，则它们共享相同的内置证书。 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] 至少每隔 90 天自动轮换这些证书。 有关 TDE 的一般说明，请参阅 [透明数据加密 (TDE)](../../../relational-databases/security/encryption/transparent-data-encryption-tde.md)。  
  
 [!INCLUDE[ssSDSFull](../../../includes/sssdsfull-md.md)] 不支持 Azure 密钥保管库与 TDE 的集成。 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 可以使用密钥保管库的非对称密钥。 有关详细信息，请参阅 [使用 Azure Key Vault 的可扩展密钥管理 (SQL Server)](../../../relational-databases/security/encryption/extensible-key-management-using-azure-key-vault-sql-server.md)能够对密钥进行管理，其中包括加密密钥层次结构和密钥备份。  
  
##  <a name="Permissions"></a> 权限  
 若要通过 Azure 门户利用 REST API 或 PowerShell 配置 TDE，你必须作为 Azure 所有者、参与者或 SQL 安全管理员进行连接。  
  
 要使用 [!INCLUDE[tsql](../../../includes/tsql-md.md)] 配置 TDE，则需要具备以下条件：  
  
-   使用 SET 选项执行 ALTER DATABASE 语句需要有 **dbmanager** 角色成员资格。  
  
##  <a name="Preview"></a> 使用门户在数据库上启用 TDE  
  
1.  请访问 [https://portal.azure.com](https://portal.azure.com) 处的 Azure 门户并使用 Azure 管理员或参与者帐户登录。  
  
2.  在左侧的标题中，单击“浏览” ，然后单击“SQL 数据库” 。  
  
3.  选择左侧窗格中“SQL 数据库”  之后，单击用户数据库。  
  
4.  在数据库边栏选项卡中，单击“所有设置” 。  
  
5.  在“设置”  边栏选项卡中，单击“透明数据加密”  部分，打开“透明数据加密”  边栏选项卡。  
  
6.  在“数据加密”边栏选项卡中，将“数据加密”按钮切换为“开”，然后单击页面顶部的“保存”应用设置。 “加密状态”  将粗略估计透明数据加密的进度。  
  
     ![SQL 数据库 TDE 开始加密](../../../relational-databases/security/encryption/media/sqldb-tde-encrypt.png "SQL 数据库 TDE 开始加密")  
  
     此外，还可以通过使用查询工具（如 [!INCLUDE[ssSDS](../../../includes/sssds-md.md)] ）作为具有“查看数据库状态” [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)]**权限的数据库用户连接到** ，以便监视加密进度。 查询 **sys.dm_database_encryption_keys** 视图的 [encryption_state](../../../relational-databases/system-dynamic-management-views/sys-dm-database-encryption-keys-transact-sql.md) 列。  
  
##  <a name="Encrypt"></a> 通过使用 Transact-SQL 在 [!INCLUDE[ssSDS](../../../includes/sssds-md.md)] 上启用 TDE  
 下面介绍了启用 TDE 的步骤。  
  
###  <a name="TsqlProcedure"></a>  
  
1.  使用管理员或主数据库中 **dbmanager** 角色成员的登录名连接到数据库。  
  
2.  执行以下语句，对数据库进行加密。  
  
    ```  
    -- Enable encryption  
    ALTER DATABASE [AdventureWorks] SET ENCRYPTION ON;  
    GO  
    ```  
  
3.  要监视 [!INCLUDE[ssSDS](../../../includes/sssds-md.md)]上的加密进度，则具有 **VIEW DATABASE STATE** 权限的数据库用户可以查询 **sys.dm_database_encryption_keys** 视图的 [encryption_state](../../../relational-databases/system-dynamic-management-views/sys-dm-database-encryption-keys-transact-sql.md) 列。  
  
##  <a name="EncryptPS"></a> 使用 PowerShell 在 [!INCLUDE[ssSDS](../../../includes/sssds-md.md)] 上启用和禁用 TDE  
 使用 Azure PowerShell 则可运行以下命令来打开/关闭 TDE。 运行命令之前，必须将你的帐户连接到 PS 窗口中。 自定义此示例，对 `ServerName`、 `ResourceGroupName`和 `DatabaseName` 参数使用你的值。 有关 PowerShell 的其他信息，请参阅 [如何安装和配置 Azure PowerShell](http://azure.microsoft.com/documentation/articles/powershell-install-configure/)。  
  
> [!NOTE]  
>  若要继续，你应该安装和配置 Azure PowerShell 版本 1.0。 虽然你可以使用版本 0.9.8，但此版本已被弃用，并且它需要使用 `PS C:\> Switch-AzureMode -Name AzureResourceManager` 命令切换到 AzureResourceManager cmdlet。  
  
###  <a name="PSlProcedure"></a>  
  
1.  若要启用 TDE，请恢复 TDE 状态，并查看加密活动：  
  
    ```  
    PS C:\> Set-AzureRMSqlDatabaseTransparentDataEncryption -ServerName "myserver" -ResourceGroupName "Default-SQL-WestUS" -DatabaseName "database1" -State "Enabled"  
  
    PS C:\> Get-AzureRMSqlDatabaseTransparentDataEncryption -ServerName "myserver" -ResourceGroupName "Default-SQL-WestUS" -DatabaseName "database1"  
  
    PS C:\> Get-AzureRMSqlDatabaseTransparentDataEncryptionActivity -ServerName "myserver" -ResourceGroupName "Default-SQL-WestUS" -DatabaseName "database1"  
    ```  
  
     如果你使用的是版本 0.9.8，请使用 Set-AzureSqlDatabaseTransparentDataEncryption、Get-AzureSqlDatabaseTransparentDataEncryption 和 Get-AzureSqlDatabaseTransparentDataEncryptionActivity 命令。  
  
2.  要禁用 TDE：  
  
    ```  
    PS C:\> Set-AzureRMSqlDatabaseTransparentDataEncryption -ServerName "myserver" -ResourceGroupName "Default-SQL-WestUS" -DatabaseName "database1" -State "Disabled"  
  
    ```  
  
     如果你使用的是版本 0.9.8，请使用 Set-AzureSqlDatabaseTransparentDataEncryption 命令。  
  
##  <a name="Decrypt"></a> 在 [!INCLUDE[ssSDS](../../../includes/sssds-md.md)]  
  
#### <a name="to-disable-tde-by-using-the-azure-portal"></a>要通过使用 Azure 门户中禁用 TDE  
  
1.  请访问 [https://portal.azure.com](https://portal.azure.com) 处的 Azure 门户并使用 Azure 管理员或参与者帐户登录。  
  
2.  在左侧的标题中，单击“浏览” ，然后单击“SQL 数据库” 。  
  
3.  选择左侧窗格中“SQL 数据库”  之后，单击用户数据库。  
  
4.  在数据库边栏选项卡中，单击“所有设置” 。  
  
5.  在“设置”  边栏选项卡中，单击“透明数据加密”  部分，打开“透明数据加密”  边栏选项卡。  
  
6.  在“透明数据加密”边栏选项卡中，将“数据加密”按钮切换为“关”，然后单击页面顶部的“保存”应用设置。 “加密状态”  将粗略估计透明数据解密的进度。  
  
     此外，还可以通过使用查询工具（如 [!INCLUDE[ssSDS](../../../includes/sssds-md.md)] ）作为具有“查看数据库状态” [!INCLUDE[ssManStudio](../../../includes/ssmanstudio-md.md)]**权限的数据库用户连接到** ，以便监视解密进度。 查询 [sys.dm_database_encryption_keys](../../../relational-databases/system-dynamic-management-views/sys-dm-database-encryption-keys-transact-sql.md) 视图的 **encryption_state** 列。  
  
#### <a name="to-disable-tde-by-using-transact-sql"></a>通过使用 Transact-SQL 禁用 TDE  
  
1.  使用管理员或主数据库中 **dbmanager** 角色成员的登录名连接到数据库。  
  
2.  执行以下语句以解密该数据库。  
  
    ```  
    -- Enable encryption  
    ALTER DATABASE [AdventureWorks] SET ENCRYPTION OFF;  
    GO  
    ```  
  
3.  要监视 [!INCLUDE[ssSDS](../../../includes/sssds-md.md)]上的加密进度，则具有 **VIEW DATABASE STATE** 权限的数据库用户可以查询 **sys.dm_database_encryption_keys** 视图的 [encryption_state](../../../relational-databases/system-dynamic-management-views/sys-dm-database-encryption-keys-transact-sql.md) 列。  
  
##  <a name="Working"></a> 在 [!INCLUDE[ssSDS](../../../includes/sssds-md.md)]  
 不需要为 Azure 中的操作解密数据库。 源数据库或主数据库上 TDE 的设置均以透明方式继承在目标系统上。 这包括涉及以下内容的操作：  
  
-   地域恢复  
  
-   自服务时点还原  
  
-   还原已删除数据库  
  
-   活动地域复制  
  
-   创建数据库副本  
  
 使用 [!INCLUDE[ssSDSFull](../../../includes/sssdsfull-md.md)] 门户或 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 导入和导出向导中的导出数据库功能导出 TDE 保护的数据库时，数据库的导出内容不加密。 此导出的内容存储在未加密的 .bacpac 文件中。 完成新数据库的导入后，请务必适当保护 .Bacpac 文件并启用 TDE。 
 
 例如，如果从本地 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]中导出 .bacpac 文件，则不会自动加密新数据库的导入的内容。 同样，如果从 [!INCLUDE[ssSDSFull](../../../includes/sssdsfull-md.md)] 将 .bacpac 文件导出到本地 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]，也不会自动加密新数据库。  
 
 一个例外情况是在 [!INCLUDE[ssSDSFull](../../../includes/sssdsfull-md.md)] 中导入和导出 – 新数据库启用 TDE，但 .bacpac 文件本身仍未加密。
  
## <a name="related-sql-server-topic"></a>相关的 SQL Server 主题  
 [使用 EKM 在 SQL Server 上启用 TDE](../../../relational-databases/security/encryption/enable-tde-on-sql-server-using-ekm.md)  
  
## <a name="see-also"></a>另请参阅  
 [透明数据加密 (TDE)](../../../relational-databases/security/encryption/transparent-data-encryption-tde.md)   
 [CREATE CREDENTIAL &#40;Transact-SQL&#41;](../../../t-sql/statements/create-credential-transact-sql.md)   
 [CREATE ASYMMETRIC KEY &#40;Transact-SQL&#41;](../../../t-sql/statements/create-asymmetric-key-transact-sql.md)   
 [ALTER DATABASE (Transact-SQL)](../../../t-sql/statements/alter-database-transact-sql.md)  
  
  

