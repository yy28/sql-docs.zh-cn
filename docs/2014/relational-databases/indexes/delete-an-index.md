---
title: 删除索引 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- dbe-indexes
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- removing indexes
- deleting indexes
- dropping indexes
- indexes [SQL Server], dropping
- index deletions [SQL Server]
ms.assetid: fd38a0ed-26c4-4c76-9ef7-e0a16147329d
caps.latest.revision: 29
author: craigg-msft
ms.author: craigg
manager: jhubbard
ms.openlocfilehash: 5bad892d6d808b056fccc067cedb34c06a7a3969
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/19/2018
ms.locfileid: "36027474"
---
# <a name="delete-an-index"></a>删除索引
  本主题将说明如何使用 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 或 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 在 [!INCLUDE[tsql](../../includes/tsql-md.md)]中删除索引。  
  
 **本主题内容**  
  
-   **开始之前：**  
  
     [限制和局限](#Restrictions)  
  
     [Security](#Security)  
  
-   **若要删除索引，请使用：**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="BeforeYouBegin"></a> 开始之前  
  
###  <a name="Restrictions"></a> 限制和局限  
 不能使用此方法删除作为 PRIMARY KEY 或 UNIQUE 约束的结果而创建的索引。 而必须删除该约束。 若要删除该约束和相应的索引，请在 [中使用带有 DROP CONSTRAINT 子句的](/sql/t-sql/statements/alter-table-transact-sql) ALTER TABLE [!INCLUDE[tsql](../../includes/tsql-md.md)]。 有关详细信息，请参阅 [Delete Primary Keys](../tables/delete-primary-keys.md)。  
  
###  <a name="Security"></a> 安全性  
  
####  <a name="Permissions"></a> Permissions  
 要求对表或视图具有 ALTER 权限。 默认情况下，将向 **sysadmin** 固定服务器角色以及 **db_ddladmin** 和 **db_owner** 固定数据库角色授予此权限。  
  
##  <a name="SSMSProcedure"></a> 使用 SQL Server Management Studio  
  
#### <a name="to-delete-an-index-by-using-object-explorer"></a>通过使用对象资源管理器删除索引  
  
1.  在“对象资源管理器”中，展开包含您要删除索引的表的数据库。  
  
2.  展开 **“表”** 文件夹。  
  
3.  展开包含您要删除的索引的表。  
  
4.  展开 **“索引”** 文件夹。  
  
5.  右键单击要删除的索引，然后选择“删除”。  
  
6.  在 **“删除对象”** 对话框中，确认正确的索引位于 **“要重删除的对象”** 网格中，然后单击 **“确定”**。  
  
#### <a name="to-delete-an-index-using-table-designer"></a>使用表设计器删除索引  
  
1.  在“对象资源管理器”中，展开包含您要删除索引的表的数据库。  
  
2.  展开 **“表”** 文件夹。  
  
3.  右键单击包含您要删除的索引的表，然后单击“设计”。  
  
4.  在“表设计器”菜单上，单击“索引/键”。  
  
5.  在“索引/键”对话框中，选择要删除的索引。  
  
6.  单击 **“删除”**。  
  
7.  单击 **“关闭”**。  
  
8.  在“文件”菜单上，选择“保存table_name”。  
  
##  <a name="TsqlProcedure"></a> 使用 Transact-SQL  
  
#### <a name="to-delete-an-index"></a>删除索引  
  
1.  在 **“对象资源管理器”** 中，连接到 [!INCLUDE[ssDE](../../includes/ssde-md.md)]实例。  
  
2.  在标准菜单栏上，单击 **“新建查询”**。  
  
3.  将以下示例复制并粘贴到查询窗口中，然后单击“执行” 。  
  
    ```  
    USE AdventureWorks2012;  
    GO  
    -- delete the IX_ProductVendor_BusinessEntityID index  
    -- from the Purchasing.ProductVendor table  
    DROP INDEX IX_ProductVendor_BusinessEntityID   
        ON Purchasing.ProductVendor;  
    GO  
    ```  
  
 有关详细信息，请参阅 [DROP INDEX (Transact-SQL)](/sql/t-sql/statements/drop-index-transact-sql)  
  
  
