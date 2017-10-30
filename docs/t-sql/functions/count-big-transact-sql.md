---
title: "COUNT_BIG (Transact SQL) |Microsoft 文档"
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
- COUNT_BIG_TSQL
- COUNT_BIG
dev_langs:
- TSQL
helpviewer_keywords:
- totals [SQL Server], COUNT_BIG function
- counting items in group
- groups [SQL Server], number of items in
- number of group items
- COUNT_BIG function
ms.assetid: f2e3601f-487e-4917-bb01-47b1047908cd
caps.latest.revision: 44
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 8ce3046c36b7d224f6294948029cef6cf5afd43c
ms.contentlocale: zh-cn
ms.lasthandoff: 09/01/2017

---
# <a name="countbig-transact-sql"></a>COUNT_BIG (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all_md](../../includes/tsql-appliesto-ss2008-all-md.md)]

返回组中的项数。 COUNT_BIG 的用法与 COUNT 函数类似。 两个函数唯一的差别是它们的返回值。 始终返回 COUNT_BIG **bigint**数据类型值。 COUNT 始终返回**int**数据类型值。
  
![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>语法  
  
```sql
-- Syntax for SQL Server and Azure SQL Database  
  
COUNT_BIG ( { [ ALL | DISTINCT ] expression } | * )  
   [ OVER ( [ partition_by_clause ] [ order_by_clause ] ) ]  
```  
  
```sql
-- Syntax for Azure SQL Data Warehouse and Parallel Data Warehouse  

-- Aggregation Function Syntax  
COUNT_BIG ( { [ [ ALL | DISTINCT ] expression ] | * } )  
  
-- Analytic Function Syntax  
COUNT_BIG ( { expression | * } ) OVER ( [ <partition_by_clause> ] )  
```  
  
## <a name="arguments"></a>参数  
ALL  
向所有值应用此聚合函数。 ALL 为默认值。
  
DISTINCT  
指定 COUNT_BIG 返回唯一非空值的数量。
  
*expression*  
是[表达式](../../t-sql/language-elements/expressions-transact-sql.md)的任何类型。 不允许使用聚合函数和子查询。
  
*\**  
指定应该计算所有行以返回表中行的总数。 COUNT_BIG (*\**) 不采用任何参数并不能与 DISTINCT 一起使用。 COUNT_BIG (*\**) 不需要*表达式*参数因为根据定义，它不使用任何特定的列的相关信息。 COUNT_BIG (*\**) 指定表中返回的行数，而不获取消除重复项。 它对各行分别计数。 包括包含空值的行。
  
ALL  
向所有值应用此聚合函数。 ALL 为默认值。
  
DISTINCT  
指定 AVG 只在每个值的唯一实例上执行，而不管该值出现了多少次。
  
*expression*  
是[表达式](../../t-sql/language-elements/expressions-transact-sql.md)的精确数字或近似数字数据类型类别，除**位**数据类型。 不允许使用聚合函数和子查询。
  
通过**(** [ *partition_by_clause* ] [ *order_by_clause* ] **)**  
*partition_by_clause*将划分为分区函数应用到的 FROM 子句生成的结果集。 如果未指定，则此函数将查询结果集的所有行视为单个组。 *order_by_clause*确定在其中执行该操作的逻辑顺序。 有关详细信息，请参阅[OVER 子句 &#40;Transact SQL &#41;](../../t-sql/queries/select-over-clause-transact-sql.md).
  
## <a name="return-types"></a>返回类型
**bigint**
  
## <a name="remarks"></a>注释  
COUNT_BIG(*) 返回组中的项数。 包括 NULL 值和重复项。
  
COUNT_BIG (所有*表达式*) 的计算结果*表达式*组中每一行，并返回非 null 值的数目。
  
COUNT_BIG (DISTINCT*表达式*) 的计算结果*表达式*组中每一行，并返回唯一、 非 null 值的数目。
  
COUNT_BIG 不与 OVER 和 ORDER BY 子句配合使用时为确定性函数。 与 OVER 和 ORDER BY 子句一同指定时，它具有不确定性。 有关详细信息，请参阅 [Deterministic and Nondeterministic Functions](../../relational-databases/user-defined-functions/deterministic-and-nondeterministic-functions.md)。
  
## <a name="examples"></a>示例  
有关示例，请参阅[计数 &#40;Transact SQL &#41;](../../t-sql/functions/count-transact-sql.md).
  
## <a name="see-also"></a>另请参阅
[聚合函数 &#40;Transact SQL &#41;](../../t-sql/functions/aggregate-functions-transact-sql.md)  
[计数 &#40;Transact SQL &#41;](../../t-sql/functions/count-transact-sql.md)  
[int、 bigint、 smallint 和 tinyint &#40;Transact SQL &#41;](../../t-sql/data-types/int-bigint-smallint-and-tinyint-transact-sql.md)  
[通过子句 &#40;Transact SQL &#41;](../../t-sql/queries/select-over-clause-transact-sql.md)
  
  

