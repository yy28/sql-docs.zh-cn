---
title: 从 C 到 SQL： 时间戳 |Microsoft Docs
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: a738712a8fb1b032ef8244f579b10fdcc22becee
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/01/2018
ms.locfileid: "47739895"
---
# <a name="c-to-sql-timestamp"></a>从 C 到 SQL：时间戳
时间戳 ODBC C 数据类型的标识符是：  
  
 SQL_C_TYPE_TIMESTAMP  
  
 下表显示 ODBC SQL 时间戳 C 数据可能会转换成的数据类型。 列和表中的条款的说明，请参阅[转换将数据从 C 到 SQL 数据类型](../../../odbc/reference/appendixes/converting-data-from-c-to-sql-data-types.md)。  
  
|SQL 类型标识符|测试|SQLSTATE|  
|-------------------------|----------|--------------|  
|SQL_CHAR<br /><br /> SQL_VARCHAR<br /><br /> SQL_LONGVARCHAR|列的字节长度 > = 字符字节长度<br /><br /> 19 < = 列的字节长度 < 字符字节长度<br /><br /> 列字节长度 < 19<br /><br /> 数据值不是有效的时间戳|不适用<br /><br /> 22001<br /><br /> 22001<br /><br /> 22008|  
|SQL_WCHAR<br /><br /> SQL_WVARCHAR<br /><br /> SQL_WLONGVARCHAR|列的字符长度 > = 字符长度的数据<br /><br /> 19 < = 列的字符长度 < 字符长度的数据<br /><br /> 列的字符长度 < 19<br /><br /> 数据值不是有效的时间戳|不适用<br /><br /> 22001<br /><br /> 22001<br /><br /> 22008|  
|SQL_TYPE_DATE|时间字段均为零<br /><br /> 时间字段均不为零<br /><br /> 数据值不包含有效的日期|不适用<br /><br /> 22008<br /><br /> 22007|  
|SQL_TYPE_TIME|秒的小数部分字段均为零 [a]<br /><br /> 秒的小数部分字段为非零值 [a]<br /><br /> 数据值不包含有效的时间|不适用<br /><br /> 22008<br /><br /> 22007|  
|SQL_TYPE_TIMESTAMP|不会截断秒的小数部分字段<br /><br /> 秒的小数部分字段将被截断<br /><br /> 数据值不是有效的时间戳|不适用<br /><br /> 22008<br /><br /> 22007|  
  
 [a] 日期时间戳结构的字段将被忽略。  
  
 有关哪些值是有效 SQL_C_TIMESTAMP 结构中的信息，请参阅[C 数据类型](../../../odbc/reference/appendixes/c-data-types.md)本附录前面。  
  
 时间戳 C 数据转换为字符 SQL 数据，生成的字符数据时，在"*yyyy*-*mm*-*dd* *hh*:*mm*:*ss*[。*f...*]"格式。  
  
 该驱动程序将数据转换从时间戳 C 数据类型时，将忽略此长度/指示器值，并假定数据缓冲区的大小是时间戳 C 数据类型的大小。 中传递的长度/指示器值*StrLen_or_Ind*中的参数**SQLPutData**并使用指定的缓冲区中*StrLen_or_IndPtr*中参数**SQLBindParameter**。 使用指定的数据缓冲区*DataPtr*中的参数**SQLPutData**并*ParameterValuePtr*中的参数**SQLBindParameter**.
