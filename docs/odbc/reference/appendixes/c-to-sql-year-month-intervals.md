---
title: 从 C 到 SQL：年月间隔 |Microsoft Docs
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: d12727f9298eb63fe10b44c48b9d3b7996a839d5
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/15/2019
ms.locfileid: "63159289"
---
# <a name="c-to-sql-year-month-intervals"></a>从 C 到 SQL：年月间隔
年-月间隔 ODBC C 数据类型的标识符是：  
  
 SQL_C_INTERVAL_MONTH SQL_C_INTERVAL_YEAR SQL_C_INTERVAL_YEAR_TO_MONTH  
  
 下表显示 ODBC SQL 数据类型到哪些年月间隔 C 数据可能转换。 列和表中的条款的说明，请参阅[转换将数据从 C 到 SQL 数据类型](../../../odbc/reference/appendixes/converting-data-from-c-to-sql-data-types.md)。  
  
|SQL 类型标识符|测试|SQLSTATE|  
|-------------------------|----------|--------------|  
|SQL_CHAR[a]<br /><br /> SQL_VARCHAR[a]<br /><br /> SQL_LONGVARCHAR[a]|列的字节长度 > = 字符字节长度<br /><br /> 列的字节长度 < 字符字节长度 [a]<br /><br /> 数据值不是有效的时间间隔文本|不适用<br /><br /> 22001<br /><br /> 22015|  
|SQL_WCHAR[a]<br /><br /> SQL_WVARCHAR[a]<br /><br /> SQL_WLONGVARCHAR[a]|列的字符长度 > = 字符长度的数据<br /><br /> 列的字符长度 < 字符长度的数据 [a]<br /><br /> 数据值不是有效的时间间隔文本|不适用<br /><br /> 22001<br /><br /> 22015|  
|SQL_TINYINT[b]<br /><br /> SQL_SMALLINT[b]<br /><br /> SQL_INTEGER[b]<br /><br /> SQL_BIGINT[b]<br /><br /> SQL_NUMERIC[b]<br /><br /> SQL_DECIMAL[b]|单字段间隔转换没有导致截断的整个数字<br /><br /> 转换导致截断的整个数字|不适用<br /><br /> 22003|  
|SQL_INTERVAL_MONTH<br /><br /> SQL_INTERVAL_YEAR<br /><br /> SQL_INTERVAL_YEAR_TO_MONTH|而无需截断的任何字段的已转换数据值<br /><br /> 在转换期间已被截断的数据值的一个或多个字段，|不适用<br /><br /> 22015|  
  
 [a] 所有的 C 间隔数据类型可以转换为字符数据类型。  
  
 [b] 如果间隔结构中的类型字段，这样的间隔是单个字段 （SQL_YEAR 或 SQL_MONTH） 的 C 间隔类型可转换为任何精确数值 （SQL_TINYINT、 SQL_SMALLINT、 SQL_INTEGER、 SQL_BIGINT、 SQL_DECIMAL 或 SQL_NUMERIC）。  
  
 C 类型的时间间隔的默认值转换为相应的年月间隔 SQL 类型。  
  
 该驱动程序将数据从间隔 C 数据类型转换时将忽略此长度/指示器值，并假定数据缓冲区的大小是间隔 C 数据类型的大小。 中传递的长度/指示器值*StrLen_or_Ind*中的参数**SQLPutData**并使用指定的缓冲区中*StrLen_or_IndPtr*中参数**SQLBindParameter**。 使用指定的数据缓冲区*DataPtr*中的参数**SQLPutData**并*ParameterValuePtr*中的参数**SQLBindParameter**.
