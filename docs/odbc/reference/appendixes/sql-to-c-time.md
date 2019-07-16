---
title: 从 SQL 到 C：时间 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- converting data from SQL to C types [ODBC], time
- time data type [ODBC]
- data conversions from SQL to C types [ODBC], time
ms.assetid: 6dc59973-7bb5-40f1-87c8-5bf68b3bf2ee
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 99f8219ef53f72b0d7ab1477bba5d24d441a3141
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/15/2019
ms.locfileid: "68065080"
---
# <a name="sql-to-c-time"></a>从 SQL 到 C：Time
ODBC SQL 数据类型是次标识符：  
  
 SQL_TYPE_TIME  
  
 下表显示 ODBC C 数据类型时 SQL 数据可能会转换为。 列和表中的条款的说明，请参阅[从 SQL 到 C 数据类型的转换的数据](../../../odbc/reference/appendixes/converting-data-from-sql-to-c-data-types.md)。  
  
|C 类型标识符|测试|**TargetValuePtr*|**StrLen_or_IndPtr*|SQLSTATE|  
|-----------------------|----------|------------------------|----------------------------|--------------|  
|SQL_C_CHAR|*BufferLength* > 字符字节长度<br /><br /> *9* <= *BufferLength* < = 字符字节长度<br /><br /> *BufferLength* < 9|Data<br /><br /> [A] 的截断的数据<br /><br /> 未定义|以字节为单位的数据的长度<br /><br /> 以字节为单位的数据的长度<br /><br /> 未定义|不适用<br /><br /> 01004<br /><br /> 22003|  
|SQL_C_WCHAR|*BufferLength* > 字符长度<br /><br /> *9* <= *BufferLength* < = 字符长度<br /><br /> *BufferLength* < 9|Data<br /><br /> [A] 的截断的数据<br /><br /> 未定义|以字符为单位的数据的长度<br /><br /> 以字符为单位的数据的长度<br /><br /> 未定义|不适用<br /><br /> 01004<br /><br /> 22003|  
|SQL_C_BINARY|数据的字节长度 < = *BufferLength*<br /><br /> 数据的字节长度 > *BufferLength*|Data<br /><br /> 未定义|以字节为单位的数据的长度<br /><br /> 未定义|不适用<br /><br /> 22003|  
|SQL_C_TYPE_TIME|无 [b]|Data|6[d]|不适用|  
|SQL_C_TYPE_TIMESTAMP|无 [b]|数据 [c]|16 [d]|不适用|  
  
 [a] 将被截断秒的小数部分的时间。  
  
 [b] 的值*BufferLength*忽略此转换。 驱动程序假定的大小 **TargetValuePtr*是 C 数据类型的大小。  
  
 [时间戳结构 c] 上，日期字段设置为当前日期和时间戳结构的秒的小数部分字段设置为零。  
  
 [d] 这是相应的 C 数据类型的大小。  
  
 时间 SQL 数据转换为 C 字符数据时，生成的字符串时，在"*hh*:*mm*:*ss*"格式。 此格式不受 Windows® 国家/地区设置。
