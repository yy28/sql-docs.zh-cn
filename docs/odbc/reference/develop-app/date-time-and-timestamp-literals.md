---
title: 日期、时间和时间戳文本 |Microsoft Docs
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
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/27/2020
ms.locfileid: "81288293"
---
# <a name="date-time-and-timestamp-literals"></a>日期、时间和时间戳文本
日期、时间和时间戳文本的转义序列是  
  
 **{**  _-type_ **"** _value_ **"}**  
  
 其中，*原义类型*是下表中列出的值之一。  
  
|*文本类型*|含义|*值*的格式|  
|---------------------|-------------|-----------------------|  
|**d**|日期|*yyyy*-*mm*mm-*dd*|  
|**关心**|阶段|*hh*：*mm*：*ss*[1]|  
|**ts**|时间戳|*yyyy*-*mm*mm-*dd* *hh*：*mm*：*ss*[。*f ...*]2|  
  
 [1] 时间或时间间隔文本中小数点右边的位数，其中包含秒部分，它取决于 SQL_DESC_PRECISION 描述符字段中包含的秒精度。 （有关详细信息，请参阅[SQLSetDescField](../../../odbc/reference/syntax/sqlsetdescfield-function.md)。）  
  
 有关日期、时间和时间戳转义序列的详细信息，请参阅附录 C： SQL 语法中的[日期、时间和时间戳转义序列](../../../odbc/reference/appendixes/date-time-and-timestamp-escape-sequences.md)。  
  
 例如，以下两个 SQL 语句均更新 Orders 表中销售订单1023的打开日期。 第一条语句使用转义序列语法。 第二个语句使用 "日期" 列的 Oracle Rdb 本机语法，它无法互操作。  
  
```  
UPDATE Orders SET OpenDate={d '1995-01-15'} WHERE OrderID=1023  
UPDATE Orders SET OpenDate='15-Jan-1995' WHERE OrderID=1023  
```  
  
 日期、时间或时间戳文字的转义序列也可以放入绑定到日期、时间或时间戳参数的字符变量中。 例如，下面的代码使用绑定到字符变量的 date 参数来更新 Orders 表中销售订单1023的开放日期：  
  
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
  
 但是，将参数直接绑定到日期结构通常更高效：  
  
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
  
 若要确定驱动程序是否支持日期、时间或时间戳文本的 ODBC 转义序列，应用程序将调用**SQLGetTypeInfo**。 如果数据源支持日期、时间或时间戳数据类型，它还必须支持相应的转义序列。  
  
 数据源还可以支持 ANSI SQL-92 规范中定义的 datetime 文本，它们不同于日期、时间或时间戳文本的 ODBC 转义序列。 若要确定数据源是否支持 ANSI 文本，应用程序需要使用 SQL_ANSI_SQL_DATETIME_LITERALS 选项调用**SQLGetInfo** 。  
  
 若要确定驱动程序是否支持用于间隔文本的 ODBC 转义序列，应用程序将调用**SQLGetTypeInfo**。 如果数据源支持日期时间间隔数据类型，它还必须支持相应的转义序列。  
  
 数据源还可以支持 ANSI SQL-92 规范中定义的 datetime 文本，它们不同于 datetime 间隔文本的 ODBC 转义序列。 若要确定数据源是否支持 ANSI 文本，应用程序需要使用 SQL_ANSI_SQL_DATETIME_LITERALS 选项调用**SQLGetInfo** 。
