---
title: 提取的数据行 |Microsoft 文档
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: odbc
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- SQLFetch function [ODBC], fetching a row of data
- cursors [ODBC], fetching rows
- result sets [ODBC], fetching
- fetches [ODBC], row of data
ms.assetid: 16d4a380-0d83-456b-aeee-f10738944e86
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: f70d67650f3a32f43f4663a744bf4e208cb766af
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
---
# <a name="fetching-a-row-of-data"></a>提取数据的行
若要提取的数据行，应用程序调用**SQLFetch**。 **SQLFetch**可以调用与任何类型的游标，但它仅会移动行集只进的方向。 **SQLFetch**将光标前进到下一行，并返回的数据绑定通过调用任何列**SQLBindCol**。 设置光标在到达结果的末尾， **SQLFetch**返回 SQL_NO_DATA。 有关调用的示例**SQLFetch**，请参阅[使用 SQLBindCol](../../../odbc/reference/develop-app/using-sqlbindcol.md)。  
  
 完全如何**SQLFetch**实现特定于驱动程序，但常规模式是，要为任何从数据源绑定列，将其类型的绑定变量，根据转换并将检索数据的驱动程序的这些变量中的已转换的数据。 如果该驱动程序不能将任何数据，转换**SQLFetch**返回错误。 应用程序可以继续执行提取行，但在当前行的数据将丢失。 未绑定的列的数据会发生什么情况取决于该驱动程序，但大多数驱动程序检索并放弃它或永远不会在所有检索它。  
  
 该驱动程序还将设置的值已绑定任何长度/指示器缓冲区。 如果列的数据值为 NULL，该驱动程序会将相应的长度/指示器缓冲区设置为 SQL_NULL_DATA。 如果数据值不为 NULL，驱动程序将设置长度/指示器缓冲区的字节长度的数据转换后。 如果无法确定此长度，因为有时是将检索的多个函数调用的长整型数据这种情况，该驱动程序会将长度/指示器缓冲区设置为 SQL_NO_TOTAL。 对于固定长度的数据类型，如整数和日期结构的字节长度为数据类型的大小。  
  
 对于可变长度数据，例如字符和二进制数据，该驱动程序会检查转换的数据对绑定到列; 缓冲区的字节长度的字节长度在指定的缓冲区长度*BufferLength*中的参数**SQLBindCol**。 如果大于缓冲区的字节长度的字节长度的转换的数据，该驱动程序将截断数据缓冲区中容纳不下，则返回长度/指示器缓冲区中的未截断的长度返回 SQL_SUCCESS_WITH_INFO，并将放 SQLSTATE 01004 （数据已截断） 诊断程序中。 唯一的例外是返回时将被截断的可变长度书签**SQLFetch**，它返回 SQLSTATE 22001 （字符串数据，右截断）。  
  
 固定长度的数据永远不会被截断，因为该驱动程序假定绑定的缓冲区的大小是数据类型的大小。 数据截断往往是少见，因为应用程序通常绑定的缓冲区大小不足以容纳整个数据值;它确定从元数据所需要的大小。 但是，应用程序可能显式绑定它知道得太小的缓冲区。 例如，它可能会检索并显示部分描述的前 20 个字符或长文本列的前 100 个字符。  
  
 字符数据必须由驱动程序以 null 结尾之前它将返回到应用程序，即使它已被截断。 Null 终止字符不包括在返回的字节长度，但需要绑定的缓冲区中的空间。 例如，假设应用程序使用字符串组成的 ASCII 字符集中的字符数据、 驱动程序包含 50 个字符的数据，若要返回，且应用程序的缓冲区是长度为 25 个字节。 在应用程序的缓冲区，该驱动程序返回 null 终止字符后跟第一次 24 个字符。 在长度/指示器缓冲区，该命令返回的字节长度为 50。  
  
 应用程序可以限制的结果集通过执行语句，以创建结果设置之前设置 SQL_ATTR_MAX_ROWS 语句属性中的行数。 例如，应用程序用于设置格式的报表中的预览模式需要仅数据不足，无法显示报表的第一页。 通过限制结果集的大小，这类功能将运行得更快。 此语句属性并不用于减少网络流量，并且可能不支持的所有驱动程序。
