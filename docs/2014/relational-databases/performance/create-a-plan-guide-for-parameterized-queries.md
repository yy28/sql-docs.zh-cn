---
title: 为参数化查询创建计划指南 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: performance
ms.topic: conceptual
helpviewer_keywords:
- parameterized queries, plan guides for
- plan guides [SQL Server], parameterized queries
ms.assetid: b532ae16-66e7-4641-9bc8-b0d805853477
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 58202b7246acf2a958523cfb874b8ce25bd13bdc
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/08/2020
ms.locfileid: "63150966"
---
# <a name="create-a-plan-guide-for-parameterized-queries"></a>为参数化查询创建计划指南
  TEMPLATE 计划指南与参数化为指定形式的独立查询匹配。  
  
 以下示例创建一个计划指南，它与被参数化为指定格式的任何查询匹配，并使 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 强制执行查询参数化。 下列两个查询在语法上是等价的，差别只是它们的常量文字值。  
  
```  
SELECT * FROM AdventureWorks2012.Sales.SalesOrderHeader AS h  
INNER JOIN AdventureWorks2012.Sales.SalesOrderDetail AS d   
    ON h.SalesOrderID = d.SalesOrderID  
WHERE h.SalesOrderID = 45639;  
  
SELECT * FROM AdventureWorks2012.Sales.SalesOrderHeader AS h  
INNER JOIN AdventureWorks2012.Sales.SalesOrderDetail AS d   
    ON h.SalesOrderID = d.SalesOrderID  
WHERE h.SalesOrderID = 45640;  
```  
  
 下面是参数化格式的查询的计划指南：  
  
```  
EXEC sp_create_plan_guide   
    @name = N'TemplateGuide1',  
    @stmt = N'SELECT * FROM AdventureWorks2012.Sales.SalesOrderHeader AS h  
              INNER JOIN AdventureWorks2012.Sales.SalesOrderDetail AS d   
                  ON h.SalesOrderID = d.SalesOrderID  
              WHERE h.SalesOrderID = @0',  
    @type = N'TEMPLATE',  
    @module_or_batch = NULL,  
    @params = N'@0 int',  
    @hints = N'OPTION(PARAMETERIZATION FORCED)';  
```  
  
 在上一个示例中， `@stmt` 参数的值是参数化格式的查询。 获取此值以在 sp_create_plan_guide 中使用的唯一可靠方法是使用 [sp_get_query_template](/sql/relational-databases/system-stored-procedures/sp-get-query-template-transact-sql) 系统存储过程。 以下脚本既可用来获得参数化查询，又可用来为它创建计划指南。  
  
```  
DECLARE @stmt nvarchar(max);  
DECLARE @params nvarchar(max);  
EXEC sp_get_query_template   
    N'SELECT * FROM AdventureWorks2012.Sales.SalesOrderHeader AS h  
      INNER JOIN AdventureWorks2012.Sales.SalesOrderDetail AS d   
          ON h.SalesOrderID = d.SalesOrderID  
      WHERE h.SalesOrderID = 45639;',  
    @stmt OUTPUT,   
    @params OUTPUT  
EXEC sp_create_plan_guide N'TemplateGuide1',   
    @stmt,   
    N'TEMPLATE',   
    NULL,   
    @params,   
    N'OPTION(PARAMETERIZATION FORCED)';  
```  
  
> [!IMPORTANT]  
>  传递到 `@stmt` 的 `sp_get_query_template` 参数中的常量文字值可能会影响为替换该文字的参数选择的数据类型。 这将影响计划指南的匹配。 可能必须创建多个计划指南，以处理不同的参数值范围。  
  
 还可以将 TEMPLATE 计划指南与 SQL 计划指南一起使用。 例如，可以创建 TEMPLATE 计划指南以确保参数化查询类。 然后，可以对该参数化形式的查询创建 SQL 计划指南。  
  
  
