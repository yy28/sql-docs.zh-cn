---
title: 设置参数值 |Microsoft Docs
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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 0bb1115290f53c19fae1aacb0a976cfcef63e086
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/15/2019
ms.locfileid: "68094233"
---
# <a name="setting-parameter-values"></a>设置参数值
若要设置参数的值，该应用程序只需设置变量绑定到该参数的值。 它并不重要时设置此值，只要设置之前执行的语句。 应用程序可以设置的值之前或之后绑定变量，并且它可以更改许多次，它想要的值。 执行该语句，该驱动程序只需检索变量的当前值。 不止一次; 执行已准备的语句时，这一点特别有用应用程序的某些或全部变量每次执行该语句将设置新值。 此示例，请参阅[准备好执行](../../../odbc/reference/develop-app/prepared-execution-odbc.md)前面在本部分中。  
  
 如果在调用绑定长度/指示器缓冲区**SQLBindParameter**，必须设置为以下值之一之前执行的语句：  
  
-   绑定的变量中的数据的字节长度。 仅当该变量是字符或二进制，驱动程序将检查此长度 (*ValueType*为 SQL_C_CHAR 或 SQL_C_BINARY)。  
  
-   SQL_NTS. 数据是一个以 null 结尾的字符串。  
  
-   SQL_NULL_DATA. 数据值为 NULL，并驱动程序忽略绑定的变量的值。  
  
-   SQL_DATA_AT_EXEC 或 SQL_LEN_DATA_AT_EXEC 宏的结果。 参数的值是使用发送**SQLPutData**。 有关详细信息，请参阅[发送长数据](../../../odbc/reference/develop-app/sending-long-data.md)，在本部分中更高版本。  
  
 下表显示了绑定的变量和应用程序设置的各种参数值的长度/指示器缓冲区的值。  
  
|参数<br /><br /> value|参数<br /><br /> (SQL)<br /><br /> 数据类型|Variable (C)<br /><br /> 数据类型|中的值<br /><br /> 绑定<br /><br /> 变量|中的值<br /><br /> 长度/指示器<br /><br /> 缓冲区 [d]|  
|-------------------------|-----------------------------------------|----------------------------------|-------------------------------------|----------------------------------------------------|  
|"ABC"|SQL_CHAR|SQL_C_CHAR|ABC\0[a]|SQL_NTS 或 3|  
|10|SQL_INTEGER|SQL_C_SLONG|10|--|  
|10|SQL_INTEGER|SQL_C_CHAR|10\0[a]|SQL_NTS 或 2|  
|下午 1 点|SQL_TYPE_TIME|SQL_C_TYPE_TIME|13,0,0 [b]|--|  
|下午 1 点|SQL_TYPE_TIME|SQL_C_CHAR|{t ' 13: 00:00'} \0 [a]、 [c]|SQL_NTS 或 14|  
|NULL|SQL_SMALLINT|SQL_C_SSHORT|--|SQL_NULL_DATA|  
  
 [a]"\0"表示 null 终止字符。 仅当长度/指示器缓冲区中的值为 SQL_NTS null 终止字符需要。  
  
 [此列表中 b] 的数字是 TIME_STRUCT 结构的字段中存储的数字。  
  
 [c] 的字符串使用 ODBC 日期转义子句。 有关详细信息，请参阅[日期、 时间和时间戳文本](../../../odbc/reference/develop-app/date-time-and-timestamp-literals.md)。  
  
 [d] 驱动程序必须始终检查此值以查看它是否是一个特殊值，如 SQL_NULL_DATA。  
  
 驱动程序在执行时的参数值的作用是驱动程序相关。 如有必要，驱动程序将值从绑定的变量的 C 数据类型和字节长度转换为 SQL 数据类型、 精度和小数位数参数。 在大多数情况下，该驱动程序然后将值发送到数据源。 在某些情况下，它设置为文本值的格式，并将其插入到之前指定语句发送到数据源的 SQL 语句。
