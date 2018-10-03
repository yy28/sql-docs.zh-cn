---
title: 将数据从 C 转换为 SQL 数据类型 |Microsoft Docs
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 0f68b53dd77305163aa2595c60a1994a13bb9964
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/01/2018
ms.locfileid: "47793805"
---
# <a name="converting-data-from-c-to-sql-data-types"></a>将数据从 C 转换为 SQL 数据类型
当应用程序调用**SQLExecute**或**SQLExecDirect**，该驱动程序检索数据的任何参数使用绑定**SQLBindParameter**从存储位置中应用程序。 当应用程序调用**SQLSetPos**，该驱动程序检索更新的数据或添加操作中使用绑定列**SQLBindCol**。 对于执行时数据参数，应用程序发送参数数据与**SQLPutData**。 如果有必要，驱动程序将数据从指定的数据类型*ValueType*中的参数**SQLBindParameter**由指定的数据类型为*ParameterType*中的参数**SQLBindParameter**，然后将数据发送到数据源。  
  
 下表显示支持的从 ODBC C 转换为 ODBC SQL 数据类型的数据类型。 实心的圆表示 SQL 数据类型的默认转换 (从其数据将转换时的 C 数据类型的值*ValueType*或 SQL_DESC_CONCISE_TYPE 描述符字段为 SQL_C_DEFAULT)。 空心圆表示支持的转换。  
  
 转换后的数据的格式不受 Windows® 国家/地区设置。  
  
 ![支持的转换： ODBC C 到 SQL 数据类型](../../../odbc/reference/appendixes/media/apd1b.gif "apd1b")  
  
 以下各节中的表介绍驱动程序或数据源将数据发送到数据源; 的转换支持从所有 ODBC C 数据类型转换为它们支持的 ODBC SQL 数据类型所需的驱动程序。 对于给定的 ODBC C 数据类型，第一列的表列出了合法的输入的值*ParameterType*中的参数**SQLBindParameter**。 第二列列出了测试驱动程序执行以确定是否它可以将数据转换的结果。 第三个列中列出了为每个得到的结果返回的 SQLSTATE **SQLExecDirect**， **SQLExecute**， **SQLBulkOperations**， **SQLSetPos**，或**SQLPutData**。 数据发送到数据源，仅当返回 SQL_SUCCESS。  
  
 如果*ParameterType*中的参数**SQLBindParameter**包含未显示对于给定的 C 数据类型，表中的 ODBC SQL 数据类型的标识符**SQLBindParameter**返回的 SQLSTATE 07006 （受限制的数据类型属性冲突）。 如果*ParameterType*参数中包含的特定于驱动程序的标识符，该驱动程序不支持从特定的 ODBC C 数据类型转换为该特定于驱动程序的 SQL 数据类型， **SQLBindParameter**返回 SQLSTATE HYC00 （未实现的可选功能）。  
  
 如果*ParameterValuePtr*并*StrLen_or_IndPtr*中指定的参数**SQLBindParameter**都是 null 指针，函数返回 SQLSTATE HY009 （无效使用 null 指针）。 尽管它不表中所示，应用程序设置指向长度/指示器缓冲区的值*StrLen_or_IndPtr*的参数**SQLBindParameter**的值或*StrLen_or_IndPtr*的参数**SQLPutData**为 SQL_NULL_DATA，若要指定 SQL NULL 数据值。 ( *StrLen_or_IndPtr*参数对应于 APD 的 SQL_DESC_OCTET_LENGTH_PTR 字段。)应用程序设置这些值为 sql_nts; 若要指定的值\* *ParameterValuePtr*中**SQLBindParameter**或\* *DataPtr*中**SQLPutData** （由 APD SQL_DESC_DATA_PTR 字段指向） 是一个以 null 结尾的字符串。  
  
 在表中使用以下术语：  
  
-   **数据的字节长度**-SQL 数据可用于将发送到数据源，无论是否发送到数据源之前，数据将被截断的字节数。 对于字符串数据，这不包括 null 终止字符的空间。  
  
-   **列的字节长度**— 将数据存储在数据源所需的字节数。  
  
-   **字符字节长度**-最大字符窗体中显示数据所需的字节数。 这是为每个 SQL 数据类型中定义的一样[显示大小](../../../odbc/reference/appendixes/display-size.md)，只是字符字节长度是以字节为单位，而显示大小是以字符为单位。  
  
-   **数字位数**— 用于表示一个数字，包括负号、 小数点和指数 （如果需要） 的字符数。  
  
-   **中的单词**   
     ***斜体***-SQL 语法元素。 为语法元素的语法，请参阅[附录 c: SQL 语法](../../../odbc/reference/appendixes/appendix-c-sql-grammar.md)。  
  
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
