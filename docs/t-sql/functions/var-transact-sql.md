---
title: VAR (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/13/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.suite: sql
ms.technology: t-sql
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- VAR
- VAR_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- statistical variances
- expressions [SQL Server], statistical variance
- VAR function [Transact-SQL]
ms.assetid: 71dfc339-16c8-42f9-8555-ad45400f7f9b
caps.latest.revision: 37
author: MashaMSFT
ms.author: mathoma
manager: craigg
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 62e710806d8eed7548cdb74448fff374272dc0e9
ms.sourcegitcommit: 4183dc18999ad243c40c907ce736f0b7b7f98235
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/27/2018
ms.locfileid: "43099345"
---
# <a name="var-transact-sql"></a>VAR (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  返回指定表达式中所有值的方差。 后面可以跟随 [OVER 子句](../../t-sql/queries/select-over-clause-transact-sql.md)。  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
-- Syntax for SQL Server and Azure SQL Database  
  
VAR ( [ ALL | DISTINCT ] expression )
   [ OVER ( [ partition_by_clause ] order_by_clause ) ]
```  
  
```  
-- Syntax for Azure SQL Data Warehouse and Parallel Data Warehouse  
  
-- Aggregate Function Syntax   
VAR ( [ ALL | DISTINCT ] expression )  
  
-- Analytic Function Syntax  
VAR (expression) OVER ( [ partition_by_clause ] order_by_clause)  
```  
  
## <a name="arguments"></a>参数  
 **ALL**  
 对所有值应用该函数。 ALL 为默认值。  
  
 DISTINCT  
 指定考虑每一个唯一值。  
  
 *expression*  
 是精确或近似数值数据类型类别（bit 数据类型除外）的[表达式](../../t-sql/language-elements/expressions-transact-sql.md)。 不允许使用聚合函数和子查询。  
  
 OVER ( [ partition_by_clause ] order_by_clause)*  
 partition_by_clause 将 FROM 子句生成的结果集划分为要应用函数的分区。 如果未指定，则此函数将查询结果集的所有行视为单个组。 order_by_clause 确定执行操作的逻辑顺序。 需要 order_by_clause。 有关详细信息，请参阅 [OVER 子句 (Transact-SQL)](../../t-sql/queries/select-over-clause-transact-sql.md)。  
  
## <a name="return-types"></a>返回类型  
 **float**  
  
## <a name="remarks"></a>Remarks  
 如果 VAR 用于 SELECT 语句中的所有项目，则结果集中的每个值都包含在计算中。 VAR 只可用于数字列。 Null 值会被忽略。  
  
 VAR 不与 OVER 和 ORDER BY 子句配合使用时为确定性函数。 与 OVER 和 ORDER BY 子句一同指定时，它具有不确定性。 有关详细信息，请参阅 [Deterministic and Nondeterministic Functions](../../relational-databases/user-defined-functions/deterministic-and-nondeterministic-functions.md)。  
  
## <a name="examples"></a>示例  
  
### <a name="a-using-var"></a>A. 使用 VAR  
 以下示例将返回 [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)] 数据库的 `SalesPerson` 表中所有奖金值的方差。  
  
```  
SELECT VAR(Bonus)  
FROM Sales.SalesPerson;  
GO  
```  
  
## <a name="examples-includesssdwfullincludessssdwfull-mdmd-and-includesspdwincludessspdw-mdmd"></a>示例：[!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] 和 [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
  
### <a name="b-using-var"></a>B. 使用 VAR  
 以下示例返回表 `dbo.FactSalesQuota` 中的销售配额值的统计方差。 第一列中包含所有非重复值的方差，第二列中包含所有值（包括任何重复值）的方差。  
  
```  
-- Uses AdventureWorks  
  
SELECT VAR(DISTINCT SalesAmountQuota)AS Distinct_Values, VAR(SalesAmountQuota) AS All_Values  
FROM dbo.FactSalesQuota;  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
 ```
Distinct_Values   All_Values
----------------  ----------------
159180469909.18   158762853821.10
 ```  
  
### <a name="c-using-var-with-over"></a>C. 在 OVER 中使用 VAR  
 以下示例返回日历年中每季度的销售配额值的统计方差。 请注意，OVER 子句中的 ORDER BY 对统计方差进行排序，SELECT 语句中的 ORDER BY 则对结果集进行排序。  
  
```  
-- Uses AdventureWorks  
  
SELECT CalendarYear AS Year, CalendarQuarter AS Quarter, SalesAmountQuota AS SalesQuota,  
       VAR(SalesAmountQuota) OVER (ORDER BY CalendarYear, CalendarQuarter) AS Variance  
FROM dbo.FactSalesQuota  
WHERE EmployeeKey = 272 AND CalendarYear = 2002  
ORDER BY CalendarQuarter;  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
 ```
Year  Quarter  SalesQuota              Variance
----  -------  ----------------------  -------------------
2002  1         91000.0000             null
2002  2        140000.0000             1200500000.00
2002  3         70000.0000             1290333333.33
2002  4        154000.0000             1580250000.00
 ```  
  
## <a name="see-also"></a>另请参阅  
 [聚合函数 (Transact-SQL)](../../t-sql/functions/aggregate-functions-transact-sql.md)   
 [OVER 子句 (Transact-SQL)](../../t-sql/queries/select-over-clause-transact-sql.md)  
  
  

