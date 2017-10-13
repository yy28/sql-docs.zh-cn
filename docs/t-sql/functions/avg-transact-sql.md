---
title: "AVG (Transact SQL) |Microsoft 文档"
ms.custom: 
ms.date: 07/24/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- AVG_TSQL
- AVG
dev_langs:
- TSQL
helpviewer_keywords:
- AVG function [Transact-SQL]
- GROUP BY clause, AVG function
- DISTINCT keyword
- values [SQL Server], average
- average values
ms.assetid: 4534b705-d946-441b-9b5d-5fbe561c9131
caps.latest.revision: 52
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 80c1228faeaaa4012afc0fd27992a2f5cf389f6e
ms.openlocfilehash: 1e7598f8ee20f88346dfcbba1757f1173b34fe5c
ms.contentlocale: zh-cn
ms.lasthandoff: 10/12/2017

---
# <a name="avg-transact-sql"></a>AVG (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all_md](../../includes/tsql-appliesto-ss2008-all-md.md)]

返回组中各值的平均值。 Null 值会被忽略。
  
![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>语法  
  
```sql
AVG ( [ ALL | DISTINCT ] expression )  
   OVER ( [ partition_by_clause ] order_by_clause )    
```  
  
## <a name="arguments"></a>参数  
ALL  
向所有值应用此聚合函数。 ALL 为默认值。
  
DISTINCT  
指定 AVG 只在每个值的唯一实例上执行，而不管该值出现了多少次。
  
*expression*  
是[表达式](../../t-sql/language-elements/expressions-transact-sql.md)的精确数字或近似数字数据类型类别，除**位**数据类型。 不允许使用聚合函数和子查询。
  
通过**(** [ *partition_by_clause* ] *order_by_clause***)**  
*partition_by_clause*将划分为分区函数应用到的 FROM 子句生成的结果集。 如果未指定，则此函数将查询结果集的所有行视为单个组。 *order_by_clause*确定在其中执行该操作的逻辑顺序。 *order_by_clause*是必需的。 有关详细信息，请参阅[OVER 子句 &#40;Transact SQL &#41;](../../t-sql/queries/select-over-clause-transact-sql.md).
  
## <a name="return-types"></a>返回类型
返回类型由的计算结果的类型确定*表达式*。
  
|表达式结果|返回类型|  
|---|---|
|**tinyint**|**int**|  
|**int**|**int**|  
|**ssNoversion**|**int**|  
|**bigint**|**bigint**|  
|**十进制**类别 （p、 s）|**decimal (38，s)**除以**decimal （10，0）**|  
|**money**和**smallmoney**类别|**money**|  
|**float**和**实际**类别|**float**|  
  
## <a name="remarks"></a>注释  
如果数据类型的*表达式*是别名数据类型，返回类型也是该别名数据类型。 但是，如果的基数据类型别名数据类型将提升，例如从**tinyint**到**int**，返回值是提升数据类型而不是别名数据类型。
  
AVG () 可计算一组值的平均值，方法是用一组值的总和除以非 Null 值的计数。 如果值的总和超过返回值数据类型的最大值，将返回错误。
  
AVG 不与 OVER 和 ORDER BY 子句配合使用时为确定性函数。 与 OVER 和 ORDER BY 子句一同指定时，它具有不确定性。 有关详细信息，请参阅 [Deterministic and Nondeterministic Functions](../../relational-databases/user-defined-functions/deterministic-and-nondeterministic-functions.md)。
  
## <a name="examples"></a>示例  
  
### <a name="a-using-the-sum-and-avg-functions-for-calculations"></a>A. 使用 SUM 和 AVG 函数进行计算  
以下示例计算 [!INCLUDE[ssSampleDBCoFull](../../includes/sssampledbcofull-md.md)] 的副总所用的平均休假小时数以及总的病假小时数。 对检索到的所有行，每个聚合函数都生成一个单独的汇总值。 该示例使用 [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)] 数据库。
  
```sql
SELECT AVG(VacationHours)AS 'Average vacation hours',   
    SUM(SickLeaveHours) AS 'Total sick leave hours'  
FROM HumanResources.Employee  
WHERE JobTitle LIKE 'Vice President%';  
```  
  
[!INCLUDE[ssResult](../../includes/ssresult-md.md)]
  
```
Average vacation hours       Total sick leave hours
 ----------------------       ----------------------
25                           97
  
(1 row(s) affected)
```
  
### <a name="b-using-the-sum-and-avg-functions-with-a-group-by-clause"></a>B. 搭配 GROUP BY 子句使用 SUM 和 AVG 函数  
当与 `GROUP BY` 子句一起使用时，每个聚合函数都针对每一组生成一个值，而不是针对整个表生成一个值。 以下示例针对 [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)] 数据库中的每个销售地区生成汇总值。 汇总中列出每个地区的销售人员得到的平均奖金以及每个地区的本年度销售总额。
  
