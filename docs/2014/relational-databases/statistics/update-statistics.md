---
title: 更新统计信息 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: performance
ms.topic: conceptual
helpviewer_keywords:
- updating statistics
- statistics [SQL Server], updating
ms.assetid: 4b97c0b4-03ff-4cfb-9c3f-3b33290b7a2c
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 7c9a628f912f382f3ee8a87276aa34d0e54e37ba
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/15/2019
ms.locfileid: "63033627"
---
# <a name="update-statistics"></a>更新统计信息
  您可以通过使用 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 或 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 更新 [!INCLUDE[tsql](../../includes/tsql-md.md)]中表或索引视图的查询优化统计信息。 默认情况下，查询优化器已根据需要更新统计信息以改进查询计划；但在某些情况下，您可以通过使用 UPDATE STATISTICS 或存储过程 `sp_updatestats` 来比默认更新更频繁地更新统计信息，提高查询性能。  
  
 更新统计信息可确保查询使用最新的统计信息进行编译。 不过，更新统计信息会导致查询重新编译。 我们建议不要太频繁地更新统计信息，因为需要在改进查询计划和重新编译查询所用时间之间权衡性能。 具体的折衷方案取决于你的应用程序。 UPDATE STATISTICS 可以使用 tempdb 对行样本进行排序以生成统计信息。  
  
 **本主题内容**  
  
-   **开始之前：**  
  
     [安全性](#Security)  
  
-   **若要更新统计信息对象，请使用：**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="BeforeYouBegin"></a> 开始之前  
  
###  <a name="Security"></a> 安全性  
  
####  <a name="Permissions"></a> Permissions  
 如果使用 UPDATE STATISTICS 或通过 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]进行更改，则要求对表或视图具有 ALTER 权限。 如果使用 `sp_updatestats`，则要求具有 **sysadmin** 固定服务器角色的成员身份或数据库 (**dbo**) 的所有者身份。  
  
##  <a name="SSMSProcedure"></a> 使用 SQL Server Management Studio  
  
#### <a name="to-update-a-statistics-object"></a>更新统计信息对象  
  
1.  在 **“对象资源管理器”** 中，单击加号以便展开要更新统计信息的数据库。  
  
2.  单击加号以便展开 **“表”** 文件夹。  
  
3.  单击加号以便展开要更新统计信息的表。  
  
4.  单击加号以便展开 **“统计信息”** 文件夹。  
  
5.  右键单击要更新的统计信息对象，然后选择  “属性”。  
  
6.  在中**统计信息属性-** _statistics_name_对话框中，选择**更新这些列的统计信息**复选框，然后单击**确定**.  
  
##  <a name="TsqlProcedure"></a> 使用 Transact-SQL  
  
#### <a name="to-update-a-specific-statistics-object"></a>更新特定的统计信息对象  
  
1.  在 **“对象资源管理器”** 中，连接到 [!INCLUDE[ssDE](../../includes/ssde-md.md)]的实例。  
  
2.  在标准菜单栏上，单击 **“新建查询”** 。  
  
3.  将以下示例复制并粘贴到查询窗口中，然后单击 **“执行”** 。  
  
    ```  
    USE AdventureWorks2012;  
    GO  
    -- The following example updates the statistics for the AK_SalesOrderDetail_rowguid index of the SalesOrderDetail table.   
    UPDATE STATISTICS Sales.SalesOrderDetail AK_SalesOrderDetail_rowguid;   
    GO  
    ```  
  
#### <a name="to-update-all-statistics-in-a-table"></a>更新表中的所有统计信息  
  
1.  在 **“对象资源管理器”** 中，连接到 [!INCLUDE[ssDE](../../includes/ssde-md.md)]的实例。  
  
2.  在标准菜单栏上，单击 **“新建查询”** 。  
  
3.  将以下示例复制并粘贴到查询窗口中，然后单击“执行”  。  
  
    ```  
    USE AdventureWorks2012;   
    GO  
    -- The following example updates the statistics for all indexes on the SalesOrderDetail table.   
    UPDATE STATISTICS Sales.SalesOrderDetail;   
    GO  
    ```  
  
 有关详细信息，请参阅 [更新统计信息 (Transact-SQL)](/sql/t-sql/statements/update-statistics-transact-sql)。  
  
#### <a name="to-update-all-statistics-in-a-database"></a>更新数据库中的所有统计信息  
  
1.  在 **“对象资源管理器”** 中，连接到 [!INCLUDE[ssDE](../../includes/ssde-md.md)]的实例。  
  
2.  在标准菜单栏上，单击 **“新建查询”** 。  
  
3.  将以下示例复制并粘贴到查询窗口中，然后单击“执行”  。  
  
    ```  
    USE AdventureWorks2012;   
    GO  
    -- The following example updates the statistics for all tables in the database.   
    EXEC sp_updatestats;  
    ```  
  
 有关详细信息，请参阅 [sp_updatestats (Transact-SQL)](/sql/relational-databases/system-stored-procedures/sp-updatestats-transact-sql)。  
  
  
