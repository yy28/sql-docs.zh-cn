---
title: To SQL 的 C： 时间戳 |Microsoft 文档
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: odbc
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- data conversions from C to SQL types [ODBC], timestamp
- timestamp data type [ODBC]
- converting data from c to SQL types [ODBC], timestamp
ms.assetid: 0e08bfff-68f9-4648-9558-09b57fea08ad
caps.latest.revision: 8
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: be38d6accb796666a62324e7a6fd5aefcfa0f372
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/16/2018
---
# <a name="c-to-sql-timestamp"></a>To SQL 的 C： 时间戳
时间戳 ODBC C 数据类型的标识符是：  
  
 SQL_C_TYPE_TIMESTAMP  
  
 下表显示 ODBC SQL 时间戳 C 数据可能转换到的目标的数据类型。 列和表中的条款的说明，请参阅[C 中为 SQL 数据类型的转换的数据](../../../odbc/reference/appendixes/converting-data-from-c-to-sql-data-types.md)。  
  
|SQL 类型标识符|测试|SQLSTATE|  
|-------------------------|----------|--------------|  
|SQL_CHAR<br /><br /> SQL_VARCHAR<br /><br /> SQL_LONGVARCHAR|列字节长度 > = 字符字节长度<br /><br /> 19 < = 列字节长度 < 字符字节长度<br /><br /> 列字节长度 < 19<br /><br /> 数据值不是有效的时间戳|不适用<br /><br /> 22001<br /><br /> 22001<br /><br /> 22008|  
|SQL_WCHAR<br /><br /> SQL_WVARCHAR<br /><br /> SQL_WLONGVARCHAR|列的字符长度 > = 字符长度的数据<br /><br /> 19 < = 列字符长度 < 字符数据的长度<br /><br /> 列字符长度 < 19<br /><br /> 数据值不是有效的时间戳|不适用<br /><br /> 22001<br /><br /> 22001<br /><br /> 22008|  
|SQL_TYPE_DATE|时间字段均为零<br /><br /> 时间字段均不为零<br /><br /> 数据值不包含有效的日期|不适用<br /><br /> 22008<br /><br /> 22007|  
|SQL_TYPE_TIME|秒的小数部分字段均为零 [a]<br /><br /> 秒的小数部分字段是零 [a]<br /><br /> 数据值不包含有效的时间|不适用<br /><br /> 22008<br /><br /> 22007|  
|SQL_TYPE_TIMESTAMP|不会截断秒的小数部分字段<br /><br /> 秒的小数部分字段将被截断<br /><br /> 数据值不是有效的时间戳|不适用<br /><br /> 22008<br /><br /> 22007|  
  
 [a] 忽略时间戳结构的字段的日期。  
  
 有关哪些值都无效 SQL_C_TIMESTAMP 结构中的信息，请参阅[C 数据类型](../../../odbc/reference/appendixes/c-data-types.md)前面本附录内容。  
  
 当时间戳 C 数据转换为字符 SQL 数据时，生成的字符数据，则在"*yyyy*-*mm*-*dd* *hh*:*mm*:*ss*[。*f...*]"格式。  
  
 该驱动程序时将数据从时间戳 C 数据类型转换忽略长度/指示器值，并假定数据缓冲区的大小为时间戳 C 数据类型的大小。 长度/指示器值将传递中*StrLen_or_Ind*中的参数**SQLPutData**和中与指定的缓冲区*StrLen_or_IndPtr*中参数**SQLBindParameter**。 使用指定的数据缓冲区*DataPtr*中的参数**SQLPutData**和*ParameterValuePtr*中的参数**SQLBindParameter**.
