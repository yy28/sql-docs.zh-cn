---
title: "附加数据库 | Microsoft Docs"
ms.custom: 
ms.date: 10/24/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- sql13.swb.attachdatabase.f1
helpviewer_keywords:
- database attaching [SQL Server]
- attaching databases [SQL Server]
ms.assetid: b4efb0ae-cfe6-4d81-a4b4-6e4916885caa
caps.latest.revision: 52
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 50e55a131e303a5303059a51797730f8bfab2581
ms.contentlocale: zh-cn
ms.lasthandoff: 04/11/2017

---
# <a name="attach-a-database"></a>附加数据库
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx_md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  本主题说明如何使用 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 或 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 在 [!INCLUDE[tsql](../../includes/tsql-md.md)]中附加数据库。 可以使用此功能来复制、移动或升级 SQL Server 数据库。  
  
 
  
##  <a name="Prerequisites"></a> 先决条件  
  
-   必须首先分离数据库。 尝试附加未分离的数据库将返回错误。 有关详细信息，请参阅 [分离数据库](../../relational-databases/databases/detach-a-database.md)。  
  
-   附加数据库时，所有数据文件（MDF 文件和 LDF 文件）都必须可用。 如果任何数据文件的路径不同于首次创建数据库或上次附加数据库时的路径，则必须指定文件的当前路径。  
  
-   在附加数据库时，如果 MDF 和 LDF 文件位于不同目录并且其中一条路径包含 \\\\?\GlobalRoot，该操作将失败。  
  
###  <a name="Recommendations"></a> “附加”是最佳选择吗？  
 我们建议在移动同一实例中的数据库文件时，你使用 ALTER DATABASE 计划重定位过程（而不是使用分离和附加操作）移动数据库。 有关详细信息，请参阅 [Move User Databases](../../relational-databases/databases/move-user-databases.md)。 
 
不建议对“备份和恢复”使用分离和附加。 没有事务日志备份，并且可能会意外删除文件。
  
###  <a name="Security"></a> 安全性  
 文件访问权限可在很多数据库操作过程中设置，其中包括分离或附加数据库。 有关分离或附加数据库时设置的文件权限的信息，请参阅 [联机丛书（仍为有效读物！）中的](http://technet.microsoft.com/library/ms189128.aspx) 保护数据和日志文件 [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)] 
  
 建议您不要附加或还原来自未知或不可信源的数据库。 此类数据库可能包含恶意代码，这些代码可能会执行非预期的 [!INCLUDE[tsql](../../includes/tsql-md.md)] 代码，或者通过修改架构或物理数据库结构导致错误。 使用来自未知源或不可信源的数据库前，请在非生产服务器上针对数据库运行 [DBCC CHECKDB](../../t-sql/database-console-commands/dbcc-checkdb-transact-sql.md) ，然后检查数据库中的代码，例如存储过程或其他用户定义代码。 有关附加数据库的详细信息以及在附加数据库时对元数据进行的更改的信息，请参阅 [数据库分离和附加 (SQL Server)](../../relational-databases/databases/database-detach-and-attach-sql-server.md)。  
  
####  <a name="Permissions"></a> Permissions  
 要求具有 CREATE DATABASE、CREATE ANY DATABASE 或 ALTER ANY DATABASE 权限。  
  
##  <a name="SSMSProcedure"></a> 使用 SQL Server Management Studio  
  
#### <a name="to-attach-a-database"></a>附加数据库  
  
1.  在 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 对象资源管理中，连接到 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] 的实例，然后单击以在 SSMS 中展开该实例视图。  
  
2.  右键单击“数据库”，然后单击“附加”。  
  
