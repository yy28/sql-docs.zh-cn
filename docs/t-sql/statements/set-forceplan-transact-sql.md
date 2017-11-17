---
title: "集 FORCEPLAN (Transact SQL) |Microsoft 文档"
ms.custom: 
ms.date: 07/26/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: t-sql|statements
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- SET_FORCEPLAN_TSQL
- SET FORCEPLAN
- FORCEPLAN
- FORCEPLAN_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- joins [SQL Server], overriding query optimizer process
- FORCEPLAN option
- SET FORCEPLAN statement
- query optimizer [SQL Server], optimizing process
- overriding query optimizer process
ms.assetid: b6c0b08f-2060-4696-9e12-50cb7e674321
caps.latest.revision: 40
author: edmacauley
ms.author: edmaca
manager: cguyer
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: df0bb88faa940a54f3b3eb14c34998b1982879c6
ms.contentlocale: zh-cn
ms.lasthandoff: 09/01/2017

---
# <a name="set-forceplan-transact-sql"></a>SET FORCEPLAN (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  当 FORCEPLAN 设置为 ON 时，[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 查询优化器处理联接的顺序与表在查询的 FROM 子句中出现的顺序相同。 此外，在将 FORCEPLAN 设置为 ON 的情况下，如果不需要其他类型的联接来构造查询计划，或者使用联接提示或查询提示请求了其他联接类型，则会强制使用嵌套循环联接。  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
  
SET FORCEPLAN { ON | OFF }  
```  
  
## <a name="remarks"></a>注释  
 SET FORCEPLAN 从本质上覆盖了查询优化器处理 [!INCLUDE[tsql](../../includes/tsql-md.md)] SELECT 语句所使用的逻辑。 SELECT 语句返回的数据同样与该设置无关。 唯一的差别是 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 为满足查询对表进行处理的方式。  
  
 在查询中也可以使用查询优化器提示影响 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 处理 SELECT 语句的方式。  
  
 SET FORCEPLAN 在执行或运行时应用，而不是在分析时应用。  
  
## <a name="permissions"></a>Permissions  
 SET FORCEPLAN 权限默认授予所有用户。  
  
## <a name="examples"></a>示例  
 以下示例执行四个表的联接。 由于启用了 `SHOWPLAN_TEXT` 设置，因此 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 返回有关在启用 `SET FORCE_PLAN` 设置后如何以不同的方式处理查询的信息。  
  
```  
USE AdventureWorks2012;  
GO  
-- Make sure FORCEPLAN is set to OFF.  
SET SHOWPLAN_TEXT OFF;  
GO  
SET FORCEPLAN OFF;  
GO  
SET SHOWPLAN_TEXT ON;  
GO  
-- Example where the query plan is not forced.  
SELECT p.LastName, p.FirstName, v.Name  
FROM Person.Person AS p  
   INNER JOIN HumanResources.Employee AS e  
   ON e.BusinessEntityID = p.BusinessEntityID  
   INNER JOIN Purchasing.PurchaseOrderHeader AS poh  
   ON e.BusinessEntityID = poh.EmployeeID  
   INNER JOIN Purchasing.Vendor AS v  
   ON poh.VendorID = v.BusinessEntityID;  
GO  
-- SET FORCEPLAN to ON.  
SET SHOWPLAN_TEXT OFF;  
GO  
SET FORCEPLAN ON;  
GO  
SET SHOWPLAN_TEXT ON;  
GO  
-- Reexecute inner join to see the effect of SET FORCEPLAN ON.  
SELECT p.LastName, p.FirstName, v.Name  
FROM Person.Person AS p  
   INNER JOIN HumanResources.Employee AS e   
   ON e.BusinessEntityID = p.BusinessEntityID  
   INNER JOIN Purchasing.PurchaseOrderHeader AS poh  
   ON e.BusinessEntityID = poh.EmployeeID  
   INNER JOIN Purchasing.Vendor AS v  
   ON poh.VendorID = v.BusinessEntityID;  
GO  
SET SHOWPLAN_TEXT OFF;  
GO  
SET FORCEPLAN OFF;  
GO  
```  
  
## <a name="see-also"></a>另请参阅  
 [SELECT (Transact-SQL)](../../t-sql/queries/select-transact-sql.md)   
 [SET 语句 (Transact-SQL)](../../t-sql/statements/set-statements-transact-sql.md)   
 [设置 SHOWPLAN_ALL &#40;Transact SQL &#41;](../../t-sql/statements/set-showplan-all-transact-sql.md)   
 [设置 SHOWPLAN_TEXT &#40;Transact SQL &#41;](../../t-sql/statements/set-showplan-text-transact-sql.md)  
  
  

