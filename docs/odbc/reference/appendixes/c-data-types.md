---
title: C 数据类型 |Microsoft Docs
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 3f948b50fae0995e16024ac41d8dd891630d1dbe
ms.sourcegitcommit: 6443f9a281904af93f0f5b78760b1c68901b7b8d
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/11/2018
ms.locfileid: "53208457"
---
# <a name="c-data-types"></a>C 数据类型
ODBC C 数据类型表示用于在应用程序中存储数据的 C 缓冲区的数据类型。  
  
 所有驱动程序必须支持所有的 C 数据类型。 这是必需的因为所有驱动程序必须支持到它们支持的 SQL 类型可以进行转换，所有 C 类型和所有驱动程序都支持至少一个字符 SQL 类型。 与所有 C 类型可以转换的字符 SQL 类型，因为所有驱动程序必须支持所有的 C 类型。  
  
 中指定的 C 数据类型**SQLBindCol**并**SQLGetData**函数与*TargetType*自变量并在**SQLBindParameter**函数与*ValueType*参数。 它还可以指定通过调用**SQLSetDescField**若要设置 SQL_DESC_CONCISE_TYPE 字段 ARD 或 APD，或通过调用**SQLSetDescRec**与*类型*自变量 （和*子类型*参数，如果需要) 和*DescriptorHandle*参数设置为 ARD 或 APD 的句柄。  
  
 下表列出了有效的类型标识符的 C 数据类型。 该表还列出对应于每个标识符和此数据类型的定义的 ODBC C 数据类型。  
  
|C 类型标识符|ODBC C typedef|C 类型|  
|-----------------------|--------------------|------------|  
|SQL_C_CHAR|SQLCHAR *|unsigned char *|  
|SQL_C_WCHAR|SQLWCHAR *|wchar_t *|  
|SQL_C_SSHORT [j]|SQLSMALLINT|short int|  
|SQL_C_USHORT [j]|SQLUSMALLINT|无符号短整数|  
|SQL_C_SLONG [j]|SQLINTEGER|long int|  
|SQL_C_ULONG [j]|SQLUINTEGER|无符号长整型|  
|SQL_C_FLOAT|SQLREAL|FLOAT|  
|SQL_C_DOUBLE|SQLDOUBLE SQLFLOAT|double|  
|SQL_C_BIT|SQLCHAR|无符号的 char|  
|SQL_C_STINYINT [j]|SQLSCHAR|有符号的字符|  
|为 SQL_C_UTINYINT [j]|SQLCHAR|无符号的 char|  
|SQL_C_SBIGINT|SQLBIGINT|_int64 [h]|  
|SQL_C_UBIGINT|SQLUBIGINT|无符号的 _int64 [h]|  
|SQL_C_BINARY|SQLCHAR *|unsigned char *|  
|SQL_C_BOOKMARK [i]|书签|无符号 long int [d]|  
|SQL_C_VARBOOKMARK|SQLCHAR *|unsigned char *|  
|所有 C 间隔数据类型|SQL_INTERVAL_STRUCT|请参阅[C 间隔结构](../../../odbc/reference/appendixes/c-interval-structure.md)部分中的，稍后在本附录中。|  
  
 **C 类型标识符**SQL_C_TYPE_DATE [c]  
  
 **ODBC C typedef** SQL_DATE_STRUCT  
  
 **C 类型**  
  
```  
struct tagDATE_STRUCT {  
   SQLSMALLINT year;  
   SQLUSMALLINT month;  
   SQLUSMALLINT day;    
} DATE_STRUCT;[a]  
```  
  
 **C 类型标识符**SQL_C_TYPE_TIME [c]  
  
 **ODBC C typedef** SQL_TIME_STRUCT  
  
 **C 类型**  
  
```  
struct tagTIME_STRUCT {  
   SQLUSMALLINT hour;  
   SQLUSMALLINT minute;  
   SQLUSMALLINT second;  
} TIME_STRUCT;[a]  
```  
  
 **C 类型标识符**SQL_C_TYPE_TIMESTAMP [c]  
  
 **ODBC C typedef** SQL_TIMESTAMP_STRUCT  
  
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
  
 **ODBC C typedef** SQL_NUMERIC_STRUCT  
  
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
  
 **ODBC C typedef** SQLGUID  
  
 **C 类型**  
  
