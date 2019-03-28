---
title: 查看或更改数据库的属性 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
helpviewer_keywords:
- displaying databases
- database viewing [SQL Server]
- databases [SQL Server], viewing
- viewing databases
ms.assetid: 9e8ac097-84b7-46c7-85e3-c1e79f94d747
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 10ad92286011f6f81fbaff5ab4908007e16bdd45
ms.sourcegitcommit: c44014af4d3f821e5d7923c69e8b9fb27aeb1afd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/27/2019
ms.locfileid: "58528459"
---
# <a name="view-or-change-the-properties-of-a-database"></a>查看或更改数据库的属性
  本主题说明如何使用 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 或 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 在 [!INCLUDE[tsql](../../includes/tsql-md.md)]中查看或更改数据库的属性。 更改数据库属性后，修改内容将立即生效。  
  
 **本主题内容**  
  
-   **开始之前：**  
  
     [建议](#Recommendations)  
  
     [安全性](#Security)  
  
-   **查看或更改数据库的属性，使用：**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="BeforeYouBegin"></a> 开始之前  
  
###  <a name="Recommendations"></a> 建议  
  
-   当 AUTO_CLOSE 为 ON 时，由于该数据库不可用于检索数据，因此 [sys.databases](/sql/relational-databases/system-catalog-views/sys-databases-transact-sql) 目录视图中的某些列和 DATABASEPROPERTYEX 函数将返回 NULL。 若要解决此问题，请执行 USE 语句打开数据库。  
  
###  <a name="Security"></a> 安全性  
  
####  <a name="Permissions"></a> Permissions  
 需要对数据库拥有 ALTER 权限。  
  
##  <a name="SSMSProcedure"></a> 使用 SQL Server Management Studio  
  
#### <a name="to-view-or-change-the-properties-of-a-database"></a>查看或更改数据库的属性  
  
1.  在 **对象资源管理器**中，连接到 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]的实例，然后展开该实例。  
  
2.  展开“数据库”，右键单击要查看的数据库，再单击“属性”。  
  
3.  在 **“数据库属性”** 对话框中，选择一个页以查看相应的信息。 例如，选择 **“文件”** 页可以查看数据和日志文件信息。  
  
##  <a name="TsqlProcedure"></a> 使用 Transact-SQL  
  
#### <a name="to-view-a-property-of-a-database-by-using-databasepropertyex"></a>使用 DATABASEPROPERTYEX 查看数据库的属性  
  
1.  连接到 [!INCLUDE[ssDE](../../includes/ssde-md.md)]。  
  
2.  在标准菜单栏上，单击 **“新建查询”**。  
  
3.  将以下示例复制并粘贴到查询窗口中，然后单击“执行” 。 此示例使用 [DATABASEPROPERTYEX](/sql/t-sql/functions/databasepropertyex-transact-sql) 系统函数返回 [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] 数据库中 AUTO_SHRINK 数据库选项的状态。 返回值 1 表示将该选项设置为 ON，返回值 0 表示将该选项设置为 OFF。  
  
```sql  
USE AdventureWorks2012;  
GO  
SELECT DATABASEPROPERTYEX('AdventureWorks2012', 'IsAutoShrink');  
GO  
  
```  
  
#### <a name="to-view-the-properties-of-a-database-by-querying-sysdatabases"></a>通过查询 sys.databases 查看数据库的属性  
  
1.  连接到[!INCLUDE[ssDE](../../includes/ssde-md.md)]。  
  
2.  在标准菜单栏上，单击 **“新建查询”**。  
  
3.  将以下示例复制并粘贴到查询窗口中，然后单击“执行” 。 此示例查询 [sys.databases](/sql/relational-databases/system-catalog-views/sys-databases-transact-sql) 目录视图来查看 [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] 数据库的几个属性。 此实例返回数据库 ID 号 (`database_id`)、数据库是只读还是读写的 (`is_read_only`)、数据库的排序规则 (`collation_name`) 和数据库兼容级别 (`compatibility_level`)。  
  
```sql  
USE AdventureWorks2012;  
GO  
SELECT database_id, is_read_only, collation_name, compatibility_level  
FROM sys.databases WHERE name = 'AdventureWorks2012';  
GO  
  
```  
  
#### <a name="to-change-the-properties-of-a-database"></a>更改数据库的属性  
  
1.  连接到 [!INCLUDE[ssDE](../../includes/ssde-md.md)]。  
  
2.  在标准菜单栏上，单击 **“新建查询”**。  
  
3.  复制以下示例并将其粘贴到查询窗口中。 此示例确定 [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] 数据库上的快照隔离状态，更改属性的状态，然后验证更改。  
  
     若要确定快照隔离的状态，请选择第一个 `SELECT` 语句，然后单击 **“执行”**。  
  
     若要更改快照隔离的状态，请选择 `ALTER DATABASE` 语句，然后单击 **“执行”**。  
  
     若要验证更改，请选择第二个 `SELECT` 语句，然后单击 **“执行”**。  
  
 [!code-sql[DatabaseDDL#AlterDatabase9](../../snippets/tsql/SQL14/tsql/databaseddl/transact-sql/alterdatabase.sql#alterdatabase9)]  
  
## <a name="see-also"></a>请参阅  
 [sys.databases (Transact-SQL)](/sql/relational-databases/system-catalog-views/sys-databases-transact-sql)   
 [ALTER DATABASE SET HADR (Transact-SQL)](/sql/t-sql/statements/alter-database-transact-sql-set-hadr)   
 [ALTER DATABASE SET 选项 (Transact-SQL)](/sql/t-sql/statements/alter-database-transact-sql-set-options)   
 [ALTER DATABASE 数据库镜像 (Transact-SQL)](/sql/t-sql/statements/alter-database-transact-sql-database-mirroring)   
 [ALTER DATABASE 兼容级别 (Transact-SQL)](/sql/t-sql/statements/alter-database-transact-sql-compatibility-level)   
 [ALTER DATABASE 文件和文件组选项 (Transact-SQL)](/sql/t-sql/statements/alter-database-transact-sql-file-and-filegroup-options)  
  
  
