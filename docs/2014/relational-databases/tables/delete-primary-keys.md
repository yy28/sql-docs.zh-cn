---
title: 删除主键 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- removing primary keys
- deleting primary keys
- primary keys [SQL Server], deleting
ms.assetid: c472e465-7bdd-4d74-8fc9-e47fca007ccb
caps.latest.revision: 15
author: craigg-msft
ms.author: craigg
manager: jhubbard
ms.openlocfilehash: b24b29caa92d8bfc3242ccf58de0a9e56fda8b96
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/19/2018
ms.locfileid: "36125581"
---
# <a name="delete-primary-keys"></a>删除主键
  您可以通过使用 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 或 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 在 [!INCLUDE[tsql](../../includes/tsql-md.md)]中删除主键。 在删除主键时，也将删除相应的索引。  
  
 **本主题内容**  
  
-   **开始之前：**  
  
     [Security](#Security)  
  
-   **使用以下工具删除主键：**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="BeforeYouBegin"></a> 开始之前  
  
###  <a name="Security"></a> 安全性  
  
####  <a name="Permissions"></a> Permissions  
 需要对表的 ALTER 权限。  
  
##  <a name="SSMSProcedure"></a> 使用 SQL Server Management Studio  
  
#### <a name="to-delete-a-primary-key-constraint-using-object-explorer"></a>使用对象资源管理器删除主键约束  
  
1.  在对象资源管理器中，展开包含主键的表，再展开 **“键”**。  
  
2.  右键单击该键，然后选择“删除”。  
  
3.  在 **“删除对象”** 对话框中，确认指定了正确的键，然后单击 **“确定”**。  
  
#### <a name="to-delete-a-primary-key-constraint-using-table-designer"></a>使用表设计器删除主键约束  
  
1.  在对象资源管理器中，右键单击具有主键的表，再单击“设计”。  
  
2.  在表网格中右键单击包含主键的行，再选择“删除主键”以将该设置从启用切换到禁用。  
  
    > [!NOTE]  
    >  若要撤消此操作，请关闭该表而不保存更改。 若要撤消删除主键操作，就无法避免丢失对表做出的所有其他更改。  
  
3.  在“文件”菜单上，单击“保存table name”。  
  
##  <a name="TsqlProcedure"></a> 使用 Transact-SQL  
  
#### <a name="to-delete-a-primary-key-constraint"></a>删除主键约束  
  
1.  在 **“对象资源管理器”** 中，连接到 [!INCLUDE[ssDE](../../includes/ssde-md.md)]的实例。  
  
2.  在标准菜单栏上，单击 **“新建查询”**。  
  
3.  将以下示例复制并粘贴到查询窗口中，然后单击“执行” 。 该示例首先标识主键约束的名称，然后删除该约束。  
  
    ```  
    USE AdventureWorks2012;  
    GO  
    -- Return the name of primary key.  
    SELECT name  
    FROM sys.key_constraints  
    WHERE type = 'PK' AND OBJECT_NAME(parent_object_id) = N'TransactionHistoryArchive';  
    GO  
    -- Delete the primary key constraint.  
    ALTER TABLE Production.TransactionHistoryArchive  
    DROP CONSTRAINT PK_TransactionHistoryArchive_TransactionID;   
    GO  
    ```  
  
 有关详细信息，请参阅 [ALTER TABLE (Transact SQL) ](/sql/t-sql/statements/alter-table-transact-sql) 和 [sys.key_constraints (Transact SQL)](/sql/relational-databases/system-catalog-views/sys-key-constraints-transact-sql)  
  
###  <a name="TsqlExample"></a>  