```  
struct tagSQLGUID {  
   DWORD Data1;  
   WORD Data2;  
   WORD Data3;  
   BYTE Data4[8];  
} SQLGUID;[k]  
```  
  
 [a] 的年、 月、 日、 小时、 分钟、 和 datetime C 数据类型中的第二个字段的值必须符合公历的约束。 (请参阅[公历的约束](../../../odbc/reference/appendixes/constraints-of-the-gregorian-calendar.md)本附录中更高版本。)  
  
 [b] 部分字段的值是第二个和范围是从 0 到 999999999 (1 小于 10 亿) 的十亿分之一。 例如，半秒的部分字段的值是 500,000,000，秒的千分位的是 1000000，对于第二个万，（1 毫秒） （一微秒） 为 1000，对于第 10 亿用户的第二个 （一纳秒） 为 1。  
  
 [c] 在 ODBC 2。*x*，C 日期、 时间和时间戳数据类型为 SQL_C_DATE、 SQL_C_TIME 和 SQL_C_TIMESTAMP。  
  
 [d] ODBC 3 *.x*应用程序应使用 SQL_C_VARBOOKMARK，不 SQL_C_BOOKMARK。 当 ODBC 3 *.x*应用程序适用于 ODBC 2。*x*驱动程序，ODBC 3 *.x*驱动程序管理器将映射到 SQL_C_BOOKMARK SQL_C_VARBOOKMARK。  
  
 [e] 的数字将存储在*val* SQL_NUMERIC_STRUCT 结构作为扩展的整数，小 endian 模式 （按最低有效字节的最左侧字节） 中的字段。 例如，数字 10.001 基数为 10，小数位数为 4，缩放为 100010 的整数。 由于这是以十六进制格式的 186AA，SQL_NUMERIC_STRUCT 中的值将为"AA 86 01 00 00...00"，由 SQL_MAX_NUMERIC_LEN 定义的字节数 **#define**。  
  
 有关详细信息**SQL_NUMERIC_STRUCT**，请参阅[操作方法：检索数值数据使用 SQL_NUMERIC_STRUCT](retrieve-numeric-data-sql-numeric-struct-kb222831.md)。  
  
 [SQL_C_NUMERIC 数据 f] 的精度和小数位数字段键入 areused 从应用程序的输入和输出从驱动程序到应用程序。 在驱动程序将数字的值写入到 SQL_NUMERIC_STRUCT，它将使用其自己特定于驱动程序的默认为值*精度*字段中，并且它将在应用程序描述符 （SQL_DESC_SCALE 字段中使用值其默认值为 0） 的*规模*字段。 应用程序可以通过设置应用程序描述符的 SQL_DESC_PRECISION 和 SQL_DESC_SCALE 字段的精度和小数位数提供其自己的值。  
  
 [g] 的登录字段为 1，如果为正数，0，如果为负数。  
  
 [小时] _int64 可能未提供的某些编译器中。  
  
 [ODBC 3 中已弃用 i] _SQL_C_BOOKMARK *.x*。  
  
 [j] _SQL_C_SHORT、 SQL_C_LONG 和 SQL_C_TINYINT 已替换为在 ODBC 中有符号和无符号类型：SQL_C_SSHORT 和 SQL_C_USHORT、 SQL_C_SLONG 和 SQL_C_ULONG，和 SQL_C_STINYINT 和 SQL_C_UTINYINT。 ODBC 3 *.x*驱动程序，它应适用于 ODBC 2。*x*应用程序应支持 SQL_C_SHORT、 SQL_C_LONG 和 SQL_C_TINYINT，因为它们调用时，驱动程序管理器将其传递通过给驱动程序。  
  
 [可以仅向 SQL_CHAR 或 SQL_WCHAR 转换 k] SQL_C_GUID。  
  
 本部分包含以下主题。  
  
-   [64 位整数结构](../../../odbc/reference/appendixes/64-bit-integer-structures.md)  
  
## <a name="see-also"></a>请参阅  
 [ODBC 中的 C 数据类型](../../../odbc/reference/develop-app/c-data-types-in-odbc.md)
