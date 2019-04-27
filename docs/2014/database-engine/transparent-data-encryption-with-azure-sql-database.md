---
title: 借助 Azure SQL 数据库实现透明数据加密 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: security
ms.topic: conceptual
helpviewer_keywords:
- TDE, SQL Database
- Transparent Data Encryption, SQL Database
- encryption (SQL Database) TDE
ms.assetid: 0bf7e8ff-1416-4923-9c4c-49341e208c62
author: CarlRabeler
ms.author: carlrab
manager: craigg
ms.openlocfilehash: 3551cf4db3ab1b84f04ba13dea414943fbb2ef44
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62773864"
---
# <a name="transparent-data-encryption-with-azure-sql-database"></a>借助 Azure SQL 数据库实现透明数据加密
  [!INCLUDE[ssSDSfull](../includes/sssdsfull-md.md)] 透明数据加密（预览）通过执行数据库的实时加密和解密、关联的备份和处于休眠状态的事务日志文件来帮助保护用户免受恶意活动的威胁，而无需更改应用程序。  
  
 TDE 使用称为数据库加密密钥的对称密钥加密整个数据库的存储。 在 [!INCLUDE[ssSDS](../includes/sssds-md.md)] 中，数据库加密密钥通过内置的服务器证书进行保护。 内置服务器证书对每个 [!INCLUDE[ssSDS](../includes/sssds-md.md)] 服务器而言是唯一的。 如果数据库是 GeoDR 关系，则将它受每个服务器上不同的密钥保护。 如果 2 个数据库连接到同一台服务器，则它们共享相同的内置证书。 [!INCLUDE[msCoName](../includes/msconame-md.md)] 至少每隔 90 天自动轮换这些证书。 有关 TDE 的一般说明，请参阅 [透明数据加密 (TDE)](../relational-databases/security/encryption/transparent-data-encryption.md)。  
  
 [!INCLUDE[ssSDSfull](../includes/sssdsfull-md.md)] 不支持 Azure 密钥保管库与 TDE 的集成。 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 可以使用密钥保管库的非对称密钥。 有关详细信息，请参阅[示例 a:通过使用密钥保管库中的非对称密钥的透明数据加密](../relational-databases/security/encryption/extensible-key-management-using-azure-key-vault-sql-server.md#ExampleA)。  
  
||  
|-|  
|**适用对象**：[!INCLUDE[sqldbesa](../includes/sqldbesa-md.md)] ([在某些区域预览](http://azure.microsoft.com/documentation/articles/sql-database-preview-whats-new/?WT.mc_id=TSQL_GetItTag))。|  
  
> [!IMPORTANT]  
>  目前这是预览功能。 我确认并同意我的数据库中的 [!INCLUDE[ssSDS](../includes/sssds-md.md)] 透明数据加密的实现遵从我的许可证协议（例如企业协议、Microsoft Azure 协议或 Microsoft 在线订阅协议）的预览版条款，以及任何适用的 [Microsoft Azure 预览版的补充使用条款](http://azure.microsoft.com/support/legal/preview-supplemental-terms/)。  
  
 即使在 [!INCLUDE[ssSDS](../includes/sssds-md.md)] 的版本系列 V12 现在宣布为处于公开发布状态的部分地理区域中，TDE 的状态预览也适用。 在 [!INCLUDE[ssSDS](../includes/sssds-md.md)] 宣布将 TDE 从预览提升为 GA 之前， [!INCLUDE[msCoName](../includes/msconame-md.md)] 的 TDE 不适用于生产数据库。 有关 [!INCLUDE[ssSDS](../includes/sssds-md.md)] V12 的详细信息，请参阅 [Azure SQL Database 中的新增功能](http://azure.microsoft.com/documentation/articles/sql-database-preview-whats-new/)。  
  
##  <a name="Permissions"></a> Permissions  
 若要通过 Azure 门户利用 REST API 或 PowerShell 注册预览并配置 TDE，则必须作为 Azure 所有者、参与者或 SQL 安全管理员连接。  
  
 要使用 [!INCLUDE[tsql](../includes/tsql-md.md)] 配置 TDE，则需要具备以下条件：  
  
-   必须已经注册 TDE 预览。  
  
-   要创建数据库加密密钥，则必须是 [!INCLUDE[ssSDS](../includes/sssds-md.md)] 管理员或主数据库中 **dbmanager** 角色的成员，并且具有数据库的 **CONTROL** 权限。  
  
-   使用 SET 选项执行 ALTER DATABASE 语句仅需要 **dbmanager** 角色的成员身份。  
  
##  <a name="Preview"></a> 在数据库上 TDE 并启用 TDE 的预览版注册  
  
1.  访问在 Azure 门户[ https://portal.azure.com ](https://portal.azure.com)和使用你的 Azure 管理员或参与者帐户登录。  
  
2.  在左侧的标题中，单击“浏览” ，然后单击“SQL 数据库” 。  
  
3.  选择左侧窗格中“SQL 数据库”  之后，单击用户数据库。  
  
4.  在数据库边栏选项卡中，单击“所有设置” 。  
  
5.  在“设置”  边栏选项卡中，单击“透明数据加密（预览）”  部分打开“透明数据加密预览”  边栏选项卡。 如果尚未注册 TDE 预览，则将在完成注册前禁用数据加密设置。  
  
6.  单击“预览条款” 。  
  
7.  阅读预览条款，如果同意条款，选择**透明数据 encryptionPreview 条款**复选框，然后依次**确定**页面底部附近。 返回到**数据 encryptionPREVIEW**边栏选项卡，其中**数据加密**现在应启用按钮。  
  
8.  在“数据加密预览”  边栏选项卡中，将“数据加密”  按钮移动为“开” ，然后单击“保存”  （在页面顶部）以应用设置。 “加密状态”  将粗略估计透明数据加密的进度。  
  
     ![SQLDB_TDE_TermsNewUI](../../2014/database-engine/media/sqldb-tde-termsnewui.png "SQLDB_TDE_TermsNewUI")  
  
     此外，还可以通过使用查询工具（如 [!INCLUDE[ssSDS](../includes/sssds-md.md)] ）作为具有“查看数据库状态” [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)]**权限的数据库用户连接到** ，以便监视加密进度。 查询`encryption_state`的列[sys.dm_database_encryption_keys](/sql/relational-databases/system-dynamic-management-views/sys-dm-database-encryption-keys-transact-sql)视图。  
  
##  <a name="Encrypt"></a> 通过使用 Transact-SQL 在 [!INCLUDE[ssSDS](../includes/sssds-md.md)] 上启用 TDE  
 以下步骤中，假定你已注册预览。  
  
###  <a name="TsqlProcedure"></a>  
  
1.  使用管理员或主数据库中 **dbmanager** 角色成员的登录名连接到数据库。  
  
2.  执行以下语句以创建数据库加密密钥并对数据库进行加密。  
  
    ```  
    -- Create the database encryption key that will be used for TDE.  
    CREATE DATABASE ENCRYPTION KEY   
    WITH ALGORITHM = AES_256   
    ENCRYPTION BY SERVER CERTIFICATE ##MS_TdeCertificate##;  
  
    -- Enable encryption  
    ALTER DATABASE [AdventureWorks] SET ENCRYPTION ON;  
    GO  
    ```  
  
3.  若要监视加密进度[!INCLUDE[ssSDS](../includes/sssds-md.md)]，数据库与用户**VIEW DATABASE STATE**权限可以查询`encryption_state`的列[sys.dm_database_encryption_keys](/sql/relational-databases/system-dynamic-management-views/sys-dm-database-encryption-keys-transact-sql)视图。  
  
## <a name="enabling-tde-on-sql-database-by-using-powershell"></a>通过使用 PowerShell 在 SQL 数据库上启用 TDE  
 使用 Azure PowerShell 则可运行以下命令来打开/关闭 TDE。 运行该命令之前，需要将帐户连接到 PS 窗口中。 以下步骤中，假定你已注册预览。 有关 PowerShell 的其他信息，请参阅 [如何安装和配置 Azure PowerShell](http://azure.microsoft.com/documentation/articles/powershell-install-configure/)。  
  
1.  要启用 TDE，则返回 TDE 状态并查看加密活动。  
  
    ```  
    PS C:\> Switch-AzureMode -Name AzureResourceManager  
  
    PS C:\> Set-AzureSqlDatabaseTransparentDataEncryption -ServerName "myserver" -ResourceGroupName "Default-SQL-WestUS" -DatabaseName "database1" -State "Enabled"  
  
    PS C:\> Get-AzureSqlDatabaseTransparentDataEncryption -ServerName "myserver" -ResourceGroupName "Default-SQL-WestUS" -DatabaseName "database1"  
  
    PS C:\> Get-AzureSqlDatabaseTransparentDataEncryptionActivity -ServerName "myserver" -ResourceGroupName "Default-SQL-WestUS" -DatabaseName "database1"  
  
    ```  
  
2.  要禁用 TDE：  
  
    ```  
    PS C:\> Set-AzureSqlDatabaseTransparentDataEncryption -ServerName "myserver" -ResourceGroupName "Default-SQL-WestUS" -DatabaseName "database1" -State "Disabled"  
  
    PS C:\> Switch-AzureMode -Name AzureServiceManagement  
    ```  
  
##  <a name="Decrypt"></a> 在 [!INCLUDE[ssSDS](../includes/sssds-md.md)]  
  
#### <a name="to-disable-tde-by-using-the-azure-portal"></a>要通过使用 Azure 门户中禁用 TDE  
  
1.  访问在 Azure 门户[ https://portal.azure.com ](https://portal.azure.com)和使用你的 Azure 管理员或参与者帐户登录。  
  
2.  在左侧的标题中，单击“浏览” ，然后单击“SQL 数据库” 。  
  
3.  选择左侧窗格中“SQL 数据库”  之后，单击用户数据库。  
  
4.  在数据库边栏选项卡中，单击“所有设置” 。  
  
5.  在“设置”  边栏选项卡中，单击“透明数据加密（预览）”  部分打开“透明数据加密预览”  边栏选项卡。  
  
6.  在“透明数据加密预览”  边栏选项卡中，将“数据加密”  按钮移动为“关” ，然后单击“保存”  （在页面顶部）以应用设置。 “加密状态”  将粗略估计透明数据解密的进度。  
  
     此外，还可以通过使用查询工具（如 [!INCLUDE[ssSDS](../includes/sssds-md.md)] ）作为具有“查看数据库状态” [!INCLUDE[ssManStudio](../includes/ssmanstudio-md.md)]**权限的数据库用户连接到** ，以便监视解密进度。 查询`encryption_state`的列[sys.dm_database_encryption_keys](/sql/relational-databases/system-dynamic-management-views/sys-dm-database-encryption-keys-transact-sql)视图。  
  
#### <a name="to-disable-tde-by-using-transact-sql"></a>通过使用 Transact-SQL 禁用 TDE  
  
1.  使用管理员或主数据库中 **dbmanager** 角色成员的登录名连接到数据库。  
  
2.  执行以下语句以解密该数据库。  
  
    ```  
    -- Enable encryption  
    ALTER DATABASE [AdventureWorks] SET ENCRYPTION OFF;  
    GO  
    ```  
  
3.  若要监视加密进度[!INCLUDE[ssSDS](../includes/sssds-md.md)]，数据库与用户**VIEW DATABASE STATE**权限可以查询`encryption_state`的列[sys.dm_database_encryption_keys](/sql/relational-databases/system-dynamic-management-views/sys-dm-database-encryption-keys-transact-sql)视图。  
  
##  <a name="Working"></a> 使用 TDE 保护的数据库上 [!INCLUDE[ssSDS](../includes/sssds-md.md)]  
 不需要为 Azure 中的操作解密数据库。 源数据库或主数据库上 TDE 的设置均以透明方式继承在目标系统上。 这包括涉及以下内容的操作：  
  
-   地域恢复  
  
-   自服务时点还原  
  
-   还原已删除数据库  
  
-   活动地域复制  
  
-   创建数据库副本  
  
##  <a name="Moving"></a> 移动 TDE 保护的数据库使用。Bacpac 文件  
 使用 [!INCLUDE[ssSDSfull](../includes/sssdsfull-md.md)] 门户或 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 导入和导出向导中的导出数据库功能导出 TDE 保护的数据库时，数据库的内容不加密。 内容存储在未加密的 .Bacpac 文件中。  完成新数据库的导入后，请务必适当保护 .Bacpac 文件并启用 TDE。  
  
## <a name="related-sql-server-topic"></a>相关的 SQL Server 主题  
 [使用 EKM 启用 TDE](../relational-databases/security/encryption/enable-tde-on-sql-server-using-ekm.md)  
  
## <a name="see-also"></a>请参阅  
 [透明数据加密 (TDE)](../relational-databases/security/encryption/transparent-data-encryption.md)   
 [CREATE CREDENTIAL &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-credential-transact-sql)   
 [CREATE ASYMMETRIC KEY &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-asymmetric-key-transact-sql)   
 [CREATE DATABASE ENCRYPTION KEY (Transact-SQL)](/sql/t-sql/statements/create-database-encryption-key-transact-sql)   
 [ALTER DATABASE (Transact-SQL)](/sql/t-sql/statements/alter-database-transact-sql)   
 [ALTER DATABASE SET 选项 (Transact-SQL)](/sql/t-sql/statements/alter-database-transact-sql-set-options)  
  
  
