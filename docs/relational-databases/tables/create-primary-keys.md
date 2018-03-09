---
title: "创建主键 | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: tables
ms.reviewer: 
ms.suite: sql
ms.technology:
- dbe-tables
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- primary keys [SQL Server], creating
ms.assetid: 85c623ca-4656-4d70-a9db-ee4d897cd214
caps.latest.revision: 
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: Active
ms.openlocfilehash: cbd22a0b9fdd7b33ff7d4ccf9999d7142acf4fb7
ms.sourcegitcommit: 6b4aae3706247ce9b311682774b13ac067f60a79
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/18/2018
---
# <a name="create-primary-keys"></a>创建主键
[!INCLUDE[tsql-appliesto-ss2016-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-asdb-xxxx-xxx-md.md)]

 > 有关与以前版本的 SQL Server 相关的内容，请参阅 [Create Primary Keys](https://msdn.microsoft.com/en-US/library/ms189039(SQL.120).aspx)（创建主键）。

  您可以使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 或 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 在 [!INCLUDE[tsql](../../includes/tsql-md.md)]中定义主键。 创建主键会自动创建相应的唯一群集索引、聚集索引或非聚集索引（如果这样指定）。  
  
##  <a name="BeforeYouBegin"></a> 开始之前  
  
###  <a name="Restrictions"></a> 限制和局限  
  
-   一个表只能包含一个 PRIMARY KEY 约束。  
  
-   在 PRIMARY KEY 约束中定义的所有列都必须定义为 NOT NULL。 如果没有指定为 Null 性，则加入 PRIMARY KEY 约束的所有列的为 Null 性都将设置为 NOT NULL。  
  
###  <a name="Security"></a> 安全性  
  
####  <a name="Permissions"></a> Permissions  
 使用主键创建新表需要在数据库中具有 CREATE TABLE 权限，并对在其中创建表的架构具有 ALTER 权限。  
  
 在某一现有表中创建主键需要对该表具有 ALTER 权限。  
  
##  <a name="SSMSProcedure"></a> 使用 SQL Server Management Studio  
  
#### <a name="to-create-a-primary-key"></a>创建主键  
  
1.  在对象资源管理器中，右键单击要为其添加唯一约束的表，然后单击“设计”。  
  
2.  在 **“表设计器”**中，单击要定义为主键的数据库列的行选择器。 若要选择多个列，请在单击其他列的行选择器时按住 Ctrl 键。  
  
3.  右键单击该列的行选择器，然后选择“设置主键”。  
  
> [!CAUTION]  
>  若要重新定义主键，则必须首先删除与现有主键之间的任何关系，然后才能创建新主键。 此时，将显示一条消息警告您：作为该过程的一部分，将自动删除现有关系。  
  
 主键列由其行选择器中的主键符号标识。  
  
 如果主键由多个列组成，则其中一个列将允许重复值，但是主键中所有列的值的各种组合必须是唯一的。  
  
 如果定义复合键，则主键中列的顺序将与表中显示的列顺序相匹配。 不过，您可以在创建主键之后更改列的顺序。 有关详细信息，请参阅 [修改主键](../../relational-databases/tables/modify-primary-keys.md)。  
  
##  <a name="TsqlProcedure"></a> 使用 Transact-SQL  

### <a name="to-create-a-primary-key-in-an-existing-table"></a>在现有表中创建主键  
  
1.  在 **“对象资源管理器”**中，连接到 [!INCLUDE[ssDE](../../includes/ssde-md.md)]实例。  
  
2.  在标准菜单栏上，单击 **“新建查询”**。  
  
3.  将以下示例复制并粘贴到查询窗口中，然后单击“执行” 。 此示例对列 `TransactionID`创建了一个主键。  
  
    ```sql  
    USE AdventureWorks2012;  
    GO  
    ALTER TABLE Production.TransactionHistoryArchive   
    ADD CONSTRAINT PK_TransactionHistoryArchive_TransactionID PRIMARY KEY CLUSTERED (TransactionID);  
    GO  
    ```  
  
### <a name="to-create-a-primary-key-in-a-new-table"></a>在新表中创建主键  
  
1.  在 **“对象资源管理器”**中，连接到 [!INCLUDE[ssDE](../../includes/ssde-md.md)]实例。  
  
2.  在标准菜单栏上，单击 **“新建查询”**。  
  
3.  将以下示例复制并粘贴到查询窗口中，然后单击“执行” 。 此示例将创建一个表并针对 `TransactionID`列定义一个主键。  
  
    ```sql  
    USE AdventureWorks2012;  
    GO  
    CREATE TABLE Production.TransactionHistoryArchive1  
    (  
       TransactionID int IDENTITY (1,1) NOT NULL,  
       CONSTRAINT PK_TransactionHistoryArchive_TransactionID PRIMARY KEY CLUSTERED (TransactionID)  
    );  
    GO  
    ```  

### <a name="to-create-a-primary-key-with-nonclustered-index-in-a-new-table"></a>在新表中创建具有非聚集索引的主键  
  
1.  在 **“对象资源管理器”**中，连接到 [!INCLUDE[ssDE](../../includes/ssde-md.md)]实例。  
  
2.  在标准菜单栏上，单击 **“新建查询”**。  
  
3.  将以下示例复制并粘贴到查询窗口中，然后单击“执行” 。 此示例创建一个表并针对 `CustomerID`列定义一个主键，针对 `TransactionID` 定义一个群集索引。  
  
    ```sql  
    USE AdventureWorks2012;  
    GO  
    CREATE TABLE Production.TransactionHistoryArchive1  
    (  
       CustomerID uniqueidentifier DEFAULT NEWSEQUENTIALID(),
       TransactionID int IDENTITY (1,1) NOT NULL,  
       CONSTRAINT PK_TransactionHistoryArchive_TransactionID PRIMARY KEY NONCLUSTERED (uniqueidentifier)  
    );  
    GO  

    -- Now add the clustered index
    CREATE CLUSTERED INDEX CIX_TransactionID ON Production.TransactionHistoryArchive1 (TransactionID);
    GO
    ```  

## <a name="see-also"></a>另请参阅    
[ALTER TABLE (Transact-SQL)](../../t-sql/statements/alter-table-transact-sql.md)    
[CREATE TABLE (Transact-SQL)](../../t-sql/statements/create-table-transact-sql.md)     
[table_constraint &#40;Transact-SQL&#41;](../../t-sql/statements/alter-table-table-constraint-transact-sql.md)    
