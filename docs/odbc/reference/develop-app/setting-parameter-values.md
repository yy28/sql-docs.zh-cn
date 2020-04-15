---
title: 设置参数值 |微软文档
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- parameter values [ODBC]
ms.assetid: 13e5da79-b60c-48d0-b467-773f481ef2a4
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 923fd57f4308fb72aca2f829ccb9d7b884c12546
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/14/2020
ms.locfileid: "81299827"
---
# <a name="setting-parameter-values"></a>设置参数值
要设置参数的值，应用程序只需设置绑定到参数的变量的值。 设置此值时并不重要，只要在执行语句之前设置此值。 应用程序可以在绑定变量之前或之后设置该值，并且它可以根据需要多次更改该值。 执行语句时，驱动程序只需检索变量的当前值。 当已准备好的语句执行多次时，这特别有用;应用程序在每次执行语句时为部分或全部变量设置新值。 有关此示例，请参阅本节前面[部的"准备执行](../../../odbc/reference/develop-app/prepared-execution-odbc.md)"。  
  
 如果在调用**SQLBind参数**时绑定了长度/指示器缓冲区，则必须在执行语句之前将其设置为以下值之一：  
  
-   绑定变量中数据的字节长度。 仅当变量为字符或二进制变量 *（ValueType*为SQL_C_CHAR或SQL_C_BINARY）时，驱动程序才会检查此长度。  
  
-   SQL_NTS 数据是一个 null 端接的字符串。  
  
-   SQL_NULL_DATA 数据值为 NULL，驱动程序忽略绑定变量的值。  
  
-   SQL_DATA_AT_EXEC或SQL_LEN_DATA_AT_EXEC宏的结果。 参数的值将与**SQLPutData**一起发送。 有关详细信息，请参阅在本部分的后面部分[发送长数据](../../../odbc/reference/develop-app/sending-long-data.md)。  
  
 下表显示了绑定变量的值以及应用程序为各种参数值设置的长度/指示器缓冲区。  
  
|参数<br /><br /> value|参数<br /><br /> （SQL）<br /><br /> 数据类型|变量 （C）<br /><br /> 数据类型| 中的值<br /><br /> 绑定<br /><br /> 可变| 中的值<br /><br /> 长度/指示器<br /><br /> 缓冲区[d]|  
|-------------------------|-----------------------------------------|----------------------------------|-------------------------------------|----------------------------------------------------|  
|"ABC"|SQL_CHAR|SQL_C_CHAR|ABC[0[a]|SQL_NTS或 3|  
|10|SQL_INTEGER|SQL_C_SLONG|10|--|  
|10|SQL_INTEGER|SQL_C_CHAR|10[0]a]|SQL_NTS或 2|  
|下午1时|SQL_TYPE_TIME|SQL_C_TYPE_TIME|13，0，0[b]|--|  
|下午1时|SQL_TYPE_TIME|SQL_C_CHAR|{t '13：00：00'{0}a}，{c}|SQL_NTS或 14|  
|Null|SQL_SMALLINT|SQL_C_SSHORT|--|SQL_NULL_DATA|  
  
 [a] "\0"表示空终止字符。 仅当长度/指示器缓冲区中的值SQL_NTS时，才需要空终止字符。  
  
 [b] 此列表中的数字是存储在TIME_STRUCT结构字段中的数字。  
  
 [c] 字符串使用 ODBC 日期转义子句。 有关详细信息，请参阅[日期、时间和时间戳文本](../../../odbc/reference/develop-app/date-time-and-timestamp-literals.md)。  
  
 [d] 驱动程序必须始终检查此值以查看它是否是特殊值，如SQL_NULL_DATA。  
  
 驱动程序在执行时使用参数值时所做的与驱动程序无关。 如有必要，驱动程序将值从绑定变量的 C 数据类型和字节长度转换为参数的 SQL 数据类型、精度和比例。 在大多数情况下，驱动程序然后将值发送到数据源。 在某些情况下，它将该值格式化为文本，并将其插入到 SQL 语句中，然后再将该语句发送到数据源。
