---
title: C 到 SQL：年月间隔 |微软文档
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- converting data from c to SQL types [ODBC], year-month intervals
- intervals [ODBC], converting
- year-month intervals [ODBC]
- data conversions from C to SQL types [ODBC], year-month intervals
ms.assetid: a0eb7b55-9db0-4375-9210-bddec4593880
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 2ec7bfda0015883c8470dd453c7ae5de9bfd6cec
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/14/2020
ms.locfileid: "81306608"
---
# <a name="c-to-sql-year-month-intervals"></a>从 C 到 SQL：年月间隔
年月间隔 ODBC C 数据类型的标识符为：  
  
 SQL_C_INTERVAL_MONTHSQL_C_INTERVAL_YEARSQL_C_INTERVAL_YEAR_TO_MONTH  
  
 下表显示了可转换为年月间隔 C 数据的 ODBC SQL 数据类型。 有关表中列和术语的说明，请参阅[将数据从 C 转换为 SQL 数据类型](../../../odbc/reference/appendixes/converting-data-from-c-to-sql-data-types.md)。  
  
|SQL 类型标识符|测试|SQLSTATE|  
|-------------------------|----------|--------------|  
|SQL_CHAR[a]<br /><br /> SQL_VARCHAR[a]<br /><br /> SQL_LONGVARCHAR[a]|列字节长度>= 字符字节长度<br /><br /> 列字节长度<字符字节长度 [a]<br /><br /> 数据值不是有效的间隔文本|不适用<br /><br /> 22001<br /><br /> 22015|  
|SQL_WCHAR[a]<br /><br /> SQL_WVARCHAR[a]<br /><br /> SQL_WLONGVARCHAR[a]|列字符长度>= 数据的字符长度<br /><br /> 列字符长度<字符长度的数据[a]<br /><br /> 数据值不是有效的间隔文本|不适用<br /><br /> 22001<br /><br /> 22015|  
|SQL_TINYINT[b]<br /><br /> SQL_SMALLINT[b]<br /><br /> SQL_INTEGER[b]<br /><br /> SQL_BIGINT[b]<br /><br /> SQL_NUMERIC[b]<br /><br /> SQL_DECIMAL[b]|单字段间隔的转换不会导致整个数字的截断<br /><br /> 转换导致整个数字的截断|不适用<br /><br /> 22003|  
|SQL_INTERVAL_MONTH<br /><br /> SQL_INTERVAL_YEAR<br /><br /> SQL_INTERVAL_YEAR_TO_MONTH|数据值已转换，无需截断任何字段<br /><br /> 转换期间截断一个或多个数据值字段|不适用<br /><br /> 22015|  
  
 [a] 所有 C 间隔数据类型都可以转换为字符数据类型。  
  
 [b] 如果间隔结构中的类型字段使间隔为单个字段（SQL_YEAR 或SQL_MONTH），则可以将间隔 C 类型转换为任何精确数值（SQL_TINYINT、SQL_SMALLINT、SQL_INTEGER、SQL_BIGINT、SQL_DECIMAL 或SQL_NUMERIC）。  
  
 间隔 C 类型的默认转换为相应的年月间隔 SQL 类型。  
  
 当从间隔 C 数据类型转换数据时，驱动程序忽略长度/指示器值，并假定数据缓冲区的大小是间隔 C 数据类型的大小。 长度/指标值在**SQLPutData**中的*StrLen_or_Ind*参数中传递，在**SQLBind 参数**中用*StrLen_or_IndPtr*参数指定的缓冲区中传递。 数据缓冲区使用**SQLPutData**中的*DataPtr*参数和**SQLBind 参数**中的*参数ValuePtr*参数指定。
