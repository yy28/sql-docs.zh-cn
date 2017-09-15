---
title: "将数据从 SQL 转换为 C 数据类型 |Microsoft 文档"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
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
caps.latest.revision: 7
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 8fae054b572cb0d61299781d67adc0038afa9a97
ms.contentlocale: zh-cn
ms.lasthandoff: 09/09/2017

---
# <a name="converting-data-from-sql-to-c-data-types"></a>将数据从 SQL 转换为 C 数据类型
在应用程序调用**SQLFetch**， **SQLFetchScroll**，或**SQLGetData**，驱动程序从数据源检索数据。 如果有必要，它将数据从转换中的驱动程序检索到到由指定的数据类型的数据类型*TargetType*中的参数**SQLBindCol**或**SQLGetData。** 最后，它指向的位置中存储数据时*TargetValuePtr*中的参数**SQLBindCol**或**SQLGetData** （和 ARD SQL_DESC_DATA_PTR 字段）。  
  
 下表显示从 ODBC SQL 的支持的转换到 ODBC C 数据类型的数据类型。 实心的圆圈指示默认值转换为 SQL 数据类型 (向其数据将转换时的 C 数据类型的值*TargetType*是 SQL_C_DEFAULT)。 空心圆指示支持的转换。  
  
 ODBC 3*.x*应用程序使用 ODBC 2。*x*驱动程序，从特定于驱动程序的数据可能不支持类型转换。  
  
 转换后的数据的格式不受 Windows® 国家/地区设置。  
  
 下列各节中的表描述了在驱动程序或数据源将从数据源，则检索数据的转换支持所有 ODBC C 数据类型从它们支持 ODBC SQL 数据类型的转换所需驱动程序。 对于给定的 ODBC SQL 数据类型，表的第一列中列出的合法的输入的值*TargetType*中的参数**SQLBindCol**和**SQLGetData**。 第二个列还列出了通常使用的测试的结果*BufferLength*中指定的自变量**SQLBindCol**或**SQLGetData**，该驱动程序执行到确定是否它可以将数据转换。 对于每个结果，第三个和第四个列列出放置在由指定的缓冲区的值*TargetValuePtr*和*StrLen_or_IndPtr*中指定自变量**SQLBindCol**或**SQLGetData**驱动程序已尝试将数据转换之后。 ( *StrLen_or_IndPtr*参数对应于的 ARD SQL_DESC_OCTET_LENGTH_PTR 字段。)最后一列列出了为每个结果的返回 SQLSTATE **SQLFetch**， **SQLFetchScroll**，或**SQLGetData**。  
  
 如果*TargetType*中的参数**SQLBindCol**或**SQLGetData**包含对于给定的 ODBC SQL 数据类型，表中不显示 ODBC C 数据类型的标识符**SQLFetch**， **SQLFetchScroll**，或**SQLGetData**返回 SQLSTATE 07006 （受限制的数据类型属性冲突）。 如果*TargetType*参数包含指定从特定于驱动程序的 SQL 数据类型转换为 ODBC C 数据类型的标识符和驱动程序，不支持此转换**SQLFetch**，**SQLFetchScroll**，或**SQLGetData**返回 SQLSTATE HYC00 （未实现的可选功能）。  
  
 尽管它不会显示在表中，该驱动程序返回指定的缓冲区中的 SQL_NULL_DATA *StrLen_or_IndPtr* SQL 数据值时 NULL 的参数。 有关使用说明*StrLen_or_IndPtr*当进行多个调用来检索数据，请参阅[SQLGetData](../../../odbc/reference/syntax/sqlgetdata-function.md)函数说明。 当 SQL 数据转换为字符 C 数据时，在中返回的字符计数\* *StrLen_or_IndPtr*不包括 null 终止字节。 如果*TargetValuePtr*是 null 指针， **SQLGetData**返回 SQLSTATE HY009 （不允许使用 null 指针）; 在**SQLBindCol**，这解除绑定列。  
  
 表中使用以下术语和约定：  
  
-   **数据的字节长度**是可用于返回中的 C 数据的字节数 **TargetValuePtr*无论之前它将返回到应用程序的数据将被截断。 对于字符串数据，这不包括 null 终止字符的空间。  
  
-   **字符字节长度**是以字符格式显示数据所需的字节总数。 这是因为每个 C 数据类型的部分中定义[显示大小](../../../odbc/reference/appendixes/display-size.md)，只不过字符字节长度是以字节为单位，而显示大小是以字符为单位。  
  
-   在指定的词*斜体*表示函数自变量或 SQL 语法的元素。 有关语法元素的语法，请参阅[附录 c: SQL 语法](../../../odbc/reference/appendixes/appendix-c-sql-grammar.md)。  
  
 本部分包含以下主题。  
  
-   [为 c： 字符的 SQL](../../../odbc/reference/appendixes/sql-to-c-character.md)  
  
-   [SQL 为 c： 数字](../../../odbc/reference/appendixes/sql-to-c-numeric.md)  
  
-   [为 c： 位的 SQL](../../../odbc/reference/appendixes/sql-to-c-bit.md)  
  
-   [为 c： 二进制 SQL](../../../odbc/reference/appendixes/sql-to-c-binary.md)  
  
-   [到 c： 日期的 SQL](../../../odbc/reference/appendixes/sql-to-c-date.md)  
  
-   [为 c: GUID 的 SQL](../../../odbc/reference/appendixes/sql-to-c-guid.md)  
  
-   [为 c： 时间 SQL](../../../odbc/reference/appendixes/sql-to-c-time.md)  
  
-   [为 c： 时间戳的 SQL](../../../odbc/reference/appendixes/sql-to-c-timestamp.md)  
  
-   [为 c： 年-月间隔的 SQL](../../../odbc/reference/appendixes/sql-to-c-year-month-intervals.md)  
  
-   [为 c： 一天时间间隔的 SQL](../../../odbc/reference/appendixes/sql-to-c-day-time-intervals.md)  
  
-   [SQL C 数据转换示例](../../../odbc/reference/appendixes/sql-to-c-data-conversion-examples.md)
