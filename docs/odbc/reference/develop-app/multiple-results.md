---
title: 多个结果 |Microsoft 文档
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- SQLMoreResults function [ODBC], multiple results
- row counts [ODBC]
- multiple results [ODBC]
- result sets [ODBC], multiple results
- SQLGetInfo function [ODBC], multiple results
ms.assetid: a3c32e4b-8fe7-4a33-ae39-ae664001f315
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: be6cb4a2f7f03e63e3da9345b833b0382edd8e9d
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
---
# <a name="multiple-results"></a>多个结果
A*结果*是内容的源返回的数据后执行的语句。 ODBC 具有两种类型的结果： 结果集和行计数。 *行计数*被删除，或 insert 语句的更新，受影响的行数。 批中所述[SQL 语句的批处理](../../../odbc/reference/develop-app/batches-of-sql-statements.md)，可以生成多个结果。  
  
 下表列出**SQLGetInfo**应用程序使用以确定数据源是否返回的每个不同类型的批处理的多个结果的选项。 具体而言，数据源可以返回整个批处理语句的单个行计数或单独的行计数为批处理中每个语句。 对于结果集生成执行的语句与参数的数组，数据源可以返回单个结果集，对所有组的参数或个别结果设置为每个参数集。  
  
|批处理类型|行计数|结果集|  
|----------------|----------------|-----------------|  
|显式批处理|SQL_BATCH_ROW_COUNT [a]|-[b]。|  
|过程|SQL_BATCH_ROW_COUNT [a]|-[b]。|  
|参数数组|SQL_PARAM_ARRAYS_ROW_COUNTS|SQL_PARAM_ARRAYS_SELECTS|  
  
 不支持生成计数-在批处理中的语句可能受支持，[a] 行尚未返回的行计数。 中的 SQL_BATCH_SUPPORT 选项**SQLGetInfo**指示在批处理中允许是否行生成计数 – 语句; SQL_BATCH_ROW_COUNTS 选项指示是否对应用程序返回这些行计数。  
  
 [b] 显式批处理和过程始终返回多个结果集时它们包括多个结果集生成语句。  
  
> [!NOTE]  
>  ODBC 1.0 中引入的 SQL_MULT_RESULT_SETS 选项提供有关是否可以返回多个结果集仅常规信息。 具体而言，它设置为"Y"为 SQL_BATCH_SUPPORT 返回 SQL_BS_SELECT_EXPLICIT 或 SQL_BS_SELECT_PROC bits 是否为 SQL_PARAM_ARRAYS_SELECT 返回 SQL_PAS_BATCH。  
  
 若要处理多个结果，应用程序调用**SQLMoreResults**。 此函数将放弃当前结果，并提供下一个结果。 没有更多结果不可用时，它返回 SQL_NO_DATA。 例如，假设以下语句作为批处理命令执行：  
  
```  
SELECT * FROM Parts WHERE Price > 100.00;  
UPDATE Parts SET Price = 0.9 * Price WHERE Price > 100.00  
```  
  
 这些语句将执行后，会应用程序创建的结果集获取行**选择**语句。 当完成提取行后时，它将调用**SQLMoreResults**要提供的已 repriced 的部分数。 如有必要， **SQLMoreResults**放弃的行会并关闭光标。 然后，应用程序调用**SQLRowCount**以确定多少个部分已由 repriced**更新**语句。  
  
 它是特定于驱动程序的任何结果可使用之前是否执行整个批处理语句。 在某些实现中，这种情况;其他情况下，调用**SQLMoreResults**触发的批次中的下一个语句执行。  
  
 如果其中一个批处理中的语句失败， **SQLMoreResults**将返回 SQL_ERROR 或 SQL_SUCCESS_WITH_INFO。 如果批处理已中止，语句失败或失败的语句的批处理中的最后一个语句时**SQLMoreResults**将返回 SQL_ERROR。 如果批处理没有中止时，语句失败而失败的语句没有批处理中的最后一个语句**SQLMoreResults**将返回 SQL_SUCCESS_WITH_INFO。 SQL_SUCCESS_WITH_INFO 指示生成至少一个结果集或计数，并且没有中止批处理。