```sql
SELECT TerritoryID, AVG(Bonus)as 'Average bonus', SUM(SalesYTD) as 'YTD sales'  
FROM Sales.SalesPerson  
GROUP BY TerritoryID;  
GO  
```  
  
[!INCLUDE[ssResult](../../includes/ssresult-md.md)]
  
```sql
TerritoryID Average Bonus         YTD Sales  
----------- --------------------- ---------------------  
NULL        0.00                  1252127.9471  
1           4133.3333             4502152.2674  
2           4100.00               3763178.1787  
3           2500.00               3189418.3662  
4           2775.00               6709904.1666  
5           6700.00               2315185.611  
6           2750.00               4058260.1825  
7           985.00                3121616.3202  
8           75.00                 1827066.7118  
9           5650.00               1421810.9242  
10          5150.00               4116871.2277  
  
(11 row(s) affected)  
```  
  
### <a name="c-using-avg-with-distinct"></a>C. 带 DISTINCT 使用 AVG  
以下语句返回 [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)] 数据库中产品的平均标价。 通过指定 DISTINCT，在计算时只考虑唯一值。
  
```sql
SELECT AVG(DISTINCT ListPrice)  
FROM Production.Product;  
```  
  
[!INCLUDE[ssResult](../../includes/ssresult-md.md)]
  
```
------------------------------
437.4042
  
(1 row(s) affected)
```
  
### <a name="d-using-avg-without-distinct"></a>D. 不带 DISTINCT 使用 AVG  
如果不使用 DISTINCT，`AVG` 函数将计算出 [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)] 数据库的 `Product` 表中所有产品的平均标价，包括任何重复值。
  
```sql
SELECT AVG(ListPrice)  
FROM Production.Product;  
```  
  
[!INCLUDE[ssResult](../../includes/ssresult-md.md)]
  
```
------------------------------
438.6662
  
(1 row(s) affected)
```
  
### <a name="e-using-the-over-clause"></a>E. 使用 OVER 子句  
以下示例将 AVG 函数与 OVER 子句结合使用，以便为 [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)] 数据库的 `Sales.SalesPerson` 表中的每个地区提供年度销售额的移动平均线。 数据按 `TerritoryID` 分区并在逻辑上按 `SalesYTD` 排序。 这意味着，将基于年度销售额为各区域计算 AVG 函数。 请注意，对于 `TerritoryID` 1，为 2005 销售年度存在两行，分别表示在该年度有销售业绩的两个销售人员。 将计算这两行的平均销售额，然后在计算中包括表示 2006 年销售额的第三行。
  
```sql
SELECT BusinessEntityID, TerritoryID   
   ,DATEPART(yy,ModifiedDate) AS SalesYear  
   ,CONVERT(varchar(20),SalesYTD,1) AS  SalesYTD  
   ,CONVERT(varchar(20),AVG(SalesYTD) OVER (PARTITION BY TerritoryID   
                                            ORDER BY DATEPART(yy,ModifiedDate)   
                                           ),1) AS MovingAvg  
   ,CONVERT(varchar(20),SUM(SalesYTD) OVER (PARTITION BY TerritoryID   
                                            ORDER BY DATEPART(yy,ModifiedDate)   
                                            ),1) AS CumulativeTotal  
FROM Sales.SalesPerson  
WHERE TerritoryID IS NULL OR TerritoryID < 5  
ORDER BY TerritoryID,SalesYear;  
```  
  
