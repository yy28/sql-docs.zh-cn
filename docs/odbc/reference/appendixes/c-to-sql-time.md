---
title: C 到 SQL：时间 |微软文档
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- data conversions from C to SQL types [ODBC], time
- time data type [ODBC]
- converting data from c to SQL types [ODBC], time
ms.assetid: a8da43c9-d9a5-45e5-bd9a-1dd633db2ee0
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 264ce7751072b79163923f0c141542680f7b02bb
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/14/2020
ms.locfileid: "81304758"
---
# <a name="c-to-sql-time"></a>从 C 到 SQL：时间
ODBC C 数据类型的时间标识符为：  
  
 SQL_C_TYPE_TIME  
  
 下表显示了可以转换时间 C 数据的 ODBC SQL 数据类型。 有关表中列和术语的说明，请参阅[将数据从 C 转换为 SQL 数据类型](../../../odbc/reference/appendixes/converting-data-from-c-to-sql-data-types.md)。  
  
|SQL 类型标识符|测试|SQLSTATE|  
|-------------------------|----------|--------------|  
|SQL_CHAR<br /><br /> SQL_VARCHAR<br /><br /> SQL_LONGVARCHAR|列字节长度>= 8<br /><br /> 列字节长度< 8<br /><br /> 数据值不是有效时间|不适用<br /><br /> 22001<br /><br /> 22008|  
|SQL_WCHAR<br /><br /> SQL_WVARCHAR<br /><br /> SQL_WLONGVARCHAR|列字符长度>= 8<br /><br /> 列字符长度< 8<br /><br /> 数据值不是有效时间|不适用<br /><br /> 22001<br /><br /> 22008|  
|SQL_TYPE_TIME|数据值是有效的时间<br /><br /> 数据值不是有效时间|不适用<br /><br /> 22007|  
|SQL_TYPE_TIMESTAMP|数据值是有效的时间[a]<br /><br /> 数据值不是有效时间|不适用<br /><br /> 22007|  
  
 [a] 时间戳的日期部分设置为当前日期，时间戳的小秒部分设置为零。  
  
 有关哪些值在SQL_C_TYPE_TIME结构中有效的信息，请参阅本附录前面介绍[C 数据类型](../../../odbc/reference/appendixes/c-data-types.md)。  
  
 当时间 C 数据转换为字符 SQL 数据时，生成的字符数据采用 *"hh**：mm*：*ss"* 格式。  
  
 驱动程序在从时间 C 数据类型转换数据时忽略长度/指示器值，并假定数据缓冲区的大小是时间 C 数据类型的大小。 长度/指标值在**SQLPutData**中的*StrLen_or_Ind*参数中传递，在**SQLBind 参数**中用*StrLen_or_IndPtr*参数指定的缓冲区中传递。 数据缓冲区使用**SQLPutData**中的*DataPtr*参数和**SQLBind 参数**中的*参数ValuePtr*参数指定。
