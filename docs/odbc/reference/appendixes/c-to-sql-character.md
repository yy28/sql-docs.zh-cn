---
title: 从 C 到 SQL：字符 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- character data type [ODBC]
- data conversions from C to SQL types [ODBC], character
- converting data from c to SQL types [ODBC], character
ms.assetid: be66188a-ebdb-4c9e-af72-c379886766fa
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 0f30e0cf7622de5124cb151288417bb508354ce0
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/15/2019
ms.locfileid: "68037721"
---
# <a name="c-to-sql-character"></a>从 C 到 SQL：字符
ODBC C 数据类型的字符的标识符是：  
  
 SQL_C_CHAR  
  
 SQL_C_WCHAR  
  
 下表显示 ODBC SQL 数据类型可能会将 C 字符数据转换为。 列和表中的条款的说明，请参阅[转换将数据从 C 到 SQL 数据类型](../../../odbc/reference/appendixes/converting-data-from-c-to-sql-data-types.md)。  
  
> [!NOTE]  
>  C 字符数据转换为 Unicode SQL 数据，Unicode 数据的长度必须为偶数。  
  
|SQL 类型标识符|测试|SQLSTATE|  
|-------------------------|----------|--------------|  
|SQL_CHAR<br /><br /> SQL_VARCHAR<br /><br /> SQL_LONGVARCHAR|数据的字节长度 < = 列长度。<br /><br /> 数据的字节长度 > 列长度。|不适用<br /><br /> 22001|  
|SQL_WCHAR<br /><br /> SQL_WVARCHAR<br /><br /> SQL_WLONGVARCHAR|字符数据的长度 < = 列长度。<br /><br /> 字符数据的长度 > 列长度。|不适用<br /><br /> 22001|  
|SQL_DECIMAL<br /><br /> SQL_NUMERIC<br /><br /> SQL_TINYINT<br /><br /> SQL_SMALLINT<br /><br /> SQL_INTEGER SQL_BIGINT|转换为而无需截断数据<br /><br /> 数据转换使用的小数位数 [e] 的截断<br /><br /> 数据的转换会导致整体 （而不是小数） 数字 [e]<br /><br /> 数据值不是*数字文本*|不适用<br /><br /> 22001<br /><br /> 22001<br /><br /> 22018|  
|SQL_REAL<br /><br /> SQL_FLOAT<br /><br /> SQL_DOUBLE|数据是数字转换到的数据类型的范围内<br /><br /> 数据是数字转换到的数据类型的范围之外<br /><br /> 数据值不是*数字文本*|不适用<br /><br /> 22003<br /><br /> 22018|  
|SQL_BIT|数据为 0 或 1<br /><br /> 数据为大于 0，小于 2，且不等于 1<br /><br /> 数据是小于 0 或大于或等于 2<br /><br /> 数据不是*数字文本*|不适用<br /><br /> 22001<br /><br /> 22003<br /><br /> 22018|  
|SQL_BINARY<br /><br /> SQL_VARBINARY<br /><br /> SQL_LONGVARBINARY|（数据的字节长度） / 2 < = 列的字节长度<br /><br /> （数据的字节长度） / 2 > 列的字节长度<br /><br /> 数据值不是十六进制值|不适用<br /><br /> 22001<br /><br /> 22018|  
|SQL_TYPE_DATE|数据值是一个有效*ODBC 日期文本*<br /><br /> 数据值是否有效*ODBC 时间戳文本*; 时间部分为零<br /><br /> 数据值是否有效*ODBC 时间戳文本*; 时间部分为非零值 [a]<br /><br /> 数据值不是有效*ODBC 日期文本*或*ODBC 时间戳文本*|不适用<br /><br /> 不适用<br /><br /> 22008<br /><br /> 22018|  
|SQL_TYPE_TIME|数据值是一个有效*ODBC 时间文字*<br /><br /> 数据值是否有效*ODBC 时间戳文本*; 小数秒部分为零 [b]<br /><br /> 数据值是否有效*ODBC 时间戳文本*; 小数秒部分为非零值 [b]<br /><br /> 数据值不是有效*ODBC 时间文字*或*ODBC 时间戳文本*|不适用<br /><br /> 不适用<br /><br /> 22008<br /><br /> 22018|  
|SQL_TYPE_TIMESTAMP|数据值是否有效*ODBC 时间戳文本*; 小数部分不会被截断的秒部分<br /><br /> 数据值是否有效*ODBC 时间戳文本*; 小数部分被截断的秒部分<br /><br /> 数据值是否有效*ODBC 日期文本*[c]<br /><br /> 数据值是否有效*ODBC 时间文字*[d]<br /><br /> 数据值不是有效*ODBC 日期文本*， *ODBC 时间文字*，或*ODBC 时间戳文本*|不适用<br /><br /> 22008<br /><br /> 不适用<br /><br /> 不适用<br /><br /> 22018|  
|所有 SQL 间隔类型|数据值是否有效*间隔值*; 不会发生截断<br /><br /> 数据值是否有效*间隔值*; 中的字段之一的值将被截断<br /><br /> 数据值不是有效的时间间隔文本|不适用<br /><br /> 22015<br /><br /> 22018|  
  
 [a] 的时间戳的时间部分被截断。  
  
 [忽略时间戳 b] 上，日期部分。  
  
 [时间戳 c] 的时间部分设置为零。  
  
 [时间戳 d] 上，日期部分设置为当前日期。  
  
 [e] 的驱动程序/数据源有效地等待，直到收到整个字符串 (即使字符数据通过调用发送分块**SQLPutData**) 然后再尝试执行转换。  
  
 C 字符数据转换为数字、 日期、 时间戳 SQL 数据时，将忽略前导空格和尾随空格。  
  
 C 字符数据转换为 SQL 的二进制数据，每个两个字节的字符数据将转换为单字节 （8 位） 的二进制数据。 字符数据的每个两个字节表示十六进制格式的数字。 例如，"01"转换为二进制 00000001 和"FF"转换为二进制 11111111。  
  
 该驱动程序始终将十六进制数字的对转换为单个字节并将忽略 null 终止字节。 因此，如果字符字符串的长度为奇数，将不转换 （如果有，不包括 null 终止字节） 的字符串的最后一个字节。  
  
> [!NOTE]  
>  应用程序开发人员我们建议您不要将字符 C 数据绑定到二进制的 SQL 数据类型。 此转换通常是效率低下，而且很慢。
