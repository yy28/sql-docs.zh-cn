---
title: "To SQL 的 C： 数值 |Microsoft 文档"
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
- numeric data type [ODBC], converting
- data conversions from C to SQL types [ODBC], numeric
- converting data from c to SQL types [ODBC], numeric
ms.assetid: af4095ff-06c3-4b04-83bf-19f9ee098dc2
caps.latest.revision: 8
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 2cbdbbd3da828d5a995dbd9bff9c6b95aed1420a
ms.contentlocale: zh-cn
ms.lasthandoff: 09/09/2017

---
# <a name="c-to-sql-numeric"></a>To SQL 的 C： 数字
对于数值 ODBC C 数据类型的标识符都是：  
  
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
  
 下表显示 ODBC SQL 数值 C 数据可能转换到的目标的数据类型。 列和表中的条款的说明，请参阅[C 中为 SQL 数据类型的转换的数据](../../../odbc/reference/appendixes/converting-data-from-c-to-sql-data-types.md)。  
  
|SQL 类型标识符|测试|SQLSTATE|  
|-------------------------|----------|--------------|  
|SQL_CHAR<br /><br /> SQL_VARCHAR<br /><br /> SQL_LONGVARCHAR|数字个数 < = 列字节长度<br /><br /> 数字个数 > 列字节长度|不适用<br /><br /> 22001|  
|SQL_WCHAR<br /><br /> SQL_WVARCHAR<br /><br /> SQL_WLONGVARCHAR|字符数 < = 列字符长度<br /><br /> 字符数 > 列字符长度|不适用<br /><br /> 22001|  
|SQL_DECIMAL [b]<br /><br /> SQL_NUMERIC [b]<br /><br /> SQL_TINYINT [b]<br /><br /> SQL_SMALLINT [b]<br /><br /> SQL_INTEGER [b]<br /><br /> SQL_BIGINT [b]|数据转换而不会截断或使用截断的小数位数<br /><br /> 转换后的整个位数截断的数据|不适用<br /><br /> 22003|  
|SQL_REAL<br /><br /> SQL_FLOAT<br /><br /> SQL_DOUBLE|数据是数转换到的目标的数据类型的范围内<br /><br /> 数据超出了范围数转换到的目标的数据类型|不适用<br /><br /> 22003|  
|SQL_BIT|数据为 0 或 1<br /><br /> 数据为大于 0，小于 2，且不等于 1<br /><br /> 数据是小于 0 或大于或等于 2|不适用<br /><br /> 22001<br /><br /> 22003|  
|SQL_INTERVAL_YEAR [a]<br /><br /> SQL_INTERVAL_MONTH [a]<br /><br /> SQL_INTERVAL_DAY [a]<br /><br /> SQL_INTERVAL_HOUR [a]<br /><br /> SQL_INTERVAL_MINUTE [a]<br /><br /> SQL_INTERVAL_SECOND [a]|不会被截断的数据。<br /><br /> 数据截断。|不适用<br /><br /> 22015|  
  
 [a] 这些转换仅支持 （SQL_C_STINYINT、 SQL_C_UTINYINT、 SQL_C_SSHORT、 SQL_C_USHORT、 SQL_C_SLONG、 SQL_C_ULONG 或 SQL_C_NUMERIC） 的精确数值数据类型。 不支持的近似数值数据类型 （SQL_C_FLOAT 或 SQL_C_DOUBLE）。 精确数字数据 C 数据类型无法转换为一个时间间隔的时间间隔精度不是单个字段的 SQL 类型。  
  
 [b] 为"不适用"用例，驱动程序可能会选择性地返回 SQL_SUCCESS_WITH_INFO 和 01S07 小数截断时。  
  
 该驱动程序时将数据从数值的 C 数据类型转换忽略长度/指示器值，并假定数据缓冲区的大小为数值的 C 数据类型的大小。 长度/指示器值将传递中*StrLen_or_Ind*中的参数**SQLPutData**和中与指定的缓冲区*StrLen_or_IndPtr*中参数**SQLBindParameter**。 使用指定的数据缓冲区*DataPtr*中的参数**SQLPutData**和*ParameterValuePtr*中的参数**SQLBindParameter**.
