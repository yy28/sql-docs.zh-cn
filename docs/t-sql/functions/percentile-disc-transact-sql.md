---
title: "PERCENTILE_DISC (Transact SQL) |Microsoft 文档"
ms.custom: 
ms.date: 10/20/2015
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: t-sql|functions
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- PERCENTILE_DISC
- PERCENTILE_DISC_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- PERCENTILE_DISC function
- analytic functions,PERCENTILE_DISC
ms.assetid: b545413d-c4f7-4c8e-8617-607599a26680
caps.latest.revision: 
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Active
ms.openlocfilehash: a1e7ebdd2303108fbf63578a288d95eb2f3f7fe4
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/21/2017
---
# <a name="percentiledisc-transact-sql"></a>PERCENTILE_DISC (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2012-all-md](../../includes/tsql-appliesto-ss2012-all-md.md)]

  计算 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 中整个行集内或行集的非重复分区内已排序值的特定百分位数。 给定的百分位数值*P*，PERCENTILE_DISC 对中的 ORDER BY 子句的表达式的值进行排序并返回具有最小 CUME_DIST 值 （对应于相同的排序规范） 大于值或等于*P*。例如，PERCENTILE_DISC (0.5) 将计算表达式的第 50 百分位数（也即中值）。 PERCENTILE_DISC 基于列值的离散分布来计算百分位数；结果等于列中的一个特定值。  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定 &#40;Transact SQL &#41;](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
PERCENTILE_DISC ( numeric_literal ) WITHIN GROUP ( ORDER BY order_by_expression [ ASC | DESC ] )  
    OVER ( [ <partition_by_clause> ] )  
```  
  
## <a name="arguments"></a>参数  
 *文本*  
 要计算的百分位数。 该值必须介于 0.0 和 1.0 之间。  
  
 组内**(** ORDER BY *order_by_expression* [ **ASC** |DESC]**)**  
 指定的值进行排序和计算通过百分位的列表。 只有一个*order_by_expression*允许。 默认的排序顺序为升序。 值列表可以是任何有效的排序操作的数据类型。  
  
 通过**(** \<partition_by_clause > **)**  
 将 FROM 子句生成的结果集划分为数个应用百分位数函数的分区。 有关详细信息，请参阅[OVER 子句 &#40;Transact SQL &#41;](../../t-sql/queries/select-over-clause-transact-sql.md). \<ORDER BY 子句 > 和\<行或 range 子句 > 无法 PERCENTILE_DISC 函数中指定。  
  
## <a name="return-types"></a>返回类型  
 返回类型由*order_by_expression*类型。  
  
## <a name="compatibility-support"></a>兼容性支持  
 在兼容级别 110 和更高级别中，WITHIN GROUP 是保留关键字。 有关详细信息，请参阅 [ALTER DATABASE 兼容级别 (Transact-SQL)](../../t-sql/statements/alter-database-transact-sql-compatibility-level.md)。  
  
## <a name="general-remarks"></a>一般备注  
 数据集中的任何 null 都将被忽略。  
  
 PERCENTILE_DISC 具有不确定性。 有关详细信息，请参阅 [Deterministic and Nondeterministic Functions](../../relational-databases/user-defined-functions/deterministic-and-nondeterministic-functions.md)。  
  
## <a name="examples"></a>示例  
  
### <a name="a-basic-syntax-example"></a>A. 基本语法示例  
 下面的示例使用 PERCENTILE_CONT 和 PERCENTILE_DISC 函数找出每个部门内雇员的薪金中值。 请注意，这些函数可能不返回相同的值。 这是因为，PERCENTILE_CONT 内插适当的值，而无论它在数据集中是否存在，而 PERCENTILE_DISC 始终从数据集中返回实际值。  
  
```  
USE AdventureWorks2012;  
  
SELECT DISTINCT Name AS DepartmentName  
      ,PERCENTILE_CONT(0.5) WITHIN GROUP (ORDER BY ph.Rate)   
                            OVER (PARTITION BY Name) AS MedianCont  
      ,PERCENTILE_DISC(0.5) WITHIN GROUP (ORDER BY ph.Rate)   
                            OVER (PARTITION BY Name) AS MedianDisc  
FROM HumanResources.Department AS d  
INNER JOIN HumanResources.EmployeeDepartmentHistory AS dh   
    ON dh.DepartmentID = d.DepartmentID  
INNER JOIN HumanResources.EmployeePayHistory AS ph  
    ON ph.BusinessEntityID = dh.BusinessEntityID  
WHERE dh.EndDate IS NULL;  
```  
  
 以下为部分结果集。  
  
 ```
DepartmentName        MedianCont    MedianDisc
--------------------   ----------   ----------
Document Control       16.8269      16.8269
Engineering            34.375       32.6923
Executive              54.32695     48.5577
Human Resources        17.427850    16.5865
```
  
## <a name="examples-includesssdwfullincludessssdwfull-mdmd-and-includesspdwincludessspdw-mdmd"></a>示例：[!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)]和[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
  
### <a name="b-basic-syntax-example"></a>B. 基本语法示例  
 下面的示例使用 PERCENTILE_CONT 和 PERCENTILE_DISC 函数找出每个部门内雇员的薪金中值。 请注意，这些函数可能不返回相同的值。 这是因为，PERCENTILE_CONT 内插适当的值，而无论它在数据集中是否存在，而 PERCENTILE_DISC 始终从数据集中返回实际值。  
  
```  
-- Uses AdventureWorks  
  
SELECT DISTINCT DepartmentName  
       ,PERCENTILE_CONT(0.5) WITHIN GROUP (ORDER BY BaseRate)  
        OVER (PARTITION BY DepartmentName) AS MedianCont  
       ,PERCENTILE_DISC(0.5) WITHIN GROUP (ORDER BY BaseRate)  
        OVER (PARTITION BY DepartmentName) AS MedianDisc  
FROM dbo.DimEmployee;  
  
```  
  
 以下为部分结果集。  
  
 ```
DepartmentName        MedianCont    MedianDisc  
--------------------   ----------   ----------  
Document Control       16.826900    16.8269  
Engineering            34.375000    32.6923  
Human Resources        17.427850    16.5865  
Shipping and Receiving  9.250000     9.0000
```  
  
## <a name="see-also"></a>另请参阅  
 [PERCENTILE_CONT &#40;Transact SQL &#41;](../../t-sql/functions/percentile-cont-transact-sql.md)  
  
  


