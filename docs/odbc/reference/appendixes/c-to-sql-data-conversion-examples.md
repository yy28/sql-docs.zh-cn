---
title: C 到 SQL 数据转换示例 |Microsoft 文档
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
ms.topic: conceptual
helpviewer_keywords:
- converting data from c to SQL types [ODBC], examples
- data conversions from C to SQL types [ODBC], examples
ms.assetid: 9f390afc-d8b8-4286-b559-98b3b8781f3d
caps.latest.revision: 7
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: f51dd54f01bacd5c36da84c71061fd71f072bc17
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
---
# <a name="c-to-sql-data-conversion-examples"></a>C 到 SQL 数据转换示例
以下示例阐释如何驱动程序将 C 数据转换为 SQL 数据：  
  
|C 类型标识符|C 数据值|SQL 类型<br /><br /> 标识符 (identifier)|列<br /><br /> 长度|SQL 数据<br /><br /> 值|SQLSTATE|  
|-----------------------|------------------|-----------------------------|-----------------------|------------------------|--------------|  
|SQL_C_CHAR|abcdef\0 [a]|SQL_CHAR|6|abcdef|不适用|  
|SQL_C_CHAR|abcdef\0 [a]|SQL_CHAR|5|abcde|22001|  
|SQL_C_CHAR|1234.56\0 [a]|SQL_DECIMAL|8 [b]|1234.56|不适用|  
|SQL_C_CHAR|1234.56\0 [a]|SQL_DECIMAL|7 [b]|1234.5|22001|  
|SQL_C_CHAR|1234.56\0 [a]|SQL_DECIMAL|4|----|22003|  
|SQL_C_FLOAT|1234.56|SQL_FLOAT|不适用|1234.56|不适用|  
|SQL_C_FLOAT|1234.56|SQL_INTEGER|不适用|1234|22001|  
|SQL_C_FLOAT|1234.56|SQL_TINYINT|不适用|----|22003|  
|SQL_C_TYPE_DATE|1992,12,31 [c]|SQL_CHAR|10|1992-12-31|不适用|  
|SQL_C_TYPE_DATE|1992,12,31 [c]|SQL_CHAR|9|----|22003|  
|SQL_C_TYPE_DATE|1992,12,31 [c]|SQL_TIMESTAMP|不适用|1992-12-31 00:00:00.0|不适用|  
|SQL_C_TYPE_TIMESTAMP|1992,12,31、 23,45,55、 120000000 [d]|SQL_CHAR|22|1992-12-31 23:45:55.12|不适用|  
|SQL_C_TYPE_TIMESTAMP|1992,12,31、 23,45,55、 120000000 [d]|SQL_CHAR|21|1992-12-31 23:45:55.1|22001|  
|SQL_C_TYPE_TIMESTAMP|1992,12,31、 23,45,55、 120000000 [d]|SQL_CHAR|18|----|22003|  
  
 [a]"\0"表示 null 终止字节。 仅当数据的长度为 sql_nts 的以 null 终止字节需要。  
  
 [b] 中除了数字的字节数，1 个字节是所必需的登录和另一个字节是所必需的小数点。  
  
 [此列表中 c] 的数字是中的字段 SQL_DATE_STRUCT 结构存储数字。  
  
 [此列表中 d] 的数字是中的字段 SQL_TIMESTAMP_STRUCT 结构存储数字。
