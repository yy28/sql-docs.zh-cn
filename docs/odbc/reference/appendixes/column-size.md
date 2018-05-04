---
title: 列大小 |Microsoft 文档
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
- data types [ODBC], column size
- size of data types [ODBC]
- SQL data types [ODBC], column characteristics
- column size of data types [ODBC]
ms.assetid: 541b83ab-b16d-4714-bcb2-3c3daa9a963b
caps.latest.revision: 6
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 5c0f4111b758421dd03be3489e7da82d78e8f181
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
---
# <a name="column-size"></a>列大小
数值数据类型的列 （或参数） 大小定义为最多的使用的数据类型的列或参数或数据的精度的位数。 对于字符类型，这是以字符为单位的数据; 的长度对于二进制数据类型，列大小被指以字节为单位的数据的长度。 对于时间、 时间戳，和所有 interval 数据类型，这是此数据的字符表示形式中的字符数。 下表中显示为每种简洁的 SQL 数据类型定义的列大小。  
  
|SQL 类型标识符|列大小|  
|-------------------------|-----------------|  
|所有字符类型 [a]，[b]。|以字符为单位的列或参数 （如 SQL_DESC_LENGTH 描述符字段中包含） 定义或最大列大小。 例如，定义为 char （10） 的单字节字符列的列大小为 10。|  
|SQL_DECIMAL SQL_NUMERIC|定义的数字个数。 例如，定义为 NUMERIC(10,3) 列的精度为 10。|  
|SQL_BIT [c]|1|  
|SQL_TINYINT [c]|3|  
|SQL_SMALLINT [c]|5|  
|SQL_INTEGER [c]|10|  
|SQL_BIGINT [c]|19 （如果有符号） 或 20 （如果无符号）|  
|SQL_REAL [c]|7|  
|SQL_FLOAT [c]|15|  
|SQL_DOUBLE [c]|15|  
|所有二进制类型 [a]，[b]。|定义或最大长度以字节为单位的列或参数。 例如，定义为 binary （10） 的列的长度为 10。|  
|SQL_TYPE_DATE [c]|10 (中的字符数*yyyy-月-日*格式)。|  
|SQL_TYPE_TIME [c]|8 (中的字符数*hh mm ss*格式)，或 9 + *s* (中的字符数*hh: mm:*[.fff...] 格式，其中*的*是秒精度)。|  
|SQL_TYPE_TIMESTAMP|16 (中的字符数*yyyy mm dd hh: mm*格式)<br /><br /> 19 (中的字符数*yyyy-月-日* *hh: mm:* 格式)<br /><br /> 或<br /><br /> 20 + *s* (中的字符数*yyyy mm dd hh: mm:*[.fff...] 格式，其中*s*是秒精度)。|  
|SQL_INTERVAL_SECOND|其中*p*前导精度的时间间隔和*s*是秒精度， *p* (如果*s*= 0) 或*p* + *s*+ 1 (如果*s*> 0)。 [d]|  
|SQL_INTERVAL_DAY_TO_SECOND|其中*p*前导精度的时间间隔和*s*是秒精度 9 +*p* (如果*s*= 0) 或 10 +*p*+ *s* (如果*s*> 0)。 [d]|  
|SQL_INTERVAL_HOUR_TO_SECOND|其中*p*前导精度的时间间隔和*s*是秒精度 6 +*p* (如果*s*= 0) 或 7 +*p* + *s* (如果*s*> 0)。 [d]|  
|SQL_INTERVAL_MINUTE_TO_SECOND|其中*p*前导精度的时间间隔和*s*是秒精度 3 +*p* (如果*s*= 0) 或 4 +*p* + *s* (如果*s*> 0)。 [d]|  
|SQL_INTERVAL_YEAR SQL_INTERVAL_MONTH SQL_INTERVAL_DAY SQL_INTERVAL_HOUR SQL_INTERVAL_MINUTE|*p*，其中*p*前导精度的时间间隔。 [d]|  
|SQL_INTERVAL_YEAR_TO_MONTH SQL_INTERVAL_DAY_TO_HOUR|3 +*p*，其中*p*前导精度的时间间隔。 [d]|  
|SQL_INTERVAL_DAY_TO_MINUTE|6 +*p*，其中*p*前导精度的时间间隔。 [d]|  
|SQL_INTERVAL_HOUR_TO_MINUTE|3 +*p*，其中*p*前导精度的时间间隔。 [d]|  
|SQL_GUID|36 (中的字符数*aaaaaaaa-bbbb-cccc-dddd-eeeeeeeeeeee*格式)|  
  
 [a] 的 ODBC 1.0 应用程序调用**SQLSetParam** ODBC 2.0 的驱动程序，以及 ODBC 2.0 应用程序调用**SQLBindParameter** ODBC 1.0 的驱动程序，当\* *StrLen_or_IndPtr*对于 SQL_LONGVARCHAR 或 SQL_LONGVARBINARY 类型，是 SQL_DATA_AT_EXEC *columnsize 类型*必须设置为数据的总长度以按顺序发送的精度不在此表中定义。  
  
 [b] 如果驱动程序无法确定变量类型的列或参数长度，则返回 SQL_NO_TOTAL。  
  
 [c] *columnsize 类型*参数**SQLBindParameter**对于此数据类型，将忽略。  
  
 [d] 有关 interval 数据类型中的列长度有关的一般规则，请参阅[间隔数据类型长度](../../../odbc/reference/appendixes/interval-data-type-length.md)前面本附录内容。  
  
 为列 （或参数） 的大小返回的值不对应中任何一个的描述符字段的值。 值可以来自 SQL_DESC_PRECISION 或 SQL_DESC_LENGTH 字段，具体取决于类型的数据下, 表中所示。  
  
|SQL 类型|描述符字段对应于<br /><br /> 列或参数的大小|  
|--------------|--------------------------------------------------------------------|  
|所有字符和二进制类型|LENGTH|  
|所有数值类型|PRECISION|  
|所有日期时间和间隔类型|LENGTH|  
|SQL_BIT|LENGTH|
