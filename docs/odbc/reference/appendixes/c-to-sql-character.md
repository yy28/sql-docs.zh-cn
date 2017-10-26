---
title: "To SQL 的 C： 字符 |Microsoft 文档"
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
- character data type [ODBC]
- data conversions from C to SQL types [ODBC], character
- converting data from c to SQL types [ODBC], character
ms.assetid: be66188a-ebdb-4c9e-af72-c379886766fa
caps.latest.revision: 8
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: e8d6ab676fc351afd7819c1fe60d59a58bfe7207
ms.contentlocale: zh-cn
ms.lasthandoff: 09/09/2017

---
# <a name="c-to-sql-character"></a>To SQL 的 C： 字符
ODBC C 数据类型的字符的标识符都是：  
  
 SQL_C_CHAR  
  
 SQL_C_WCHAR  
  
 下表显示 ODBC SQL C 字符数据可能转换到的目标的数据类型。 列和表中的条款的说明，请参阅[C 中为 SQL 数据类型的转换的数据](../../../odbc/reference/appendixes/converting-data-from-c-to-sql-data-types.md)。  
  
> [!NOTE]  
>  当 C 字符数据转换为 Unicode SQL 数据时，Unicode 数据的长度必须为偶数。  
  
|SQL 类型标识符|测试|SQLSTATE|  
|-------------------------|----------|--------------|  
|SQL_CHAR<br /><br /> SQL_VARCHAR<br /><br /> SQL_LONGVARCHAR|数据的字节长度 < = 列长度。<br /><br /> 数据的字节长度 > 列长度。|不适用<br /><br /> 22001|  
|SQL_WCHAR<br /><br /> SQL_WVARCHAR<br /><br /> SQL_WLONGVARCHAR|字符数据的长度 < = 列长度。<br /><br /> 字符数据的长度 > 列长度。|不适用<br /><br /> 22001|  
|SQL_DECIMAL<br /><br /> SQL_NUMERIC<br /><br /> SQL_TINYINT<br /><br /> SQL_SMALLINT<br /><br /> SQL_INTEGER SQL_BIGINT|转换而不会截断数据<br /><br /> 数据转换使用的小数位数 [e] 的截断<br /><br /> 数据的转换将导致丢失的整体 （而不是小数） 位数 [e]<br /><br /> 数据值不是*数字文本*|不适用<br /><br /> 22001<br /><br /> 22001<br /><br /> 22018|  
|SQL_REAL<br /><br /> SQL_FLOAT<br /><br /> SQL_DOUBLE|数据是数转换到的目标的数据类型的范围内<br /><br /> 数据超出了范围数转换到的目标的数据类型<br /><br /> 数据值不是*数字文本*|不适用<br /><br /> 22003<br /><br /> 22018|  
|SQL_BIT|数据为 0 或 1<br /><br /> 数据为大于 0，小于 2，且不等于 1<br /><br /> 数据是小于 0 或大于或等于 2<br /><br /> 数据不是*数字文本*|不适用<br /><br /> 22001<br /><br /> 22003<br /><br /> 22018|  
|SQL_BINARY<br /><br /> SQL_VARBINARY<br /><br /> SQL_LONGVARBINARY|（数据的字节长度） / 2 < = 列字节长度<br /><br /> （数据的字节长度） / 2 > 列字节长度<br /><br /> 数据值不是十六进制值|不适用<br /><br /> 22001<br /><br /> 22018|  
|SQL_TYPE_DATE|数据值是一个有效*ODBC 日期文本*<br /><br /> 数据值是一个有效*ODBC 时间戳文本*; 时间部分为零<br /><br /> 数据值是一个有效*ODBC 时间戳文本*; 时间部分为非零 [a]<br /><br /> 数据值不是有效*ODBC 日期文字*或*ODBC 时间戳文本*|不适用<br /><br /> 不适用<br /><br /> 22008<br /><br /> 22018|  
|SQL_TYPE_TIME|数据值是一个有效*ODBC 时间文字*<br /><br /> 数据值是一个有效*ODBC 时间戳文本*; 小数秒部分是零 [b]<br /><br /> 数据值是一个有效*ODBC 时间戳文本*; 小数秒部分为非零 [b]<br /><br /> 数据值不是有效*ODBC 时间文字*或*ODBC 时间戳文本*|不适用<br /><br /> 不适用<br /><br /> 22008<br /><br /> 22018|  
|SQL_TYPE_TIMESTAMP|数据值是一个有效*ODBC 时间戳文本*; 小数秒部分不会被截断<br /><br /> 数据值是一个有效*ODBC 时间戳文本*; 小数秒部分被截断<br /><br /> 数据值是一个有效*ODBC 日期文字*[c]<br /><br /> 数据值是一个有效*ODBC 时间文字*[d]<br /><br /> 数据值不是有效*ODBC 日期文字*， *ODBC 时间文字*，或*ODBC 时间戳文本*|不适用<br /><br /> 22008<br /><br /> 不适用<br /><br /> 不适用<br /><br /> 22018|  
|所有 SQL 间隔类型|数据值是一个有效*间隔值*; 不会发生截断<br /><br /> 数据值是一个有效*间隔值*; 中的字段之一的值将被截断<br /><br /> 数据值不是文本的有效间隔|不适用<br /><br /> 22015<br /><br /> 22018|  
  
 [a] 的时间戳的时间部分将被截断。  
  
 [b] 的日期部分的时间戳将被忽略。  
  
 [c] 的时间部分的时间戳设置为零。  
  
 [d] 上，日期部分的时间戳设置为当前日期。  
  
 [e] 上，驱动程序中的数据源有效地等待，直到收到整个字符串 (即使字符数据分段发送到调用**SQLPutData**) 然后再尝试执行转换。  
  
 C 字符数据转换为数字、 日期、 时间戳 SQL 数据时，将忽略前导空格和尾随空格。  
  
 当 C 字符数据转换为二进制 SQL 数据时，每个两个字节的字符数据将转换为二进制数据的一个字节 （8 位）。 字符数据每两个字节表示以十六进制格式的数字。 例如，"01"将转换为二进制 00000001 和"FF"转换为二进制 11111111。  
  
 该驱动程序始终将对十六进制数字转换为单个字节，并忽略 null 终止字节。 因此，如果字符串的长度为奇数，将不转换 （如果有的话，不包括的 null 终止字节，） 的字符串的最后一个字节。  
  
> [!NOTE]  
>  应用程序开发人员我们建议您不要将字符 C 数据绑定到二进制的 SQL 数据类型。 此转换通常是效率低下，而且很慢。