[!INCLUDE[ssResult](../../includes/ssresult-md.md)]
  
```sql
BusinessEntityID TerritoryID SalesYear   SalesYTD             MovingAvg            CumulativeTotal  
---------------- ----------- ----------- -------------------- -------------------- --------------------  
274              NULL        2005        559,697.56           559,697.56           559,697.56  
287              NULL        2006        519,905.93           539,801.75           1,079,603.50  
285              NULL        2007        172,524.45           417,375.98           1,252,127.95  
283              1           2005        1,573,012.94         1,462,795.04         2,925,590.07  
280              1           2005        1,352,577.13         1,462,795.04         2,925,590.07  
284              1           2006        1,576,562.20         1,500,717.42         4,502,152.27  
275              2           2005        3,763,178.18         3,763,178.18         3,763,178.18  
277              3           2005        3,189,418.37         3,189,418.37         3,189,418.37  
276              4           2005        4,251,368.55         3,354,952.08         6,709,904.17  
281              4           2005        2,458,535.62         3,354,952.08         6,709,904.17  
  
(10 row(s) affected)  
  
```  
  
在这个例子中，OVER 子句未包含 PARTITION BY。 这意味着该函数将应用于查询所返回的所有行。 在 OVER 子句中指定的 ORDER BY 子句将确定应用 AVG 函数的逻辑顺序。 该查询将按年为在 WHERE 子句中指定的所有销售区域返回销售额的移动平均值。 在 SELECT 语句中指定的 ORDER BY 子句将确定显示查询行的顺序。
  
```sql
SELECT BusinessEntityID, TerritoryID   
   ,DATEPART(yy,ModifiedDate) AS SalesYear  
   ,CONVERT(varchar(20),SalesYTD,1) AS  SalesYTD  
   ,CONVERT(varchar(20),AVG(SalesYTD) OVER (ORDER BY DATEPART(yy,ModifiedDate)   
                                            ),1) AS MovingAvg  
   ,CONVERT(varchar(20),SUM(SalesYTD) OVER (ORDER BY DATEPART(yy,ModifiedDate)   
                                            ),1) AS CumulativeTotal  
FROM Sales.SalesPerson  
WHERE TerritoryID IS NULL OR TerritoryID < 5  
ORDER BY SalesYear;  
```  
  
[!INCLUDE[ssResult](../../includes/ssresult-md.md)]
  
```sql
BusinessEntityID TerritoryID SalesYear   SalesYTD             MovingAvg            CumulativeTotal  
---------------- ----------- ----------- -------------------- -------------------- --------------------  
274              NULL        2005        559,697.56           2,449,684.05         17,147,788.35  
275              2           2005        3,763,178.18         2,449,684.05         17,147,788.35  
276              4           2005        4,251,368.55         2,449,684.05         17,147,788.35  
277              3           2005        3,189,418.37         2,449,684.05         17,147,788.35  
280              1           2005        1,352,577.13         2,449,684.05         17,147,788.35  
281              4           2005        2,458,535.62         2,449,684.05         17,147,788.35  
283              1           2005        1,573,012.94         2,449,684.05         17,147,788.35  
284              1           2006        1,576,562.20         2,138,250.72         19,244,256.47  
287              NULL        2006        519,905.93           2,138,250.72         19,244,256.47  
285              NULL        2007        172,524.45           1,941,678.09         19,416,780.93  
(10 row(s) affected)  
```  
  
## <a name="see-also"></a>另请参阅
[聚合函数 &#40;Transact SQL &#41;](../../t-sql/functions/aggregate-functions-transact-sql.md)  
[通过子句 &#40;Transact SQL &#41;](../../t-sql/queries/select-over-clause-transact-sql.md)
  
  

