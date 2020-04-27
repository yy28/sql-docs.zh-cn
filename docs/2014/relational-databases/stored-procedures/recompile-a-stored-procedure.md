---
title: 重新编译存储过程 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.technology: stored-procedures
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- sp_recompile
- WITH RECOMPILE clause
- recompiling stored procedures
- stored procedures [SQL Server], recompiling
ms.assetid: b90deb27-0099-4fe7-ba60-726af78f7c18
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 43ae01b9173693370d5e422d4f26b6175101ff12
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/26/2020
ms.locfileid: "62721045"
---
# <a name="recompile-a-stored-procedure"></a>重新编译存储过程
  本主题介绍如何在 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 中使用 [!INCLUDE[tsql](../../includes/tsql-md.md)]重新编译存储过程。 有三种方法可以执行此操作`WITH RECOMPILE` ：过程定义中的选项或过程的调用时间、单个`RECOMPILE`语句的查询提示或使用`sp_recompile`系统存储过程。 本主题介绍在创建过程定义或执行现有过程时使用 WITH RECOMPILE 选项。 它还描述如何使用 sp_recompile 系统存储过程重新编译现有过程。  
  
 **本主题内容**  
  
-   **开始之前：**  
  
     [建议](#Recommendations)  
  
     [安全性](#Security)  
  
-   **若要重新编译存储过程，请使用：**  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="before-you-begin"></a><a name="BeforeYouBegin"></a> 开始之前  
  
###  <a name="recommendations"></a><a name="Recommendations"></a> 建议  
  
-   在首次编译或重新编译过程时，该过程的查询计划针对该数据库及其对象的当前状态进行优化。 如果数据库对其数据或结构进行了重要更改，则重新编译过程会进行更新并针对这些更改优化过程的查询计划。 这样可以提高过程的处理性能。  
  
-   有时必须强制执行过程重新编译，而其他时间将自动执行。 只要重新启动 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ，就会发生自动重新编译操作。 当该过程引用的基础表发生物理设计更改时，也会执行此操作。  
  
-   强制过程重新编译的另一个原因是抵消过程编译的“参数查找”行为。 当 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 执行过程时，该过程在编译时使用的任何参数值都作为生成查询计划的一部分包括在内。 如果这些值表示随后调用此过程时使用的典型值，则该过程在每次编译和执行时都会从查询计划中获益。 如果过程的参数值频繁异常，则强制执行过程的重新编译和基于其他参数值的新计划可以改善性能。  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 具有对过程执行语句级重新编译的特点。 当 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 重新编译存储过程时，只编译导致重新编译的语句，而不编译整个过程。  
  
-   如果过程的中某些查询定期使用非典型值或临时值，则可通过使用这些查询中的 RECOMPILE 查询提示来改善过程性能。 由于仅使用此查询提示的查询将进行重新编译，而不是整个过程进行重新编译，因此将模仿 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]语句级重新编译行为。 但除了使用过程的当前参数值外，RECOMPILE 查询提示还在编译该语句时使用存储过程中本地变量的值。 有关详细信息，请参阅 [查询提示 (Transact-SQL)](/sql/t-sql/queries/hints-transact-sql-query)。  
  
###  <a name="security"></a><a name="Security"></a> Security  
  
####  <a name="permissions"></a><a name="Permissions"></a> 权限  
 `WITH RECOMPILE`选  
 如果在创建过程定义时使用此选项，则要求数据库中的 CREATE PROCEDURE 权限，还必须具有对架构（在其下创建过程）的 ALTER 权限。  
  
 如果在 EXECUTE 语句中使用此选项，则需要对该过程的 EXECUTE 权限。 需要对 EXECUTE 语句本身的权限，而无需对 EXECUTE 语句中引用的过程的执行权限。 有关详细信息，请参阅 [EXECUTE (Transact-SQL)](/sql/t-sql/language-elements/execute-transact-sql)。  
  
 `RECOMPILE`查询提示  
 创建过程时使用该功能，并且此提示包含在该过程中的 [!INCLUDE[tsql](../../includes/tsql-md.md)] 语句中。 因此，它需要在数据库中有 CREATE PROCEDURE 权限，对在其中创建过程的架构有 ALTER 权限。  
  
 `sp_recompile`系统存储过程  
 需要具有对指定过程的 ALTER 权限。  
  
##  <a name="using-transact-sql"></a><a name="TsqlProcedure"></a> 使用 Transact-SQL  
  
#### <a name="to-recompile-a-stored-procedure-by-using-the-with-recompile-option"></a>使用 WITH RECOMPILE 选项重新编译存储过程  
  
1.  连接到 [!INCLUDE[ssDE](../../../includes/ssde-md.md)]。  
  
2.  在标准菜单栏上，单击 **“新建查询”** 。  
  
3.  将以下示例复制并粘贴到查询窗口中，然后单击“执行”  。 该示例将创建过程定义。  
  
```  
USE AdventureWorks2012;  
GO  
IF OBJECT_ID ( 'dbo.uspProductByVendor', 'P' ) IS NOT NULL   
    DROP PROCEDURE dbo.uspProductByVendor;  
GO  
CREATE PROCEDURE dbo.uspProductByVendor @Name varchar(30) = '%'  
WITH RECOMPILE  
AS  
    SET NOCOUNT ON;  
    SELECT v.Name AS 'Vendor name', p.Name AS 'Product name'  
    FROM Purchasing.Vendor AS v   
    JOIN Purchasing.ProductVendor AS pv   
      ON v.BusinessEntityID = pv.BusinessEntityID   
    JOIN Production.Product AS p   
      ON pv.ProductID = p.ProductID  
    WHERE v.Name LIKE @Name;  
  
```  
  
#### <a name="to-recompile-a-stored-procedure-by-using-the-with-recompile-option"></a>使用 WITH RECOMPILE 选项重新编译存储过程  
  
1.  连接到 [!INCLUDE[ssDE](../../../includes/ssde-md.md)]。  
  
2.  在标准菜单栏上，单击 **“新建查询”** 。  
  
3.  将以下示例复制并粘贴到查询窗口中，然后单击“执行”  。 该示例将创建一个简单过程，该过程将从视图中返回所有雇员（提供姓和名）、职务以及部门名称。  
  
     然后，将第二个代码示例复制并粘贴到查询窗口中，然后单击 **“执行”**。 此操作将执行该过程，并重新编译过程的查询计划。  
  
```sql  
USE AdventureWorks2012;  
GO  
EXECUTE HumanResources.uspGetAllEmployees WITH RECOMPILE;  
GO  
  
```  
  
#### <a name="to-recompile-a-stored-procedure-by-using-sp_recompile"></a>使用 sp_recompile 重新编译存储过程  
  
1.  连接到 [!INCLUDE[ssDE](../../../includes/ssde-md.md)]。  
  
2.  在标准菜单栏上，单击 **“新建查询”** 。  
  
3.  将以下示例复制并粘贴到查询窗口中，然后单击“执行”  。 该示例将创建一个简单过程，该过程将从视图中返回所有雇员（提供姓和名）、职务以及部门名称。  
  
     然后，将以下示例复制并粘贴到查询窗口中，然后单击 **“执行”**。 这将不执行过程，但将该过程标记为重新编译，以便在下次执行该过程时更新其查询计划。  
  
```sql  
USE AdventureWorks2012;  
GO  
EXEC sp_recompile N'HumanResources.uspGetAllEmployees';  
GO  
  
```  
  
## <a name="see-also"></a>另请参阅  
 [创建存储过程](../stored-procedures/create-a-stored-procedure.md)   
 [修改存储过程](../stored-procedures/modify-a-stored-procedure.md)   
 [重命名存储过程](rename-a-stored-procedure.md)   
 [查看存储过程的定义](view-the-definition-of-a-stored-procedure.md)   
 [查看存储过程的依赖关系](view-the-dependencies-of-a-stored-procedure.md)   
 [DROP PROCEDURE (Transact-SQL)](/sql/t-sql/statements/drop-procedure-transact-sql)  
  
  
