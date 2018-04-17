---
title: To SQL 的 C： 日期 |Microsoft 文档
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
- date data type [ODBC]
- converting data from c to SQL types [ODBC], date
- data conversions from C to SQL types [ODBC], date
ms.assetid: bea087d3-911f-418b-b483-d2b5b334da19
caps.latest.revision: 8
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 0c14da46be67b8b945f167f408dd15005514e013
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/16/2018
---
# <a name="c-to-sql-date"></a>To SQL 的 C： 日期
日期 ODBC C 数据类型的标识符是：  
  
 SQL_C_TYPE_DATE  
  
 下表显示 ODBC SQL 日期 C 数据可能转换到的目标的数据类型。 列和表中的条款的说明，请参阅[C 中为 SQL 数据类型的转换的数据](../../../odbc/reference/appendixes/converting-data-from-c-to-sql-data-types.md)。  
  
|SQL 类型标识符|测试|SQLSTATE|  
|-------------------------|----------|--------------|  
|SQL_CHAR<br /><br /> SQL_VARCHAR<br /><br /> SQL_LONGVARCHAR|列字节长度 > = 10<br /><br /> 列字节长度 < 10<br /><br /> 数据值不是有效的日期|不适用<br /><br /> 22001<br /><br /> 22008|  
|SQL_WCHAR<br /><br /> SQL_WVARCHAR<br /><br /> SQL_WLONGVARCHAR|列的字符长度 > = 10<br /><br /> 列字符长度 < 10<br /><br /> 数据值不是有效的日期|不适用<br /><br /> 22001<br /><br /> 22008|  
|SQL_TYPE_DATE|数据值为有效日期<br /><br /> 数据值不是有效的日期|不适用<br /><br /> 22007|  
|SQL_TYPE_TIMESTAMP|数据值为有效日期 [a]<br /><br /> 数据值不是有效的日期|不适用<br /><br /> 22007|  
  
 [a] 的时间部分的时间戳设置为零。  
  
 有关哪些值都无效 SQL_C_TYPE_DATE 结构中的信息，请参阅[C 数据类型](../../../odbc/reference/appendixes/c-data-types.md)前面本附录内容。  
  
 当日期 C 数据转换为字符 SQL 数据时，生成的字符数据，则在"*yyyy*-*mm*-*dd*"格式。  
  
 该驱动程序时将数据从日期 C 数据类型转换忽略长度/指示器值，并假定数据缓冲区的大小是日期 C 数据类型的大小。 长度/指示器值将传递中*StrLen_or_Ind*中的参数**SQLPutData**和中与指定的缓冲区*StrLen_or_IndPtr*中参数**SQLBindParameter**。 使用指定的数据缓冲区*DataPtr*中的参数**SQLPutData**和*ParameterValuePtr*中的参数**SQLBindParameter**.
