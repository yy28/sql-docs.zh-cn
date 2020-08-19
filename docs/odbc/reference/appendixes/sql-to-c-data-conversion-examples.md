---
description: 从 SQL 到 C 的数据转换示例
title: SQL 到 C 数据转换示例 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2019
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- data conversions from SQL to C types [ODBC], examples
- converting data from SQL to C types [ODBC], examples
ms.assetid: 0190c76c-7f9b-42f4-be9d-cef7284840fd
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: a7a3d70a6f74a814262ddad580b5e5a2b0d79927
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/17/2020
ms.locfileid: "88429579"
---
# <a name="sql-to-c-data-conversion-examples"></a>从 SQL 到 C 的数据转换示例

下表中所示的示例说明了驱动程序如何将 SQL 数据转换为 C 数据：  
  
|SQL 类型<br /><br /> 标识符 (identifier)|SQL 数据<br /><br /> value|C 类型<br /><br /> 标识符 (identifier)|Buffer<br /><br /> length|**TargetValuePtr*|SQLSTATE|  
|-----------------------------|------------------------|---------------------------|-----------------------|------------------------|--------------|  
|SQL_CHAR|abcdef|SQL_C_CHAR|7|abcdef\0 [a]|不适用|  
|SQL_CHAR|abcdef|SQL_C_CHAR|6|abcde\0 [a]|01004|  
|SQL_DECIMAL|1234.56|SQL_C_CHAR|8|1234.56 \ 0 [a]|不适用|  
|SQL_DECIMAL|1234.56|SQL_C_CHAR|5|1234 \ 0 [a]|01004|  
|SQL_DECIMAL|1234.56|SQL_C_CHAR|4|----|22003|  
|SQL_DECIMAL|1234.56|SQL_C_FLOAT|已忽略|1234.56|不适用|  
|SQL_DECIMAL|1234.56|SQL_C_SSHORT|已忽略|1234|01S07|  
|SQL_DECIMAL|1234.56|SQL_C_STINYINT|已忽略|----|22003|  
|SQL_DOUBLE|1.2345678|SQL_C_DOUBLE|已忽略|1.2345678|不适用|  
|SQL_DOUBLE|1.2345678|SQL_C_FLOAT|已忽略|1.234567|不适用|  
|SQL_DOUBLE|1.2345678|SQL_C_STINYINT|已忽略|1|不适用|  
|SQL_TYPE_DATE|1992-12-31|SQL_C_CHAR|11|1992-12-31 \ 0 [a]|不适用|  
|SQL_TYPE_DATE|1992-12-31|SQL_C_CHAR|10|-----|22003|  
|SQL_TYPE_DATE|1992-12-31|SQL_C_TIMESTAMP|已忽略|1992，12，31，0，0，0，0 [b]|不适用|  
|SQL_TYPE_TIMESTAMP|1992-12-31 23：45：55.12|SQL_C_CHAR|23|1992-12-31 23：45： 55.12 \ 0 [a]|不适用|  
|SQL_TYPE_TIMESTAMP|1992-12-31 23：45：55.12|SQL_C_CHAR|22|1992-12-31 23：45： 55.1 \ 0 [a]|01004|  
|SQL_TYPE_TIMESTAMP|1992-12-31 23：45：55.12|SQL_C_CHAR|18|----|22003|  
  
 [a] "\ 0" 表示 null 终止字节。 驱动程序始终以 null 终止 SQL_C_CHAR 数据。  
  
 [b] 此列表中的数字是存储在 TIMESTAMP_STRUCT 结构的字段中的数字。
