---
title: 从 C 到 SQL： 数字 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- numeric data type [ODBC], converting
- data conversions from C to SQL types [ODBC], numeric
- converting data from c to SQL types [ODBC], numeric
ms.assetid: af4095ff-06c3-4b04-83bf-19f9ee098dc2
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 816394bb8469148504c1b2b416e77fec814bef8f
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/01/2018
ms.locfileid: "47786665"
---
# <a name="c-to-sql-numeric"></a>从 C 到 SQL：数字
数值的 ODBC C 数据类型的标识符是：  
  
 SQL_C_STINYINT  
  
 SQL_C_SLONG  
  
 SQL_C_UTINYINT  
  
 SQL_C_ULONG  
  
 SQL_C_TINYINT  
  
 SQL_C_LONG  
  
 SQL_C_SSHORT  
  
 SQL_C_FLOAT  
  
 SQL_C_USHORT  
  
 SQL_C_DOUBLE  
  
 SQL_C_SHORT  
  
 SQL_C_NUMERIC  
  
 SQL_C_SBIGINT  
  
 SQL_C_UBIGINT  
  
 下表显示 ODBC SQL 数值 C 数据可能会转换成的数据类型。 列和表中的条款的说明，请参阅[转换将数据从 C 到 SQL 数据类型](../../../odbc/reference/appendixes/converting-data-from-c-to-sql-data-types.md)。  
  
|SQL 类型标识符|测试|SQLSTATE|  
|-------------------------|----------|--------------|  
|SQL_CHAR<br /><br /> SQL_VARCHAR<br /><br /> SQL_LONGVARCHAR|数字位数 < = 列的字节长度<br /><br /> 数字位数 > 列的字节长度|不适用<br /><br /> 22001|  
|SQL_WCHAR<br /><br /> SQL_WVARCHAR<br /><br /> SQL_WLONGVARCHAR|字符数 < = 列的字符长度<br /><br /> 字符数 > 列的字符长度|不适用<br /><br /> 22001|  
|SQL_DECIMAL [b]<br /><br /> SQL_NUMERIC [b]<br /><br /> SQL_TINYINT [b]<br /><br /> SQL_SMALLINT [b]<br /><br /> SQL_INTEGER [b]<br /><br /> SQL_BIGINT [b]|数据转换而无需截断或截断的小数位数<br /><br /> 转换为具有整数数字串截断数据|不适用<br /><br /> 22003|  
|SQL_REAL<br /><br /> SQL_FLOAT<br /><br /> SQL_DOUBLE|数据是数字转换到的数据类型的范围内<br /><br /> 数据是数字转换到的数据类型的范围之外|不适用<br /><br /> 22003|  
|SQL_BIT|数据为 0 或 1<br /><br /> 数据为大于 0，小于 2，且不等于 1<br /><br /> 数据是小于 0 或大于或等于 2|不适用<br /><br /> 22001<br /><br /> 22003|  
|SQL_INTERVAL_YEAR [a]<br /><br /> SQL_INTERVAL_MONTH [a]<br /><br /> SQL_INTERVAL_DAY [a]<br /><br /> SQL_INTERVAL_HOUR [a]<br /><br /> SQL_INTERVAL_MINUTE [a]<br /><br /> SQL_INTERVAL_SECOND [a]|不会被截断的数据。<br /><br /> 数据截断。|不适用<br /><br /> 22015|  
  
 [a] 仅的精确数值数据类型 （SQL_C_STINYINT、 SQL_C_UTINYINT、 SQL_C_SSHORT、 SQL_C_USHORT、 SQL_C_SLONG、 SQL_C_ULONG 或 SQL_C_NUMERIC） 支持这些转换。 不支持的近似数值数据类型 （SQL_C_FLOAT 或 SQL_C_DOUBLE）。 精确数字的 C 数据类型不能转换为时间间隔的时间间隔精度不是单个字段的 SQL 类型。  
  
 [b] 为"n/a"的情况下，驱动程序可能会选择性地返回 SQL_SUCCESS_WITH_INFO 和 01S07 时截断小数部分。  
  
 该驱动程序将数据转换的数字的 C 数据类型时，将忽略此长度/指示器值，并假定数据缓冲区的大小是数值的 C 数据类型的大小。 中传递的长度/指示器值*StrLen_or_Ind*中的参数**SQLPutData**并使用指定的缓冲区中*StrLen_or_IndPtr*中参数**SQLBindParameter**。 使用指定的数据缓冲区*DataPtr*中的参数**SQLPutData**并*ParameterValuePtr*中的参数**SQLBindParameter**.
