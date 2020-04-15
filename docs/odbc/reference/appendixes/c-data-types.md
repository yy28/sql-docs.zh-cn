---
title: C 数据类型 |微软文档
ms.custom: ''
ms.date: 07/12/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- data types [ODBC], C data types
- C data types [ODBC], about C data types
- C data types [ODBC]
- C buffers [ODBC]
ms.assetid: b681d260-3dbb-47df-a616-4910d727add7
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 979bfe85e1e78b55718e1f12fdcfcc7583097bb4
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/14/2020
ms.locfileid: "81292297"
---
# <a name="c-data-types"></a>C 数据类型
ODBC C 数据类型指示用于在应用程序中存储数据的 C 缓冲区的数据类型。  
  
 所有驱动程序必须支持所有 C 数据类型。 这是必需的，因为所有驱动程序都必须支持它们支持的所有 C 类型，并且所有驱动程序都至少支持一个字符 SQL 类型。 由于字符 SQL 类型可以转换为和从所有 C 类型，因此所有驱动程序都必须支持所有 C 类型。  
  
 C 数据类型在**SQLBindCol**和**SQLGetData**函数中指定，这些函数带有*TargetType*参数，在**SQLBind参数**函数中使用*ValueType*参数指定。 还可以通过调用**SQLSetDescField**来设置 ARD 或 APD 的SQL_DESC_CONCISE_TYPE字段，或者使用*Type*参数（如果需要*的子类型*参数）调用**SQLSetDescRec**和设置为 ARD 或 APD 句柄*的描述符处理*参数来指定它。  
  
 下表列出了 C 数据类型的有效类型标识符。 该表还列出了对应于每个标识符的 ODBC C 数据类型以及此数据类型的定义。  
  
|C 类型标识符|ODBC C 型定义|C 类型|  
|-----------------------|--------------------|------------|  
|SQL_C_CHAR|SQLCHAR ||unsigned char *|  
|SQL_C_WCHAR|SQLWCHAR ||wchar_t *|  
|SQL_C_SSHORT[j]|SQLSMALLINT|short int|  
|SQL_C_USHORT[j]|SQLUSMALLINT|unsigned short int|  
|SQL_C_SLONG[j]|SQLINTEGER|long int|  
|SQL_C_ULONG[j]|SQLUINTEGER|unsigned long int|  
|SQL_C_FLOAT|SQLREAL|FLOAT|  
|SQL_C_DOUBLE|SQLDOUBLE，SQLFLOAT|double|  
|SQL_C_BIT|SQLCHAR|unsigned char|  
|SQL_C_STINYINT[j]|SQLSCHAR|signed char|  
|SQL_C_UTINYINT[j]|SQLCHAR|unsigned char|  
|SQL_C_SBIGINT|SQLBIGINT|_int64[h]|  
|SQL_C_UBIGINT|SQLUBIGINT|无符号_int64[h]|  
|SQL_C_BINARY|SQLCHAR ||unsigned char *|  
|SQL_C_BOOKMARK[i]|书签|无符号长 int_d_|  
|SQL_C_VARBOOKMARK|SQLCHAR ||unsigned char *|  
|所有 C 间隔数据类型|SQL_INTERVAL_STRUCT|请参阅本附录后面的[C 间隔结构](../../../odbc/reference/appendixes/c-interval-structure.md)部分。|  
  
 **C 类型标识符**SQL_C_TYPE_DATE[c]  
  
 **ODBC C 型定义**SQL_DATE_STRUCT  
  
 **C 类型**  
  
```  
struct tagDATE_STRUCT {  
   SQLSMALLINT year;  
   SQLUSMALLINT month;  
   SQLUSMALLINT day;    
} DATE_STRUCT;[a]  
```  
  
 **C 类型标识符**SQL_C_TYPE_TIME[c]  
  
 **ODBC C 型定义**SQL_TIME_STRUCT  
  
 **C 类型**  
  
```  
struct tagTIME_STRUCT {  
   SQLUSMALLINT hour;  
   SQLUSMALLINT minute;  
   SQLUSMALLINT second;  
} TIME_STRUCT;[a]  
```  
  
 **C 类型标识符**SQL_C_TYPE_TIMESTAMP[c]  
  
 **ODBC C 型定义**SQL_TIMESTAMP_STRUCT  
  
 **C 类型**  
  
```  
struct tagTIMESTAMP_STRUCT {  
   SQLSMALLINT year;  
   SQLUSMALLINT month;  
   SQLUSMALLINT day;  
   SQLUSMALLINT hour;  
   SQLUSMALLINT minute;  
   SQLUSMALLINT second;  
   SQLUINTEGER fraction;[b]   
} TIMESTAMP_STRUCT;[a]  
```  
  
 **C 类型标识符**SQL_C_NUMERIC  
  
 **ODBC C 型定义**SQL_NUMERIC_STRUCT  
  
 **C 类型**  
  
