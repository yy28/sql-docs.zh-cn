---
title: 多个结果 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQLMoreResults function [ODBC], multiple results
- row counts [ODBC]
- multiple results [ODBC]
- result sets [ODBC], multiple results
- SQLGetInfo function [ODBC], multiple results
ms.assetid: a3c32e4b-8fe7-4a33-ae39-ae664001f315
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: d90414b631a7e81a7868ab7974b64ea84a0ea452
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/27/2020
ms.locfileid: "81302406"
---
# <a name="multiple-results"></a>多个结果
*结果*是在执行语句后数据源返回的内容。 ODBC 有两种类型的结果：结果集和行计数。 *行计数*是受更新、删除或插入语句影响的行数。 [SQL 语句的批处理](../../../odbc/reference/develop-app/batches-of-sql-statements.md)中所述的批处理可以生成多个结果。  
  
 下表列出了应用程序用来确定数据源是否为每种不同类型的批处理返回多个结果的**SQLGetInfo**选项。 特别是，数据源可以为批处理中的每个语句返回单个行计数或单个行计数。 对于使用参数数组执行的结果集生成语句，数据源可以为每组参数的所有参数集或单个结果集返回单个结果集。  
  
|批处理类型|行计数|结果集|  
|----------------|----------------|-----------------|  
|显式批处理|SQL_BATCH_ROW_COUNT [a]|--[b]|  
|过程|SQL_BATCH_ROW_COUNT [a]|--[b]|  
|参数数组|SQL_PARAM_ARRAYS_ROW_COUNTS|SQL_PARAM_ARRAYS_SELECTS|  
  
 [a] 可能支持批处理中的行计数生成语句，但不支持返回行计数。 **SQLGetInfo**中的 SQL_BATCH_SUPPORT 选项指示批处理中是否允许生成行计数语句;SQL_BATCH_ROW_COUNTS 选项指示是否将这些行计数返回到应用程序。  
  
 [b] 当显式批处理和过程包含多个结果集生成语句时，它们始终返回多个结果集。  
  
> [!NOTE]  
>  ODBC 1.0 中引入的 SQL_MULT_RESULT_SETS 选项仅提供有关是否可以返回多个结果集的一般信息。 特别是，如果为 SQL_BATCH_SUPPORT 返回 SQL_BS_SELECT_EXPLICIT 或 SQL_BS_SELECT_PROC 位，则设置为 "Y"; 如果为 SQL_PARAM_ARRAYS_SELECT 返回 SQL_PAS_BATCH，则设置为 "Y"。  
  
 若要处理多个结果，应用程序将调用**SQLMoreResults**。 此函数放弃当前结果，并使下一个结果可用。 当没有更多结果可用时，它将返回 SQL_NO_DATA。 例如，假设以下语句以批处理方式执行：  
  
```  
SELECT * FROM Parts WHERE Price > 100.00;  
UPDATE Parts SET Price = 0.9 * Price WHERE Price > 100.00  
```  
  
 执行这些语句后，应用程序将从**SELECT**语句创建的结果集中提取行。 完成提取行后，它将调用**SQLMoreResults** ，使其可供 repriced 的部分使用。 如有必要， **SQLMoreResults**将丢弃 unfetched 行并关闭游标。 然后，应用程序调用**SQLRowCount**来确定**UPDATE**语句 repriced 的部分数量。  
  
 它是特定于驱动程序的，无论是否执行整个批处理语句，都可以使用任何结果。 在某些实现中，这种情况如下：在其他情况下，调用**SQLMoreResults**会触发批处理中下一条语句的执行。  
  
 如果批处理中的某个语句失败， **SQLMoreResults**将返回 SQL_ERROR 或 SQL_SUCCESS_WITH_INFO。 如果批处理在语句失败时中止，或失败语句是批处理中的最后一个语句，则**SQLMoreResults**将返回 SQL_ERROR。 如果在语句失败时未中止批处理，并且失败的语句不是批处理中的最后一个语句，则**SQLMoreResults**将返回 SQL_SUCCESS_WITH_INFO。 SQL_SUCCESS_WITH_INFO 指示至少生成一个结果集或计数，并且未中止该批。
