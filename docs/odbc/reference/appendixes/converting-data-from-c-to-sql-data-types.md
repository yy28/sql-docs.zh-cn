---
title: "将 C 中的数据转换为 SQL 数据类型 |Microsoft 文档"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: reference
ms.reviewer: 
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
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
caps.latest.revision: 9
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: c8f3f8c3c62c7a4d4c6765d52c48d592ff92a21e
ms.contentlocale: zh-cn
ms.lasthandoff: 09/09/2017

---
# <a name="converting-data-from-c-to-sql-data-types"></a>将 C 中的数据转换为 SQL 数据类型
在应用程序调用**SQLExecute**或**SQLExecDirect**，驱动程序检索数据的任何参数绑定与**SQLBindParameter**从存储位置中应用程序。 在应用程序调用**SQLSetPos**，驱动程序检索更新的数据，或者从与绑定的列添加操作**SQLBindCol**。 对于数据在执行参数，应用程序发送具有的参数数据**SQLPutData**。 如果有必要，该驱动程序将数据从指定的数据类型*ValueType*中的参数**SQLBindParameter**到由指定的数据类型*ParameterType*中的参数**SQLBindParameter**，然后将数据发送到数据源。  
  
 下表显示从 ODBC C 的支持的转换到 ODBC SQL 数据类型的数据类型。 实心的圆圈指示默认值转换为 SQL 数据类型 (从其数据将转换时的 C 数据类型的值*ValueType*或 SQL_DESC_CONCISE_TYPE 描述符字段是 SQL_C_DEFAULT)。 空心圆指示支持的转换。  
  
 转换后的数据的格式不受 Windows® 国家/地区设置。  
  
 ![支持转换： 与 SQL 数据类型的 ODBC C](../../../odbc/reference/appendixes/media/apd1b.gif "apd1b")  
  
 下列各节中的表描述了在驱动程序或数据源将数据发送到数据源; 的转换支持从所有 ODBC C 数据类型到它们支持的 ODBC SQL 数据类型转换所需驱动程序。 对于给定的 ODBC C 数据类型，表的第一列中列出的合法的输入的值*ParameterType*中的参数**SQLBindParameter**。 第二个列中列出驱动程序执行以确定是否它可以将数据转换的测试的结果。 第三列列出了为每个结果的返回 SQLSTATE **SQLExecDirect**， **SQLExecute**， **SQLBulkOperations**， **SQLSetPos**，或**SQLPutData**。 数据发送到数据源中，仅当返回 SQL_SUCCESS。  
  
 如果*ParameterType*中的参数**SQLBindParameter**包含对于给定的 C 数据类型，表中不会显示 ODBC SQL 数据类型的标识符**SQLBindParameter**返回 SQLSTATE 07006 （受限制的数据类型属性冲突）。 如果*ParameterType*参数包含特定于驱动程序的标识符和驱动程序不支持从特定 ODBC C 数据类型转换为特定于驱动程序的 SQL 数据类型， **SQLBindParameter**返回 SQLSTATE HYC00 （未实现的可选功能）。  
  
 如果*ParameterValuePtr*和*StrLen_or_IndPtr*中指定自变量**SQLBindParameter**都是 null 指针，函数返回 SQLSTATE HY009 （无效使用空指针）。 尽管它不会显示在表中，应用程序将设置指向长度/指示器缓冲区的值*StrLen_or_IndPtr*参数**SQLBindParameter**或值*StrLen_or_IndPtr*参数**SQLPutData**到 SQL_NULL_DATA 指定 NULL SQL 数据值。 ( *StrLen_or_IndPtr*参数对应于的 APD SQL_DESC_OCTET_LENGTH_PTR 字段。)应用程序设置这些值到 sql_nts 以指定的值\* *ParameterValuePtr*中**SQLBindParameter**或\* *DataPtr*中**SQLPutData** （由 APD SQL_DESC_DATA_PTR 字段指向） 是以 null 结尾的字符串。  
  
 在表中使用以下术语：  
  
-   **数据的字节长度**— 可用于将发送到数据源，无论是否发送到数据源之前，数据将被截断的 SQL 数据的字节数。 对于字符串数据，这不包括 null 终止字符的空间。  
  
-   **列字节长度**-存储在数据源的数据所需的字节数。  
  
-   **字符字节长度**-最大字符窗体中显示数据所需的字节数。 这是因为每个 SQL 数据类型中定义[显示大小](../../../odbc/reference/appendixes/display-size.md)，只是字符字节长度是以字节为单位，而显示大小是以字符为单位。  
  
-   **数字个数**-用于表示一个数字，包括负号、 小数点和指数 （如果需要） 的字符数。  
  
-   **中的单词**   
     ***斜体***-SQL 语法的元素。 有关语法元素的语法，请参阅[附录 c: SQL 语法](../../../odbc/reference/appendixes/appendix-c-sql-grammar.md)。  
  
 本部分包含以下主题。  
  
-   [To SQL 的 C： 字符](../../../odbc/reference/appendixes/c-to-sql-character.md)  
  
-   [To SQL 的 C： 数字](../../../odbc/reference/appendixes/c-to-sql-numeric.md)  
  
-   [To SQL 的 C： 位](../../../odbc/reference/appendixes/c-to-sql-bit.md)  
  
-   [To SQL 的 C： 二进制](../../../odbc/reference/appendixes/c-to-sql-binary.md)  
  
-   [To SQL 的 C： 日期](../../../odbc/reference/appendixes/c-to-sql-date.md)  
  
-   [To SQL 的 C: GUID](../../../odbc/reference/appendixes/c-to-sql-guid.md)  
  
-   [To SQL 的 C： 时间](../../../odbc/reference/appendixes/c-to-sql-time.md)  
  
-   [To SQL 的 C： 时间戳](../../../odbc/reference/appendixes/c-to-sql-timestamp.md)  
  
-   [To SQL 的 C： 年-月间隔](../../../odbc/reference/appendixes/c-to-sql-year-month-intervals.md)  
  
-   [To SQL 的 C： 天时间间隔](../../../odbc/reference/appendixes/c-to-sql-day-time-intervals.md)  
  
-   [C 到 SQL 数据转换示例](../../../odbc/reference/appendixes/c-to-sql-data-conversion-examples.md)

