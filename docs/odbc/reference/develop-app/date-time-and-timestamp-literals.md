---
title: 日期、 时间和时间戳文本 |Microsoft Docs
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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: e6191995c9d1c488fc5af056248ba39dd3eb4607
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/15/2019
ms.locfileid: "68076985"
---
# <a name="date-time-and-timestamp-literals"></a>日期、时间和时间戳文本
日期、 时间和时间戳文本的转义序列是  
  
 **{**  _-type_ **'** _value_ **'}**  
  
 其中*文本类型*下表中列出的值之一。  
  
|*literal-type*|含义|设置格式的*值*|  
|---------------------|-------------|-----------------------|  
|**d**|Date|*yyyy*-*mm*-*dd*|  
|**t**|时间 *|*hh*:*mm*:*ss*[1]|  
|**ts**|时间戳|*yyyy*-*mm*-*dd* *hh*:*mm*:*ss*[.*f...* ][1]|  
  
 [1] 的数字文本，其中包含秒组成部分的时间戳间隔中小数点右侧位数是依赖于的秒精度，因为 SQL_DESC_PRECISION 描述符字段中包含。 (有关详细信息，请参阅[SQLSetDescField](../../../odbc/reference/syntax/sqlsetdescfield-function.md)。)  
  
 有关日期、 时间和时间戳转义序列的详细信息，请参阅[日期、 时间和时间戳转义序列](../../../odbc/reference/appendixes/date-time-and-timestamp-escape-sequences.md)附录 c： 驱动器中SQL 语法。  
  
 例如，这两个以下的 SQL 语句更新销售订单 1023 Orders 表中的打开的日期。 第一个语句使用的转义序列语法。 第二个语句的日期列中使用 Oracle Rdb 本机语法并不是可互操作。  
  
```  
UPDATE Orders SET OpenDate={d '1995-01-15'} WHERE OrderID=1023  
UPDATE Orders SET OpenDate='15-Jan-1995' WHERE OrderID=1023  
```  
  
 此外可以绑定到日期、 时间或时间戳参数的字符变量中放置日期、 时间或时间戳文本的转义序列。 例如，下面的代码使用日期参数绑定到字符变量来更新 Orders 表中的销售订单 1023年打开日期：  
  
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
  
 但是，它是参数直接绑定到的日期结构通常更高效：  
  
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
  
 若要确定是否有驱动程序支持 ODBC 转义序列的日期、 时间或时间戳文本，应用程序调用**SQLGetTypeInfo**。 如果数据源支持的日期、 时间戳数据类型，它还必须支持相应的转义序列。  
  
 数据源还可以支持 ANSI SQL-92 规范中定义的日期时间文字的日期、 时间或时间戳文本的 ODBC 转义序列从不同的。 若要确定数据源是否支持 ANSI 文本，应用程序调用**SQLGetInfo** SQL_ANSI_SQL_DATETIME_LITERALS 选项。  
  
 若要确定驱动程序是否支持间隔文字的 ODBC 转义序列，应用程序调用**SQLGetTypeInfo**。 如果数据源支持的日期时间间隔数据类型，它还必须支持相应的转义序列。  
  
 数据源还可以支持 ANSI SQL-92 规范中定义的日期时间文字的日期时间间隔文字的 ODBC 转义序列从不同的。 若要确定数据源是否支持 ANSI 文本，应用程序调用**SQLGetInfo** SQL_ANSI_SQL_DATETIME_LITERALS 选项。
