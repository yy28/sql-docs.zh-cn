---
title: 从 SQL 到 C：Timestamp | Microsoft Docs
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 69c9f1258f35a69d6554783f5d1b4ca79be313d2
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/15/2019
ms.locfileid: "63259260"
---
# <a name="sql-to-c-timestamp"></a>从 SQL 到 C：时间戳

以下是时间戳 ODBC SQL 数据类型的标识符：

- SQL_TYPE_TIMESTAMP  

下表显示 ODBC C 数据类型可以转换成的 SQL 时间戳数据。 列和表中的条款的说明，请参阅[从 SQL 到 C 数据类型的转换的数据](../../../odbc/reference/appendixes/converting-data-from-sql-to-c-data-types.md)。  

|C 类型标识符|测试|**TargetValuePtr*|**StrLen_or_IndPtr*|SQLSTATE|  
|-----------------------|----------|------------------------|----------------------------|--------------|  
|SQL_C_CHAR|*BufferLength* > 字符字节长度<br /><br /> 20 < = *BufferLength* < = 字符字节长度<br /><br /> *BufferLength* < 20|数据<br /><br /> 截断的数据 [b]<br /><br /> 未定义|以字节为单位的数据的长度<br /><br /> 以字节为单位的数据的长度<br /><br /> 未定义|不适用<br /><br /> 01004<br /><br /> 22003|  
|SQL_C_WCHAR|*BufferLength* > 字符长度<br /><br /> 20 < = *BufferLength* < = 字符长度<br /><br /> *BufferLength* < 20|数据<br /><br /> 截断的数据 [b]<br /><br /> 未定义|以字符为单位的数据的长度<br /><br /> 以字符为单位的数据的长度<br /><br /> 未定义|不适用<br /><br /> 01004<br /><br /> 22003|  
|SQL_C_BINARY|数据的字节长度 < = *BufferLength*<br /><br /> 数据的字节长度 > *BufferLength*|数据<br /><br /> 未定义|以字节为单位的数据的长度<br /><br /> 未定义|不适用<br /><br /> 22003|  
|SQL_C_TYPE_DATE|时间戳的时间部分为零 [a]<br /><br /> 时间戳的时间部分为非零值 [a]|数据<br /><br /> 截断的数据 [c]|6[f]<br /><br /> 6[f]|不适用<br /><br /> 01S07|  
|SQL_C_TYPE_TIME|秒小数部分的时间戳为零 [a]<br /><br /> 时间戳的秒小数部分为非零值 [a]|Data[d]<br /><br /> 截断的数据 [d]、 [e]|6[f]<br /><br /> 6[f]|不适用<br /><br /> 01S07|  
|SQL_C_TYPE_TIMESTAMP|不会截断秒小数部分的时间戳 [a]<br /><br /> 截断秒小数部分的时间戳 [a]|Data[e]<br /><br /> [E] 的截断的数据|16[f]<br /><br /> 16[f]|不适用<br /><br /> 01S07|  

 [a] 的值*BufferLength*忽略此转换。 驱动程序假定的大小 **TargetValuePtr*是 C 数据类型的大小。  
  
 [b] 上，时间戳的秒的小数部分将被截断。  
  
 [截断时间戳 c] 的时间部分。  
  
 [忽略时间戳 d] 上，日期部分。  
  
 [e] 秒的小数部分的时间戳会被截断。  
  
 [f] 这是相应的 C 数据类型的大小。  

时间戳 SQL 数据转换为 C 字符数据时，生成的字符串时，在"*yyyy*-*mm*-*dd* *hh*:*mm*:*ss*[。*f...* ]"格式，其中在秒的小数部分使用最多到九位。 此格式不受 Windows® 国家/地区设置。 （除了小数点和秒的小数部分，整个格式必须使用，而不考虑时间戳 SQL 数据类型的精度。）
