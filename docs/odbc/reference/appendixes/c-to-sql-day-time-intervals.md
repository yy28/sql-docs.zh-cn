---
title: C 到 SQL：白天间隔 |微软文档
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- day-time intervals [ODBC]
- data conversions from C to SQL types [ODBC], day-time intervals
- converting data from c to SQL types [ODBC], day-time intervals
- intervals [ODBC], converting
ms.assetid: f9ee1ddb-dec7-4f78-b6e2-5ba34e7d6f59
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 1c3f7efb443b442d44a94cfd43629cdaedd6195b
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/14/2020
ms.locfileid: "81291917"
---
# <a name="c-to-sql-day-time-intervals"></a>从 C 到 SQL：日期时间间隔
白天间隔 ODBC C 数据类型的标识符包括：  
  
 SQL_C_INTERVAL_DAY  
  
 SQL_C_INTERVAL_HOUR  
  
 SQL_C_INTERVAL_MINUTE  
  
 SQL_C_INTERVAL_SECOND  
  
 SQL_C_INTERVAL_DAY_TO_HOUR  
  
 SQL_C_INTERVAL_DAY_TO_MINUTE  
  
 SQL_C_INTERVAL_DAY_TO_SECOND  
  
 SQL_C_INTERVAL_HOUR_TO_MINUTE  
  
 SQL_C_INTERVAL_HOUR_TO_SECOND  
  
 SQL_C_INTERVAL_MINUTE_TO_SECOND  
  
 下表显示了可转换为间隔 C 数据的 ODBC SQL 数据类型。 有关表中列和术语的说明，请参阅[将数据从 C 转换为 SQL 数据类型](../../../odbc/reference/appendixes/converting-data-from-c-to-sql-data-types.md)。  
  
|SQL 类型标识符|测试|SQLSTATE|  
|-------------------------|----------|--------------|  
|SQL_CHAR[a]<br /><br /> SQL_VARCHAR[a]<br /><br /> SQL_LONGVARCHAR[a]|列字节长度>= 字符字节长度<br /><br /> 列字节长度<字符字节长度 [a]<br /><br /> 数据值不是有效的间隔文本|不适用<br /><br /> 22001<br /><br /> 22015|  
|SQL_WCHAR[a]<br /><br /> SQL_WVARCHAR[a]<br /><br /> SQL_WLONGVARCHAR[a]|列字符长度>= 数据的字符长度<br /><br /> 列字符长度<字符长度的数据[a]<br /><br /> 数据值不是有效的间隔文本|不适用<br /><br /> 22001<br /><br /> 22015|  
|SQL_TINYINT[b]<br /><br /> SQL_SMALLINT[b] SQL_INTEGER[b]<br /><br /> SQL_BIGINT[b] SQL_NUMERIC[b]<br /><br /> SQL_DECIMAL[b]|单字段间隔的转换不会导致整个数字的截断<br /><br /> 转换导致整个数字的截断|不适用<br /><br /> 22003|  
|SQL_INTERVAL_DAY<br /><br /> SQL_INTERVAL_HOUR<br /><br /> SQL_INTERVAL_MINUTE<br /><br /> SQL_INTERVAL_SECOND<br /><br /> SQL_INTERVAL_DAY_TO_HOUR<br /><br /> SQL_INTERVAL_DAY_TO_MINUTE<br /><br /> SQL_INTERVAL_DAY_TO_SECOND<br /><br /> SQL_INTERVAL_HOUR_TO_MINUTE<br /><br /> SQL_INTERVAL_HOUR_TO_SECOND<br /><br /> SQL_INTERVAL_MINUTE_TO_SECOND|数据值已转换，无需截断任何字段<br /><br /> 转换期间截断一个或多个数据值字段|不适用<br /><br /> 22015|  
  
 [a] 所有 C 间隔数据类型都可以转换为字符数据类型。  
  
 [b] 如果间隔结构中的类型字段使间隔为单个字段（SQL_DAY、SQL_HOUR、SQL_MINUTE 或SQL_SECOND），则可以将间隔 C 类型转换为任何精确数值（SQL_TINYINT、SQL_SMALLINT、SQL_INTEGER、SQL_BIGINT、SQL_DECIMAL或SQL_NUMERIC）。  
  
 间隔 C 类型的默认转换为相应的日间间隔 SQL 类型。  
  
 当从间隔 C 数据类型转换数据时，驱动程序忽略长度/指示器值，并假定数据缓冲区的大小是间隔 C 数据类型的大小。 长度/指标值在**SQLPutData**中的*StrLen_or_Ind*参数中传递，在**SQLBind 参数**中用*StrLen_or_IndPtr*参数指定的缓冲区中传递。 数据缓冲区使用**SQLPutData**中的*DataPtr*参数和**SQLBind 参数**中的*参数ValuePtr*参数指定。  
  
 下面的示例演示如何将存储在SQL_INTERVAL_STRUCT结构中的间隔 C 数据发送到数据库列。 间隔结构包含DAY_TO_SECOND间隔;它将存储在SQL_INTERVAL_DAY_TO_MINUTE类型的数据库列中。  
  
```  
SQL_INTERVAL_STRUCT is;  
SQLINTEGER cbValue;  
  
// Initialize the interval struct to contain the DAY_TO_SECOND  
// interval "154 days, 22 hours, 44 minutes, and 10 seconds"  
is.intval.day_second.day      = 154;  
is.intval.day_second.hour     = 22;  
is.intval.day_second.minute   = 44;  
is.intval.day_second.second   = 10;  
is.interval_sign              = SQL_FALSE;  
  
// Bind the dynamic parameter  
SQLBindParameter(hstmt, 1, SQL_PARAM_INPUT, SQL_C_INTERVAL_DAY_TO_SECOND,  
                  SQL_INTERVAL_DAY_TO_MINUTE, 0, 0, &is,  
                  sizeof(SQL_INTERVAL_STRUCT), &cbValue);  
  
// Execute an insert statement; "interval_column" is a column  
// whose data type is SQL_INTERVAL_DAY_TO_MINUTE.  
SQLExecDirect(hstmt,"INSERT INTO table(interval_column) VALUES (?)",SQL_NTS);  
```
