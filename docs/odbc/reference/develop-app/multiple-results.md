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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 47e1250a92b78aefdc1611fd88e0ee9b0f772ad0
ms.sourcegitcommit: 2429fbcdb751211313bd655a4825ffb33354bda3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/28/2018
ms.locfileid: "52539904"
---
# <a name="multiple-results"></a>多个结果
一个*结果*内容过后未返回数据源执行的语句。 ODBC 具有两种类型的结果： 结果集和行计数。 *行计数*的更新，受影响的行数删除，或 insert 语句。 批处理中所述[SQL 语句的批处理](../../../odbc/reference/develop-app/batches-of-sql-statements.md)，可以生成多个结果。  
  
 下表列出**SQLGetInfo**应用程序使用以确定数据源是否返回每种不同类型的批处理的多个结果的选项。 具体而言，数据源可以返回整个批处理语句的单个行计数或单独的行计数为批处理中每个语句。 结果集生成执行的语句使用的参数数组，对于数据源可以返回单个结果集，对所有组的参数或各自的结果集的每组参数。  
  
|批处理类型|行计数|结果集|  
|----------------|----------------|-----------------|  
|显式批处理|SQL_BATCH_ROW_COUNT [a]|-[b]。|  
|过程|SQL_BATCH_ROW_COUNT [a]|-[b]。|  
|参数的数组|SQL_PARAM_ARRAYS_ROW_COUNTS|SQL_PARAM_ARRAYS_SELECTS|  
  
 [a] 行计数生成批处理中的语句可能受支持，但返回的行计数不受支持。 中的 SQL_BATCH_SUPPORT 选项**SQLGetInfo**指示行计数生成语句批处理中允许是否; SQL_BATCH_ROW_COUNTS 选项指示这些行计数返回到应用程序。  
  
 [b] 显式批处理和过程始终返回多个结果集时它们包括多个结果集生成语句。  
  
> [!NOTE]  
>  ODBC 1.0 中引入的 SQL_MULT_RESULT_SETS 选项提供了有关是否可以返回多个结果集仅常规信息。 具体而言，它设置为"Y"为 SQL_BATCH_SUPPORT 返回 SQL_BS_SELECT_EXPLICIT 或 SQL_BS_SELECT_PROC 位是否为 SQL_PARAM_ARRAYS_SELECT 返回 SQL_PAS_BATCH。  
  
 若要处理多个结果，应用程序调用**SQLMoreResults**。 此函数将放弃当前结果并提供下一个结果。 没有更多结果不可用时，其返回 sql_no_data 为止。 例如，假设以批形式执行以下语句：  
  
```  
SELECT * FROM Parts WHERE Price > 100.00;  
UPDATE Parts SET Price = 0.9 * Price WHERE Price > 100.00  
```  
  
 执行这些语句后，会在应用程序创建的结果集提取行**选择**语句。 完成提取行后，它将调用**SQLMoreResults**提供了 repriced 的部分数。 如果有必要，请**SQLMoreResults**放弃的行会并关闭游标。 然后，应用程序调用**SQLRowCount**来确定多少个部分通过 repriced**更新**语句。  
  
 它是特定于驱动程序的任何结果之前是否执行整个批处理语句。 在某些实现中，这是区分大小写;其他情况下，调用**SQLMoreResults**触发批处理中的下一个语句执行。  
  
 如果一个批处理中语句失败， **SQLMoreResults**将返回 SQL_ERROR 或 SQL_SUCCESS_WITH_INFO。 如果批处理已中止，语句失败或失败的语句是批处理中的最后一个语句时**SQLMoreResults**将返回 SQL_ERROR。 如果批处理没有中止时，语句失败，失败的语句是批处理中的最后一个语句**SQLMoreResults**将返回 SQL_SUCCESS_WITH_INFO。 Sql_success_with_info 以指示已生成至少一个结果集或计数和没有中止批处理。
