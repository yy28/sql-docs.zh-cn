---
title: C 到 SQL：时间戳 |微软文档
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- data conversions from C to SQL types [ODBC], timestamp
- timestamp data type [ODBC]
- converting data from c to SQL types [ODBC], timestamp
ms.assetid: 0e08bfff-68f9-4648-9558-09b57fea08ad
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 3102e5043527a1aa9463980c9dd546839cb92f37
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/14/2020
ms.locfileid: "81283747"
---
# <a name="c-to-sql-timestamp"></a>从 C 到 SQL：时间戳
时间戳 ODBC C 数据类型的标识符是：  
  
 SQL_C_TYPE_TIMESTAMP  
  
 下表显示了可转换为时间戳 C 数据的 ODBC SQL 数据类型。 有关表中列和术语的说明，请参阅[将数据从 C 转换为 SQL 数据类型](../../../odbc/reference/appendixes/converting-data-from-c-to-sql-data-types.md)。  
  
|SQL 类型标识符|测试|SQLSTATE|  
|-------------------------|----------|--------------|  
|SQL_CHAR<br /><br /> SQL_VARCHAR<br /><br /> SQL_LONGVARCHAR|列字节长度>= 字符字节长度<br /><br /> 19 <= 列字节长度<字符字节长度<br /><br /> 列字节长度< 19<br /><br /> 数据值不是有效的时间戳|不适用<br /><br /> 22001<br /><br /> 22001<br /><br /> 22008|  
|SQL_WCHAR<br /><br /> SQL_WVARCHAR<br /><br /> SQL_WLONGVARCHAR|列字符长度>= 数据的字符长度<br /><br /> 19 <= 列字符长度<字符长度的数据<br /><br /> 列字符长度< 19<br /><br /> 数据值不是有效的时间戳|不适用<br /><br /> 22001<br /><br /> 22001<br /><br /> 22008|  
|SQL_TYPE_DATE|时间字段为零<br /><br /> 时间字段为非零<br /><br /> 数据值不包含有效日期|不适用<br /><br /> 22008<br /><br /> 22007|  
|SQL_TYPE_TIME|分数秒字段为零 [a]<br /><br /> 分数秒字段是非零 [a]<br /><br /> 数据值不包含有效时间|不适用<br /><br /> 22008<br /><br /> 22007|  
|SQL_TYPE_TIMESTAMP|分数秒字段未截断<br /><br /> 分数秒字段被截断<br /><br /> 数据值不是有效的时间戳|不适用<br /><br /> 22008<br /><br /> 22007|  
  
 [a] 时间戳结构的日期字段将被忽略。  
  
 有关哪些值在SQL_C_TIMESTAMP结构中有效的信息，请参阅本附录前面介绍[C 数据类型](../../../odbc/reference/appendixes/c-data-types.md)。  
  
 当时间戳 C 数据转换为字符 SQL 数据时，生成的字符数据位于 *"yyyymm*-*mm*-*dd* *hh**：mm**：ss*"中。*f...* 格式。  
  
 当从时间戳 C 数据类型转换数据时，驱动程序会忽略长度/指示器值，并假定数据缓冲区的大小是时间戳 C 数据类型的大小。 长度/指标值在**SQLPutData**中的*StrLen_or_Ind*参数中传递，在**SQLBind 参数**中用*StrLen_or_IndPtr*参数指定的缓冲区中传递。 数据缓冲区使用**SQLPutData**中的*DataPtr*参数和**SQLBind 参数**中的*参数ValuePtr*参数指定。
