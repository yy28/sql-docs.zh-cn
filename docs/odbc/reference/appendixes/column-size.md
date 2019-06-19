---
title: 列的大小 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- data types [ODBC], column size
- size of data types [ODBC]
- SQL data types [ODBC], column characteristics
- column size of data types [ODBC]
ms.assetid: 541b83ab-b16d-4714-bcb2-3c3daa9a963b
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 22271cd37069123d0e11a3d0ab660134c61e283b
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/15/2019
ms.locfileid: "63224465"
---
# <a name="column-size"></a>列大小
数值数据类型的列 （或参数） 的大小被指由列或参数的数据类型或数据的精度的最大位数。 对于字符类型，这是以字符为单位的数据; 的长度对于二进制数据类型，列大小被指数据的长度以字节为单位。 对于时间、 时间戳和所有 interval 数据类型，这是此数据的字符表示形式中的字符数。 为每种简洁的 SQL 数据类型定义的列大小是下表中所示。  
  
|SQL 类型标识符|列大小|  
|-------------------------|-----------------|  
|所有字符类型 [a]，[b]。|以字符为单位的列或参数 （如 SQL_DESC_LENGTH 描述符字段中包含） 定义或最大列大小。 例如，定义为 char （10） 的单字节字符列的列大小为 10。|  
|SQL_DECIMAL SQL_NUMERIC|定义的数字位数。 例如，定义为 NUMERIC(10,3) 列的精度为 10。|  
|SQL_BIT[c]|1|  
|SQL_TINYINT[c]|3|  
|SQL_SMALLINT[c]|5|  
|SQL_INTEGER[c]|10|  
|SQL_BIGINT[c]|19 （有符号） 或 20 （如果无符号）|  
|SQL_REAL[c]|7|  
|SQL_FLOAT[c]|15|  
|SQL_DOUBLE[c]|15|  
|所有二进制类型 [a]，[b]。|定义或最大长度以字节为单位的列或参数。 例如，定义为 BINARY(10) 的列的长度为 10。|  
|SQL_TYPE_DATE[c]|10 (中的字符数*年-月-日*格式)。|  
|SQL_TYPE_TIME[c]|8 (中的字符数*hh mm ss*格式)，或 9 + *s* (中的字符数*hh: mm:* [.fff...] 格式，其中*的*秒精度)。|  
|SQL_TYPE_TIMESTAMP|16 (中的字符数*年-月-日 hh: mm*格式)<br /><br /> 19 (中的字符数*年-月-日* *hh: mm:* 格式)<br /><br /> 或<br /><br /> 20 + *s* (中的字符数*年-月-日： 分： 秒*[.fff...] 格式，其中*s*秒精度)。|  
|SQL_INTERVAL_SECOND|其中*p*为间隔起始精度和*s*秒精度*p* (如果*s*= 0) 或*p* + *s*+ 1 (如果*s*> 0)。 [d]|  
|SQL_INTERVAL_DAY_TO_SECOND|其中*p*为间隔起始精度和*s*秒精度 9 +*p* (如果*s*= 0) 或 10 +*p*+ *s* (如果*s*> 0)。 [d]|  
|SQL_INTERVAL_HOUR_TO_SECOND|其中*p*为间隔起始精度和*s*秒精度 6 +*p* (如果*s*= 0) 或 7 +*p* + *s* (如果*s*> 0)。 [d]|  
|SQL_INTERVAL_MINUTE_TO_SECOND|其中*p*为间隔起始精度和*s*秒精度 3 +*p* (如果*s*= 0) 或 4 +*p* + *s* (如果*s*> 0)。 [d]|  
|SQL_INTERVAL_YEAR  SQL_INTERVAL_MONTH SQL_INTERVAL_DAY SQL_INTERVAL_HOUR SQL_INTERVAL_MINUTE|*p*，其中*p*为间隔起始精度。 [d]|  
|SQL_INTERVAL_YEAR_TO_MONTH SQL_INTERVAL_DAY_TO_HOUR|3 +*p*，其中*p*为间隔起始精度。 [d]|  
|SQL_INTERVAL_DAY_TO_MINUTE|6 +*p*，其中*p*为间隔起始精度。 [d]|  
|SQL_INTERVAL_HOUR_TO_MINUTE|3 +*p*，其中*p*为间隔起始精度。 [d]|  
|SQL_GUID|36 (中的字符数*aaaaaaaa-bbbb-cccc-dddd-eeeeeeeeeeee*格式)|  
  
 [a] 为 ODBC 1.0 应用程序调用**SQLSetParam** ODBC 2.0 的驱动程序，在中，对于 ODBC 2.0 应用程序调用**SQLBindParameter**中的 ODBC 1.0 驱动程序，当\* *StrLen_or_IndPtr* SQL_LONGVARCHAR 或 SQL_LONGVARBINARY 类型，是 SQL_DATA_AT_EXEC *ColumnSize*必须设置数据的总长度为要发送的精度不定义此表中。  
  
 [b] 如果驱动程序无法确定变量类型的列或参数长度，它将返回 SQL_NO_TOTAL。  
  
 [c] *ColumnSize*的参数**SQLBindParameter**忽略此数据类型。  
  
 [d] 为单位 interval 数据类型的列长度有关的一般规则，请参阅[间隔数据类型长度](../../../odbc/reference/appendixes/interval-data-type-length.md)本附录前面。  
  
 返回的列 （或参数） 的大小的值不对应任何一个的描述符字段中的值。 值可以来自 SQL_DESC_PRECISION 或 SQL_DESC_LENGTH 字段，具体取决于类型的数据下, 表中所示。  
  
|SQL 类型|相对应的描述符字段<br /><br /> 列或参数大小|  
|--------------|--------------------------------------------------------------------|  
|所有字符和二进制类型|LENGTH|  
|所有数值类型|PRECISION|  
|所有日期时间和间隔类型|LENGTH|  
|SQL_BIT|LENGTH|
