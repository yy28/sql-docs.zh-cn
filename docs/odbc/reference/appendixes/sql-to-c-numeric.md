---
title: SQL 到 C：数字 |微软文档
ms.custom: ''
ms.date: 01/19/2019
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- data conversions from SQL to C types [ODBC], numeric
- numeric data type [ODBC], converting
- converting data from SQL to C types [ODBC], numeric
ms.assetid: 76f8b5d5-4bd0-4dcb-a90a-698340e0d36e
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 36b24da4023a96b686742416b83bb5790e129278
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/14/2020
ms.locfileid: "81296407"
---
# <a name="sql-to-c-numeric"></a>从 SQL 到 C：数字

数字 ODBC SQL 数据类型的标识符如下：

- SQL_DECIMAL  
- SQL_BIGINT  
- SQL_NUMERIC  
- SQL_REAL  
- SQL_TINYINT  
- SQL_FLOAT  
- SQL_SMALLINT  
- SQL_DOUBLESQL_INTEGER  

下表显示了可转换为数字 SQL 数据的 ODBC C 数据类型。 有关表中列和术语的说明，请参阅[将数据从 SQL 转换为 C 数据类型](../../../odbc/reference/appendixes/converting-data-from-sql-to-c-data-types.md)。  

|C 类型标识符|测试|**目标价值Ptr*|**StrLen_or_IndPtr*|SQLSTATE|  
|-----------------------|----------|------------------------|----------------------------|--------------|  
|SQL_C_CHAR|字符字节长度<*缓冲区长度*<br /><br /> *缓冲区长度*<整数（与小数）位数<br /><br /> >=*缓冲区长度*的整个（与小数）数字数|数据<br /><br /> 截断的数据<br /><br /> Undefined|以字节为单位的数据长度<br /><br /> 以字节为单位的数据长度<br /><br /> Undefined|不适用<br /><br /> 01004<br /><br /> 22003|  
|SQL_C_WCHAR|字符长度<*缓冲区长度*<br /><br /> *缓冲区长度*<整数（与小数）位数<br /><br /> >=*缓冲区长度*的整个（与小数）数字数|数据<br /><br /> 截断的数据<br /><br /> Undefined|字符中的数据长度<br /><br /> 字符中的数据长度<br /><br /> Undefined|不适用<br /><br /> 01004<br /><br /> 22003|  
|SQL_C_STINYINT<br /><br /> SQL_C_UTINYINT<br /><br /> SQL_C_TINYINT<br /><br /> SQL_C_SBIGINT<br /><br /> SQL_C_UBIGINT<br /><br /> SQL_C_SSHORT<br /><br /> SQL_C_USHORT<br /><br /> SQL_C_SHORT<br /><br /> SQL_C_SLONG<br /><br /> SQL_C_ULONG<br /><br /> SQL_C_LONG<br /><br /> SQL_C_NUMERIC|在不截断的情况下转换的数据[a]<br /><br /> 使用小数数字截断转换的数据[a]<br /><br /> 数据转换将导致整体数字（相对于小数）的丢失[a]|数据<br /><br /> 截断的数据<br /><br /> Undefined|C 数据类型的大小<br /><br /> C 数据类型的大小<br /><br /> Undefined|不适用<br /><br /> 01S07<br /><br /> 22003|  
|SQL_C_FLOAT<br /><br /> SQL_C_DOUBLE|数据在要转换数字的数据类型范围内[a]<br /><br /> 数据不在要转换数字的数据类型范围之外[a]|数据<br /><br /> Undefined|C 数据类型的大小<br /><br /> Undefined|不适用<br /><br /> 22003|  
|SQL_C_BIT|数据为 0 或 1[a]<br /><br /> 数据大于 0，小于 2，不等于 1[a]<br /><br /> 数据小于 0 或大于或等于 2[a]|数据<br /><br /> 截断的数据<br /><br /> Undefined|1[b]<br /><br /> 1[b]<br /><br /> Undefined|不适用<br /><br /> 01S07<br /><br /> 22003|  
|SQL_C_BINARY|数据<字节长度 =*缓冲区长度*<br /><br /> >*缓冲区长度*的数据字节长度|数据<br /><br /> Undefined|数据长度<br /><br /> Undefined|不适用<br /><br /> 22003|  
|SQL_C_INTERVAL_MONTH[c] SQL_C_INTERVAL_YEAR[c] SQL_C_INTERVAL_DAY[c] SQL_C_INTERVAL_HOUR[c] SQL_C_INTERVAL_MINUTE[c] SQL_C_INTERVAL_SECOND[c]|数据未截断<br /><br /> 分段秒部分截断<br /><br /> 被截断的整部分数字|数据<br /><br /> 截断的数据<br /><br /> Undefined|以字节为单位的数据长度<br /><br /> 以字节为单位的数据长度<br /><br /> Undefined|不适用<br /><br /> 01S07<br /><br /> 22015|  
|SQL_C_INTERVAL_YEAR_TO_MONTHSQL_C_INTERVAL_DAY_TO_HOURSQL_C_INTERVAL_DAY_TO_MINUTESQL_C_INTERVAL_HOUR_TO_MINUTESQL_C_INTERVAL_HOUR_TO_SECONDSQL_C_INTERVAL_DAY_TO_SECOND|被截断的整部分数字|Undefined|Undefined|22015|  
  
 [a] 此转换将忽略*缓冲区长度*的值。 驱动程序假定 **目标价值Ptr*的大小是 C 数据类型的大小。  
  
 [b] 这是相应的 C 数据类型的大小。  
  
 [c] 仅支持精确数值数据类型（SQL_DECIMAL、SQL_NUMERIC、SQL_TINYINT、SQL_SMALLINT、SQL_INTEGER和SQL_BIGINT） 转换。 对于近似数值数据类型（SQL_REAL、SQL_FLOAT或SQL_DOUBLE），不支持它。  

