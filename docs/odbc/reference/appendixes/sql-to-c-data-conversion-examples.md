---
title: "C 数据转换示例 SQL |Microsoft 文档"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: reference
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- data conversions from SQL to C types [ODBC], examples
- converting data from SQL to C types [ODBC], examples
ms.assetid: 0190c76c-7f9b-42f4-be9d-cef7284840fd
caps.latest.revision: "7"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 6e2c763d78eb6ea0cf854a455e09fc09b8a7de2c
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/20/2017
---
# <a name="sql-to-c-data-conversion-examples"></a>SQL C 数据转换示例
下表中所示的示例说明了如何驱动程序将 SQL 数据转换为 C 数据：  
  
|SQL 类型<br /><br /> 标识符 (identifier)|SQL 数据<br /><br /> 值|C 类型<br /><br /> 标识符 (identifier)|缓冲区<br /><br /> 长度|**TargetValuePtr*|SQLSTATE|  
|-----------------------------|------------------------|---------------------------|-----------------------|------------------------|--------------|  
|SQL_CHAR|abcdef|SQL_C_CHAR|7|abcdef\0 [a]|不适用|  
|SQL_CHAR|abcdef|SQL_C_CHAR|6|abcde\0 [a]|01004|  
|SQL_DECIMAL|1234.56|SQL_C_CHAR|8|1234.56\0 [a]|不适用|  
|SQL_DECIMAL|1234.56|SQL_C_CHAR|5|1234\0 [a]|01004|  
|SQL_DECIMAL|1234.56|SQL_C_CHAR|4|----|22003|  
|SQL_DECIMAL|1234.56|SQL_C_FLOAT|忽略|1234.56|不适用|  
|SQL_DECIMAL|1234.56|SQL_C_SSHORT|忽略|1234|01S07|  
|SQL_DECIMAL|1234.56|SQL_C_STINYINT|忽略|----|22003|  
SQL_DOUBLE|1.2345678|SQL_C_DOUBLE|忽略|1.2345678|不适用|  
|SQL_DOUBLE|1.2345678|SQL_C_FLOAT|忽略|1.234567|不适用|  
|SQL_DOUBLE|1.2345678|SQL_C_STINYINT|忽略|1|不适用|  
|SQL_TYPE_DATE|1992-12-31|SQL_C_CHAR|11|1992-12-31\0 [a]|不适用|  
|SQL_TYPE_DATE|1992-12-31|SQL_C_CHAR|10|-----|22003|  
|SQL_TYPE_DATE|1992-12-31|SQL_C_TIMESTAMP|忽略|1992,12,31、 0,0,0,0 [b]|不适用|  
|SQL_TYPE_TIMESTAMP|1992-12-31 23:45:55.12|SQL_C_CHAR|23|1992-12-31 23:45:55.12\0 [a]|不适用|  
SQL_TYPE_TIMESTAMP|1992-12-31 23:45:55.12|SQL_C_CHAR|22|1992-12-31 23:45:55.1\0 [a]|01004|  
|SQL_TYPE_TIMESTAMP|1992-12-31 23:45:55.12|SQL_C_CHAR|18|----|22003|  
  
 [a]"\0"表示 null 终止字节。 该驱动程序始终 null 终止 SQL_C_CHAR 数据。  
  
 [此列表中 b] 的数字是中的字段 TIMESTAMP_STRUCT 结构存储数字。
