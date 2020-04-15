---
title: C 到 SQL：字符 |微软文档
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: acde0d2a79492607185d56d3082797c79a100fa2
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/14/2020
ms.locfileid: "81292028"
---
# <a name="c-to-sql-character"></a>从 C 到 SQL：字符
字符 ODBC C 数据类型的标识符为：  
  
 SQL_C_CHAR  
  
 SQL_C_WCHAR  
  
 下表显示了可以转换为 C 字符数据的 ODBC SQL 数据类型。 有关表中列和术语的说明，请参阅[将数据从 C 转换为 SQL 数据类型](../../../odbc/reference/appendixes/converting-data-from-c-to-sql-data-types.md)。  
  
> [!NOTE]  
>  当字符 C 数据转换为 Unicode SQL 数据时，Unicode 数据的长度必须为偶数。  
  
|SQL 类型标识符|测试|SQLSTATE|  
|-------------------------|----------|--------------|  
|SQL_CHAR<br /><br /> SQL_VARCHAR<br /><br /> SQL_LONGVARCHAR|数据<字节长度 = 列长度。<br /><br /> 数据字节长度>列长度。|不适用<br /><br /> 22001|  
|SQL_WCHAR<br /><br /> SQL_WVARCHAR<br /><br /> SQL_WLONGVARCHAR|数据<的字符长度 = 列长度。<br /><br /> >列长度的数据的字符长度。|不适用<br /><br /> 22001|  
|SQL_DECIMAL<br /><br /> SQL_NUMERIC<br /><br /> SQL_TINYINT<br /><br /> SQL_SMALLINT<br /><br /> SQL_INTEGERSQL_BIGINT|在不截断的情况下转换的数据<br /><br /> 使用小数数字截断转换的数据[e]<br /><br /> 数据转换将导致整体（相对于小数）数字的丢失[e]<br /><br /> 数据值不是*数字文本*|不适用<br /><br /> 22001<br /><br /> 22001<br /><br /> 22018|  
|SQL_REAL<br /><br /> SQL_FLOAT<br /><br /> SQL_DOUBLE|数据在要转换数字的数据类型范围内<br /><br /> 数据超出要转换数字的数据类型的范围<br /><br /> 数据值不是*数字文本*|不适用<br /><br /> 22003<br /><br /> 22018|  
|SQL_BIT|数据为 0 或 1<br /><br /> 数据大于 0，小于 2，不等于 1<br /><br /> 数据小于 0 或大于或等于 2<br /><br /> 数据不是*数字文本*|不适用<br /><br /> 22001<br /><br /> 22003<br /><br /> 22018|  
|SQL_BINARY<br /><br /> SQL_VARBINARY<br /><br /> SQL_LONGVARBINARY|（数据字节长度） / 2 <= 列字节长度<br /><br /> （数据字节长度） / 2 >列字节长度<br /><br /> 数据值不是十六进制值|不适用<br /><br /> 22001<br /><br /> 22018|  
|SQL_TYPE_DATE|数据值是有效的*ODBC 日期文本*<br /><br /> 数据值是有效的*ODBC 时间戳文本*;时间部分为零<br /><br /> 数据值是有效的*ODBC 时间戳文本*;时间部分是非零[a]<br /><br /> 数据值不是有效的*ODBC-日期文本*或*ODBC 时间戳-文本*|不适用<br /><br /> 不适用<br /><br /> 22008<br /><br /> 22018|  
|SQL_TYPE_TIME|数据值是有效的*ODBC 时间文本*<br /><br /> 数据值是有效的*ODBC 时间戳文本*;小数秒部分为零[b]<br /><br /> 数据值是有效的*ODBC 时间戳文本*;小数秒部分是非零[b]<br /><br /> 数据值不是有效的*ODBC-时间文本*或*ODBC 时间戳-文本*|不适用<br /><br /> 不适用<br /><br /> 22008<br /><br /> 22018|  
|SQL_TYPE_TIMESTAMP|数据值是有效的*ODBC 时间戳文本*;分数秒部分未截断<br /><br /> 数据值是有效的*ODBC 时间戳文本*;小数秒部分截断<br /><br /> 数据值是有效的*ODBC-日期文本*[c]<br /><br /> 数据值是有效的*ODBC 时间文本*[d]<br /><br /> 数据值不是有效的*ODBC-日期文本**、ODBC 时间-文本*或*ODBC 时间戳-文本*|不适用<br /><br /> 22008<br /><br /> 不适用<br /><br /> 不适用<br /><br /> 22018|  
|所有 SQL 间隔类型|数据值是有效的*间隔值*;未发生截断<br /><br /> 数据值是有效的*间隔值*;其中一个字段中的值被截断<br /><br /> 数据值不是有效的间隔文本|不适用<br /><br /> 22015<br /><br /> 22018|  
  
 [a] 时间戳的时间部分被截断。  
  
 [b] 时间戳的日期部分将被忽略。  
  
 [c] 时间戳的时间部分设置为零。  
  
 [d] 时间戳的日期部分设置为当前日期。  
  
 [e] 驱动程序/数据源有效地等待整个字符串已收到（即使字符数据通过调用**SQLPutData**分批发送），然后再尝试执行转换。  
  
 当字符 C 数据转换为数字、日期、时间或时间戳 SQL 数据时，将忽略前导和尾随空格。  
  
 当字符 C 数据转换为二进制 SQL 数据时，字符数据的每两个字节将转换为二进制数据的单个字节（8 位）。 字符数据的每两个字节以十六进制形式表示数字。 例如，"01"转换为二进制 00000001，"FF"转换为二进制 11111111。  
  
 驱动程序始终将十六进制数字对转换为单个字节，并忽略 null 端接字节。 因此，如果字符串的长度为奇数，则不会转换字符串的最后一个字节（不包括 null 端接字节（如果有）。  
  
> [!NOTE]  
>  禁止应用程序开发人员将字符 C 数据绑定到二进制 SQL 数据类型。 此转换通常效率低下且速度缓慢。