3.  在 **“附加数据库”** 对话框中，若要指定要附加的数据库，请单击 **“添加”**，然后在 **“定位数据库文件”** 对话框中选择数据库所在的磁盘驱动器并展开目录树，以查找并选择数据库的 .mdf 文件。例如：  
  
     `C:\Program Files\Microsoft SQL Server\MSSQL13.MSSQLSERVER\MSSQL\DATA\AdventureWorks2012_Data.mdf`  
  
    > [!IMPORTANT]  
    >  尝试选择已附加的数据库将生成错误。  
  
     **要附加的数据库**  
     显示所选数据库的有关信息。  
  
     \<无列标题>  
     显示一个图标，用以指示附加操作的状态。 下面的 **“状态”** 说明中介绍可能的图标。  
  
     **MDF 文件位置**  
     显示选定 MDF 文件的路径和文件名。  
  
     **Database Name**  
     显示数据库的名称。  
  
     **附加为**  
     根据需要，可以指定要附加数据库的其他名称。  
  
     **“所有者”**  
     提供数据库可能所有者的下拉列表，您可以根据需要从其中选择其他所有者。  
  
     **状态**  
     显示下表中相应的数据库状态。  
  
    |图标|状态文本|说明|  
    |----------|-----------------|-----------------|  
    |（无图标）|（无文本）|此对象的附加操作尚未启动或者可能挂起。 这是打开该对话框时的默认值。|  
    |绿色的右向三角形|正在进行|已启动附加操作，但是该操作未完成。|  
    |绿色的选中标记|成功|已成功附加该对象。|  
    |包含白色十字形的红色圆圈|错误|附加操作遇到错误，未成功完成。|  
    |包含左、右两个黑色象限和上、下两个白色象限的圆圈|已停止|由于用户停止了附加操作，该操作未成功完成。|  
    |包含一个指向逆时针方向的曲线箭头的圆圈|已回滚|附加操作已成功，但已对其进行回滚，因为在附加其他对象的过程中出现了错误。|  
  
     **消息**  
     显示空消息或“找不到文件”超链接。  
  
     **“添加”**  
     查找必需的主数据库文件。 当用户选择 .mdf 文件时，就会在 **“要附加的数据库”** 网格的相应字段中自动填充合适的信息。  
  
     **删除**  
     从 **“要附加的数据库”** 网格中删除选定文件。  
  
     **"** *<database_name>* **”数据库详细信息**  
     显示要附加的文件的名称。 若要验证或更改文件的路径名，请单击 **“浏览”** 按钮 (**…**)。  
  
    > [!NOTE]  
    >  如果文件不存在，则 **“消息”** 列显示“找不到”。 如果找不到日志文件，则说明它位于其他目录中或者已被删除。 您需要更新 **“数据库详细信息”** 网格中该文件的路径使其指向正确的位置，或者从网格中删除该日志文件。 如果找不到 .ndf 数据文件，则需要更新网格中该文件的路径使其指向正确的位置。  
  
     **原始文件名**  
     显示属于数据库的已附加文件的名称。  
  
     **文件类型**  
     指示文件类型，即 **“数据”** 或 **“日志”**。  
  
     **当前文件路径**  
     显示所选数据库文件的路径。 可以手动编辑该路径。  
  
     **消息**  
     显示空消息或**“找不到文件”**超链接。  
  
##  <a name="TsqlProcedure"></a> 使用 Transact-SQL  
  
#### <a name="to-attach-a-database"></a>附加数据库  
  
1.  连接到 [!INCLUDE[ssDE](../../includes/ssde-md.md)]。  
  
2.  在标准菜单栏上，单击 **“新建查询”**。  
  
3.  使用关闭 FOR ATTACH 的 [CREATE DATABASE](../../t-sql/statements/create-database-sql-server-transact-sql.md) 语句。  
  
     将以下示例复制并粘贴到查询窗口中，然后单击 **“执行”**。 此示例附加 [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)] 数据库的文件并将该数据库重命名为 `MyAdventureWorks`。  
  
    ```  
    CREATE DATABASE MyAdventureWorks   
        ON (FILENAME = 'C:\MySQLServer\AdventureWorks_Data.mdf'),   
        (FILENAME = 'C:\MySQLServer\AdventureWorks_Log.ldf')   
        FOR ATTACH;  
  
    ```  
  
    > [!NOTE]  
    >  或者，你可以使用 [sp_attach_db](../../relational-databases/system-stored-procedures/sp-attach-db-transact-sql.md) 或 [sp_attach_single_file_db](../../relational-databases/system-stored-procedures/sp-attach-single-file-db-transact-sql.md) 存储过程。 但是，Microsoft [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]的未来版本中将删除这些存储过程。 请避免在新的开发工作中使用该功能，并着手修改当前还在使用该功能的应用程序。 但我们建议你使用 CREATE DATABASE … FOR ATTACH。  
  
##  <a name="FollowUp"></a> 跟进：在升级 SQL Server 数据库之后  
 在使用附加方法升级数据库后，该数据库将立即变为可用，然后自动进行升级。 如果数据库具有全文检索，升级过程将导入、重置或重新生成它们，具体取决于**全文升级选项**服务器属性的设置。 如果将升级选项设置为“导入”或“重新生成”，在升级过程中将无法使用全文检索。 导入可能需要数小时，而重新生成所需的时间最多时可能十倍于此，具体取决于要编制索引的数据量。 另请注意，当升级选项设置为“导入”时，如果全文目录不可用，将重新生成关联的全文检索。  
  
 如果升级前用户数据库的兼容级别为 100 或更高，升级后将保持相应级别。 如果升级前兼容级别为 90，则在升级后的数据库中，兼容级别将设置为 100，该级别为 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 支持的最低兼容级别。 有关详细信息，请参阅 [ALTER DATABASE 兼容级别 (Transact-SQL)](../../t-sql/statements/alter-database-transact-sql-compatibility-level.md)。  
  
  > [!NOTE]
  > 如果从运行启用了变更数据捕获 (CDC) 的 SQL Server 2014 或更低版本的实例附加数据库，也需执行以下命令升级变更数据捕获 (CDC) 元数据。
  ```
  USE <database name>
  EXEC sys.sp_cdc_vupgrade  
  ``` 
  
## <a name="see-also"></a>另请参阅  
 [CREATE DATABASE (SQL Server Transact-SQL)](../../t-sql/statements/create-database-sql-server-transact-sql.md)   
 [分离数据库](../../relational-databases/databases/detach-a-database.md)  
  
  

