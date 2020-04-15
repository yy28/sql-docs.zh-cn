---
title: 获取一行数据 |微软文档
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: a702f561b756d5305020df9f015d3ea4b444caa6
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/14/2020
ms.locfileid: "81305668"
---
# <a name="fetching-a-row-of-data"></a>提取数据的行
要获取一行数据，应用程序调用**SQLFetch**。 **SQLFetch**可以使用任何类型的游标调用，但它仅向前移动行集游标。 **SQLFetch**将光标推进到下一行，并返回与**SQLBindCol**调用绑定的任何列的数据。 当光标到达结果集的末尾时 **，SQLFetch**将返回SQL_NO_DATA。 有关调用**SQLFetch**的示例，请参阅[使用 SQLBindCol](../../../odbc/reference/develop-app/using-sqlbindcol.md)。  
  
 **SQLFetch**的实现方式正是特定于驱动程序的，但一般模式是驱动程序从数据源检索任何绑定列的数据，根据绑定变量的类型进行转换，并将转换后的数据放在这些变量中。 如果驱动程序无法转换任何数据 **，SQLFetch**将返回一个错误。 应用程序可以继续提取行，但当前行的数据将丢失。 未绑定列的数据会发生什么情况取决于驱动程序，但大多数驱动程序要么检索并丢弃它，要么根本不检索它。  
  
 驱动程序还设置已绑定的任何长度/指示器缓冲区的值。 如果列的数据值为 NULL，则驱动程序将相应的长度/指示器缓冲区设置为SQL_NULL_DATA。 如果数据值不是 NULL，驱动程序将长度/指示器缓冲区设置为转换后数据的字节长度。 如果无法确定此长度（有时对于由多个函数调用检索的长数据的情况），驱动程序会将长度/指示器缓冲区设置为SQL_NO_TOTAL。 对于固定长度数据类型（如整数和日期结构），字节长度是数据类型的大小。  
  
 对于变量长度数据（如字符和二进制数据），驱动程序根据绑定到列的缓冲区的字节长度检查转换数据的字节长度;缓冲区的长度在**SQLBindCol**中的*缓冲区长度*参数中指定。 如果转换数据的字节长度大于缓冲区的字节长度，驱动程序会截断以放入缓冲区的数据，返回长度/指示器缓冲区中的未压缩长度，返回SQL_SUCCESS_WITH_INFO，并将 SQLSTATE 01004（数据截断）置于诊断中。 唯一的例外是，如果**SQLFetch**返回时截断可变长度书签，它返回 SQLSTATE 22001（字符串数据，右截断）。  
  
 固定长度数据永远不会被截断，因为驱动程序假定绑定缓冲区的大小是数据类型的大小。 数据截断往往很少见，因为应用程序通常绑定足够大的缓冲区来保存整个数据值;它确定元数据中的必要大小。 但是，应用程序可能会显式绑定它知道太小的缓冲区。 例如，它可能会检索和显示零件说明的前 20 个字符或长文本列的前 100 个字符。  
  
 字符数据必须由驱动程序在返回到应用程序之前为 null 终止，即使已截断。 返回的字节长度中不包括空终止字符，但确实需要绑定缓冲区中的空格。 例如，假设应用程序使用由 ASCII 字符集中的字符数据组成的字符串，驱动程序有 50 个字符的数据要返回，并且应用程序的缓冲区是 25 字节长。 在应用程序的缓冲区中，驱动程序返回前 24 个字符，后跟一个空终止字符。 在长度/指示器缓冲区中，它返回字节长度为 50。  
  
 应用程序可以通过在执行创建结果集的语句之前设置SQL_ATTR_MAX_ROWS语句属性来限制结果集中的行数。 例如，用于设置报表格式的应用程序中的预览模式只需要足够的数据来显示报表的第一页。 通过限制结果集的大小，此类功能将运行得更快。 此语句属性旨在减少网络流量，并且可能不受所有驱动程序的支持。
