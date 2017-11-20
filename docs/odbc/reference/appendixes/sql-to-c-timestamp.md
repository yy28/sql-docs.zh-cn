---
title: "为 c： 时间戳的 SQL |Microsoft 文档"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: reference
ms.reviewer: 
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- timestamp data type [ODBC]
- converting data from SQL to C types [ODBC], timestamp
- data conversions from SQL to C types [ODBC], timestamp
ms.assetid: 6a0617cf-d8c0-4316-8bb4-e6ddb45d7bf1
caps.latest.revision: 8
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: a551d51a434d17162a5f5bcf0091e593d25f283a
ms.contentlocale: zh-cn
ms.lasthandoff: 09/09/2017

---
# <a name="sql-to-c-timestamp"></a>为 c： 时间戳的 SQL
时间戳 ODBC SQL 数据类型的标识符是：  
  
 SQL_TYPE_TIMESTAMP  
  
 下表显示 ODBC C 数据类型的时间戳 SQL 数据可以转换到的目标。 列和表中的条款的说明，请参阅[转换数据从 SQL C 数据类型到](../../../odbc/reference/appendixes/converting-data-from-sql-to-c-data-types.md)。  
  
|C 类型标识符|测试|**TargetValuePtr*|**StrLen_or_IndPtr*|SQLSTATE|  
|-----------------------|----------|------------------------|----------------------------|--------------|  
|SQL_C_CHAR|*BufferLength* > 字符字节长度<br /><br /> 20 < = *BufferLength* < = 字符字节长度<br /><br /> *BufferLength* < 20|data<br /><br /> 截断的数据 [b]<br /><br /> 未定义|以字节为单位的数据的长度<br /><br /> 以字节为单位的数据的长度<br /><br /> 未定义|不适用<br /><br /> 01004<br /><br /> 22003|  
|SQL_C_WCHAR|*BufferLength* > 字符长度<br /><br /> 20 < = *BufferLength* < = 字符长度<br /><br /> *BufferLength* < 20|data<br /><br /> 截断的数据 [b]<br /><br /> 未定义|以字符为单位的数据的长度<br /><br /> 以字符为单位的数据的长度<br /><br /> 未定义|不适用<br /><br /> 01004<br /><br /> 22003|  
|SQL_C_BINARY|数据的字节长度 < = *BufferLength*<br /><br /> 数据的字节长度 > *BufferLength*|data<br /><br /> 未定义|以字节为单位的数据的长度<br /><br /> 未定义|不适用<br /><br /> 22003|  
|SQL_C_TYPE_DATE|时间部分的时间戳为零 [a]<br /><br /> 时间部分的时间戳为非零 [a]|data<br /><br /> 截断的数据 [c]|6 [f]<br /><br /> 6 [f]|不适用<br /><br /> 01S07|  
|SQL_C_TYPE_TIME|时间戳的秒的小数部分部分为零 [a]<br /><br /> 秒的小数部分的时间戳的部分为非零 [a]|数据 [d]<br /><br /> 截断的数据 [d]、 [e]|6 [f]<br /><br /> 6 [f]|不适用<br /><br /> 01S07|  
_C_TYPE_TIMESTAMP|时间戳的秒的小数部分部分不会被截断 [a]<br /><br /> 截断的时间戳的秒的小数部分部分 [a]|数据 [e]<br /><br /> 截断的数据 [e]|16 [f]<br /><br /> 16 [f]|不适用<br /><br /> 01S07|  
  
 [a] 的值*BufferLength*忽略此转换。 该驱动程序假定的大小 **TargetValuePtr*是 C 数据类型的大小。  
  
 [秒的时间戳 b] 的小数部分将被截断。  
  
 [c] 的时间部分的时间戳将被截断。  
  
 [d] 上，日期部分的时间戳将被忽略。  
  
 [时间戳 e] 的秒的小数部分部分将被截断。  
  
 [f] 这是对应的 C 数据类型的大小。  
  
 当时间戳 SQL 数据转换为字符 C 数据时，生成的字符串是在"*yyyy*-*mm*-*dd* *hh*:*mm*:*ss*[。*f...*]"格式，其中最多 9 个数字，可以用秒的小数部分。 此格式不受 Windows® 国家/地区设置。 （除外的小数点和秒的小数部分，整个格式必须为，则无论使用的时间戳 SQL 数据类型的精度。）

