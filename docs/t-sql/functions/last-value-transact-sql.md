---
title: "(Transact SQL) LAST_VALUE |Microsoft 文档"
ms.custom: 
ms.date: 10/20/2015
ms.prod: sql-non-specified
ms.prod_service: sql-data-warehouse, database-engine, sql-database
ms.service: 
ms.component: t-sql|functions
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- LAST_VALUE
- LAST_VALUE_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- analytic functions, LAST_VALUE
- LAST_VALUE function
ms.assetid: fd833e34-8092-42b7-80fc-95ca6b0eab6b
caps.latest.revision: 16
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Active
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 680f3e88f31c413c7ceaa40fbec63bd3acf81e14
ms.contentlocale: zh-cn
ms.lasthandoff: 09/01/2017

---
# <a name="lastvalue-transact-sql"></a>LAST_VALUE (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2012-asdb-asdw-xxx-md](../../includes/tsql-appliesto-ss2012-asdb-asdw-xxx-md.md)]

  返回 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 中有序值集中的最后一个值。  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
  
LAST_VALUE ( [scalar_expression )   
    OVER ( [ partition_by_clause ] order_by_clause rows_range_clause )   
```  
  
## <a name="arguments"></a>参数  
 *scalar_expression*  
 是要返回的值。 *scalar_expression*可以是列、 子查询或单个值会导致其他表达式。 不允许使用其他分析函数。  
  
 通过**(** [ *partition_by_clause* ] *order_by_clause* [ *rows_range_clause* ] **)**  
 *partition_by_clause*将划分为分区函数应用到的 FROM 子句生成的结果集。 如果未指定，则此函数将查询结果集的所有行视为单个组。  
  
 *order_by_clause*应用函数之前确定数据的顺序。 *Order_by_clause*是必需的。 *rows_range_clause*进一步限制在分区内的行，通过指定开始和结束点。 有关详细信息，请参阅[OVER 子句 &#40;Transact SQL &#41;](../../t-sql/queries/select-over-clause-transact-sql.md).  
  
## <a name="return-types"></a>返回类型  
 相同类型与*scalar_expression*。  
  
## <a name="general-remarks"></a>一般备注  
 LAST_VALUE 具有不确定性。 有关详细信息，请参阅 [Deterministic and Nondeterministic Functions](../../relational-databases/user-defined-functions/deterministic-and-nondeterministic-functions.md)。  
  
## <a name="examples"></a>示例  
  
### <a name="a-using-lastvalue-over-partitions"></a>A. 对分区使用 LAST_VALUE  
 下面的示例给定每个部门中给定薪金（比率）的最后一个雇员的雇佣日期。 PARTITION BY 子句按部门对员工分区，而 LAST_VALUE 函数独立应用于每个分区。 在 OVER 子句中指定的 ORDER BY 子句确定对每个分区中的行应用 LAST_VALUE 函数的逻辑顺序。  
  
```  
USE AdventureWorks2012;  
GO  
SELECT Department, LastName, Rate, HireDate,   
    LAST_VALUE(HireDate) OVER (PARTITION BY Department ORDER BY Rate) AS LastValue  
FROM HumanResources.vEmployeeDepartmentHistory AS edh  
INNER JOIN HumanResources.EmployeePayHistory AS eph    
    ON eph.BusinessEntityID = edh.BusinessEntityID  
INNER JOIN HumanResources.Employee AS e  
    ON e.BusinessEntityID = edh.BusinessEntityID  
WHERE Department IN (N'Information Services',N'Document Control');  
  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```  
  
Department                  LastName                Rate         HireDate     LastValue  
--------------------------- ----------------------- ------------ ----------   ----------  
Document Control            Chai                    10.25        2003-02-23   2003-03-13  
Document Control            Berge                   10.25        2003-03-13   2003-03-13  
Document Control            Norred                  16.8269      2003-04-07   2003-01-17  
Document Control            Kharatishvili           16.8269      2003-01-17   2003-01-17  
Document Control            Arifin                  17.7885      2003-02-05   2003-02-05  
Information Services        Berg                    27.4038      2003-03-20   2003-01-24  
Information Services        Meyyappan               27.4038      2003-03-07   2003-01-24  
Information Services        Bacon                   27.4038      2003-02-12   2003-01-24  
Information Services        Bueno                   27.4038      2003-01-24   2003-01-24  
Information Services        Sharma                  32.4519      2003-01-05   2003-03-27  
Information Services        Connelly                32.4519      2003-03-27   2003-03-27  
Information Services        Ajenstat                38.4615      2003-02-18   2003-02-23  
Information Services        Wilson                  38.4615      2003-02-23   2003-02-23  
Information Services        Conroy                  39.6635      2003-03-08   2003-03-08  
Information Services        Trenary                 50.4808      2003-01-12   2003-01-12  
  
```  
  
### <a name="b-using-firstvalue-and-lastvalue-in-a-computed-expression"></a>B. 在计算表达式中使用 FIRST_VALUE 和 LAST_VALUE  
 以下示例在计算表达式中使用 FIRST_VALUE 和 LAST_VALUE 函数，显示给定数量的员工当前季度分别与一年中第一季度和最后一季度之间的销售配额值差异。 FIRST_VALUE 函数返回该年度第一季度的销售配额值，并将该值从当前季度的销售配额值中减去。 它在名为 DifferenceFromFirstQuarter 的派生列中返回。 对于一年的第一季度，DifferenceFromFirstQuarter 列的值为 0。 LAST_VALUE 函数返回该年度最后一个季度的销售配额值，并从当前季度的销售配额值中减去它。 它在名为 DifferenceFromLastQuarter 的派生列中返回。 对于一年的最后一个季度，DifferenceFromLastQuarter 列的值为 0。  
  
 如下所示，对于要在 DifferenceFromLastQuarter 列中返回的非零值，子句“RANGE BETWEEN CURRENT ROW AND UNBOUNDED FOLLOWING”在此示例中是必需的。 默认范围为“RANGE BETWEEN UNBOUNDED PRECEDING AND CURRENT ROW”。 在此示例中，使用默认范围（或不包括范围，导致使用默认范围）将导致在 DifferenceFromLastQuarter 列中返回零。 有关详细信息，请参阅[OVER 子句 &#40;Transact SQL &#41;](../../t-sql/queries/select-over-clause-transact-sql.md).  
  
```  
USE AdventureWorks2012;  
SELECT BusinessEntityID, DATEPART(QUARTER,QuotaDate)AS Quarter, YEAR(QuotaDate) AS SalesYear,   
    SalesQuota AS QuotaThisQuarter,   
    SalesQuota - FIRST_VALUE(SalesQuota)   
        OVER (PARTITION BY BusinessEntityID, YEAR(QuotaDate)   
              ORDER BY DATEPART(QUARTER,QuotaDate) ) AS DifferenceFromFirstQuarter,   
    SalesQuota - LAST_VALUE(SalesQuota)   
        OVER (PARTITION BY BusinessEntityID, YEAR(QuotaDate)   
              ORDER BY DATEPART(QUARTER,QuotaDate)   
              RANGE BETWEEN CURRENT ROW AND UNBOUNDED FOLLOWING ) AS DifferenceFromLastQuarter   
FROM Sales.SalesPersonQuotaHistory   
WHERE YEAR(QuotaDate) > 2005   
AND BusinessEntityID BETWEEN 274 AND 275   
ORDER BY BusinessEntityID, SalesYear, Quarter;  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```  
BusinessEntityID Quarter     SalesYear   QuotaThisQuarter      DifferenceFromFirstQuarter DifferenceFromLastQuarter  
---------------- ----------- ----------- --------------------- --------------------------- -----------------------  
274              1           2006        91000.00              0.00                        -63000.00  
274              2           2006        140000.00             49000.00                    -14000.00  
274              3           2006        70000.00              -21000.00                   -84000.00  
274              4           2006        154000.00             63000.00                    0.00  
274              1           2007        107000.00             0.00                        -9000.00  
274              2           2007        58000.00              -49000.00                   -58000.00  
274              3           2007        263000.00             156000.00                   147000.00  
274              4           2007        116000.00             9000.00                     0.00  
274              1           2008        84000.00              0.00                        -103000.00  
274              2           2008        187000.00             103000.00                   0.00  
275              1           2006        502000.00             0.00                        -822000.00  
275              2           2006        550000.00             48000.00                    -774000.00  
275              3           2006        1429000.00            927000.00                   105000.00  
275              4           2006        1324000.00            822000.00                   0.00  
275              1           2007        729000.00             0.00                        -489000.00  
275              2           2007        1194000.00            465000.00                   -24000.00  
275              3           2007        1575000.00            846000.00                   357000.00  
275              4           2007        1218000.00            489000.00                   0.00  
275              1           2008        849000.00             0.00                        -20000.00  
275              2           2008        869000.00             20000.00                    0.00  
  
(20 row(s) affected)  
  
```  
  
  

