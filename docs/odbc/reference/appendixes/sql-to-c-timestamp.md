---
title: SQL 到 C：时间戳 |微软文档
ms.custom: ''
ms.date: 01/19/2019
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- timestamp data type [ODBC]
- converting data from SQL to C types [ODBC], timestamp
- data conversions from SQL to C types [ODBC], timestamp
ms.assetid: 6a0617cf-d8c0-4316-8bb4-e6ddb45d7bf1
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 552bab585e4480fd922c9b9a6b112830f5c11ad9
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/14/2020
ms.locfileid: "81296347"
---
# <a name="sql-to-c-timestamp"></a>从 SQL 到 C：时间戳

时间戳 ODBC SQL 数据类型的标识符如下：

- SQL_TYPE_TIMESTAMP  

下表显示了可转换为时间戳 SQL 数据的 ODBC C 数据类型。 有关表中列和术语的说明，请参阅[将数据从 SQL 转换为 C 数据类型](../../../odbc/reference/appendixes/converting-data-from-sql-to-c-data-types.md)。  

|C 类型标识符|测试|**目标价值Ptr*|**StrLen_or_IndPtr*|SQLSTATE|  
|-----------------------|----------|------------------------|----------------------------|--------------|  
|SQL_C_CHAR|*缓冲区长度*>字符字节长度<br /><br /> 20 个<=*缓冲区长度*<= 字符字节长度<br /><br /> *缓冲区长度*< 20|数据<br /><br /> 截断的数据[b]<br /><br /> Undefined|以字节为单位的数据长度<br /><br /> 以字节为单位的数据长度<br /><br /> Undefined|不适用<br /><br /> 01004<br /><br /> 22003|  
|SQL_C_WCHAR|*缓冲区长度*>字符长度<br /><br /> 20 <=*缓冲区长度*<= 字符长度<br /><br /> *缓冲区长度*< 20|数据<br /><br /> 截断的数据[b]<br /><br /> Undefined|字符中的数据长度<br /><br /> 字符中的数据长度<br /><br /> Undefined|不适用<br /><br /> 01004<br /><br /> 22003|  
|SQL_C_BINARY|数据<字节长度 =*缓冲区长度*<br /><br /> >*缓冲区长度*的数据字节长度|数据<br /><br /> Undefined|以字节为单位的数据长度<br /><br /> Undefined|不适用<br /><br /> 22003|  
|SQL_C_TYPE_DATE|时间戳的时间部分为零[a]<br /><br /> 时间戳的时间部分是非零[a]|数据<br /><br /> 截断数据[c]|6[f]<br /><br /> 6[f]|不适用<br /><br /> 01S07|  
|SQL_C_TYPE_TIME|时间戳的分数秒部分为零 [a]<br /><br /> 时间戳的分数秒部分是非零[a]|数据[d]<br /><br /> 截断数据[d]，[e]|6[f]<br /><br /> 6[f]|不适用<br /><br /> 01S07|  
|SQL_C_TYPE_TIMESTAMP|时间戳的分数秒部分不会截断[a]<br /><br /> 时间戳的分数秒部分被截断[a]|数据[e]<br /><br /> 截断数据[e]|16[f]<br /><br /> 16[f]|不适用<br /><br /> 01S07|  

 [a] 此转换将忽略*缓冲区长度*的值。 驱动程序假定 **目标价值Ptr*的大小是 C 数据类型的大小。  
  
 [b] 时间戳的小数秒被截断。  
  
 [c] 时间戳的时间部分被截断。  
  
 [d] 时间戳的日期部分将被忽略。  
  
 [e] 时间戳的小秒部分被截断。  
  
 [f] 这是相应的 C 数据类型的大小。  

当时间戳 SQL 数据转换为字符 C 数据时，生成的字符串位于 *"yyyymm*-*mm*-*dd* *hh**：mm**：ss*"中。*f...* 格式，其中最多九位数字可用于小数秒。 此格式不受 Windows ®国家/地区设置的影响。 （除了小数点和小数秒外，无论时间戳 SQL 数据类型的精度如何，都必须使用整个格式。
