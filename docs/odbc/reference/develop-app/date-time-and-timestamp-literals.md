---
title: 日期、 时间和时间戳文本 |Microsoft 文档
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
- escape sequences [ODBC], literals
ms.assetid: 2b42a52a-6353-494c-a179-3a7533cd729f
caps.latest.revision: 7
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 19cc77adb85cca9aa2c273c02f3090bc2ae0ae19
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
---
# <a name="date-time-and-timestamp-literals"></a>日期、 时间和时间戳文本
日期、 时间和时间戳文本的转义序列是  
  
 **{***-类型*  *值* **}**  
  
 其中*文本类型*下表中列出的值之一。  
  
|*文本类型*|含义|格式化的*值*|  
|---------------------|-------------|-----------------------|  
|**d**|日期|*yyyy*-*mm*-*dd*|  
|**T**|时间 *|*hh*:*mm*:*ss*[1]|  
|**ts**|时间戳|*yyyy*-*mm*-*dd* *hh*:*mm*:*ss*[。*f...*] [1]|  
  
 [SQL_DESC_PRECISION 描述符字段中包含就依赖于秒精度，1] 的数字文本，其中包含秒数部分的时间戳间隔中小数点右侧位数。 (有关详细信息，请参阅[SQLSetDescField](../../../odbc/reference/syntax/sqlsetdescfield-function.md)。)  
  
 有关日期、 时间和时间戳转义序列的详细信息，请参阅[日期、 时间和时间戳转义序列](../../../odbc/reference/appendixes/date-time-and-timestamp-escape-sequences.md)附录 c: SQL 语法中。  
  
 例如，这两个以下的 SQL 语句更新销售订单 1023 Orders 表中的打开日期。 第一个语句中使用转义序列语法。 第二个语句的 Oracle Rdb 本机语法用于日期列，并不是可互操作。  
  
```  
UPDATE Orders SET OpenDate={d '1995-01-15'} WHERE OrderID=1023  
UPDATE Orders SET OpenDate='15-Jan-1995' WHERE OrderID=1023  
```  
  
 此外可以在字符变量绑定到日期、 时间或时间戳参数放置日期、 时间或时间戳文本的转义序列。 例如，下面的代码使用绑定到一个字符变量的日期参数若要更新的 Orders 表中的销售订单 1023年打开日期：  
  
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
  
 但是，它是将参数绑定到的日期结构直接通常更高效：  
  
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
  
 若要确定是否则驱动程序支持 ODBC 转义序列的日期、 时间或时间戳文本，应用程序调用**SQLGetTypeInfo**。 如果数据源支持的日期、 时间戳数据类型，它还必须支持相应的转义序列。  
  
 数据源还可以支持的日期时间文字 ANSI sql-92 规范中定义的日期、 时间或时间戳文本的不同从 ODBC 转义序列。 若要确定数据源是否支持 ANSI 文本，应用程序调用**SQLGetInfo** SQL_ANSI_SQL_DATETIME_LITERALS 选项。  
  
 若要确定驱动程序是否支持间隔文字 ODBC 转义序列，应用程序调用**SQLGetTypeInfo**。 如果数据源支持的日期时间间隔数据类型，它还必须支持相应的转义序列。  
  
 数据源还可以支持 ANSI sql-92 规范中定义的日期时间间隔文本中的 ODBC 转义序列从不同的日期时间文字。 若要确定数据源是否支持 ANSI 文本，应用程序调用**SQLGetInfo** SQL_ANSI_SQL_DATETIME_LITERALS 选项。
