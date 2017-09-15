---
title: "为 c： 一天时间间隔的 SQL |Microsoft 文档"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- converting data from SQL to C types [ODBC], day-time intervals
- day-time intervals [ODBC]
- data conversions from SQL to C types [ODBC], day-time intervals
- intervals [ODBC], converting
ms.assetid: 8ea84d69-2292-4128-89a0-f184f68abb98
caps.latest.revision: 8
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: cf87c74d4b2667daa032e814bae3655b83a46c31
ms.contentlocale: zh-cn
ms.lasthandoff: 09/09/2017

---
# <a name="sql-to-c-day-time-intervals"></a>为 c： 一天时间间隔的 SQL
一天时间间隔 ODBC SQL 数据类型的标识符都是：  
  
 SQL_INTERVAL_DAY  
  
 SQL_INTERVAL_DAY_TO_MINUTE  
  
 SQL_INTERVAL_HOUR  
  
 SQL_INTERVAL_DAY_TO_SECOND  
  
 SQL_INTERVAL_MINUTE  
  
 SQL_INTERVAL_HOUR_TO_MINUTE  
  
 SQL_INTERVAL_SECOND  
  
 SQL_INTERVAL_HOUR_TO_SECOND  
  
 SQL_INTERVAL_DAY_TO_HOUR  
  
 SQL_INTERVAL_MINUTE_TO_SECOND  
  
 下表显示 ODBC C 数据类型天时间间隔 SQL 数据可能转换到的目标。 列和表中的条款的说明，请参阅[转换数据从 SQL C 数据类型到](../../../odbc/reference/appendixes/converting-data-from-sql-to-c-data-types.md)。  
  
|C 类型标识符|测试|**TargetValuePtr*|**StrLen_or_IndPtr*|SQLSTATE|  
|-----------------------|----------|------------------------|----------------------------|--------------|  
|所有的一天时间 C 间隔类型|不会被截断的尾随字段部分<br /><br /> 尾随字段部分被截断<br /><br /> 前导精度不是目标的不够大，无法从源中保存数据|data<br /><br /> 截断的数据<br /><br /> 未定义|数据的长度<br /><br /> 数据的长度<br /><br /> 未定义|不适用<br /><br /> 01S07<br /><br /> 22015|  
|SQL_C_STINYINT [b] SQL_C_UTINYINT [b] SQL_C_USHORT [b] SQL_C_SHORT [b] SQL_C_SLONG [b] SQL_C_ULONG [b] SQL_C_NUMERIC [b] SQL_C_BIGINT [b]|间隔精度是单个字段和数据转换而不发生截断<br /><br /> 间隔精度是单个字段和截断小数<br /><br /> 间隔精度是单个字段的和已截断整个<br /><br /> 间隔精度不是单个字段|data<br /><br /> 截断的数据<br /><br /> 截断的数据<br /><br /> 未定义|C 数据类型的大小<br /><br /> 数据的长度<br /><br /> 数据的长度<br /><br /> C 数据类型的大小|不适用<br /><br /> 01S07<br /><br /> 22003<br /><br /> 07006|  
|SQL_C_BINARY|数据的字节长度 < = *BufferLength*<br /><br /> 数据的字节长度 > *BufferLength*|data<br /><br /> 未定义|数据的长度<br /><br /> 未定义|不适用<br /><br /> 22003|  
|SQL_C_CHAR|字符字节长度 < *BufferLength*<br /><br /> 整体 （而不是小数） 数字个数 < *BufferLength*<br /><br /> 整体 （而不是小数） 数字个数 > = *BufferLength*|data<br /><br /> 截断的数据<br /><br /> 未定义|C 数据类型的大小<br /><br /> C 数据类型的大小<br /><br /> 未定义|不适用<br /><br /> 01004<br /><br /> 22003|  
_C_WCHAR|字符长度 < *BufferLength*<br /><br /> 整体 （而不是小数） 数字个数 < *BufferLength*<br /><br /> 整体 （而不是小数） 数字个数 > = *BufferLength*|data<br /><br /> 截断的数据<br /><br /> 未定义|C 数据类型的大小<br /><br /> C 数据类型的大小<br /><br /> 未定义|不适用<br /><br /> 01004<br /><br /> 22003|  
  
 可以为任何一天时间间隔 C 类型转换 [a] 的一天时间间隔 SQL 类型。  
  
 [b] 如果间隔精度，单个字段 （一个天、 小时、 分钟或秒的） 间隔 SQL 类型可转换为任何具体的数字 （SQL_C_STINYINT、 SQL_C_UTINYINT、 SQL_C_USHORT、 SQL_C_SHORT、 SQL_C_SLONG、 SQL_C_ULONG 或 SQL_C_NUMERIC）。  
  
 一个时间间隔 SQL 类型的默认转换是相应的 C 间隔数据类型。 应用程序然后将绑定的列或参数 （或设置 SQL_DESC_DATA_PTR 字段中的 ARD 相应的记录） 以指向初始化 SQL_INTERVAL_STRUCT 结构 (或将指针传递给 SQL_ INTERVAL_STRUCT 结构用作*TargetValuePtr*对的调用中的自变量**SQLGetData**)。  
  
 下面的示例演示如何将数据从类型 SQL_INTERVAL_DAY_TO_MINUTE 的列传输到 SQL_INTERVAL_STRUCT 结构以便返回为 DAY_TO_HOUR 间隔。  
  
```  
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
