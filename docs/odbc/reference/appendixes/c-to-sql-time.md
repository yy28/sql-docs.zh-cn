---
title: "To SQL 的 C： 时间 |Microsoft 文档"
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
- data conversions from C to SQL types [ODBC], time
- time data type [ODBC]
- converting data from c to SQL types [ODBC], time
ms.assetid: a8da43c9-d9a5-45e5-bd9a-1dd633db2ee0
caps.latest.revision: 8
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 6f1a59c15d2ebf1866d4543fa89662888154d4da
ms.contentlocale: zh-cn
ms.lasthandoff: 09/09/2017

---
# <a name="c-to-sql-time"></a>To SQL 的 C： 时间
时间 ODBC C 数据类型的标识符是：  
  
 SQL_C_TYPE_TIME  
  
 下表显示 ODBC SQL 数据类型时间 C 数据可能转换到的目标。 列和表中的条款的说明，请参阅[C 中为 SQL 数据类型的转换的数据](../../../odbc/reference/appendixes/converting-data-from-c-to-sql-data-types.md)。  
  
|SQL 类型标识符|测试|SQLSTATE|  
|-------------------------|----------|--------------|  
|SQL_CHAR<br /><br /> SQL_VARCHAR<br /><br /> SQL_LONGVARCHAR|列字节长度 > = 8<br /><br /> 列字节长度 < 8<br /><br /> 数据值不是有效的时间|不适用<br /><br /> 22001<br /><br /> 22008|  
|SQL_WCHAR<br /><br /> SQL_WVARCHAR<br /><br /> SQL_WLONGVARCHAR|列的字符长度 > = 8<br /><br /> 列字符长度 < 8<br /><br /> 数据值不是有效的时间|不适用<br /><br /> 22001<br /><br /> 22008|  
|SQL_TYPE_TIME|数据值是有效的时间<br /><br /> 数据值不是有效的时间|不适用<br /><br /> 22007|  
|SQL_TYPE_TIMESTAMP|数据值是有效的时间 [a]<br /><br /> 数据值不是有效的时间|不适用<br /><br /> 22007|  
  
 [a] 的时间戳的部分被设置为当前的日期和时间戳的部分设置为零的秒的小数部分的日期。  
  
 有关哪些值都无效 SQL_C_TYPE_TIME 结构中的信息，请参阅[C 数据类型](../../../odbc/reference/appendixes/c-data-types.md)前面本附录内容。  
  
 当时间 C 数据转换为字符 SQL 数据时，生成的字符数据，则在"*hh*:*mm*:*ss*"格式。  
  
 从 C 数据类型，并假定数据缓冲区的大小是时间 C 数据类型的大小的时间转换数据时，该驱动程序将忽略长度/指示器值。 长度/指示器值将传递中*StrLen_or_Ind*中的参数**SQLPutData**和中与指定的缓冲区*StrLen_or_IndPtr*中参数**SQLBindParameter**。 使用指定的数据缓冲区*DataPtr*中的参数**SQLPutData**和*ParameterValuePtr*中的参数**SQLBindParameter**.
