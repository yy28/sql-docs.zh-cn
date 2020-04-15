---
title: SQL 到 C：日期 |微软文档
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- converting data from SQL to C types [ODBC], date
- date data type [ODBC]
- data conversions from SQL to C types [ODBC], date
ms.assetid: 703c7960-9cf4-4d7a-9920-53b29c184f97
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: fe9656c0c02c0ff5a10029525da3d38280530cc3
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/14/2020
ms.locfileid: "81296527"
---
# <a name="sql-to-c-date"></a>从 SQL 到 C：日期
日期 ODBC SQL 数据类型的标识符是：  
  
 SQL_TYPE_DATE  
  
 下表显示了可以转换 SQL 数据的 ODBC C 数据类型。 有关表中列和术语的说明，请参阅[将数据从 SQL 转换为 C 数据类型](../../../odbc/reference/appendixes/converting-data-from-sql-to-c-data-types.md)。  
  
|C 类型标识符|测试|**目标价值Ptr*|**StrLen_or_IndPtr*|SQLSTATE|  
|-----------------------|----------|------------------------|----------------------------|--------------|  
|SQL_C_CHAR|*缓冲区长度*>字符字节长度<br /><br /> 11 <=*缓冲区长度*<= 字符字节长度<br /><br /> *缓冲区长度*< 11|数据<br /><br /> 截断的数据<br /><br /> Undefined|10<br /><br /> 以字节为单位的数据长度<br /><br /> Undefined|不适用<br /><br /> 01004<br /><br /> 22003|  
|SQL_C_WCHAR|*缓冲区长度*>字符长度<br /><br /> 11<=*缓冲区长度*<= 字符长度<br /><br /> *缓冲区长度*< 11|数据<br /><br /> 截断的数据<br /><br /> Undefined|10<br /><br /> 字符中的数据长度<br /><br /> Undefined|不适用<br /><br /> 01004<br /><br /> 22003|  
|SQL_C_BINARY|数据<字节长度 =*缓冲区长度*<br /><br /> >*缓冲区长度*的数据字节长度|数据<br /><br /> Undefined|以字节为单位的数据长度<br /><br /> Undefined|不适用<br /><br /> 22003|  
|SQL_C_TYPE_DATE|无[a]|数据|6[c]|不适用|  
|SQL_C_TYPE_TIMESTAMP|无[a]|数据[b]|16[c]|不适用|  
  
 [a] 此转换将忽略*缓冲区长度*的值。 驱动程序假定 **目标价值Ptr*的大小是 C 数据类型的大小。  
  
 [b] 时间戳结构的时间字段设置为零。  
  
 [c] 这是相应的 C 数据类型的大小。  
  
 当 SQL 数据转换为字符 C 数据的日期时，生成的字符串采用 *"yyyymm*-*mm*-*dd"* 格式。 此格式不受 Windows ®国家/地区设置的影响。
