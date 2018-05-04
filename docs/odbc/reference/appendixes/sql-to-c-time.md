---
title: 为 c： 时间 SQL |Microsoft 文档
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
- converting data from SQL to C types [ODBC], time
- time data type [ODBC]
- data conversions from SQL to C types [ODBC], time
ms.assetid: 6dc59973-7bb5-40f1-87c8-5bf68b3bf2ee
caps.latest.revision: 7
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 079722668c6bce9a7d5ca2012aa947d6a87951d6
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
---
# <a name="sql-to-c-time"></a>为 c： 时间 SQL
ODBC SQL 数据类型是次标识符：  
  
 SQL_TYPE_TIME  
  
 下表显示 ODBC C 数据类型时 SQL 数据可能转换到的目标。 列和表中的条款的说明，请参阅[转换数据从 SQL C 数据类型到](../../../odbc/reference/appendixes/converting-data-from-sql-to-c-data-types.md)。  
  
|C 类型标识符|测试|**TargetValuePtr*|**StrLen_or_IndPtr*|SQLSTATE|  
|-----------------------|----------|------------------------|----------------------------|--------------|  
|SQL_C_CHAR|*BufferLength* > 字符字节长度<br /><br /> *9* <= *BufferLength* < = 字符字节长度<br /><br /> *BufferLength* < 9|Data<br /><br /> 截断的数据 [a]<br /><br /> 未定义|以字节为单位的数据的长度<br /><br /> 以字节为单位的数据的长度<br /><br /> 未定义|不适用<br /><br /> 01004<br /><br /> 22003|  
|SQL_C_WCHAR|*BufferLength* > 字符长度<br /><br /> *9* <= *BufferLength* < = 字符长度<br /><br /> *BufferLength* < 9|Data<br /><br /> 截断的数据 [a]<br /><br /> 未定义|以字符为单位的数据的长度<br /><br /> 以字符为单位的数据的长度<br /><br /> 未定义|不适用<br /><br /> 01004<br /><br /> 22003|  
|SQL_C_BINARY|数据的字节长度 < = *BufferLength*<br /><br /> 数据的字节长度 > *BufferLength*|Data<br /><br /> 未定义|以字节为单位的数据的长度<br /><br /> 未定义|不适用<br /><br /> 22003|  
|SQL_C_TYPE_TIME|无 [b]|Data|6 [d]|不适用|  
|SQL_C_TYPE_TIMESTAMP|无 [b]|数据 [c]|16 [d]|不适用|  
  
 [a] 时间的秒的小数部分将被截断。  
  
 [b] 的值*BufferLength*忽略此转换。 该驱动程序假定的大小 **TargetValuePtr*是 C 数据类型的大小。  
  
 [时间戳结构 c] 上，日期字段设置为当前日期和时间戳结构的秒的小数部分字段设置为零。  
  
 [d] 这是对应的 C 数据类型的大小。  
  
 当时间 SQL 数据转换为字符 C 数据时，生成的字符串是在"*hh*:*mm*:*ss*"格式。 此格式不受 Windows® 国家/地区设置。
