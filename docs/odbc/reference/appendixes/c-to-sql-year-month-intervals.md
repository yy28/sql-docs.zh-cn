---
title: "To SQL 的 C： 年-月间隔 |Microsoft 文档"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: reference
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- converting data from c to SQL types [ODBC], year-month intervals
- intervals [ODBC], converting
- year-month intervals [ODBC]
- data conversions from C to SQL types [ODBC], year-month intervals
ms.assetid: a0eb7b55-9db0-4375-9210-bddec4593880
caps.latest.revision: "8"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 24246f654c492d10cf06d069c48e3f31abe7b396
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/20/2017
---
# <a name="c-to-sql-year-month-intervals"></a>To SQL 的 C： 年-月间隔
年-月间隔 ODBC C 数据类型的标识符都是：  
  
 SQL_C_INTERVAL_MONTH SQL_C_INTERVAL_YEAR SQL_C_INTERVAL_YEAR_TO_MONTH  
  
 下表显示 ODBC SQL 数据类型到哪些年-月间隔 C 数据可能转换。 列和表中的条款的说明，请参阅[C 中为 SQL 数据类型的转换的数据](../../../odbc/reference/appendixes/converting-data-from-c-to-sql-data-types.md)。  
  
|SQL 类型标识符|测试|SQLSTATE|  
|-------------------------|----------|--------------|  
|SQL_CHAR [a]<br /><br /> SQL_VARCHAR [a]<br /><br /> SQL_LONGVARCHAR [a]|列字节长度 > = 字符字节长度<br /><br /> 列字节长度 < 字符字节长度 [a]<br /><br /> 数据值不是文本的有效间隔|不适用<br /><br /> 22001<br /><br /> 22015|  
|SQL_WCHAR [a]<br /><br /> SQL_WVARCHAR [a]<br /><br /> SQL_WLONGVARCHAR [a]|列的字符长度 > = 字符长度的数据<br /><br /> 列的字符长度 < 字符长度的数据 [a]<br /><br /> 数据值不是文本的有效间隔|不适用<br /><br /> 22001<br /><br /> 22015|  
|SQL_TINYINT [b]<br /><br /> SQL_SMALLINT [b]<br /><br /> SQL_INTEGER [b]<br /><br /> SQL_BIGINT [b]<br /><br /> SQL_NUMERIC [b]<br /><br /> SQL_DECIMAL [b]|单一字段间隔的转换不会导致整个位数截断<br /><br /> 转换导致的整个位数截断|不适用<br /><br /> 22003|  
|SQL_INTERVAL_MONTH<br /><br /> SQL_INTERVAL_YEAR<br /><br /> SQL_INTERVAL_YEAR_TO_MONTH|而不发生截断任何字段的已转换数据值<br /><br /> 在转换期间被截断的数据值的一个或多个字段|不适用<br /><br /> 22015|  
  
 [a] 所有 C interval 数据类型可以转换为字符数据类型。  
  
 [b] 如果间隔结构中的类型字段，以便的时间间隔是单个字段 （SQL_YEAR 或 SQL_MONTH） 间隔 C 类型可转换为任何精确数字 （SQL_TINYINT、 SQL_SMALLINT、 SQL_INTEGER、 SQL_BIGINT、 SQL_DECIMAL 或 SQL_NUMERIC）。  
  
 一个时间间隔 C 类型的默认转换是为相应的年-月间隔 SQL 类型。  
  
 该驱动程序时将数据从间隔 C 数据类型转换忽略长度/指示器值，并假定数据缓冲区的大小为间隔 C 数据类型的大小。 长度/指示器值将传递中*StrLen_or_Ind*中的参数**SQLPutData**和中与指定的缓冲区*StrLen_or_IndPtr*中参数**SQLBindParameter**。 使用指定的数据缓冲区*DataPtr*中的参数**SQLPutData**和*ParameterValuePtr*中的参数**SQLBindParameter**.
