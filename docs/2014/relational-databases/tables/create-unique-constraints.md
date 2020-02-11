---
title: 创建唯一约束 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: table-view-index
ms.topic: conceptual
helpviewer_keywords:
- UNIQUE constraints [SQL Server], creating
- constraints [SQL Server], creating
- constraints [SQL Server], unique
ms.assetid: a86f9d6f-f242-43be-b65d-b3435b71b62a
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 77581cc6d8838e0cfed4bb7cc615f4d1f58de0d5
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/08/2020
ms.locfileid: "62761465"
---
# <a name="create-unique-constraints"></a>创建唯一约束
  您可以通过使用 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 或 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 在 [!INCLUDE[tsql](../../includes/tsql-md.md)] 中创建唯一约束，以便确保在未参与主键的特定列中不输入重复值。 创建唯一约束会自动创建相应的唯一索引。  
  
 **本主题内容**  
  
-   **开始之前：**  
  
     [安全性](#Security)  
  
-   **使用以下工具创建唯一约束：**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="BeforeYouBegin"></a> 开始之前  
  
###  <a name="Security"></a> Security  
  
####  <a name="Permissions"></a> 权限  
 需要对表的 ALTER 权限。  
  
##  <a name="SSMSProcedure"></a> 使用 SQL Server Management Studio  
  
#### <a name="to-create-a-unique-constraint"></a>创建唯一约束  
  
1.  在“对象资源管理器”  中，右键单击要为其添加唯一约束的表，再单击“设计”  。  
  
2.  在“表设计器”  菜单上，单击“索引/键”  。  
  
3.  在“索引/键”  对话框中，单击“添加”  。  
  
4.  在“常规”  下的网格中，单击“类型”  ，然后从该属性右侧的下拉列表框中选择“唯一键”  。  
  
5.  在“文件”  菜单上，单击“保存”  以保存表名  。  
  
##  <a name="TsqlProcedure"></a> 使用 Transact-SQL  
  
#### <a name="to-create-a-unique-constraint"></a>创建唯一约束  
  
1.  在 **“对象资源管理器”** 中，连接到 [!INCLUDE[ssDE](../../includes/ssde-md.md)]的实例。  
  
2.  在标准菜单栏上，单击 **“新建查询”** 。  
  
3.  将以下示例复制并粘贴到查询窗口中，然后单击“执行”  。 该示例将创建表 `TransactionHistoryArchive4` ，并且在列 `TransactionID`上创建唯一约束。  
  
    ```  
    USE AdventureWorks2012;  
    GO  
    CREATE TABLE Production.TransactionHistoryArchive4  
     (  
       TransactionID int NOT NULL,   
       CONSTRAINT AK_TransactionID UNIQUE(TransactionID)   
    );   
    GO  
  
    ```  
  
#### <a name="to-create-a-unique-constraint-on-an-existing-table"></a>在现有表中创建唯一约束  
  
1.  在 **“对象资源管理器”** 中，连接到 [!INCLUDE[ssDE](../../includes/ssde-md.md)]的实例。  
  
2.  在标准菜单栏上，单击 **“新建查询”** 。  
  
3.  将以下示例复制并粘贴到查询窗口中，然后单击“执行”  。 该示例在表 `PasswordHash` 中的 `PasswordSalt` 和 `Person.Password`列上创建唯一约束。  
  
    ```  
    USE AdventureWorks2012;   
    GO  
    ALTER TABLE Person.Password   
    ADD CONSTRAINT AK_Password UNIQUE (PasswordHash, PasswordSalt);   
    GO  
  
    ```  
  
#### <a name="to-create-a-unique-constraint-in-an-new-table"></a>在新表中创建唯一约束  
  
1.  在 **“对象资源管理器”** 中，连接到 [!INCLUDE[ssDE](../../includes/ssde-md.md)]的实例。  
  
2.  在标准菜单栏上，单击 **“新建查询”** 。  
  
3.  将以下示例复制并粘贴到查询窗口中，然后单击“执行”  。 该示例创建一个表并在 `TransactionID`列上定义唯一约束。  
  
    ```  
    USE AdventureWorks2012;  
    GO  
    CREATE TABLE Production.TransactionHistoryArchive2  
    (  
       TransactionID int NOT NULL,  
       CONSTRAINT AK_TransactionID UNIQUE(TransactionID)  
    );  
    GO  
  
    ```  
  
     有关详细信息，请参阅 [ALTER TABLE (Transact-SQL)](/sql/t-sql/statements/alter-table-transact-sql)、[CREATE TABLE (Transact-SQL)](/sql/t-sql/statements/create-table-transact-sql) 和 [table_constraint (Transact-SQL)](/sql/relational-databases/system-information-schema-views/table-constraints-transact-sql)。  
  
###  <a name="TsqlExample"></a>  
