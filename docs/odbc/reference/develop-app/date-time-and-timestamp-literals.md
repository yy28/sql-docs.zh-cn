---
title: 日期、时间和时间戳文本 |微软文档
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- escape sequences [ODBC], literals
ms.assetid: 2b42a52a-6353-494c-a179-3a7533cd729f
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: d899938be4689daab50a773f189219a797794006
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/14/2020
ms.locfileid: "81288293"
---
# <a name="date-time-and-timestamp-literals"></a>日期、时间和时间戳文本
日期、时间和时间戳文本的转义序列是  
  
 **[**  _- 类型_ **'** _值_ **']**  
  
 *其中文本类型*是下表中列出的值之一。  
  
|*字面类型*|含义|*价值*格式|  
|---------------------|-------------|-----------------------|  
|**D**|Date|*yyyy*-*mm*-*dd*|  
|**t**|时间*|*hh*：*毫米*：*ss*[1]|  
|**Ts**|时间戳|*yyyymm*-*mm*-*dd* *hh*：*毫米*：*ss*_..*f...*[1]|  
  
 [1] 时间或时间戳间隔文本中包含秒分的十进制点右侧的位数取决于秒精度，如SQL_DESC_PRECISION描述符字段中所包含的。 （有关详细信息，请参阅[SQLSetDescField](../../../odbc/reference/syntax/sqlsetdescfield-function.md)。  
  
 有关日期、时间和时间戳转义序列的详细信息，请参阅附录 C 中[的日期、时间和时间戳转义序列](../../../odbc/reference/appendixes/date-time-and-timestamp-escape-sequences.md)：SQL 语法。  
  
 例如，以下两个 SQL 语句都会更新订单表中销售订单 1023 的打开日期。 第一个语句使用转义序列语法。 第二个语句对 DATE 列使用 Oracle Rdb 本机语法，并且不可互操作。  
  
```  
UPDATE Orders SET OpenDate={d '1995-01-15'} WHERE OrderID=1023  
UPDATE Orders SET OpenDate='15-Jan-1995' WHERE OrderID=1023  
```  
  
 日期、时间或时间戳文本的转义序列也可以放置在绑定到日期、时间或时间戳参数的字符变量中。 例如，以下代码使用绑定到字符变量的日期参数来更新订单表中销售订单 1023 的打开日期：  
  
```  
SQLCHAR      OpenDate[56]; // The size of a date literal is 55.  
SQLINTEGER   OpenDateLenOrInd = SQL_NTS;  
  
// Bind the parameter.  
SQLBindParameter(hstmt, 1, SQL_PARAM_INPUT, SQL_C_CHAR, SQL_TYPE_DATE, 0, 0,  
                  OpenDate, sizeof(OpenDate), &OpenDateLenOrInd);  
  
// Place the date in the OpenDate variable. In addition to the escape  
// sequence shown, it would also be possible to use either of the  
// strings "{d '1995-01-15'}" and "15-Jan-1995", although the latter  
// is data source-specific.  
strcpy_s( (char*) OpenDate, _countof(OpenDate), "{d '1995-01-15'}");  
  
// Execute the statement.  
SQLExecDirect(hstmt, "UPDATE Orders SET OpenDate=? WHERE OrderID = 1023", SQL_NTS);  
```  
  
 但是，将参数直接绑定到日期结构通常更有效：  
  
```  
SQL_DATE_STRUCT   OpenDate;  
SQLINTEGER        OpenDateInd = 0;  
  
// Bind the parameter.  
SQLBindParameter(hstmt, 1, SQL_PARAM_INPUT, SQL_C_TYPE_DATE, SQL_TYPE_DATE, 0, 0,  
                  &OpenDate, 0, &OpenDateLen);  
  
// Place the date in the dsOpenDate structure.  
OpenDate.year = 1995;  
OpenDate.month = 1;  
OpenDate.day = 15;  
  
// Execute the statement.  
SQLExecDirect(hstmt, "UPDATE Employee SET OpenDate=? WHERE OrderID = 1023", SQL_NTS);  
```  
  
 要确定驱动程序是否支持日期、时间或时间戳文本的 ODBC 转义序列，应用程序调用**SQLGetTypeInfo**。 如果数据源支持日期、时间或时间戳数据类型，则它还必须支持相应的转义序列。  
  
 数据源还可以支持 ANSI SQL-92 规范中定义的日期时间文本，这与日期、时间或时间戳文本的 ODBC 转义序列不同。 要确定数据源是否支持 ANSI 文本，应用程序使用SQL_ANSI_SQL_DATETIME_LITERALS选项调用**SQLGetInfo。**  
  
 要确定驱动程序是否支持间隔文本的 ODBC 转义序列，应用程序调用**SQLGetTypeInfo**。 如果数据源支持日期时间间隔数据类型，则还必须支持相应的转义序列。  
  
 数据源还可以支持 ANSI SQL-92 规范中定义的日期时间文本，这与日期时间间隔文本的 ODBC 转义序列不同。 要确定数据源是否支持 ANSI 文本，应用程序使用SQL_ANSI_SQL_DATETIME_LITERALS选项调用**SQLGetInfo。**
