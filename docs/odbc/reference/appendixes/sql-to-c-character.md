---
title: SQL 到 C：字符 |微软文档
ms.custom: ''
ms.date: 01/19/2019
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- converting data from SQL to C types [ODBC], character
- character data type [ODBC]
- data conversions from SQL to C types [ODBC], character
ms.assetid: 7fdb7f38-b64d-48f2-bcb4-1ca96b2bbdb6
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 3486c0fcf5cefc39c4b85af814d7d3c1d609b4e3
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/14/2020
ms.locfileid: "81296667"
---
# <a name="sql-to-c-character"></a>从 SQL 到 C：字符

字符 ODBC SQL 数据类型的标识符如下：

- SQL_CHAR
- SQL_VARCHAR
- SQL_LONGVARCHAR
- SQL_WCHAR
- SQL_WVARCHAR
- SQL_WLONGVARCHAR

下表显示了可转换为字符 SQL 数据的 ODBC C 数据类型。 有关表中列和术语的说明，请参阅[将数据从 SQL 转换为 C 数据类型](../../../odbc/reference/appendixes/converting-data-from-sql-to-c-data-types.md)。  

|C 类型标识符|测试|目标价值Ptr|StrLen_or_IndPtr|SQLSTATE|
|:----------------|:---|:-------------|:---------------|:-------|
|SQL_C_CHAR|<*缓冲区长度*的数据字节长度<br /><br /> 数据>字节长度 =*缓冲区长度*|数据<br /><br /> 截断的数据|以字节为单位的数据长度<br /><br /> 以字节为单位的数据长度|不适用<br /><br /> 01004|  
|SQL_C_WCHAR|<*缓冲区长度*的数据字符长度<br /><br /> 数据>的字符长度 =*缓冲区长度*|数据<br /><br /> 截断的数据|字符中的数据长度<br /><br /> 字符中的数据长度|不适用<br /><br /> 01004|  
|SQL_C_STINYINTSQL_C_UTINYINT SQL_C_TINYINT SQL_C_USHORT SQL_C_SSHORTSQL_C_SBIGINTSQL_C_UBIGINTSQL_C_UBIGINTSQL_C_UBIGINTSQL_C_LONGSQL_C_LONGSQL_C_LONG SQL_C_NUMERIC SQL_C_ULONG SQL_C_SLONGSQL_C_SHORTSQL_C_SHORT|在不截断的情况下转换的数据[b]<br /><br /> 使用小数数字截断转换的数据[a]<br /><br /> 数据转换将导致整体数字（相对于小数）的丢失[a]<br /><br /> 数据不是*数字文本*[b]|数据<br /><br /> 截断的数据<br /><br /> Undefined<br /><br /> Undefined|C 数据类型的字节数<br /><br /> C 数据类型的字节数<br /><br /> Undefined<br /><br /> Undefined|不适用<br /><br /> 01S07<br /><br /> 22003<br /><br /> 22018|  
|SQL_C_FLOATSQL_C_DOUBLE|数据在要转换数字的数据类型范围内[a]<br /><br /> 数据不在要转换数字的数据类型范围之外[a]<br /><br /> 数据不是*数字文本*[b]|数据<br /><br /> Undefined<br /><br /> Undefined|C 数据类型的大小<br /><br /> Undefined<br /><br /> Undefined|不适用<br /><br /> 22003<br /><br /> 22018|  
|SQL_C_BIT|数据为 0 或 1<br /><br /> 数据大于 0，小于 2，不等于 1<br /><br /> 数据小于 0 或大于或等于 2<br /><br /> 数据不是*数字文本*|数据<br /><br /> 截断的数据<br /><br /> Undefined<br /><br /> Undefined|1[b]<br /><br /> 1[b]<br /><br /> Undefined<br /><br /> Undefined|不适用<br /><br /> 01S07<br /><br /> 22003<br /><br /> 22018|  
|SQL_C_BINARY|数据<字节长度 =*缓冲区长度*<br /><br /> >*缓冲区长度*的数据字节长度|数据<br /><br /> 截断的数据|以字节为单位的数据长度<br /><br /> 数据长度|不适用<br /><br /> 01004|  
|SQL_C_TYPE_DATE|数据值是有效的*日期值*[a]<br /><br /> 数据值是有效的*时间戳值*;时间部分为零[a]<br /><br /> 数据值是有效的*时间戳值*;时间部分是非零[a]，[c]<br /><br /> 数据值不是有效的*日期值*或*时间戳值*[a]|数据<br /><br /> 数据<br /><br /> 截断的数据<br /><br /> Undefined|6[b]<br /><br /> 6[b]<br /><br /> 6[b]<br /><br /> Undefined|不适用<br /><br /> 不适用<br /><br /> 01S07<br /><br /> 22018|  
|SQL_C_TYPE_TIME|数据值是有效的*时间值，小数秒值为 0*[a]<br /><br /> 数据值是有效的*时间戳值或有效的时间值*;小数秒部分为零[a]，[d]<br /><br /> 数据值是有效的*时间戳值*;小数秒部分是非零[a]，[d]，[e]<br /><br /> 数据值不是有效的*时间值*或*时间戳值*[a]|数据<br /><br /> 数据<br /><br /> 截断的数据<br /><br /> Undefined|6[b]<br /><br /> 6[b]<br /><br /> 6[b]<br /><br /> Undefined|不适用<br /><br /> 不适用<br /><br /> 01S07<br /><br /> 22018|  
|SQL_C_TYPE_TIMESTAMP|数据值是有效的*时间戳值或有效的时间值*;分数秒部分未截断 [a]<br /><br /> 数据值是有效的*时间戳值或有效的时间值*;小数秒部分截断[a]<br /><br /> 数据值是有效的*日期值*[a]<br /><br /> 数据值是有效的*时间值*[a]<br /><br /> 数据值不是有效的*日期值*、*时间值*或*时间戳值*[a]|数据<br /><br /> 截断的数据<br /><br /> 数据[f]<br /><br /> 数据[g]<br /><br /> Undefined|16[b]<br /><br /> 16[b]<br /><br /> 16[b]<br /><br /> 16[b]<br /><br /> Undefined|不适用<br /><br /> 01S07<br /><br /> 不适用<br /><br /> 不适用<br /><br /> 22018|  
|所有 C 间隔类型|数据值是有效的*间隔值*;无截断<br /><br /> 数据值是有效的*间隔值*;截断一个或多个尾随字段<br /><br /> 数据是有效的间隔;前导场显著精度丢失<br /><br /> 数据值不是有效的间隔值|数据<br /><br /> 截断的数据<br /><br /> Undefined<br /><br /> Undefined|以字节为单位的数据长度<br /><br /> 以字节为单位的数据长度<br /><br /> Undefined<br /><br /> Undefined|不适用<br /><br /> 01S07<br /><br /> 22015<br /><br /> 22018|  
|&nbsp;|&nbsp;|&nbsp;|&nbsp;|&nbsp;|

 [a] 此转换将忽略*缓冲区长度*的值。 驱动程序假定 **目标价值Ptr*的大小是 C 数据类型的大小。  
  
 [b] 这是相应的 C 数据类型的大小。  
  
 [c]*时间戳值*的时间部分被截断。  
  
 [d]*时间戳值*的日期部分将被忽略。  
  
 [e] 时间戳的小秒部分被截断。  
  
 [f] 时间戳结构的时间字段设置为零。  
  
 [g] 时间戳结构的日期字段设置为当前日期。  

**额外空间**

将 SQL 字符数据转换为以下任一类型时，将忽略前导空格和尾随空格：

- date
- numeric
- time
- timestamp
- 间隔 C 数据
