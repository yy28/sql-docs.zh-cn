---
title: "聚合函数 (Transact SQL) |Microsoft 文档"
ms.custom: 
ms.date: 07/24/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
dev_langs:
- TSQL
helpviewer_keywords:
- functions [SQL Server], aggregate
- aggregate functions [SQL Server], about aggregate functions
- summarizing functions
- aggregate functions [SQL Server]
ms.assetid: 0c06ae42-eb0a-4d77-9d74-aa1e7f344009
caps.latest.revision: 30
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 5a97d68c641d2a3deb1d3fd3a674f65cafc3854c
ms.contentlocale: zh-cn
ms.lasthandoff: 09/01/2017

---
# <a name="aggregate-functions-transact-sql"></a>聚合函数 (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all_md](../../includes/tsql-appliesto-ss2008-all-md.md)]

聚合函数对一组值执行计算，并返回单个值。 除了 COUNT 以外，聚合函数都会忽略空值。 聚合函数经常与 SELECT 语句的 GROUP BY 子句一起使用。
  
所有聚合函数均为确定性函数。 这表示任何时候使用一组特定的输入值调用聚合函数，所返回的值都是相同的。 有关函数的确定性的详细信息，请参阅[Deterministic and Nondeterministic Functions](../../relational-databases/user-defined-functions/deterministic-and-nondeterministic-functions.md)。 [OVER 子句](../../t-sql/queries/select-over-clause-transact-sql.md)可能遵循除分组和 GROUPING_ID 以外的所有聚合函数。
  
聚合函数只能在以下位置作为表达式使用：
-   SELECT 语句的选择列表（子查询或外部查询）。  
-   HAVING 子句。  
  
[!INCLUDE[tsql](../../includes/tsql-md.md)] 提供下列聚合函数：
  
|||  
|-|-|  
|[AVG](../../t-sql/functions/avg-transact-sql.md)|[最小值](../../t-sql/functions/min-transact-sql.md)|  
|[CHECKSUM_AGG](../../t-sql/functions/checksum-agg-transact-sql.md)|[总和](../../t-sql/functions/sum-transact-sql.md)|  
|[计数](../../t-sql/functions/count-transact-sql.md)|[STDEV](../../t-sql/functions/stdev-transact-sql.md)|  
|[COUNT_BIG](../../t-sql/functions/count-big-transact-sql.md)|[STDEVP 函数](../../t-sql/functions/stdevp-transact-sql.md)|  
|[分组](../../t-sql/functions/grouping-transact-sql.md)|[VAR](../../t-sql/functions/var-transact-sql.md)|  
|[GROUPING_ID](../../t-sql/functions/grouping-id-transact-sql.md)|[VARP](../../t-sql/functions/varp-transact-sql.md)|  
|[最大值](../../t-sql/functions/max-transact-sql.md)||  
  
## <a name="see-also"></a>另请参阅
[内置函数 (Transact-SQL)](../../t-sql/functions/functions.md)  
[通过子句 & #40;Transact SQL & #41;](../../t-sql/queries/select-over-clause-transact-sql.md)
  
  

