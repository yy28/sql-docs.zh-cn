---
title: SQL 到 C：时间戳 |Microsoft Docs
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
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/27/2020
ms.locfileid: "81296347"
---
# <a name="sql-to-c-timestamp"></a>从 SQL 到 C：时间戳

Timestamp ODBC SQL 数据类型的标识符如下：

- SQL_TYPE_TIMESTAMP  

下表显示了可将 timestamp SQL 数据转换为的 ODBC C 数据类型。 有关表中的列和字词的说明，请参阅将[数据从 SQL 转换为 C 数据类型](../../../odbc/reference/appendixes/converting-data-from-sql-to-c-data-types.md)。  

|C 类型标识符|测试|**TargetValuePtr*|**StrLen_or_IndPtr*|SQLSTATE|  
|-----------------------|----------|------------------------|----------------------------|--------------|  
|SQL_C_CHAR|*BufferLength* > 字符字节长度<br /><br /> 20 <= *BufferLength* <= 字符字节长度<br /><br /> *BufferLength* < 20|数据<br /><br /> 截断的数据 [b]<br /><br /> Undefined|数据的长度（以字节为单位）<br /><br /> 数据的长度（以字节为单位）<br /><br /> Undefined|不适用<br /><br /> 01004<br /><br /> 22003|  
|SQL_C_WCHAR|*BufferLength* > 字符长度<br /><br /> 20 <= *BufferLength* <= 字符长度<br /><br /> *BufferLength* < 20|数据<br /><br /> 截断的数据 [b]<br /><br /> Undefined|数据的长度（以字符为长度）<br /><br /> 数据的长度（以字符为长度）<br /><br /> Undefined|不适用<br /><br /> 01004<br /><br /> 22003|  
|SQL_C_BINARY|Data <的字节长度 = *BufferLength*<br /><br /> 数据 > 的字节长度*BufferLength*|数据<br /><br /> Undefined|数据的长度（以字节为单位）<br /><br /> Undefined|不适用<br /><br /> 22003|  
|SQL_C_TYPE_DATE|时间戳的时间部分为零 [a]<br /><br /> 时间戳的时间部分为非零值 [a]|数据<br /><br /> 截断的数据 [c]|6 [f]<br /><br /> 6 [f]|不适用<br /><br /> 01S07|  
|SQL_C_TYPE_TIME|时间戳的秒小数部分为零 [a]<br /><br /> 时间戳的秒小数部分为非零值 [a]|数据 [d]<br /><br /> 截断的数据 [d]，[e]|6 [f]<br /><br /> 6 [f]|不适用<br /><br /> 01S07|  
|SQL_C_TYPE_TIMESTAMP|不截断时间戳的秒小数部分<br /><br /> 时间戳的秒小数部分被截断 [a]|数据 [e]<br /><br /> 截断的数据 [e]|16 [f]<br /><br /> 16 [f]|不适用<br /><br /> 01S07|  

 [a] 此转换将忽略*BufferLength*的值。 驱动程序假设大小 **TargetValuePtr*是 C 数据类型的大小。  
  
 [b] 时间戳的秒的小数部分被截断。  
  
 [c] 时间戳的时间部分被截断。  
  
 [d] 忽略时间戳的日期部分。  
  
 [e] 时间戳的秒的小数部分被截断。  
  
 [f] 这是对应的 C 数据类型的大小。  

当时间戳 SQL 数据转换为字符 C 数据时，生成的字符串在 "*yyyy*-*mm*-*dd* *hh*：*mm*：*ss*[.*f ...*] "format，最多可使用9位数作为秒的小数部分。 此格式不受 Windows®的 "国家/地区" 设置的影响。 （小数点和秒的小数部分除外，无论 timestamp SQL 数据类型的精度如何，都必须使用整个格式。）
