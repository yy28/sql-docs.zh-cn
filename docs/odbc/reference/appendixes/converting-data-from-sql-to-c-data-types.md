---
title: 将数据从 SQL 转换为 C 数据类型 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- data conversions from SQL to C types [ODBC]
- data conversions from SQL to C types [ODBC], about converting
- data types [ODBC], C data types
- data types [ODBC], converting data
- data types [ODBC], SQL data types
- SQL data types [ODBC], converting to C types
- converting data from SQL to c types [ODBC]
- converting data from SQL to c types [ODBC], about converting
- C data types [ODBC], converting from SQL types
ms.assetid: 029727f6-d3f0-499a-911c-bcaf9714e43b
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 95a44698c12abf0de64c8d6f7d316e9156dc139c
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/15/2019
ms.locfileid: "68019115"
---
# <a name="converting-data-from-sql-to-c-data-types"></a>将数据从 SQL 转换为 C 数据类型
当应用程序调用**SQLFetch**， **SQLFetchScroll**，或**SQLGetData**，驱动程序从数据源检索数据。 如果有必要，它将数据从转换中的驱动程序在检索到指定的数据类型的数据类型*TargetType*中的参数**SQLBindCol**或**SQLGetData。** 最后，它将数据存储在指向的位置*TargetValuePtr*中的参数**SQLBindCol**或**SQLGetData** （和 ARD SQL_DESC_DATA_PTR 字段）。  
  
 下表显示支持的从 ODBC SQL 转换到 ODBC C 数据类型的数据类型。 实心的圆表示默认值转换为 SQL 数据类型 (数据将转换成时的 C 数据类型的值*TargetType*为 SQL_C_DEFAULT)。 空心圆表示支持的转换。  
  
 用于 ODBC *3.x*应用程序使用 ODBC *2.x*驱动程序，从特定于驱动程序的数据类型可能不受支持的转换。  
  
 转换后的数据的格式不受 Windows® 国家/地区设置。  
  
 以下各节中的表介绍驱动程序或数据源将数据从数据源; 检索到的转换支持所有 ODBC C 数据类型从它们支持的 ODBC SQL 数据类型的转换所需的驱动程序。 对于给定的 ODBC SQL 数据类型，第一列的表列出了合法的输入的值*TargetType*中的参数**SQLBindCol**并**SQLGetData**。 第二列列出了通常使用的测试结果*BufferLength*中指定的参数**SQLBindCol**或**SQLGetData**，该驱动程序执行到确定是否可以将转换数据。 对于每个结果的第三个和第四个列列出放置在指定的缓冲区中的值*TargetValuePtr*并*StrLen_or_IndPtr*中指定的参数**SQLBindCol**或**SQLGetData**驱动程序已尝试将数据转换之后。 ( *StrLen_or_IndPtr*参数对应于 ARD 的 SQL_DESC_OCTET_LENGTH_PTR 字段。)最后一列列出了为每个得到的结果返回的 SQLSTATE **SQLFetch**， **SQLFetchScroll**，或**SQLGetData**。  
  
 如果*TargetType*中的参数**SQLBindCol**或**SQLGetData**包含未显示对于给定的 ODBC SQL 数据类型，表中的 ODBC C 数据类型的标识符**SQLFetch**， **SQLFetchScroll**，或**SQLGetData**返回 SQLSTATE 07006 （受限制的数据类型属性冲突）。 如果*TargetType*参数中包含的指定从特定于驱动程序的 SQL 数据类型转换为 ODBC C 数据类型的标识符和驱动程序，不支持此转换**SQLFetch**，**SQLFetchScroll**，或**SQLGetData**返回 SQLSTATE HYC00 （未实现的可选功能）。  
  
 尽管它不会显示表中，但驱动程序将在指定的缓冲区中返回 SQL_NULL_DATA *StrLen_or_IndPtr*时 SQL 数据值为 NULL 的参数。 有关使用的说明*StrLen_or_IndPtr*当进行多个调用时检索数据，请参阅[SQLGetData](../../../odbc/reference/syntax/sqlgetdata-function.md)函数说明。 字符计数时，SQL 数据转换为字符 C 数据，以返回\* *StrLen_or_IndPtr*不包括 null 终止字节。 如果*TargetValuePtr*为 null 指针**SQLGetData**返回 SQLSTATE HY009 （null 指针的使用无效）; 在**SQLBindCol**，这将解除绑定列。  
  
 表中使用以下术语和约定：  
  
-   **数据的字节长度**是 C 数据可用于在返回的字节数 **TargetValuePtr*、 是否返回到应用程序之前，数据将被截断。 对于字符串数据，这不包括 null 终止字符的空间。  
  
-   **字符字节长度**是以字符格式显示数据所需的字节总数。 这是为每个 C 数据类型的部分中定义的一样[显示大小](../../../odbc/reference/appendixes/display-size.md)，只不过字符字节长度是以字节为单位，而显示大小是以字符为单位。  
  
-   中的词*斜体*表示函数自变量或 SQL 语法元素。 为语法元素的语法，请参阅[附录 c:SQL 语法](../../../odbc/reference/appendixes/appendix-c-sql-grammar.md)。  
  
 本部分包含以下主题。  
  
-   [从 SQL 到 c:字符](../../../odbc/reference/appendixes/sql-to-c-character.md)  
  
-   [从 SQL 到 c:数值](../../../odbc/reference/appendixes/sql-to-c-numeric.md)  
  
-   [从 SQL 到 c:位](../../../odbc/reference/appendixes/sql-to-c-bit.md)  
  
-   [从 SQL 到 c:二进制文件](../../../odbc/reference/appendixes/sql-to-c-binary.md)  
  
-   [从 SQL 到 c:日期](../../../odbc/reference/appendixes/sql-to-c-date.md)  
  
-   [从 SQL 到 c:GUID](../../../odbc/reference/appendixes/sql-to-c-guid.md)  
  
-   [从 SQL 到 c:时间](../../../odbc/reference/appendixes/sql-to-c-time.md)  
  
-   [从 SQL 到 c:时间戳](../../../odbc/reference/appendixes/sql-to-c-timestamp.md)  
  
-   [从 SQL 到 c:年月间隔](../../../odbc/reference/appendixes/sql-to-c-year-month-intervals.md)  
  
-   [从 SQL 到 c:日期时间间隔](../../../odbc/reference/appendixes/sql-to-c-day-time-intervals.md)  
  
-   [从 SQL 到 C 的数据转换示例](../../../odbc/reference/appendixes/sql-to-c-data-conversion-examples.md)
