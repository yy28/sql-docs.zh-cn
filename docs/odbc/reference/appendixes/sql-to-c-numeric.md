---
title: 从 SQL 到 C：Numeric | Microsoft Docs
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 9abd536110222f8e30a781b6d648402335837f61
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63151279"
---
# <a name="sql-to-c-numeric"></a>从 SQL 到 C：Numeric

数值的 ODBC SQL 数据类型标识符如下所示：

- SQL_DECIMAL  
- SQL_BIGINT  
- SQL_NUMERIC  
- SQL_REAL  
- SQL_TINYINT  
- SQL_FLOAT  
- SQL_SMALLINT  
- SQL_DOUBLE SQL_INTEGER  

下表显示 ODBC C 数据类型可能会转换为数值的 SQL 数据。 列和表中的条款的说明，请参阅[从 SQL 到 C 数据类型的转换的数据](../../../odbc/reference/appendixes/converting-data-from-sql-to-c-data-types.md)。  

|C 类型标识符|测试|**TargetValuePtr*|**StrLen_or_IndPtr*|SQLSTATE|  
|-----------------------|----------|------------------------|----------------------------|--------------|  
|SQL_C_CHAR|字符字节长度 < *BufferLength*<br /><br /> 数字位数 （而不是小数部分） 的整个 < *BufferLength*<br /><br /> 数字位数整体 （而不是小数） > = *BufferLength*|数据<br /><br /> 截断的数据<br /><br /> 未定义|以字节为单位的数据的长度<br /><br /> 以字节为单位的数据的长度<br /><br /> 未定义|不适用<br /><br /> 01004<br /><br /> 22003|  
|SQL_C_WCHAR|字符长度 < *BufferLength*<br /><br /> 数字位数 （而不是小数部分） 的整个 < *BufferLength*<br /><br /> 数字位数整体 （而不是小数） > = *BufferLength*|数据<br /><br /> 截断的数据<br /><br /> 未定义|以字符为单位的数据的长度<br /><br /> 以字符为单位的数据的长度<br /><br /> 未定义|不适用<br /><br /> 01004<br /><br /> 22003|  
|SQL_C_STINYINT<br /><br /> SQL_C_UTINYINT<br /><br /> SQL_C_TINYINT<br /><br /> SQL_C_SBIGINT<br /><br /> SQL_C_UBIGINT<br /><br /> SQL_C_SSHORT<br /><br /> SQL_C_USHORT<br /><br /> SQL_C_SHORT<br /><br /> SQL_C_SLONG<br /><br /> SQL_C_ULONG<br /><br /> SQL_C_LONG<br /><br /> SQL_C_NUMERIC|数据转换而无需截断 [a]<br /><br /> 数据转换使用的小数位数 [a] 的截断<br /><br /> 数据的转换会导致整体 （而不是小数） 数字，[a]|数据<br /><br /> 截断的数据<br /><br /> 未定义|C 数据类型的大小<br /><br /> C 数据类型的大小<br /><br /> 未定义|不适用<br /><br /> 01S07<br /><br /> 22003|  
|SQL_C_FLOAT<br /><br /> SQL_C_DOUBLE|数据位于范围内数字转换到的数据类型 [a]<br /><br /> 数据不在范围内的数字转换到的数据类型 [a]|数据<br /><br /> 未定义|C 数据类型的大小<br /><br /> 未定义|不适用<br /><br /> 22003|  
|SQL_C_BIT|数据为 0 或 1 [a]<br /><br /> 数据为大于 0，小于 2，且不等于 1，[a]<br /><br /> 数据是小于 0 或大于或等于 2 [a]|数据<br /><br /> 截断的数据<br /><br /> 未定义|1[b]<br /><br /> 1[b]<br /><br /> 未定义|不适用<br /><br /> 01S07<br /><br /> 22003|  
|SQL_C_BINARY|数据的字节长度 < = *BufferLength*<br /><br /> 数据的字节长度 > *BufferLength*|数据<br /><br /> 未定义|数据的长度<br /><br /> 未定义|不适用<br /><br /> 22003|  
|SQL_C_INTERVAL_MONTH[c] SQL_C_INTERVAL_YEAR[c] SQL_C_INTERVAL_DAY[c] SQL_C_INTERVAL_HOUR[c] SQL_C_INTERVAL_MINUTE[c] SQL_C_INTERVAL_SECOND[c]|不会被截断的数据<br /><br /> 秒小数部分被截断<br /><br /> 整数部分被截断的数字|数据<br /><br /> 截断的数据<br /><br /> 未定义|以字节为单位的数据的长度<br /><br /> 以字节为单位的数据的长度<br /><br /> 未定义|不适用<br /><br /> 01S07<br /><br /> 22015|  
|SQL_C_INTERVAL_YEAR_TO_MONTH SQL_C_INTERVAL_DAY_TO_HOUR SQL_C_INTERVAL_DAY_TO_MINUTE SQL_C_INTERVAL_DAY_TO_SECOND SQL_C_INTERVAL_HOUR_TO_MINUTE SQL_C_INTERVAL_HOUR_TO_SECOND|整数部分被截断的数字|未定义|未定义|22015|  
  
 [a] 的值*BufferLength*忽略此转换。 驱动程序假定的大小 **TargetValuePtr*是 C 数据类型的大小。  
  
 [b] 这是相应的 C 数据类型的大小。  
  
 [仅为精确数字数据类型 （SQL_DECIMAL、 SQL_NUMERIC、 SQL_TINYINT、 SQL_SMALLINT、 SQL_INTEGER 和 SQL_BIGINT） 支持 c] 此转换。 它不被支持近似数值数据类型 （SQL_REAL、 SQL_FLOAT 或 SQL_DOUBLE）。  

## <a name="sqlcnumeric-and-sqlsetdescfield"></a>SQL_C_NUMERIC 和 SQLSetDescField

 [SQLSetDescField 函数](../../../odbc/reference/syntax/sqlsetdescfield-function.md)需执行手动绑定 SQL_C_NUMERIC 值。 （请注意 ODBC 3.0 中新增了 SQLSetDescField。）若要执行手动绑定，必须先获取描述符句柄。  

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
