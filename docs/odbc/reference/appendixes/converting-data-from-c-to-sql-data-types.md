---
title: 将数据从 C 转换为 SQL 数据类型 |微软文档
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- converting data from c to SQL types [ODBC], about converting
- converting data from c to SQL types [ODBC]
- data conversions from C to SQL types [ODBC], about converting
- data types [ODBC], C data types
- data types [ODBC], converting data
- SQL data types [ODBC], converting from C types
- data types [ODBC], SQL data types
- data conversions from C to SQL types [ODBC]
- C data types [ODBC], converting to SQL types
ms.assetid: ee0afe78-b58f-4d34-ad9b-616bb23653bd
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 8fb707e77df7d793277d4a23146adc980eede6fd
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/14/2020
ms.locfileid: "81304656"
---
# <a name="converting-data-from-c-to-sql-data-types"></a>将数据从 C 转换为 SQL 数据类型
当应用程序调用**SQLExecute**或**SQLExecDirect**时，驱动程序从应用程序中的存储位置检索与**SQLBind参数**绑定的任何参数的数据。 当应用程序调用**SQLSetPos**时，驱动程序检索更新的数据，或从绑定**到 SQLBindCol**的列中添加操作。 对于执行时的数据参数，应用程序使用**SQLPutData**发送参数数据。 如有必要，驱动程序将数据从**SQLBind 参数**中*ValueType*参数指定的数据类型转换为**SQLBind 参数**中的*参数类型*参数指定的数据类型，然后将数据发送到数据源。  
  
 下表显示了支持的从 ODBC C 数据类型到 ODBC SQL 数据类型的转换。 填充圆指示 SQL 数据类型的默认转换（当*ValueType*的值或SQL_DESC_CONCISE_TYPE描述符字段SQL_C_DEFAULT时，将转换数据的 C 数据类型）。 空心圆表示支持的转换。  
  
 转换数据的格式不受 Windows ® 国家/地区设置的影响。  
  
 ![支持的转换：从 ODBC C 到 SQL 数据类型](../../../odbc/reference/appendixes/media/apd1b.gif "apd1b")  
  
 以下各节中的表描述了驱动程序或数据源如何转换发送到数据源的数据;需要驱动程序来支持从所有 ODBC C 数据类型转换为他们支持的 ODBC SQL 数据类型。 对于给定的 ODBC C 数据类型，表的第一列在**SQLBind参数**中列出了*参数类型*参数的合法输入值。 第二列列出了驱动程序执行以确定是否可以转换数据的测试的结果。 第三列列出了 SQLExecDirect、SQLExecute、SQLBulk**操作****、SQLSetPos**或**SQLPutData**为每个结果返回的 SQLSTATE。 **SQLExecDirect** **SQLExecute** 仅当返回SQL_SUCCESS时，才会将数据发送到数据源。  
  
 如果**SQLBind 参数**中的*参数类型*参数包含未在给定 C 数据类型的表中显示的 ODBC SQL 数据类型的标识符，则**SQLBind参数**将返回 SQLSTATE 07006（受限数据类型属性冲突）。 如果*参数类型*参数包含特定于驱动程序的标识符，并且驱动程序不支持从特定的 ODBC C 数据类型转换为该驱动程序特定的 SQL 数据类型，**则 SQLBind参数**将返回 SQLSTATE HYC00（未实现可选功能）。  
  
 如果**SQLBind参数**中指定的*参数ValuePtr*和*StrLen_or_IndPtr*参数都是空指针，则该函数将返回 SQLSTATE HY009（无效使用空指针）。 尽管表中未显示，但应用程序会设置**SQLBind参数***StrLen_or_IndPtr*参数指向的长度/指示器缓冲区的值，或者**SQLPutData** *StrLen_or_IndPtr*参数的值SQL_NULL_DATA以指定 NULL SQL 数据值。 （StrLen_or_IndPtr*StrLen_or_IndPtr*参数对应于 APD 的SQL_DESC_OCTET_LENGTH_PTR字段。应用程序将这些值设置为SQL_NTS，以指定**SQLBind参数**或\* **SQLPutData**中的*DataPtr*中的\**参数ValuePtr*中的值（由 APD 的SQL_DESC_DATA_PTR字段指向）是一个空端字符串。  
  
 下表中使用了以下术语：  
  
-   **数据字节长度**- 可用于发送到数据源的 SQL 数据字节数，无论数据在发送到数据源之前是否会被截断。 对于字符串数据，这不包括 null 终止字符的空间。  
  
-   **列字节长度**- 将数据存储在数据源中所需的字节数。  
  
-   **字符字节长度**- 以字符形式显示数据所需的最大字节数。 这是为[显示大小](../../../odbc/reference/appendixes/display-size.md)中的每个 SQL 数据类型定义的，但字符字节长度以字节为单位，而显示大小以字符为单位。  
  
-   **数字数**- 用于表示数字的字符数，包括减号、小数点和指数（如果需要）。  
  
-   **单词在**   
     ***斜体***- SQL 语法的元素。 有关语法元素的语法，请参阅[附录 C：SQL 语法](../../../odbc/reference/appendixes/appendix-c-sql-grammar.md)。  
  
 本部分包含以下主题。  
  
-   [从 C 到 SQL：字符](../../../odbc/reference/appendixes/c-to-sql-character.md)  
  
-   [从 C 到 SQL：数字](../../../odbc/reference/appendixes/c-to-sql-numeric.md)  
  
-   [从 C 到 SQL：位](../../../odbc/reference/appendixes/c-to-sql-bit.md)  
  
-   [从 C 到 SQL：二进制](../../../odbc/reference/appendixes/c-to-sql-binary.md)  
  
-   [从 C 到 SQL：日期](../../../odbc/reference/appendixes/c-to-sql-date.md)  
  
-   [从 C 到 SQL：GUID](../../../odbc/reference/appendixes/c-to-sql-guid.md)  
  
-   [从 C 到 SQL：时间](../../../odbc/reference/appendixes/c-to-sql-time.md)  
  
-   [从 C 到 SQL：时间戳](../../../odbc/reference/appendixes/c-to-sql-timestamp.md)  
  
-   [从 C 到 SQL：年月间隔](../../../odbc/reference/appendixes/c-to-sql-year-month-intervals.md)  
  
-   [从 C 到 SQL：日期时间间隔](../../../odbc/reference/appendixes/c-to-sql-day-time-intervals.md)  
  
-   [从 C 到 SQL 的数据转换示例](../../../odbc/reference/appendixes/c-to-sql-data-conversion-examples.md)
