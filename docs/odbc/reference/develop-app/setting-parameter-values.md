---
title: 设置参数值 |Microsoft 文档
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
- parameter values [ODBC]
ms.assetid: 13e5da79-b60c-48d0-b467-773f481ef2a4
caps.latest.revision: 6
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 88b8ea3a21f7b2d0bd5790aad934e784b4ca3e87
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/16/2018
---
# <a name="setting-parameter-values"></a>设置参数值
若要设置参数的值，应用程序只需将设置绑定到参数变量的值。 它并不重要时设置此值，只要它设置之前执行的语句。 应用程序可以设置值之前或之后绑定变量，并且它可以更改它想多次的值。 当执行语句时，该驱动程序只需检索变量的当前值。 不止一次; 执行已准备的语句时，这是特别有用应用程序为某些或所有变量每次执行该语句时将设置新值。 此示例，请参阅[已准备的执行](../../../odbc/reference/develop-app/prepared-execution-odbc.md)，本部分前面的。  
  
 如果长度/指示器缓冲区已绑定到调用中**SQLBindParameter**，必须设置为以下值之一之前执行的语句：  
  
-   绑定变量中的数据字节长度。 该驱动程序将检查此长度，仅当变量是字符串或二进制 (*ValueType* SQL_C_CHAR 或 SQL_C_BINARY)。  
  
-   SQL_NTS 以。 数据是以 null 结尾的字符串。  
  
-   SQL_NULL_DATA。 数据值为 NULL，和驱动程序将忽略绑定变量的值。  
  
-   SQL_DATA_AT_EXEC 或 SQL_LEN_DATA_AT_EXEC 宏的结果。 参数的值是与发送**SQLPutData**。 有关详细信息，请参阅[发送长整型数据](../../../odbc/reference/develop-app/sending-long-data.md)，本部分中更高版本。  
  
 下表显示绑定的变量和应用程序将设置各种不同的参数值的长度/指示器缓冲区的值。  
  
|参数<br /><br /> 值|参数<br /><br /> (SQL)<br /><br /> 数据类型|Variable (C)<br /><br /> 数据类型|中的值<br /><br /> 绑定<br /><br /> 变量|中的值<br /><br /> 长度/指示器<br /><br /> 缓冲区 [d]|  
|-------------------------|-----------------------------------------|----------------------------------|-------------------------------------|----------------------------------------------------|  
|"ABC"|SQL_CHAR|SQL_C_CHAR|ABC\0 [a]|Sql_nts 以或 3|  
|10|SQL_INTEGER|SQL_C_SLONG|10|--|  
|10|SQL_INTEGER|SQL_C_CHAR|10\0 [a]|Sql_nts 以或 2|  
|下午 1|SQL_TYPE_TIME|SQL_C_TYPE_TIME|13,0,0 [b]|--|  
|下午 1|SQL_TYPE_TIME|SQL_C_CHAR|{t ' 13: 00:00'} \0 [a]、 [c]|Sql_nts 以或 14|  
|NULL|SQL_SMALLINT|SQL_C_SSHORT|--|SQL_NULL_DATA|  
  
 [a]"\0"表示 null 终止字符。 仅当长度/指示器缓冲区中的值为 sql_nts 的以 null 终止字符需要。  
  
 [此列表中 b] 的数字是中的字段 TIME_STRUCT 结构存储数字。  
  
 [c] 该字符串使用 ODBC 日期 escape 子句。 有关详细信息，请参阅[日期、 时间和时间戳文本](../../../odbc/reference/develop-app/date-time-and-timestamp-literals.md)。  
  
 [d] 驱动程序必须始终检查此值，以确定它是否是一个特殊的值，如 SQL_NULL_DATA。  
  
 驱动程序使用的参数值在执行时的用途是驱动程序相关的。 如有必要，该驱动程序将值从绑定变量的 C 数据类型和字节长度转换为 SQL 数据类型、 精度和小数位数。 在大多数情况下，该驱动程序然后将值发送到数据源。 在某些情况下，它设置为文本值的格式，并将其插入到 SQL 语句中之前将语句发送到数据源。
