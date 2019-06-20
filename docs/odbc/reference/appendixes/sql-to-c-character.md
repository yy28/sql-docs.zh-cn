---
title: 从 SQL 到 C：字符 |Microsoft Docs
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: e3a0a7036d67716a3d90bd8953a3c7ba2c575c92
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/15/2019
ms.locfileid: "63259511"
---
# <a name="sql-to-c-character"></a>从 SQL 到 C：字符

对于字符 ODBC SQL 数据类型标识符如下所示：

- SQL_CHAR
- SQL_VARCHAR
- SQL_LONGVARCHAR
- SQL_WCHAR
- SQL_WVARCHAR
- SQL_WLONGVARCHAR

下表显示 ODBC C 数据类型可能会转换成字符 SQL 数据。 列和表中的条款的说明，请参阅[从 SQL 到 C 数据类型的转换的数据](../../../odbc/reference/appendixes/converting-data-from-sql-to-c-data-types.md)。  

|C 类型标识符|测试|TargetValuePtr|StrLen_or_IndPtr|SQLSTATE|
|:----------------|:---|:-------------|:---------------|:-------|
|SQL_C_CHAR|数据的字节长度 < *BufferLength*<br /><br /> 数据的字节长度 > = *BufferLength*|数据<br /><br /> 截断的数据|以字节为单位的数据的长度<br /><br /> 以字节为单位的数据的长度|不适用<br /><br /> 01004|  
|SQL_C_WCHAR|字符数据的长度 < *BufferLength*<br /><br /> 字符数据的长度 > = *BufferLength*|数据<br /><br /> 截断的数据|以字符为单位的数据的长度<br /><br /> 以字符为单位的数据的长度|不适用<br /><br /> 01004|  
|SQL_C_STINYINT SQL_C_UTINYINT SQL_C_TINYINT  SQL_C_SBIGINT SQL_C_UBIGINT SQL_C_SSHORT SQL_C_USHORT SQL_C_SHORT  SQL_C_SLONG SQL_C_ULONG SQL_C_LONG  SQL_C_NUMERIC|数据转换而无需截断 [b]<br /><br /> 数据转换使用的小数位数 [a] 的截断<br /><br /> 数据的转换会导致整体 （而不是小数） 数字，[a]<br /><br /> 数据不是*数值文字*[b]。|数据<br /><br /> 截断的数据<br /><br /> 未定义<br /><br /> 未定义|C 数据类型的字节数<br /><br /> C 数据类型的字节数<br /><br /> 未定义<br /><br /> 未定义|不适用<br /><br /> 01S07<br /><br /> 22003<br /><br /> 22018|  
|SQL_C_FLOAT SQL_C_DOUBLE|数据位于范围内数字转换到的数据类型 [a]<br /><br /> 数据不在范围内的数字转换到的数据类型 [a]<br /><br /> 数据不是*数值文字*[b]。|数据<br /><br /> 未定义<br /><br /> 未定义|C 数据类型的大小<br /><br /> 未定义<br /><br /> 未定义|不适用<br /><br /> 22003<br /><br /> 22018|  
|SQL_C_BIT|数据为 0 或 1<br /><br /> 数据为大于 0，小于 2，且不等于 1<br /><br /> 数据是小于 0 或大于或等于 2<br /><br /> 数据不是*数字文本*|数据<br /><br /> 截断的数据<br /><br /> 未定义<br /><br /> 未定义|1[b]<br /><br /> 1[b]<br /><br /> 未定义<br /><br /> 未定义|不适用<br /><br /> 01S07<br /><br /> 22003<br /><br /> 22018|  
|SQL_C_BINARY|数据的字节长度 < = *BufferLength*<br /><br /> 数据的字节长度 > *BufferLength*|数据<br /><br /> 截断的数据|以字节为单位的数据的长度<br /><br /> 数据的长度|不适用<br /><br /> 01004|  
|SQL_C_TYPE_DATE|数据值是否有效*日期值*[a]<br /><br /> 数据值是否有效*时间戳值*; 时间部分为零 [a]<br /><br /> 数据值是否有效*时间戳值*; 时间部分为非零值 [a]，[c]<br /><br /> 数据值不是有效*日期值*或*时间戳值*[a]|数据<br /><br /> 数据<br /><br /> 截断的数据<br /><br /> 未定义|6[b]<br /><br /> 6[b]<br /><br /> 6[b]<br /><br /> 未定义|不适用<br /><br /> 不适用<br /><br /> 01S07<br /><br /> 22018|  
|SQL_C_TYPE_TIME|数据值是否有效*时间值和值为 0 秒的小数部分*[a]<br /><br /> 数据值是否有效*时间戳值或有效的时间值*; 小数秒部分为零 [a]，[d]<br /><br /> 数据值是否有效*时间戳值*; 小数秒部分为非零值 [a]，[d] [e]<br /><br /> 数据值不是有效*时间值*或*时间戳值*[a]|数据<br /><br /> 数据<br /><br /> 截断的数据<br /><br /> 未定义|6[b]<br /><br /> 6[b]<br /><br /> 6[b]<br /><br /> 未定义|不适用<br /><br /> 不适用<br /><br /> 01S07<br /><br /> 22018|  
|SQL_C_TYPE_TIMESTAMP|数据值是否有效*时间戳值或有效的时间值*; 小数秒部分不会被截断 [a]<br /><br /> 数据值是否有效*时间戳值或有效的时间值*; 小数秒部分截断 [a]<br /><br /> 数据值是否有效*日期值*[a]<br /><br /> 数据值是否有效*时间值*[a]<br /><br /> 数据值不是有效*日期值*，*时间值*，或*时间戳值*[a]|数据<br /><br /> 截断的数据<br /><br /> Data[f]<br /><br /> Data[g]<br /><br /> 未定义|16[b]<br /><br /> 16[b]<br /><br /> 16[b]<br /><br /> 16[b]<br /><br /> 未定义|不适用<br /><br /> 01S07<br /><br /> 不适用<br /><br /> 不适用<br /><br /> 22018|  
|所有 C 间隔类型|数据值是否有效*间隔值*; 未截断<br /><br /> 数据值是否有效*间隔值*; 的一个或多个尾部字段截断<br /><br /> 数据是有效的时间间隔;前导字段重要精度将丢失<br /><br /> 数据值不是有效的间隔值|数据<br /><br /> 截断的数据<br /><br /> 未定义<br /><br /> 未定义|以字节为单位的数据的长度<br /><br /> 以字节为单位的数据的长度<br /><br /> 未定义<br /><br /> 未定义|不适用<br /><br /> 01S07<br /><br /> 22015<br /><br /> 22018|  
|&nbsp;|&nbsp;|&nbsp;|&nbsp;|&nbsp;|

 [a] 的值*BufferLength*忽略此转换。 驱动程序假定的大小 **TargetValuePtr*是 C 数据类型的大小。  
  
 [b] 这是相应的 C 数据类型的大小。  
  
 [c] 的时间部分*时间戳值*被截断。  
  
 [d] 的日期部分*时间戳值*将被忽略。  
  
 [e] 秒的小数部分的时间戳会被截断。  
  
 [时间戳结构 f] 的时间字段设置为零。  
  
 [时间戳结构 g] 上，日期字段将设置为当前日期。  

**多余的空格**

SQL 字符数据转换为任何以下类型时，将忽略前导空格和尾随空格：

- date
- NUMERIC
- time
- TIMESTAMP
- 数据间隔 C
