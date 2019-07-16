---
title: 从 SQL 到 C：日期时间间隔 |Microsoft Docs
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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: db39751059d84e4e3a7950acbbbcb7f1a2b0b00d
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/15/2019
ms.locfileid: "68056858"
---
# <a name="sql-to-c-day-time-intervals"></a>从 SQL 到 C：日期时间间隔

日期时间间隔 ODBC SQL 数据类型的标识符如下所示：

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

下表显示 ODBC C 数据类型可能会转换为日期时间间隔 SQL 数据。 列和表中的条款的说明，请参阅[从 SQL 到 C 数据类型的转换的数据](../../../odbc/reference/appendixes/converting-data-from-sql-to-c-data-types.md)。

|C 类型标识符|测试|**TargetValuePtr*|**StrLen_or_IndPtr*|SQLSTATE|  
|-----------------------|----------|------------------------|----------------------------|--------------|  
|所有日期时间 C 间隔类型|不会被截断尾随的字段部分<br /><br /> 截断尾随的字段部分<br /><br /> 前导精度是目标的不足够大以保存数据源中|Data<br /><br /> 截断的数据<br /><br /> 未定义|数据的长度<br /><br /> 数据的长度<br /><br /> 未定义|不适用<br /><br /> 01S07<br /><br /> 22015|  
|SQL_C_STINYINT[b] SQL_C_UTINYINT[b] SQL_C_USHORT[b] SQL_C_SHORT[b] SQL_C_SLONG[b] SQL_C_ULONG[b] SQL_C_NUMERIC[b] SQL_C_BIGINT[b]|时间间隔精度是单个字段和数据转换而无需截断<br /><br /> 时间间隔精度是单个字段，并截断小数部分<br /><br /> 时间间隔精度是单个字段或整个已截断<br /><br /> 时间间隔精度不是单个字段|Data<br /><br /> 截断的数据<br /><br /> 截断的数据<br /><br /> 未定义|C 数据类型的大小<br /><br /> 数据的长度<br /><br /> 数据的长度<br /><br /> C 数据类型的大小|不适用<br /><br /> 01S07<br /><br /> 22003<br /><br /> 07006|  
|SQL_C_BINARY|数据的字节长度 < = *BufferLength*<br /><br /> 数据的字节长度 > *BufferLength*|Data<br /><br /> 未定义|数据的长度<br /><br /> 未定义|不适用<br /><br /> 22003|  
|SQL_C_CHAR|字符字节长度 < *BufferLength*<br /><br /> 数字位数 （而不是小数部分） 的整个 < *BufferLength*<br /><br /> 数字位数整体 （而不是小数） > = *BufferLength*|Data<br /><br /> 截断的数据<br /><br /> 未定义|C 数据类型的大小<br /><br /> C 数据类型的大小<br /><br /> 未定义|不适用<br /><br /> 01004<br /><br /> 22003|  
|SQL_C_WCHAR|字符长度 < *BufferLength*<br /><br /> 数字位数 （而不是小数部分） 的整个 < *BufferLength*<br /><br /> 数字位数整体 （而不是小数） > = *BufferLength*|Data<br /><br /> 截断的数据<br /><br /> 未定义|C 数据类型的大小<br /><br /> C 数据类型的大小<br /><br /> 未定义|不适用<br /><br /> 01004<br /><br /> 22003|  
  
 [a] 的日期时间间隔 SQL 类型可以转换为任何一天时间间隔 C 类型。  
  
 [b] 如果时间间隔精度为单个字段 （天、 小时、 分钟或秒的一个），可将 SQL 类型的时间间隔转换任何精确数值 （SQL_C_STINYINT、 SQL_C_UTINYINT、 SQL_C_USHORT、 SQL_C_SHORT、 SQL_C_SLONG、 SQL_C_ULONG 或 SQL_C_NUMERIC）。  
  
SQL 类型的时间间隔的默认转换为相应的 C 间隔数据类型。 应用程序然后将列或参数绑定 （或 ARD 的相应记录中设置 SQL_DESC_DATA_PTR 字段） 以指向已初始化 SQL_INTERVAL_STRUCT 结构 (或将指针传递给SQL_INTERVAL_STRUCT结构*TargetValuePtr*的调用中的自变量**SQLGetData**)。  
  
下面的示例演示如何将数据从 SQL_INTERVAL_DAY_TO_MINUTE 类型的列的传输到 SQL_INTERVAL_STRUCT 结构，以便返回 DAY_TO_HOUR 时间间隔。  

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
