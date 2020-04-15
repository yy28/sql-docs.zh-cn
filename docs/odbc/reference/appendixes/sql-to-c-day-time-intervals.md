---
title: SQL 到 C：白天间隔 |微软文档
ms.custom: ''
ms.date: 01/19/2019
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- converting data from SQL to C types [ODBC], day-time intervals
- day-time intervals [ODBC]
- data conversions from SQL to C types [ODBC], day-time intervals
- intervals [ODBC], converting
ms.assetid: 8ea84d69-2292-4128-89a0-f184f68abb98
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 1318da5285ba2384dd23e4c235e698aa72c7658e
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/14/2020
ms.locfileid: "81296467"
---
# <a name="sql-to-c-day-time-intervals"></a>从 SQL 到 C：日期时间间隔

白天间隔 ODBC SQL 数据类型的标识符如下：

- SQL_INTERVAL_DAY
- SQL_INTERVAL_DAY_TO_MINUTE
- SQL_INTERVAL_HOUR
- SQL_INTERVAL_DAY_TO_SECOND
- SQL_INTERVAL_MINUTE
- SQL_INTERVAL_HOUR_TO_MINUTE
- SQL_INTERVAL_SECOND
- SQL_INTERVAL_HOUR_TO_SECOND
- SQL_INTERVAL_DAY_TO_HOUR
- SQL_INTERVAL_MINUTE_TO_SECOND

下表显示了可以转换为白天间隔 SQL 数据的 ODBC C 数据类型。 有关表中列和术语的说明，请参阅[将数据从 SQL 转换为 C 数据类型](../../../odbc/reference/appendixes/converting-data-from-sql-to-c-data-types.md)。

|C 类型标识符|测试|**目标价值Ptr*|**StrLen_or_IndPtr*|SQLSTATE|  
|-----------------------|----------|------------------------|----------------------------|--------------|  
|所有白天 C 间隔类型|尾随字段部分未截断<br /><br /> 尾随字段部分截断<br /><br /> 目标的领先精度不足以保存来自源的数据|数据<br /><br /> 截断的数据<br /><br /> Undefined|数据长度<br /><br /> 数据长度<br /><br /> Undefined|不适用<br /><br /> 01S07<br /><br /> 22015|  
|SQL_C_STINYINT[b] SQL_C_UTINYINT[b] SQL_C_USHORT[b] SQL_C_SHORT[b] SQL_C_SLONG[b] SQL_C_ULONG[b] SQL_C_NUMERIC[b] SQL_C_BIGINT[b]|间隔精度是单个字段，数据在不截断的情况下被转换<br /><br /> 间隔精度为单个字段，并截断小数<br /><br /> 间隔精度是单个字段，并截断整个<br /><br /> 间隔精度不是单个字段|数据<br /><br /> 截断的数据<br /><br /> 截断的数据<br /><br /> Undefined|C 数据类型的大小<br /><br /> 数据长度<br /><br /> 数据长度<br /><br /> C 数据类型的大小|不适用<br /><br /> 01S07<br /><br /> 22003<br /><br /> 07006|  
|SQL_C_BINARY|数据<字节长度 =*缓冲区长度*<br /><br /> >*缓冲区长度*的数据字节长度|数据<br /><br /> Undefined|数据长度<br /><br /> Undefined|不适用<br /><br /> 22003|  
|SQL_C_CHAR|字符字节长度<*缓冲区长度*<br /><br /> *缓冲区长度*<整数（与小数）位数<br /><br /> >=*缓冲区长度*的整个（与小数）数字数|数据<br /><br /> 截断的数据<br /><br /> Undefined|C 数据类型的大小<br /><br /> C 数据类型的大小<br /><br /> Undefined|不适用<br /><br /> 01004<br /><br /> 22003|  
|SQL_C_WCHAR|字符长度<*缓冲区长度*<br /><br /> *缓冲区长度*<整数（与小数）位数<br /><br /> >=*缓冲区长度*的整个（与小数）数字数|数据<br /><br /> 截断的数据<br /><br /> Undefined|C 数据类型的大小<br /><br /> C 数据类型的大小<br /><br /> Undefined|不适用<br /><br /> 01004<br /><br /> 22003|  
  
 [a] 日间间隔 SQL 类型可以转换为任何日间间隔 C 类型。  
  
 [b] 如果间隔精度是单个字段（DAY、HOUR、MINUTE 或秒），则可以将间隔 SQL 类型转换为任何精确数值（SQL_C_STINYINT、SQL_C_UTINYINT、SQL_C_USHORT、SQL_C_SHORT、SQL_C_SLONG、SQL_C_ULONG 或SQL_C_NUMERIC）。  
  
间隔 SQL 类型的默认转换为相应的 C 间隔数据类型。 然后，应用程序绑定列或参数（或在 ARD 的适当记录中设置SQL_DESC_DATA_PTR字段），以指向初始化SQL_INTERVAL_STRUCT结构（或将指向SQL_INTERVAL_STRUCT结构的指针作为对**SQLGetData**调用中的*TargetValuePtr*参数）。  
  
下面的示例演示如何将数据从类型SQL_INTERVAL_DAY_TO_MINUTE列传输到SQL_INTERVAL_STRUCT结构中，以便以DAY_TO_HOUR间隔的形式返回。  

```cpp
SQL_INTERVAL_STRUCT is;  
SQLINTEGER    cbValue;  
SQLUINTEGER   days, hours;  
  
// Execute a select statement; "interval_column" is a column  
// whose data type is SQL_INTERVAL_DAY_TO_MINUTE.  
SQLExecDirect(hstmt, "SELECT interval_column FROM table", SQL_NTS);  
  
// Bind  
SQLBindCol(hstmt, 1, SQL_C_INTERVAL_DAY_TO_MINUTE, &is, sizeof(SQL_INTERVAL_STRUCT), &cbValue);  
  
// Fetch  
SQLFetch(hstmt);  
  
// Process data  
days = is.intval.day_second.day;  
hours = is.intval.day_second.hour;  
```
