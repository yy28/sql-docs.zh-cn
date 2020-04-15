---
title: 将数据从 SQL 转换为 C 数据类型 |微软文档
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 1a10730cb3910c55679c264583801cd57c83bfc3
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/14/2020
ms.locfileid: "81284747"
---
# <a name="converting-data-from-sql-to-c-data-types"></a>将数据从 SQL 转换为 C 数据类型
当应用程序调用**SQLFetch、SQLFetchScroll**或**SQLGetData**时，驱动程序将从数据源检索数据。 **SQLFetchScroll** 如有必要，它将数据从驱动程序检索数据的数据类型转换为**SQLBindCol**或**SQLGetData**中*的目标类型*参数指定的数据类型。 最后，它将数据存储在**SQLBindCol**或**SQLGetData**中*TargetValuePtr*参数指向的位置（以及 ARD 的SQL_DESC_DATA_PTR字段）。  
  
 下表显示了支持的从 ODBC SQL 数据类型到 ODBC C 数据类型的转换。 填充圆指示 SQL 数据类型的默认转换（当*TargetType*的值SQL_C_DEFAULT时，数据将转换为 C 数据类型）。 空心圆表示支持的转换。  
  
 对于使用 ODBC *2.x*驱动程序的 ODBC *3.x*应用程序，可能不支持从特定于驱动程序的数据类型转换。  
  
 转换数据的格式不受 Windows ® 国家/地区设置的影响。  
  
 以下各节中的表描述了驱动程序或数据源如何转换从数据源检索到的数据;驱动程序需要支持从它们支持的 ODBC SQL 数据类型转换为所有 ODBC C 数据类型。 对于给定的 ODBC SQL 数据类型，表的第一列在**SQLBindCol**和**SQLGetData**中列出了*TargetType*参数的合法输入值。 第二列列出了测试的结果，通常使用**SQLBindCol**或**SQLGetData**中指定的*BufferLength*参数，驱动程序执行该参数以确定是否可以转换数据。 对于每个结果，第三列和第四列列出放置在*TargetValuePtr*指定的缓冲区中的值，并在驱动程序尝试转换数据后在**SQLBindCol**或**SQLGetData**中指定的*StrLen_or_IndPtr*参数。 （StrLen_or_IndPtr*StrLen_or_IndPtr*参数对应于 ARD 的SQL_DESC_OCTET_LENGTH_PTR字段。最后一列列出了**SQLFetch、SQLFetchScroll****SQLFetch**或**SQLGetData**为每个结果返回的 SQLSTATE。  
  
 如果**SQLBindCol**或**SQLGetData**中*的目标类型*参数包含未在表中显示给定 ODBC SQL 数据类型的 ODBC C 数据类型的标识符，**则 SQLFetch、SQLFetchScroll**或**SQLGetData**返回 SQLSTATE 07006（受限数据类型属性冲突）。 **SQLFetchScroll** 如果*TargetType*参数包含一个标识符，该标识符指定从特定于驱动程序的 SQL 数据类型转换为 ODBC C 数据类型，并且驱动程序不支持此转换，**则 SQLFetch、SQLFetchScroll**或**SQLGetData**将返回 SQLSTATE HYC00（未实现可选功能）。 **SQLFetchScroll**  
  
 尽管表中未显示该驱动程序，但当 SQL 数据值为 NULL 时，驱动程序将返回*StrLen_or_IndPtr*参数指定的缓冲区中的SQL_NULL_DATA。 有关在进行多次调用以检索数据时使用*StrLen_or_IndPtr*的说明，请参阅[SQLGetData](../../../odbc/reference/syntax/sqlgetdata-function.md)函数说明。 将 SQL 数据转换为字符 C 数据时\**，StrLen_or_IndPtr*中返回的字符计数不包括空终止字节。 如果*TargetValuePtr*是空指针 **，SQLGetData**将返回 SQLSTATE HY009（无效使用空指针）;在**SQLBindCol**中，这将取消绑定列。  
  
 下表中使用了以下术语和约定：  
  
-   **数据字节长度**是可在 **TargetValuePtr*中返回的 C 数据字节数，无论数据在返回到应用程序之前是否会被截断。 对于字符串数据，这不包括 null 端接字符的空间。  
  
-   **字符字节长度**是以字符格式显示数据所需的字节总数。 这是为["显示大小"](../../../odbc/reference/appendixes/display-size.md)部分中的每个 C 数据类型定义的，只不过字符字节长度以字节为单位，而显示大小以字符为单位。  
  
-   *斜体字*中的单词表示函数参数或 SQL 语法的元素。 有关语法元素的语法，请参阅[附录 C：SQL 语法](../../../odbc/reference/appendixes/appendix-c-sql-grammar.md)。  
  
 本部分包含以下主题。  
  
-   [从 SQL 到 C：字符](../../../odbc/reference/appendixes/sql-to-c-character.md)  
  
-   [从 SQL 到 C：数字](../../../odbc/reference/appendixes/sql-to-c-numeric.md)  
  
-   [从 SQL 到 C：位](../../../odbc/reference/appendixes/sql-to-c-bit.md)  
  
-   [从 SQL 到 C：二进制](../../../odbc/reference/appendixes/sql-to-c-binary.md)  
  
-   [从 SQL 到 C：日期](../../../odbc/reference/appendixes/sql-to-c-date.md)  
  
-   [从 SQL 到 C：GUID](../../../odbc/reference/appendixes/sql-to-c-guid.md)  
  
-   [从 SQL 到 C：时间](../../../odbc/reference/appendixes/sql-to-c-time.md)  
  
-   [从 SQL 到 C：时间戳](../../../odbc/reference/appendixes/sql-to-c-timestamp.md)  
  
-   [从 SQL 到 C：年月间隔](../../../odbc/reference/appendixes/sql-to-c-year-month-intervals.md)  
  
-   [从 SQL 到 C：日期时间间隔](../../../odbc/reference/appendixes/sql-to-c-day-time-intervals.md)  
  
-   [从 SQL 到 C 的数据转换示例](../../../odbc/reference/appendixes/sql-to-c-data-conversion-examples.md)
