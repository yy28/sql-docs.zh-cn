---
title: "为 c： 数字 SQL |Microsoft 文档"
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
- data conversions from SQL to C types [ODBC], numeric
- numeric data type [ODBC], converting
- converting data from SQL to C types [ODBC], numeric
ms.assetid: 76f8b5d5-4bd0-4dcb-a90a-698340e0d36e
caps.latest.revision: 12
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 5513983bcd8d7858629bb1a9f45ff5489ad46246
ms.contentlocale: zh-cn
ms.lasthandoff: 09/09/2017

---
# <a name="sql-to-c-numeric"></a>SQL 为 c： 数字
数值 ODBC SQL 数据类型的标识符都是：  
  
 SQL_DECIMAL  
  
 SQL_BIGINT  
  
 SQL_NUMERIC  
  
 SQL_REAL  
  
 SQL_TINYINT  
  
 SQL_FLOAT  
  
 SQL_SMALLINT  
  
 SQL_DOUBLE SQL_INTEGER  
  
 下表显示 ODBC C 数据类型数值 SQL 数据可能转换到的目标。 列和表中的条款的说明，请参阅[转换数据从 SQL C 数据类型到](../../../odbc/reference/appendixes/converting-data-from-sql-to-c-data-types.md)。  
  
|C 类型标识符|测试|**TargetValuePtr*|**StrLen_or_IndPtr*|SQLSTATE|  
|-----------------------|----------|------------------------|----------------------------|--------------|  
|SQL_C_CHAR|字符字节长度 < *BufferLength*<br /><br /> 整体 （而不是小数） 数字个数 < *BufferLength*<br /><br /> 整体 （而不是小数） 数字个数 > = *BufferLength*|data<br /><br /> 截断的数据<br /><br /> 未定义|以字节为单位的数据的长度<br /><br /> 以字节为单位的数据的长度<br /><br /> 未定义|不适用<br /><br /> 01004<br /><br /> 22003|  
|SQL_C_WCHAR|字符长度 < *BufferLength*<br /><br /> 整体 （而不是小数） 数字个数 < *BufferLength*<br /><br /> 整体 （而不是小数） 数字个数 > = *BufferLength*|data<br /><br /> 截断的数据<br /><br /> 未定义|以字符为单位的数据的长度<br /><br /> 以字符为单位的数据的长度<br /><br /> 未定义|不适用<br /><br /> 01004<br /><br /> 22003|  
|SQL_C_STINYINT<br /><br /> SQL_C_UTINYINT<br /><br /> SQL_C_TINYINT<br /><br /> SQL_C_SBIGINT<br /><br /> SQL_C_UBIGINT<br /><br /> SQL_C_SSHORT<br /><br /> SQL_C_USHORT<br /><br /> SQL_C_SHORT<br /><br /> SQL_C_SLONG<br /><br /> SQL_C_ULONG<br /><br /> SQL_C_LONG<br /><br /> SQL_C_NUMERIC|数据转换而不会截断 [a]<br /><br /> 数据转换使用的小数位数 [a] 的截断<br /><br /> 数据的转换将导致丢失的整体 （而不是小数） 数字，[a]|data<br /><br /> 截断的数据<br /><br /> 未定义|C 数据类型的大小<br /><br /> C 数据类型的大小<br /><br /> 未定义|不适用<br /><br /> 01S07<br /><br /> 22003|  
_C_FLOAT<br /><br /> SQL_C_DOUBLE|数据是数转换到的目标的数据类型的范围内 [a]<br /><br /> 数据超出了范围数转换到的目标的数据类型 [a]|data<br /><br /> 未定义|C 数据类型的大小<br /><br /> 未定义|不适用<br /><br /> 22003|  
|SQL_C_BIT|数据为 0 或 1 [a]<br /><br /> 数据为大于 0，小于 2，且不等于 1，[a]<br /><br /> 数据是小于 0 或大于或等于 2 [a]|data<br /><br /> 截断的数据<br /><br /> 未定义|1 [b]<br /><br /> 1 [b]<br /><br /> 未定义|不适用<br /><br /> 01S07<br /><br /> 22003|  
|SQL_C_BINARY|数据的字节长度 < = *BufferLength*<br /><br /> 数据的字节长度 > *BufferLength*|data<br /><br /> 未定义|数据的长度<br /><br /> 未定义|不适用<br /><br /> 22003|  
|SQL_C_INTERVAL_MONTH [c] SQL_C_INTERVAL_YEAR [c] SQL_C_INTERVAL_DAY [c] SQL_C_INTERVAL_HOUR [c] SQL_C_INTERVAL_MINUTE [c] SQL_C_INTERVAL_SECOND [c]|不会被截断的数据<br /><br /> 秒的小数部分部分被截断<br /><br /> 截断的数字的整数部分|data<br /><br /> 截断的数据<br /><br /> 未定义|以字节为单位的数据的长度<br /><br /> 以字节为单位的数据的长度<br /><br /> 未定义|不适用<br /><br /> 01S07<br /><br /> 22015|  
_C_INTERVAL_YEAR_TO_MONTH SQL_C_INTERVAL_DAY_TO_HOUR SQL_C_INTERVAL_DAY_TO_MINUTE SQL_C_INTERVAL_DAY_TO_SECOND SQL_C_INTERVAL_HOUR_TO_MINUTE SQL_C_INTERVAL_HOUR_TO_SECOND|截断的数字的整数部分|未定义|未定义|22015|  
  
 [a] 的值*BufferLength*忽略此转换。 该驱动程序假定的大小 **TargetValuePtr*是 C 数据类型的大小。  
  
 [b] 这是对应的 C 数据类型的大小。  
  
 [只对精确数值数据类型 （SQL_DECIMAL、 SQL_NUMERIC、 SQL_TINYINT、 SQL_SMALLINT、 SQL_INTEGER 和 SQL_BIGINT） 支持 c] 此转换。 近似数值数据类型 （SQL_REAL、 SQL_FLOAT 或 SQL_DOUBLE） 不支持它。  
  
## <a name="sqlcnumeric-and-sqlsetdescfield"></a>SQL_C_NUMERIC 和 SQLSetDescField  
 [SQLSetDescField 函数](../../../odbc/reference/syntax/sqlsetdescfield-function.md)执行带有 SQL_C_NUMERIC 值手动绑定所需。 （请注意 SQLSetDescField 已在 ODBC 3.0 中添加。）若要执行手动绑定，则必须先获取的描述符句柄。  
  
```  
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

