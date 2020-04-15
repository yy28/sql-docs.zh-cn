---
title: 相对和绝对滚动 |微软文档
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
ms.openlocfilehash: ae0ed5af8d116a3038b55b1e3d68231154c2a35c
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/14/2020
ms.locfileid: "81300097"
---
# <a name="relative-and-absolute-scrolling"></a>相对和绝对滚动
**SQLFetchScroll**中的大多数滚动选项将光标相对于当前位置或绝对位置的位置放置。 **SQLFetchScroll**支持提取下一个、先行、第一行和最后一个行集，以及相对提取（从当前行集的开头提取行*n*行）和绝对提取（从行*n*开始提取行集）。 如果*n*在绝对提取中为负数，则行将从结果集的末尾计数。 因此，行 -1 的绝对提取意味着获取以结果集中的最后一行开头的行集。  
  
 动态游标检测插入的结果集并从中删除的行，因此，除了从结果集的开头读取行之外，动态游标无法轻松检索行，这可能很慢。 此外，绝对提取在动态游标中不是很有用，因为行号会随着行的插入和删除而变化;因此，连续获取同一行号可以产生不同的行。  
  
 仅对其块游标功能（如报表）使用**SQLFetchScroll**的应用程序可能会通过结果集一次，仅使用该选项获取下一个行集。 另一方面，基于屏幕的应用程序可以利用**SQLFetchScroll**的所有功能。 如果应用程序将行集大小设置为屏幕上显示的行数，并将屏幕缓冲区绑定到结果集，则可以将滚动条操作直接转换为对**SQLFetchScroll**的调用。  
  
|滚动条操作|SQLFetchScroll 滚动选项|  
|--------------------------|-------------------------------------|  
|向上翻页|SQL_FETCH_PRIOR|  
|向下翻页|SQL_FETCH_NEXT|  
|向上移动一行|SQL_FETCH_RELATIVE*提取偏移*量等于 -1|  
|向下移动一行|SQL_FETCH_RELATIVE*提取偏移*等于 1|  
|顶部滚动框|SQL_FETCH_FIRST|  
|底部滚动框|SQL_FETCH_LAST|  
|滚动框位于随机位置|SQL_FETCH_ABSOLUTE|  
  
 此类应用程序还需要在滚动操作后定位滚动框，此操作需要当前行号和行数。 对于当前行号，应用程序可以跟踪当前行号，也可以使用SQL_ATTR_ROW_NUMBER属性调用**SQLGetStmtAttr**来检索它。  
  
 游标中的行数（结果集的大小）可作为诊断标头的SQL_DIAG_CURSOR_ROW_COUNT字段提供。 此字段中的值仅在调用**SQLExecute、SQLExecDirect**或**SQLMoreResult**后定义。 **SQLExecute** 此计数可以是近似计数或精确计数，具体取决于驱动程序的功能。 可以通过调用**SQLGetInfo**与游标属性信息类型并检查是否为游标类型返回SQL_CA2_CRC_APPROXIMATE位或SQL_CA2_CRC_EXACT位来确定驱动程序的支持。  
  
 动态游标从不支持确切的行计数。 对于其他类型的游标，驱动程序可以支持精确或近似行计数，但不能同时支持这两者。 如果驱动程序既不支持特定游标类型的精确行计数，也不支持近似行计数，则SQL_DIAG_CURSOR_ROW_COUNT字段包含到目前为止已提取的行数。 无论驱动程序支持什么，具有 SQL_FETCH_LAST*操作*的**SQLFetchScroll**都将导致SQL_DIAG_CURSOR_ROW_COUNT字段包含确切的行计数。
