---
description: 相对和绝对滚动
title: 相对和绝对滚动 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- absolute scrolling [ODBC]
- relative scrolling [ODBC]
- scrollable cursors [ODBC]
- cursors [ODBC], scrollable
ms.assetid: 3d0ff48d-fef5-4c01-bb1d-a583e6269b66
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 6c7471e7ee245d9cf70adc8c3453705453bc1aac
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/17/2020
ms.locfileid: "88482939"
---
# <a name="relative-and-absolute-scrolling"></a>相对和绝对滚动
**SQLFetchScroll**中的大部分滚动选项将光标相对于当前位置或绝对位置定位。 **SQLFetchScroll** 支持提取下一个、以前的、第一个和最后一个行集，以及 (从当前行集的开头提取行集 *n* 行) 和绝对提取 (从第 *n* 行开始) 提取行集。 如果在绝对提取中 *n* 为负，则从结果集的末尾开始对行进行计数。 因此，第1行的绝对提取意味着提取从结果集中的最后一行开始的行集。  
  
 动态游标检测从结果集插入和删除的行，因此，动态游标不能简单地在从结果集开头开始读取的特定数字上检索行，这可能会很慢。 此外，绝对提取在动态游标中并不十分有用，因为行号会随着行的插入和删除而更改;因此，连续提取同一行号可能会产生不同的行。  
  
 仅对其块游标功能（如报表）使用 **SQLFetchScroll** 的应用程序可能只使用用于提取下一个行集的选项传递结果集。 另一方面，基于屏幕的应用程序可以利用 **SQLFetchScroll**的所有功能。 如果应用程序将行集大小设置为屏幕上显示的行数，并将屏幕缓冲区绑定到结果集，则可以直接将滚动条操作转换为对 **SQLFetchScroll**的调用。  
  
|滚动条操作|SQLFetchScroll 滚动选项|  
|--------------------------|-------------------------------------|  
|向上翻页|SQL_FETCH_PRIOR|  
|向下翻页|SQL_FETCH_NEXT|  
|向上移动一行|*FetchOffset*等于-1 的 SQL_FETCH_RELATIVE|  
|向下移动一行|*FetchOffset*等于1的 SQL_FETCH_RELATIVE|  
|顶部滚动框|SQL_FETCH_FIRST|  
|滚动框位于底部|SQL_FETCH_LAST|  
|滚动框位于随机位置|SQL_FETCH_ABSOLUTE|  
  
 此类应用程序还需要在滚动操作之后定位滚动框，这需要当前行号和行数。 对于当前行号，应用程序可以跟踪当前行号或调用 SQL_ATTR_ROW_NUMBER **SQLGetStmtAttr** 属性来检索它。  
  
 游标中的行数是结果集的大小，作为诊断标头的 SQL_DIAG_CURSOR_ROW_COUNT 字段提供。 此字段中的值仅在调用 **SQLExecute**、 **SQLExecDirect**或 **SQLMoreResult** 后定义。 此计数可以是大约计数，也可以是精确计数，具体取决于驱动程序的功能。 可以通过使用游标属性信息类型调用 **SQLGetInfo** 并检查是否为游标类型返回 SQL_CA2_CRC_APPROXIMATE 或 SQL_CA2_CRC_EXACT 位来确定驱动程序的支持。  
  
 动态游标从不支持确切的行计数。 对于其他类型的游标，驱动程序可以支持精确行计数或大概行计数，但不能同时支持两者。 如果驱动程序既不支持特定游标类型的确切行计数，也不支持估计行计数，则 "SQL_DIAG_CURSOR_ROW_COUNT" 字段将包含到目前为止已提取的行数。 无论驱动程序支持哪个驱动程序， **SQLFetchScroll** 的 SQL_FETCH_LAST *操作* 都将导致 SQL_DIAG_CURSOR_ROW_COUNT 字段包含确切的行计数。
