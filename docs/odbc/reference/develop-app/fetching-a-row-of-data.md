---
title: 提取数据行 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQLFetch function [ODBC], fetching a row of data
- cursors [ODBC], fetching rows
- result sets [ODBC], fetching
- fetches [ODBC], row of data
ms.assetid: 16d4a380-0d83-456b-aeee-f10738944e86
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 010d05990396c10836c0a2130e5d9f4392ae56ec
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/08/2020
ms.locfileid: "68069860"
---
# <a name="fetching-a-row-of-data"></a>提取数据的行
若要提取数据行，应用程序将调用**SQLFetch**。 可以使用任意类型的游标调用**SQLFetch** ，但它仅以只进方向移动行集游标。 **SQLFetch**使光标前进到下一行，并返回与对**SQLBindCol**的调用绑定的所有列的数据。 当光标到达结果集的末尾时， **SQLFetch**将返回 SQL_NO_DATA。 有关调用**SQLFetch**的示例，请参阅[使用 SQLBindCol](../../../odbc/reference/develop-app/using-sqlbindcol.md)。  
  
 确切地说，如何实现**SQLFetch**是特定于驱动程序的，但常规模式是驱动程序从数据源中检索任何绑定列的数据，根据绑定变量的类型来转换数据，并将转换后的数据放入这些变量。 如果驱动程序无法转换任何数据， **SQLFetch**将返回错误。 应用程序可以继续提取行，但当前行的数据将丢失。 未绑定列的数据所发生的情况取决于驱动程序，但大多数驱动程序要么检索并放弃它，要么根本不检索它。  
  
 驱动程序还设置已绑定的任何长度/指示器缓冲区的值。 如果列的数据值为 NULL，则驱动程序将相应的长度/指示器缓冲区设置为 SQL_NULL_DATA。 如果数据值不为 NULL，则驱动程序会在转换后将长度/指示器缓冲区设置为数据的字节长度。 如果无法确定此长度，则有时，对于多个函数调用检索的长数据，驱动程序会将长度/指示器缓冲区设置为 SQL_NO_TOTAL。 对于固定长度的数据类型，例如整数和日期结构，字节长度为数据类型的大小。  
  
 对于长度可变的数据（如字符和二进制数据），驱动程序会对照绑定到列的缓冲区的字节长度来检查转换后的数据的字节长度。缓冲区的长度在**SQLBindCol**的*BufferLength*参数中指定。 如果转换后的数据的字节长度大于缓冲区的字节长度，则驱动程序会截断数据，使其适合缓冲区，并返回长度/指示器缓冲区中的未截断长度，返回 SQL_SUCCESS_WITH_INFO，并将 SQLSTATE 01004 （数据截断）置于诊断中。 唯一的例外是，如果**SQLFetch**返回可变长度的书签，这将返回 SQLSTATE 22001 （字符串数据，右端被截断）。  
  
 固定长度的数据永远不会被截断，因为驱动程序假定绑定缓冲区的大小是数据类型的大小。 数据截断往往非常罕见，因为应用程序通常会将足够大的缓冲区绑定到足以保存整个数据值;它从元数据确定所需的大小。 但是，应用程序可能会将它知道的缓冲区显式绑定到过小。 例如，它可能会检索并显示部分说明的前20个字符或长文本列的前100个字符。  
  
 字符数据必须在返回到应用程序之前以 null 结尾（即使已被截断）。 Null 终止字符不包含在返回的字节长度中，但它需要绑定缓冲区中的空间。 例如，假设应用程序使用 ASCII 字符集中的字符数据组成的字符串，驱动程序包含50个要返回的数据，而应用程序的缓冲区长度为25个字节。 在应用程序的缓冲区中，驱动程序返回后跟 null 终止字符的前24个字符。 在长度/指示器缓冲区中，它返回的字节长度为50。  
  
 在执行创建结果集的语句之前，应用程序可以通过设置 SQL_ATTR_MAX_ROWS 语句特性来限制结果集中的行数。 例如，用于设置报表格式的应用程序中的预览模式只需要足够的数据来显示报表的第一页。 通过限制结果集的大小，可以更快地运行此类功能。 此语句属性旨在减少网络流量，并且可能不会受到所有驱动程序的支持。
