---
title: "使用 INSERT 和 UPDATE 语句禁用外键约束 | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: tables
ms.reviewer: 
ms.suite: sql
ms.technology: dbe-tables
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- constraints [SQL Server], foreign keys
- foreign keys [SQL Server], disabling constraints
- disabling constraints
- UPDATE statement [SQL Server], foreign key constraints
- INSERT statement [SQL Server], foreign key constraints
ms.assetid: 029168d7-085e-4b13-9b86-5644b67c6e24
caps.latest.revision: "18"
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: On Demand
ms.openlocfilehash: a68c8f5c1d80447889e528c09a145789f932a946
ms.sourcegitcommit: 66bef6981f613b454db465e190b489031c4fb8d3
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/17/2017
---
# <a name="disable-foreign-key-constraints-with-insert-and-update-statements"></a>使用 INSERT 和 UPDATE 语句禁用外键约束
[!INCLUDE[tsql-appliesto-ss2016-all-md](../../includes/tsql-appliesto-ss2016-all-md.md)]

  在 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 中，您可以通过使用 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 或 [!INCLUDE[tsql](../../includes/tsql-md.md)]，在 INSERT 和 UPDATE 事务期间禁用外键约束。 如果您知道新数据将与现有约束冲突或者如果约束仅适用于数据库中已有的数据，则可选择此选项。  
  
 **本主题内容**  
  
-   **开始之前：**  
  
     [限制和局限](#Restrictions)  
  
     [安全性](#Security)  
  
-   **对 INSERT 和 UPDATE 语句禁用外键约束，使用：**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="BeforeYouBegin"></a> 开始之前  
  
###  <a name="Restrictions"></a> 限制和局限  
 在禁用这些约束后，在将来插入或更新列时，将不会根据约束条件进行验证。  
  
###  <a name="Security"></a> 安全性  
  
####  <a name="Permissions"></a> 权限  
 需要对表的 ALTER 权限。  
  
##  <a name="SSMSProcedure"></a> 使用 SQL Server Management Studio  
  
#### <a name="to-disable-a-foreign-key-constraint-for-insert-and-update-statements"></a>对 INSERT 和 UPDATE 语句禁用外键约束  
  
1.  在 **“对象资源管理器”**中，展开具有约束的表，再展开 **“键”** 文件夹。  
  
2.  右键单击该约束，再选择“修改”。  
  
3.  在“表设计器”下的网格中，单击“强制外键约束”，然后从下拉菜单中选择“否”。  
  
4.  单击 **“关闭”**。  
  
##  <a name="TsqlProcedure"></a> 使用 Transact-SQL  
  
#### <a name="to-disable-a-foreign-key-constraint-for-insert-and-update-statements"></a>对 INSERT 和 UPDATE 语句禁用外键约束  
  
1.  在 **“对象资源管理器”**中，连接到 [!INCLUDE[ssDE](../../includes/ssde-md.md)]的实例。  
  
2.  在标准菜单栏上，单击 **“新建查询”**。  
  
3.  将以下示例复制并粘贴到查询窗口中，然后单击 **“执行”**。  
  
    ```  
    USE AdventureWorks2012;  
    GO  
    ALTER TABLE Purchasing.PurchaseOrderHeader  
    NOCHECK CONSTRAINT FK_PurchaseOrderHeader_Employee_EmployeeID;  
    GO  
    ```  
  
 有关详细信息，请参阅 [ALTER TABLE (Transact-SQL)](../../t-sql/statements/alter-table-transact-sql.md)。  
  
###  <a name="TsqlExample"></a>  