```  
struct tagSQL_NUMERIC_STRUCT {  
   SQLCHAR precision;  
   SQLSCHAR scale;  
   SQLCHAR sign[g];  
   SQLCHAR val[SQL_MAX_NUMERIC_LEN];[e], [f]   
} SQL_NUMERIC_STRUCT;  
```  
  
 **C 类型标识符**SQL_C_GUID  
  
 **ODBC C 型定义**SQLGUID  
  
 **C 类型**  
  
```  
struct tagSQLGUID {  
   DWORD Data1;  
   WORD Data2;  
   WORD Data3;  
   BYTE Data4[8];  
} SQLGUID;[k]  
```  
  
 [a] 日期时间 C 数据类型中的年份、月份、天、小时、分钟和第二个字段的值必须符合公历的约束。 （请参阅本附录后面的[公历约束](../../../odbc/reference/appendixes/constraints-of-the-gregorian-calendar.md)。  
  
 [b] 分数字段的值是每秒十亿分之一的数值，范围从 0 到 999，999，999（1 小于 10 亿）。 例如，半秒的分数字段的值为 500，000，000，000，000，000，千分之一秒（一毫秒）为 1，000，000，000，百万分之一秒（一微秒）的值为 1，000，十亿分之一秒（一纳秒）为 1。  
  
 [c] 在ODBC 2中。*x*，C 日期、时间和时间戳数据类型SQL_C_DATE、SQL_C_TIME和SQL_C_TIMESTAMP。  
  
 [d] ODBC 3 *.x*应用程序应使用SQL_C_VARBOOKMARK，而不是SQL_C_BOOKMARK。 当 ODBC 3 *.x*应用程序与 ODBC 2 配合使用时。*x*驱动程序，ODBC 3 *.x*驱动程序管理器将SQL_C_VARBOOKMARK映射到SQL_C_BOOKMARK。  
  
 [e] 数字以缩放整数的形式存储在SQL_NUMERIC_STRUCT结构的*val*字段中，采用小端整模式（最左侧字节是最不重要的字节）。 例如，数字 10.001 基 10（比例为 4）将缩放为 100010 整数。 由于这是十六进制格式的 186AA，因此SQL_NUMERIC_STRUCT的值将是"AA 86 01 00 00 ...00"，**由SQL_MAX_NUMERIC_LEN定义**#define字节数。  
  
 有关**SQL_NUMERIC_STRUCT**的详细信息，请参阅[HOWTO：使用SQL_NUMERIC_STRUCT检索数字数据](retrieve-numeric-data-sql-numeric-struct-kb222831.md)。  
  
 [f] SQL_C_NUMERIC数据类型的精度和缩放字段用于从应用程序输入以及从驱动程序输出到应用程序。 当驱动程序将数值写入SQL_NUMERIC_STRUCT时，它将使用自己的特定于驱动程序的默认值作为*精度*字段的值，它将在*缩放*字段的应用程序描述符的SQL_DESC_SCALE字段中使用该值（默认值为 0）。 应用程序可以通过设置应用程序描述符的SQL_DESC_PRECISION和SQL_DESC_SCALE字段来提供其自己的精度和缩放值。  
  
 [g] 符号字段为 1（如果为正），0（如果为负）。  
  
 [h] _int64可能无法由某些编译器提供。  
  
 [i] _SQL_C_BOOKMARK已在 ODBC 3 *.x*中弃用。  
  
 [j] _SQL_C_SHORT、SQL_C_LONG 和 SQL_C_TINYINT已在 ODBC 中替换为已签名和未签名的类型：SQL_C_SSHORT和SQL_C_USHORT、SQL_C_SLONG和SQL_C_ULONG以及SQL_C_STINYINT和SQL_C_UTINYINT。 应与 ODBC 2 配合使用的 ODBC 3 *.x*驱动程序。*x*应用程序应支持SQL_C_SHORT、SQL_C_LONG和SQL_C_TINYINT，因为调用它们时，驱动程序管理器会将它们传递给驱动程序。  
  
 [k] SQL_C_GUID只能转换为SQL_CHAR或SQL_WCHAR。  
  
 本节包含以下主题。  
  
-   [64 位整数结构](../../../odbc/reference/appendixes/64-bit-integer-structures.md)  
  
## <a name="see-also"></a>另请参阅  
 [ODBC 中的 C 数据类型](../../../odbc/reference/develop-app/c-data-types-in-odbc.md)
