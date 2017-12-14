---
title: "执行用户定义函数 | Microsoft Docs"
ms.custom: 
ms.date: 10/24/2016
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: udf
ms.reviewer: 
ms.suite: sql
ms.technology: dbe-udf
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- invoking user-defined functions
- user-defined functions [SQL Server], executing
ms.assetid: 0de7744d-9b73-463f-ae80-e31a020004b5
caps.latest.revision: "35"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: On Demand
ms.openlocfilehash: 637dbc59f1aaad1bf6fbbf5c11c8a92a504ef847
ms.sourcegitcommit: 66bef6981f613b454db465e190b489031c4fb8d3
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/17/2017
---
# <a name="execute-user-defined-functions"></a>执行用户定义函数
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]使用 Transact-SQL 执行用户定义函数。
  

> **注意：** 有关用户定义函数的详细信息，请访问  [用户定义函数](user-defined-functions.md) 和 [CREATE FUNCTION (Transact-SQL)](../../t-sql/statements/create-function-transact-sql.md) 。 
  
 
##  <a name="BeforeYouBegin"></a> 开始之前  
  
###  <a name="Restrictions"></a> 限制和局限  
 在 Transact-SQL 中，可通过使用 *value* 或使用 @*parameter_name*=*value*来提供参数。 来提供参数。参数不是事务的一部分；因此，如果在以后回退的事务中更改了参数，则此参数的值不会恢复为以前的值。 返回给调用方的值总是模块返回时的值。  
  
###  <a name="Security"></a> 安全性  
  
 运行 [EXECUTE](../../t-sql/language-elements/execute-transact-sql.md) 语句无需权限。 但是，EXECUTE 字符串内引用的安全对象上 **需要** 权限。 例如，如果字符串包含 [INSERT](../../t-sql/statements/insert-transact-sql.md) 语句，则 EXECUTE 语句的调用方必须具有对目标表的 INSERT 权限。 在遇到 EXECUTE 语句时，即使 EXECUTE 语句包含于模块内，也将检查权限。 有关详细信息，请参阅 [EXECUTE (Transact-SQL)](../../t-sql/language-elements/execute-transact-sql.md)  
  
##  <a name="TsqlProcedure"></a> 使用 Transact-SQL  
  
### <a name="example"></a>示例 
  
此示例中所使用的 `ufnGetSalesOrderStatusText` 标量值函数在大多数 `AdventureWorks`版本中都适用。  该函数的目的是为来自给定整数的销售状态返回文本值。  通过将整数 1 至 7 传递到 **\@状态** 参数来更改示例。
  
~~~tsql
USE [AdventureWorks2016CTP3]
GO  

-- Declare a variable to return the results of the function. 
DECLARE @ret nvarchar(15);   

-- Execute the function while passing a value to the @status parameter
EXEC @ret = dbo.ufnGetSalesOrderStatusText 
    @Status = 5; 

-- View the returned value.  The Execute and Select statements must be executed at the same time.  
SELECT N'Order Status: ' + @ret; 

-- Result:
-- Order Status: Shipped
~~~
  
  
  