## <a name="sql_c_numeric-and-sqlsetdescfield"></a>SQL_C_NUMERIC和 SQLSetDesc 字段

 [SQLSetDescField 函数](../../../odbc/reference/syntax/sqlsetdescfield-function.md)需要执行具有SQL_C_NUMERIC值的手动绑定。 （请注意，SQLSetDescField 是在 ODBC 3.0 中添加的。要执行手动绑定，必须首先获取描述符句柄。  

```cpp
if (fCType == SQL_C_NUMERIC) {   
   // special processing required for NUMERIC to get right scale & precision  
   // Modify the fields in the implicit application parameter descriptor  
   SQLHDESC hdesc=NULL;  
  
   // Use SQL_ATTR_APP_ROW_DESC for calls to SQLBindCol()  
   // Use SQL_ATTR_APP_PARAM_DESC for calls to SQLBindParameter()  
   //  
   // retcode = SQLGetStmtAttr(hstmt, SQL_ATTR_APP_ROW_DESC, &hdesc, 0, NULL);  
   retcode = SQLGetStmtAttr(hstmt, SQL_ATTR_APP_PARAM_DESC, &hdesc, 0, NULL);  
   if (!ODBC_CALL_SUCCESS(retcode)) {  
      printf ("\nSQLGetStmtAttr failed");  
      i = 1;  
      sqlstate[7] = '\0';  
      while (SQLGetDiagRec(SQL_HANDLE_STMT, hstmt, i, sqlstate, &NativeError, wrkbuf, sizeof(wrkbuf), &len) != SQL_NO_DATA) {  
         printf("\niTestCase = %d Failed...Precision = %d, Scale = %d\nNativeError=%d, State=%s, \n  Message=%s",   
            iTestCase, Precision, Scale, NativeError, sqlstate, wrkbuf);  
         i++;  
      }  
      continue;  
   }  
   retcode = SQLSetDescField(hdesc, iCol, SQL_DESC_TYPE, (SQLPOINTER) SQL_C_NUMERIC, 0);  
   if (!ODBC_CALL_SUCCESS(retcode))  
      goto error;  
   retcode = SQLSetDescField(hdesc, iCol, SQL_DESC_PRECISION, (SQLPOINTER)num.precision, 0);  
   if (!ODBC_CALL_SUCCESS(retcode))  
      goto error;  
   retcode = SQLSetDescField(hdesc, iCol, SQL_DESC_SCALE, (SQLPOINTER)num.scale, 0);  
   if (!ODBC_CALL_SUCCESS(retcode))  
      goto error;  
   retcode = SQLSetDescField(hdesc, iCol, SQL_DESC_DATA_PTR, (SQLPOINTER) &(num), sizeof(num));  
```
