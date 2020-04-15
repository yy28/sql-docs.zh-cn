---
title: 多个结果 |微软文档
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
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/14/2020
ms.locfileid: "81302406"
---
# <a name="multiple-results"></a>多个结果
*结果是*执行语句后数据源返回的内容。 ODBC 有两种类型的结果：结果集和行计数。 *行计数*是受更新、删除或插入语句影响的行数。 批处理（在[SQL 语句的批处理](../../../odbc/reference/develop-app/batches-of-sql-statements.md)中描述）可以生成多个结果。  
  
 下表列出了应用程序用于确定数据源是否返回每种不同类型的批处理的多个结果的**SQLGetInfo**选项。 特别是，数据源可以为批处理中的每个语句返回整个语句的单个行计数或单个行计数。 对于使用参数数组执行的结果集生成语句，数据源可以为每个参数集返回一个结果集或每个参数集的单个结果集。  
  
|批次类型|行计数|结果集|  
|----------------|----------------|-----------------|  
|显式批处理|SQL_BATCH_ROW_COUNT[a]|--[b]|  
|过程|SQL_BATCH_ROW_COUNT[a]|--[b]|  
|参数数组|SQL_PARAM_ARRAYS_ROW_COUNTS|SQL_PARAM_ARRAYS_SELECTS|  
  
 [a] 批处理中的行计数生成语句可能受支持，但不支持行计数的返回。 **SQLGetInfo**中的SQL_BATCH_SUPPORT选项指示是否允许批量生成行计数语句;因此，是否允许批量生成行计数语句。SQL_BATCH_ROW_COUNTS选项指示是否将这些行计数返回到应用程序。  
  
 [b] 显式批处理和过程在包含多个结果集生成语句时始终返回多个结果集。  
  
> [!NOTE]  
>  ODBC 1.0 中引入的SQL_MULT_RESULT_SETS选项仅提供有关是否可以返回多个结果集的一般信息。 特别是，如果返回SQL_BS_SELECT_EXPLICIT位或SQL_BS_SELECT_PROC位以SQL_BATCH_SUPPORT，或者返回SQL_PAS_BATCH以SQL_PARAM_ARRAYS_SELECT，则设置为"Y"。  
  
 要处理多个结果，应用程序调用**SQLMore 结果**。 此函数放弃当前结果，并使下一个结果可用。 当没有更多结果可用时，它将返回SQL_NO_DATA。 例如，假设以下语句作为批处理执行：  
  
```  
SELECT * FROM Parts WHERE Price > 100.00;  
UPDATE Parts SET Price = 0.9 * Price WHERE Price > 100.00  
```  
  
 执行这些语句后，应用程序将从**SELECT**语句创建的结果集中提取行。 提取行后，它将调用**SQLMore结果**以提供重新定价的零件数。 如有必要 **，SQLMore结果**将丢弃未提取的行并关闭游标。 然后，应用程序调用**SQLRowCount**以确定**更新**语句重新定价了多少部件。  
  
 在任何结果可用之前是否执行整个批处理语句，都是特定于驱动程序的。 在某些实现中，情况就是这样;在另一些操作中，调用**SQLMore 结果**会触发批处理中下一个语句的执行。  
  
 如果批处理中的一个语句失败 **，SQLMore 结果**将返回SQL_ERROR或SQL_SUCCESS_WITH_INFO。 如果当语句失败时批处理中止，或者失败语句是批处理中的最后一个语句 **，SQLMore结果**将返回SQL_ERROR。 如果当语句失败且失败语句不是批处理中的最后一个语句时批处理未中止 **，SQLMore 结果**将返回SQL_SUCCESS_WITH_INFO。 SQL_SUCCESS_WITH_INFO指示至少生成了一个结果集或计数，并且批处理未中止。
