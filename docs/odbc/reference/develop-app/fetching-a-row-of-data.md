---
title: 正在提取数据行 |Microsoft Docs
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
manager: craigg
ms.openlocfilehash: 012e454d03a0eb4ad16095353351d67e50d9586a
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/01/2018
ms.locfileid: "47792807"
---
# <a name="fetching-a-row-of-data"></a>提取数据的行
若要提取的数据行，应用程序调用**SQLFetch**。 **SQLFetch**可以调用与任何类型的游标，但它仅会移动行集只进的方向。 **SQLFetch**将光标前进到下一行，并返回调用绑定所有列的数据**SQLBindCol**。 光标在到达最终结果的设置，请**SQLFetch**返回 sql_no_data 为止。 例如，调用**SQLFetch**，请参阅[使用 SQLBindCol](../../../odbc/reference/develop-app/using-sqlbindcol.md)。  
  
 精确**SQLFetch**实现是特定于驱动程序，但常规模式是，若要检索的数据的任何列绑定从数据源，将其根据绑定变量的类型转换并将该驱动程序在这些变量的已转换的数据。 如果该驱动程序不能将任何数据，转换**SQLFetch**返回错误。 应用程序可以继续提取行，但当前行数据都将丢失。 未绑定列的数据会发生什么情况取决于该驱动程序，但大多数驱动程序检索，放弃它或者永远不会在所有检索它。  
  
 驱动程序还将设置都已绑定任何长度/指示器缓冲区的值。 如果列的数据值为 NULL，驱动程序会将相应的长度/指示器缓冲区设置为 SQL_NULL_DATA。 如果数据值不为 NULL，驱动程序将设置的长度/指示器缓冲区的字节长度的数据的转换后。 如果此长度不能确定，因为有时是由多个函数调用检索的长整型数据与这种情况，该驱动程序将设置为 SQL_NO_TOTAL 长度/指示器缓冲区。 对于固定长度的数据类型，如整数和日期结构的字节长度是数据类型的大小。  
  
 对于可变长度数据，例如字符和二进制数据的驱动程序检查转换后的数据对绑定到列; 的缓冲区的字节长度的字节长度在指定缓冲区的长度*BufferLength*中的参数**SQLBindCol**。 如果转换后的数据的字节长度大于缓冲区的字节长度，该驱动程序将截断数据缓冲区中容纳不下，则返回长度/指示器缓冲区中的未截断的长度返回 SQL_SUCCESS_WITH_INFO，并将放 SQLSTATE 01004 （数据已截断） 诊断中。 唯一的例外是返回时，如果截断长度可变的书签**SQLFetch**，这会返回 SQLSTATE 22001 （字符串数据，右端被截断）。  
  
 固定长度的数据永远不会被截断，因为驱动程序假定绑定的缓冲区的大小是数据类型的大小。 数据截断往往很少见，因为应用程序通常将绑定的缓冲区大小不足以容纳整个数据值;它确定从元数据所需大小。 但是，应用程序可能显式绑定它知道得太小的缓冲区。 例如，它可能会检索并显示一部分说明的前 20 个字符或长文本列的前 100 个字符。  
  
 字符数据必须由驱动程序以 null 结尾之前它将返回到应用程序，即使它已被截断。 Null 终止字符未包含在返回的字节长度，但需要绑定的缓冲区中的空间。 例如，假设应用程序使用字符串组成的 ASCII 字符集中的字符数据、 驱动程序包含 50 个字符的数据，若要返回，且应用程序的缓冲区是 25 个字节。 在应用程序的缓冲区中的驱动程序将返回 null 终止字符后跟第一次 24 个字符。 在长度/指示器缓冲区，它将返回字节长度为 50。  
  
 应用程序可以限制结果集通过执行语句，创建结果集之前设置 SQL_ATTR_MAX_ROWS 语句属性中的行数。 例如，用于设置格式的报表的应用程序中的预览模式下需要仅数据不足，无法显示报表的第一页。 通过限制结果集的大小，此类功能会更快地运行。 此语句属性用于减少网络流量，并且可能不支持的所有驱动程序。
