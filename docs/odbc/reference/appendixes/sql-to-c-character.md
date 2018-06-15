---
title: SQL 为 c： 字符 |Microsoft 文档
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- converting data from SQL to C types [ODBC], character
- character data type [ODBC]
- data conversions from SQL to C types [ODBC], character
ms.assetid: 7fdb7f38-b64d-48f2-bcb4-1ca96b2bbdb6
caps.latest.revision: 8
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: db139b1307fa1817e0b9ed709be5ee5db2086756
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
ms.locfileid: "32913942"
---
# <a name="sql-to-c-character"></a>为 c： 字符的 SQL
对于字符 ODBC SQL 数据类型的标识符都是：  
  
 SQL_CHAR  
  
 SQL_VARCHAR  
  
 SQL_LONGVARCHAR  
  
 SQL_WCHAR  
  
 SQL_WVARCHAR  
  
 SQL_WLONGVARCHAR  
  
 下表显示 ODBC C 数据类型字符 SQL 数据可能转换到的目标。 列和表中的条款的说明，请参阅[转换数据从 SQL C 数据类型到](../../../odbc/reference/appendixes/converting-data-from-sql-to-c-data-types.md)。  
  
|C 类型标识符|测试|**TargetValuePtr*|**StrLen_or_IndPtr*|SQLSTATE|  
|-----------------------|----------|------------------------|----------------------------|--------------|  
|SQL_C_CHAR|数据的字节长度 < *BufferLength*<br /><br /> 数据的字节长度 > = *BufferLength*|Data<br /><br /> 截断的数据|以字节为单位的数据的长度<br /><br /> 以字节为单位的数据的长度|不适用<br /><br /> 01004|  
|SQL_C_WCHAR|字符数据的长度 < *BufferLength*<br /><br /> 字符数据的长度 > = *BufferLength*|Data<br /><br /> 截断的数据|以字符为单位的数据的长度<br /><br /> 以字符为单位的数据的长度|不适用<br /><br /> 01004|  
|SQL_C_STINYINT SQL_C_UTINYINT SQL_C_TINYINT SQL_C_SBIGINT SQL_C_UBIGINT SQL_C_SSHORT SQL_C_USHORT SQL_C_SHORT SQL_C_SLONG SQL_C_ULONG SQL_C_LONG SQL_C_NUMERIC|数据转换而不会截断 [b]<br /><br /> 数据转换使用的小数位数 [a] 的截断<br /><br /> 数据的转换将导致丢失的整体 （而不是小数） 数字，[a]<br /><br /> 数据不是*数字文本*[b]。|Data<br /><br /> 截断的数据<br /><br /> 未定义<br /><br /> 未定义|C 数据类型的字节数<br /><br /> C 数据类型的字节数<br /><br /> 未定义<br /><br /> 未定义|不适用<br /><br /> 01S07<br /><br /> 22003<br /><br /> 22018|  
|SQL_C_FLOAT SQL_C_DOUBLE|数据是数转换到的目标的数据类型的范围内 [a]<br /><br /> 数据超出了范围数转换到的目标的数据类型 [a]<br /><br /> 数据不是*数字文本*[b]。|Data<br /><br /> 未定义<br /><br /> 未定义|C 数据类型的大小<br /><br /> 未定义<br /><br /> 未定义|不适用<br /><br /> 22003<br /><br /> 22018|  
_C_BIT|数据为 0 或 1<br /><br /> 数据为大于 0，小于 2，且不等于 1<br /><br /> 数据是小于 0 或大于或等于 2<br /><br /> 数据不是*数字文本*|Data<br /><br /> 截断的数据<br /><br /> 未定义<br /><br /> 未定义|1 [b]<br /><br /> 1 [b]<br /><br /> 未定义<br /><br /> 未定义|不适用<br /><br /> 01S07<br /><br /> 22003<br /><br /> 22018|  
|SQL_C_BINARY|数据的字节长度 < = *BufferLength*<br /><br /> 数据的字节长度 > *BufferLength*|Data<br /><br /> 截断的数据|以字节为单位的数据的长度<br /><br /> 数据的长度|不适用<br /><br /> 01004|  
|SQL_C_TYPE_DATE|数据值是一个有效*日期值*[a]<br /><br /> 数据值是一个有效*时间戳值*; 时间部分为零 [a]<br /><br /> 数据值是一个有效*时间戳值*; 时间部分为非零 [a]，[c]<br /><br /> 数据值不是有效*日期值*或*时间戳值*[a]|Data<br /><br /> Data<br /><br /> 截断的数据<br /><br /> 未定义|6 [b]<br /><br /> 6 [b]<br /><br /> 6 [b]<br /><br /> 未定义|不适用<br /><br /> 不适用<br /><br /> 01S07<br /><br /> 22018|  
|SQL_C_TYPE_TIME|数据值是一个有效*时间值和值为 0 秒的小数部分*[a]<br /><br /> 数据值是一个有效*时间戳值或有效的时间值*; 小数秒部分为零 [a]，[d]<br /><br /> 数据值是一个有效*时间戳值*; 小数秒部分为非零值 [a]，[d] [e]<br /><br /> 数据值不是有效*时间值*或*时间戳值*[a]|Data<br /><br /> Data<br /><br /> 截断的数据<br /><br /> 未定义|6 [b]<br /><br /> 6 [b]<br /><br /> 6 [b]<br /><br /> 未定义|不适用<br /><br /> 不适用<br /><br /> 01S07<br /><br /> 22018|  
_C_TYPE_TIMESTAMP|数据值是一个有效*时间戳值或有效的时间值*; 小数秒部分不会被截断 [a]<br /><br /> 数据值是一个有效*时间戳值或有效的时间值*; 小数秒部分被截断 [a]<br /><br /> 数据值是一个有效*日期值*[a]<br /><br /> 数据值是一个有效*时间值*[a]<br /><br /> 数据值不是有效*日期值*，*时间值*，或*时间戳值*[a]|Data<br /><br /> 截断的数据<br /><br /> 数据 [f]<br /><br /> 数据 [g]<br /><br /> 未定义|16 [b]<br /><br /> 16 [b]<br /><br /> 16 [b]<br /><br /> 16 [b]<br /><br /> 未定义|不适用<br /><br /> 01S07<br /><br /> 不适用<br /><br /> 不适用<br /><br /> 22018|  
|所有 C 间隔类型|数据值是一个有效*间隔值*; 未截断<br /><br /> 数据值是一个有效*间隔值*; 的一个或多个尾随字段的截断<br /><br /> 数据是有效的时间间隔;前导字段重要精度将丢失<br /><br /> 数据值不是有效的间隔值|Data<br /><br /> 截断的数据<br /><br /> 未定义<br /><br /> 未定义|以字节为单位的数据的长度<br /><br /> 以字节为单位的数据的长度<br /><br /> 未定义<br /><br /> 未定义|不适用<br /><br /> 01S07<br /><br /> 22015<br /><br /> 22018|  
  
 [a] 的值*BufferLength*忽略此转换。 该驱动程序假定的大小 **TargetValuePtr*是 C 数据类型的大小。  
  
 [b] 这是对应的 C 数据类型的大小。  
  
 [c] 的时间部分的*时间戳值*将被截断。  
  
 [d] 的日期部分*时间戳值*将被忽略。  
  
 [时间戳 e] 的秒的小数部分部分将被截断。  
  
 [时间戳结构 f] 上，时间字段设置为零。  
  
 [时间戳结构 g] 上，日期字段将设置为当前日期。  
  
 当字符 SQL 数据转换为数值时，将忽略日期、 时间、 时间戳或间隔 C 数据，前导空格和尾随空格。
