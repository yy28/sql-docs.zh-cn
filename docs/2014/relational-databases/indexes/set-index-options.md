---
title: 设置索引选项 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: table-view-index
ms.topic: conceptual
helpviewer_keywords:
- ALLOW_ROW_LOCKS option
- SORT_IN_TEMPDB option
- DROP_EXISTING clause
- large data, indexes
- PAD_INDEX
- STATISTICS_NORECOMPUTE
- MAXDOP index option, setting
- index options [SQL Server]
- MAXDOP index option
- IGNORE_DUP_KEY option
- ALLOW_PAGE_LOCKS option
- ONLINE
ms.assetid: 7969af33-e94c-41f7-ab89-9d9a2747cd5c
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: a9feaa3be20692b89b0d0568f1ccacc49c992667
ms.sourcegitcommit: 1ab115a906117966c07d89cc2becb1bf690e8c78
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/27/2018
ms.locfileid: "52408267"
---
# <a name="set-index-options"></a>设置索引选项
  本主题说明如何使用 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 或 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 在 [!INCLUDE[tsql](../../includes/tsql-md.md)]中修改索引的属性。  
  
 **本主题内容**  
  
-   **开始之前：**  
  
     [限制和局限](#Restrictions)  
  
     [安全性](#Security)  
  
-   **修改索引的属性，使用：**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="BeforeYouBegin"></a> 开始之前  
  
###  <a name="Restrictions"></a> 限制和局限  
  
-   以下选项立即应用于索引的 ALTER INDEX 语句中使用的 SET 子句：ALLOW_PAGE_LOCKS、 ALLOW_ROW_LOCKS、 IGNORE_DUP_KEY 和 STATISTICS_NORECOMPUTE。  
  
-   通过使用 ALTER INDEX REBUILD 或 CREATE INDEX WITH DROP_EXISTING 重新生成索引时，可以设置以下选项：PAD_INDEX、 FILLFACTOR、 SORT_IN_TEMPDB、 IGNORE_DUP_KEY、 STATISTICS_NORECOMPUTE、 ONLINE、 ALLOW_ROW_LOCKS、 ALLOW_PAGE_LOCKS、 MAXDOP 和 DROP_EXISTING (仅 CREATE INDEX)。  
  
###  <a name="Security"></a> 安全性  
  
####  <a name="Permissions"></a> Permissions  
 要求对表或视图具有 ALTER 权限。  
  
##  <a name="SSMSProcedure"></a> 使用 SQL Server Management Studio  
  
#### <a name="to-modify-the-properties-of-an-index-in-table-designer"></a>在表设计器中修改索引的属性  
  
1.  在对象资源管理器中，单击加号以便展开包含您要修改索引属性的表的数据库。  
  
2.  单击加号以便展开 **“表”** 文件夹。  
  
3.  右键单击你要修改索引属性的表，然后选择“设计”。  
  
4.  在“表设计器”菜单上，单击“索引/键”。  
  
5.  选择要修改的索引。 其属性将显示在主网格中。  
  
6.  更改任意属性的设置以自定义索引。  
  
7.  单击 **“关闭”**。  
  
8.  在“文件”菜单上，选择“保存table_name”。  
  
#### <a name="to-modify-the-properties-of-an-index-in-object-explorer"></a>在对象资源管理器中修改索引的属性  
  
1.  在对象资源管理器中，单击加号以便展开包含您要修改索引属性的表的数据库。  
  
2.  单击加号以便展开 **“表”** 文件夹。  
  
3.  单击加号以展开您要修改索引属性的表。  
  
4.  单击加号以便展开 **“索引”** 文件夹。  
  
5.  右键单击要修改其属性的索引，然后选择“属性”。  
  
6.  在 **“选择页”** 下，选择 **“选项”**。  
  
7.  更改任意属性的设置以自定义索引。  
  
8.  若要添加、删除或更改索引列的位置，请从“索引属性 - index_name”对话框中选择“常规”页。 有关详细信息，请参阅 [Index Properties F1 Help](index-properties-f1-help.md)  
  
##  <a name="TsqlProcedure"></a> 使用 Transact-SQL  
  
#### <a name="to-see-the-properties-of-all-the-indexes-in-a-table"></a>查看表中所有索引的属性  
  
1.  在 **“对象资源管理器”** 中，连接到 [!INCLUDE[ssDE](../../includes/ssde-md.md)]的实例。  
  
2.  在标准菜单栏上，单击 **“新建查询”**。  
  
3.  将以下示例复制并粘贴到查询窗口中，然后单击“执行” 。  
  
    ```  
    USE AdventureWorks2012;  
    GO  
    SELECT i.name AS index_name,   
        i.type_desc,   
        i.is_unique,   
        ds.type_desc AS filegroup_or_partition_scheme,   
        ds.name AS filegroup_or_partition_scheme_name,   
        i.ignore_dup_key,   
        i.is_primary_key,   
        i.is_unique_constraint,   
        i.fill_factor,   
        i.is_padded,   
        i.is_disabled,   
        i.allow_row_locks,   
        i.allow_page_locks,   
        i.has_filter,   
        i.filter_definition  
    FROM sys.indexes AS i  
       INNER JOIN sys.data_spaces AS ds ON i.data_space_id = ds.data_space_id  
    WHERE is_hypothetical = 0 AND i.index_id <> 0   
       AND i.object_id = OBJECT_ID('HumanResources.Employee');   
    GO  
  
    ```  
  
#### <a name="to-set-the-properties-of-an-index"></a>设置索引的属性  
  
1.  在 **“对象资源管理器”** 中，连接到 [!INCLUDE[ssDE](../../includes/ssde-md.md)]的实例。  
  
2.  在标准菜单栏上，单击 **“新建查询”**。  
  
3.  将以下示例复制并粘贴到查询窗口中，然后单击 **“执行”**。  
  
     [!code-sql[IndexDDL#AlterIndex4](../../snippets/tsql/SQL14/tsql/indexddl/transact-sql/alterindex.sql#alterindex4)]  
  
     [!code-sql[IndexDDL#AlterIndex2](../../snippets/tsql/SQL14/tsql/indexddl/transact-sql/alterindex.sql#alterindex2)]  
  
 有关详细信息，请参阅 [ALTER INDEX (Transact-SQL)](/sql/t-sql/statements/alter-index-transact-sql)。  
  
  
