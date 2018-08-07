---
title: EXCEPT 和 INTERSECT (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/16/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.suite: sql
ms.technology: t-sql
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- INTERSECT_TSQL
- EXCEPT_TSQL
- INTERSECT
- EXCEPT
dev_langs:
- TSQL
helpviewer_keywords:
- EXCEPT operator [Transact-SQL]
- queries [SQL Server], comparing
- comparing queries
- INTERSECT operator
ms.assetid: b1019300-171a-4a1a-854f-e1e751de3565
caps.latest.revision: 39
author: douglaslMS
ms.author: douglasl
manager: craigg
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017'
ms.openlocfilehash: b9c519ca1595ed9831a88549bea58d8c16477a3e
ms.sourcegitcommit: e02c28b0b59531bb2e4f361d7f4950b21904fb74
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/02/2018
ms.locfileid: "39453231"
---
# <a name="set-operators---except-and-intersect-transact-sql"></a>SET 运算符 - EXCEPT 和 INTERSECT (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  比较两个查询的结果，返回非重复行。  
  
 EXCEPT 从左侧输入查询返回非由右侧输入查询输出的非重复行。  
  
 INTERSECT 返回由左右双侧输入查询运算符输出的非重复行。  
  
 以下是将使用 EXCEPT 或 INTERSECT 的两个查询的结果集组合起来的基本规则：  
  
-   所有查询中的列数和列的顺序必须相同。  
  
-   数据类型必须兼容。  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
{ <query_specification> | ( <query_expression> ) }   
{ EXCEPT | INTERSECT }  
{ <query_specification> | ( <query_expression> ) }  
```  
  
## <a name="arguments"></a>参数  
 \<query_specification> | ( \<query_expression> )  
 查询规范或查询表达式返回与来自另一个查询规范或查询表达式的数据相比较的数据。 在 EXCEPT 或 INTERSECT 运算中，列的定义可以不同，但它们必须在隐式转换后进行比较。 如果数据类型不同，则用于执行比较并返回结果的类型是基于[数据类型优先级](../../t-sql/data-types/data-type-precedence-transact-sql.md)的规则确定的。  
  
 如果类型相同，但精度、小数位数或长度不同，则根据用于合并表达式的相同规则来确定结果。 有关详细信息，请参阅[精度、小数位数和长度 (Transact-SQL)](../../t-sql/data-types/precision-scale-and-length-transact-sql.md)。  
  
 查询规范或表达式不能返回 xml、text、ntext、image 或非二进制 CLR 用户定义类型列，因为这些数据类型不可比较。  
  
 EXCEPT  
 从 EXCEPT 运算符左边的查询中返回右边的查询未返回的所有非重复值。  
  
 INTERSECT  
 返回由 INTERSECT 运算符左侧和右侧的查询都返回的所有非重复值。  
  
## <a name="remarks"></a>Remarks  
 如果 EXCEPT 或 INTERSECT 运算符左边和右边的查询返回的可比较列的数据类型是具有不同排序规则的字符数据类型，则根据[排序规则优先级](../../t-sql/statements/collation-precedence-transact-sql.md)的规则执行所需的比较。 如果无法执行此转换，[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]将返回错误。  
  
 通过比较列值来确定非重复行时，两个 NULL 值被视为相等。  
  
 EXCEPT 或 INTERSECT 返回的结果集的列名与运算符左侧的查询返回的列名相同。  
  
 ORDER BY 子句中的列名或别名必须引用左侧查询返回的列名。  
  
 EXCEPT 或 INTERSECT 返回的结果集中的任何列的为空性与运算符左侧的查询返回的对应列的为空性相同。  
  
 如果 EXCEPT 或 INTERSECT 与表达式中的其他运算符一起使用，则在以下优先顺序的上下文中对其进行评估：  
  
1.  括号中的表达式  
  
2.  INTERSECT 运算符  
  
3.  基于在表达式中的位置从左到右求值的 EXCEPT 和 UNION  
  
 如果 EXCEPT 或 INTERSECT 用于比较两个以上的查询集，则数据类型转换是通过一次比较两个查询来确定的，并遵循前面提到的表达式求值规则。  
  
 EXCEPT 和 INTERSECT 不能在分布式分区视图定义、查询通知中使用。  
  
 EXCEPT 和 INTERSECT 可在分布式查询中使用，但只在本地服务器上执行，不会被推送到链接服务器。 因此，在分布式查询中使用 EXCEPT 和 INTERSECT 可能会影响性能。  
  
 快速只进游标和静态游标与 EXCEPT 或 INTERSECT 运算一起使用时，在结果集中完全受支持。 如果由键集驱动的游标或动态游标与 EXCEPT 或 INTERSECT 运算一起使用，则运算的结果集的游标转换为静态游标。  
  
 使用 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 中的图形显示计划功能显示 EXCEPT 运算时，该运算显示为 [left anti semi join](../../relational-databases/showplan-logical-and-physical-operators-reference.md)，INTERSECT 运算显示为 [left semi join](../../relational-databases/showplan-logical-and-physical-operators-reference.md)。  
  
## <a name="examples"></a>示例  
 以下示例说明如何使用 `INTERSECT` 和 `EXCEPT` 运算符。 第一个查询返回 `Production.Product` 表中的所有值，以便对 `INTERSECT` 和 `EXCEPT` 所返回的结果进行比较。  
  
```  
-- Uses AdventureWorks  
  
SELECT ProductID   
FROM Production.Product ;  
--Result: 504 Rows  
```  
  
 以下查询返回 `INTERSECT` 运算符左右两侧的两个查询均返回的所有非重复值。  
  
```  
-- Uses AdventureWorks  
  
SELECT ProductID   
FROM Production.Product  
INTERSECT  
SELECT ProductID   
FROM Production.WorkOrder ;  
--Result: 238 Rows (products that have work orders)  
```  
  
 以下查询从 `EXCEPT` 运算符左侧的查询返回右侧查询没有找到的所有非重复值。  
  
```  
-- Uses AdventureWorks  
  
SELECT ProductID   
FROM Production.Product  
EXCEPT  
SELECT ProductID   
FROM Production.WorkOrder ;  
--Result: 266 Rows (products without work orders)  
```  
  
 以下查询从 `EXCEPT` 运算符左侧的查询返回右侧查询没有找到的所有非重复值。 对上例中的表进行了互换。  
  
```  
-- Uses AdventureWorks  
  
SELECT ProductID   
FROM Production.WorkOrder  
EXCEPT  
SELECT ProductID   
FROM Production.Product ;  
--Result: 0 Rows (work orders without products)  
```  
  
## <a name="examples-includesssdwfullincludessssdwfull-mdmd-and-includesspdwincludessspdw-mdmd"></a>示例：[!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] 和 [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
 以下示例说明如何使用 `INTERSECT` 和 `EXCEPT` 运算符。 第一个查询返回 `FactInternetSales` 表中的所有值，以便对 `INTERSECT` 和 `EXCEPT` 所返回的结果进行比较。  
  
```  
-- Uses AdventureWorks  
  
SELECT CustomerKey   
FROM FactInternetSales;  
--Result: 60398 Rows  
```  
  
 以下查询返回 `INTERSECT` 运算符左右两侧的两个查询均返回的所有非重复值。  
  
```  
-- Uses AdventureWorks  
  
SELECT CustomerKey   
FROM FactInternetSales    
INTERSECT   
SELECT CustomerKey   
FROM DimCustomer   
WHERE DimCustomer.Gender = 'F'  
ORDER BY CustomerKey;  
--Result: 9133 Rows (Sales to customers that are female.)  
```  
  
 以下查询从 `EXCEPT` 运算符左侧的查询返回右侧查询没有找到的所有非重复值。  
  
```  
-- Uses AdventureWorks  
  
SELECT CustomerKey   
FROM FactInternetSales    
EXCEPT   
SELECT CustomerKey   
FROM DimCustomer   
WHERE DimCustomer.Gender = 'F'  
ORDER BY CustomerKey;  
--Result: 9351 Rows (Sales to customers that are not female.)  
```  
  
  

