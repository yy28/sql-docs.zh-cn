---
title: "Microsoft SQL 数据库函数有哪些？ | Microsoft Docs"
ms.custom: 
ms.date: 06/28/2017
ms.prod: sql-non-specified
ms.prod_service: sql-data-warehouse, database-engine, pdw, sql-database
ms.service: 
ms.component: t-sql|functions
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
dev_langs:
- TSQL
helpviewer_keywords:
- built-in functions [SQL Server]
- function [SQL Server] See functions [SQL Server]
- functions [Transact-SQL]
- functions [SQL Server], about functions
- scalar functions
- functions [SQL Server]
ms.assetid: 17186213-5ab5-40b0-b470-b660af1ec44c
caps.latest.revision: 38
author: edmacauley
ms.author: edmaca
manager: cguyer
ms.workload: Active
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 53a2a1be1099b2224b14f8c8d856b7ae07d42ac6
ms.contentlocale: zh-cn
ms.lasthandoff: 09/01/2017

---
# <a name="what-are-the-sql-database-functions"></a>SQL 数据库函数有哪些？
[!INCLUDE[tsql-appliesto-ss2008-asdb-asdw-pdw-md](../../includes/tsql-appliesto-ss2008-asdb-asdw-pdw-md.md)]

了解你可以使用 SQL 数据库使用的内置函数的类别。 你可以使用内置函数，或创建您自己的用户定义函数。
  
## <a name="aggregate-functions"></a>聚合函数

聚合函数对一组值执行计算，并返回单个值。 它们可以用在 select 列表或 HAVING 子句的 SELECT 语句。 可以使用与 GROUP BY 子句结合使用的聚合计算的行的类别的聚合。 使用 OVER 子句来计算上特定范围的值的聚合。 OVER 子句不能跟 GROUPING 或 GROUPING_ID 聚合。

所有聚合函数都具有确定性，这意味着对相同的输入值在运行时，它们会始终返回相同的值。 有关详细信息，请参阅[Deterministic and Nondeterministic Functions](../../relational-databases/user-defined-functions/deterministic-and-nondeterministic-functions.md)。 |

## <a name="analytic-functions"></a>分析函数
解析函数基于一组行计算聚合值。 但是，与聚合函数，不同分析函数可以返回的每个组的多个行。 你可以使用分析函数来计算移动平均线，运行总计百分比或组中的前 N 结果。

## <a name="ranking-functions"></a>排名函数
排名函数为分区中的每一行返回一个排名值。 根据所用函数的不同，某些行可能与其他行接收到相同的值。 排名函数具有不确定性。

## <a name="rowset-functions"></a>行集函数
行集函数将返回一个可像表引用 SQL 语句中使用的对象。

## <a name="scalar-functions"></a>标量函数
对单一值进行运算，然后返回单一值。 只要表达式有效，即可使用标量函数。

### <a name="categories-of-scalar-functions"></a>标量函数类别
  
|函数类别|Description|  
|-----------------------|-----------------|  
|[配置函数](configuration-functions-transact-sql.md)|返回当前配置信息。|  
|[转换函数](conversion-functions-transact-sql.md)|支持数据类型强制转换和转换。|  
|[游标函数](cursor-functions-transact-sql.md)|返回游标信息。|  
|[日期和时间数据类型和函数](date-and-time-data-types-and-functions-transact-sql.md)|对日期和时间输入值执行运算，然后返回字符串、数字或日期和时间值。|  
|[JSON 函数](json-functions-transact-sql.md)|验证、 查询或更改 JSON 数据。|  
|[逻辑函数](http://msdn.microsoft.com/library/5b2b4546-951b-462d-91d5-e41fc5acd6f9)|执行逻辑运算。|  
|[数学函数](mathematical-functions-transact-sql.md)|基于作为函数的参数提供的输入值执行运算，然后返回数字值。|  
|[元数据函数](metadata-functions-transact-sql.md)|返回有关数据库和数据库对象的信息。|  
|[安全函数](security-functions-transact-sql.md)|返回有关用户和角色的信息。|  
|[字符串函数](string-functions-transact-sql.md)|对字符串执行操作 (**char**或**varchar**) 输入值，并返回一个字符串或数值的值。|  
|[系统函数](../../relational-databases/system-functions/system-functions-for-transact-sql.md)|执行运算后返回 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实例中有关值、对象和设置的信息。|  
|[系统统计函数](system-statistical-functions-transact-sql.md)|返回系统的统计信息。|  
|[文本和图像函数](http://msdn.microsoft.com/library/b9c70488-1bf5-4068-a003-e548ccbc5199)|对文本或图像输入值或列执行运算，然后返回有关值的信息。|  
  
## <a name="function-determinism"></a>函数确定性  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 内置函数可以是确定的或是不确定的。 如果任何时候用一组特定的输入值调用内置函数，返回的结果总是相同的，则这些内置函数为确定的。 如果每次调用内置函数时，即使用的是同一组特定输入值，也总返回不同结果，则这些内置函数为不确定的。 有关详细信息，请参阅[Deterministic and Nondeterministic Functions](../../relational-databases/user-defined-functions/deterministic-and-nondeterministic-functions.md)  
  
## <a name="function-collation"></a>函数排序规则  
 使用字符串输入并返回字符串输出的函数，对输出使用输入字符串的排序规则。  
  
 使用非字符输入并返回字符串的函数对输出使用当前数据库的默认排序规则。  
  
 使用多个字符串输入并返回字符串的函数，使用排序规则的优先顺序规则设置输出字符串的排序规则。 有关详细信息，请参阅[排序规则优先顺序 &#40;Transact SQL &#41;](../../t-sql/statements/collation-precedence-transact-sql.md).  
  
## <a name="see-also"></a>另请参阅  
 [CREATE FUNCTION (Transact-SQL)](../../t-sql/statements/create-function-transact-sql.md)   
 [确定性和不确定性函数](../../relational-databases/user-defined-functions/deterministic-and-nondeterministic-functions.md)   
 [使用存储的过程 &#40;MDX &#41;](../../mdx/using-stored-procedures-mdx.md)  
  
  

