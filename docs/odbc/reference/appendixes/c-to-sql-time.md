---
title: 从 C 到 SQL： 时间 |Microsoft Docs
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 7ea11803847505698ea42d13727b6177f3a24bda
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/01/2018
ms.locfileid: "47606175"
---
# <a name="c-to-sql-time"></a>从 C 到 SQL：时间
时间 ODBC C 数据类型的标识符是：  
  
 SQL_C_TYPE_TIME  
  
 下表显示 ODBC SQL 时间 C 数据可能会转换成的数据类型。 列和表中的条款的说明，请参阅[转换将数据从 C 到 SQL 数据类型](../../../odbc/reference/appendixes/converting-data-from-c-to-sql-data-types.md)。  
  
|SQL 类型标识符|测试|SQLSTATE|  
|-------------------------|----------|--------------|  
|SQL_CHAR<br /><br /> SQL_VARCHAR<br /><br /> SQL_LONGVARCHAR|列的字节长度 > = 8<br /><br /> 列字节长度 < 8<br /><br /> 数据值不是有效的时间|不适用<br /><br /> 22001<br /><br /> 22008|  
|SQL_WCHAR<br /><br /> SQL_WVARCHAR<br /><br /> SQL_WLONGVARCHAR|列的字符长度 > = 8<br /><br /> 列的字符长度 < 8<br /><br /> 数据值不是有效的时间|不适用<br /><br /> 22001<br /><br /> 22008|  
|SQL_TYPE_TIME|数据值是有效的时间<br /><br /> 数据值不是有效的时间|不适用<br /><br /> 22007|  
|SQL_TYPE_TIMESTAMP|数据值是有效的时间 [a]<br /><br /> 数据值不是有效的时间|不适用<br /><br /> 22007|  
  
 [a] 时间戳部分设置为当前日期和时间戳部分设置为零秒的小数部分的日期。  
  
 有关哪些值是有效 SQL_C_TYPE_TIME 结构中的信息，请参阅[C 数据类型](../../../odbc/reference/appendixes/c-data-types.md)本附录前面。  
  
 当时间 C 数据转换为字符 SQL 数据时，生成的字符数据，在"*hh*:*mm*:*ss*"格式。  
  
 将数据从 C 数据类型，并假定数据缓冲区的大小是时间 C 数据类型的大小的时间转换时，该驱动程序将忽略长度/指示器值。 中传递的长度/指示器值*StrLen_or_Ind*中的参数**SQLPutData**并使用指定的缓冲区中*StrLen_or_IndPtr*中参数**SQLBindParameter**。 使用指定的数据缓冲区*DataPtr*中的参数**SQLPutData**并*ParameterValuePtr*中的参数**SQLBindParameter**.
