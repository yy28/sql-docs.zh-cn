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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 923fd57f4308fb72aca2f829ccb9d7b884c12546
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/27/2020
ms.locfileid: "81299827"
---
# <a name="setting-parameter-values"></a>设置参数值
若要设置参数的值，应用程序只需将绑定到参数的变量的值设置为。 如果设置了此值，则它并不重要，只要在执行语句之前设置该值。 应用程序可以在绑定变量之前或之后设置值，并且它可以根据需要更改多次。 执行语句时，驱动程序只检索变量的当前值。 当多次执行预定义语句时，此方法特别有用;每次执行语句时，应用程序都会为某些或所有变量设置新值。 有关此操作的示例，请参阅本部分前面的[准备执行](../../../odbc/reference/develop-app/prepared-execution-odbc.md)。  
  
 如果在对**SQLBindParameter**的调用中绑定了长度/指示器缓冲区，则在执行该语句之前，必须将其设置为以下值之一：  
  
-   绑定变量中数据的字节长度。 仅当变量为字符或二进制（*ValueType*为 SQL_C_CHAR 或 SQL_C_BINARY）时，驱动程序才会检查此长度。  
  
-   SQL_NTS。 数据为以 null 值结束的字符串。  
  
-   SQL_NULL_DATA。 数据值为 NULL，驱动程序将忽略绑定变量的值。  
  
-   SQL_DATA_AT_EXEC 或 SQL_LEN_DATA_AT_EXEC 宏的结果。 参数的值将与**SQLPutData**一起发送。 有关详细信息，请参阅本部分后面的[发送长数据](../../../odbc/reference/develop-app/sending-long-data.md)。  
  
 下表显示了绑定变量的值和应用程序为各种参数值设置的长度/指示器缓冲区。  
  
|参数<br /><br /> value|参数<br /><br /> TRANSACT-SQL<br /><br /> 数据类型|变量（C）<br /><br /> 数据类型| 中的值<br /><br /> 绑定<br /><br /> 可变| 中的值<br /><br /> 长度/指示器<br /><br /> 缓冲区 [d]|  
|-------------------------|-----------------------------------------|----------------------------------|-------------------------------------|----------------------------------------------------|  
|"ABC"|SQL_CHAR|SQL_C_CHAR|ABC\0 [a]|SQL_NTS 或3|  
|10|SQL_INTEGER|SQL_C_SLONG|10|--|  
|10|SQL_INTEGER|SQL_C_CHAR|10 \ 0 [a]|SQL_NTS 或2|  
|1 P。M|SQL_TYPE_TIME|SQL_C_TYPE_TIME|13，0，0 [b]|--|  
|1 P。M|SQL_TYPE_TIME|SQL_C_CHAR|{t ' 13：00： 00 '} \ 0 [a]，[c]|SQL_NTS 或14|  
|Null|SQL_SMALLINT|SQL_C_SSHORT|--|SQL_NULL_DATA|  
  
 [a] "\ 0" 表示 null 终止字符。 仅当长度/指示器缓冲区中的值 SQL_NTS 时，才需要 null 终止字符。  
  
 [b] 此列表中的数字是存储在 TIME_STRUCT 结构的字段中的数字。  
  
 [c] 字符串使用 ODBC date escape 子句。 有关详细信息，请参阅[日期、时间和时间戳文本](../../../odbc/reference/develop-app/date-time-and-timestamp-literals.md)。  
  
 [d] 驱动程序必须始终检查此值，以确定它是否是一个特殊值，如 SQL_NULL_DATA。  
  
 在执行时，驱动程序使用参数值执行的操作取决于驱动程序。 必要时，驱动程序将值从绑定变量的 C 数据类型和字节长度转换为参数的 SQL 数据类型、精度和小数位数。 在大多数情况下，驱动程序会将值发送到数据源。 在某些情况下，它会将值设置为文本格式，并将其插入到 SQL 语句中，然后再将语句发送到数据源。
