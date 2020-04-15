---
title: 列大小 |微软文档
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 07b6151c723cb5e05189791100338e9e343c28aa
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/14/2020
ms.locfileid: "81306578"
---
# <a name="column-size"></a>列大小
数字数据类型的列（或参数）大小定义为列或参数的数据类型使用的最大位数或数据的精度。 对于字符类型，这是数据的长度;对于二进制数据类型，列大小定义为数据的长度（以字节为单位）。 对于时间、时间戳和所有间隔数据类型，这是此数据字符表示中的字符数。 为每种简洁的 SQL 数据类型定义的列大小显示在下表中。  
  
|SQL 类型标识符|列大小|  
|-------------------------|-----------------|  
|所有字符类型[a]，[b]|以列或参数的字符表示定义的或最大列大小（如SQL_DESC_LENGTH描述符字段中所示）。 例如，定义为 CHAR （10） 的单字节字符列的列大小为 10。|  
|SQL_DECIMALSQL_NUMERIC|定义的位数。 例如，定义为数字（10，3）的列的精度为 10。|  
|SQL_BIT[c]|1|  
|SQL_TINYINT[c]|3|  
|SQL_SMALLINT[c]|5|  
|SQL_INTEGER[c]|10|  
|SQL_BIGINT[c]|19 （如果签名） 或 20 （如果未签名）|  
|SQL_REAL[c]|7|  
|SQL_FLOAT[c]|15|  
|SQL_DOUBLE[c]|15|  
|所有二进制类型[a]，[b]|列或参数的已定义长度或最大长度（以字节为单位）。 例如，定义为 BINARY（10） 的列的长度为 10。|  
|SQL_TYPE_DATE[c]|*10（yyyy-mm-dd*格式的字符数）。|  
|SQL_TYPE_TIME[c]|*8（hh-mm-s 格式*的字符数）或 9 = *s* s（hh：mm：ss [.fff...] 格式的字符数，其中*s*是秒精度）。 *hh:mm:ss*|  
|SQL_TYPE_TIMESTAMP|16 *（yyyy-mm-dd hh：mm*格式的字符数）<br /><br /> 19 *（yyyy-mm-dd* *hh：mm：ss*格式中的字符数）<br /><br /> or<br /><br /> 20+ *s* *（yyyy-mm-dd hh：mm：ss*[.fff...] 格式的字符数，其中*s*是秒精度）。|  
|SQL_INTERVAL_SECOND|*p*是间隔前导精度 *，s*是秒精度 *，p（* 如果*s*=0）或*p*+*s*=1（如果*s*>0）。[d]|  
|SQL_INTERVAL_DAY_TO_SECOND|*p*是间隔前导精度 *，s*是秒精度，9+*p（* 如果*s*=0）或 10°*p*+*s（* 如果*s*>0）。[d]|  
|SQL_INTERVAL_HOUR_TO_SECOND|*p*是间隔前导精度 *，s*是秒精度，6°*p（* 如果*s*=0）或 7°*p*+*s（* 如果*s*>0）。[d]|  
|SQL_INTERVAL_MINUTE_TO_SECOND|*p*是间隔前导精度 *，s*是秒精度，3+*p（* 如果*s*=0）或 4°*p*+*s（* 如果*s*>0）。[d]|  
|SQL_INTERVAL_MONTH SQL_INTERVAL_DAYSQL_INTERVAL_MONTHSQL_INTERVAL_HOURSQL_INTERVAL_MINUTESQL_INTERVAL_YEAR|*p*，其中*p*是间隔前导精度。[d]|  
|SQL_INTERVAL_YEAR_TO_MONTHSQL_INTERVAL_DAY_TO_HOUR|3+*p*，其中*p*是间隔前导精度。[d]|  
|SQL_INTERVAL_DAY_TO_MINUTE|6+*p*，其中*p*是间隔前导精度。[d]|  
|SQL_INTERVAL_HOUR_TO_MINUTE|3+*p*，其中*p*是间隔前导精度。[d]|  
|SQL_GUID|36 *（aaaaaaa-bbbb-cccc-ddd-eeeeeeeeeee*格式的字符数）|  
  
 [a] 对于在 ODBC 2.0 驱动程序中调用**SQLSetParam**的 ODBC 1.0 应用程序，对于在 ODBC 1.0 驱动程序中调用**SQLBind参数**的 ODBC 2.0 应用程序，当\**StrLen_or_IndPtrSQL_LONGVARCHAR*或SQL_LONGVARBINARY类型SQL_DATA_AT_EXEC时，列*Size*必须设置为要发送的数据的总长度，而不是本表中定义的精度。  
  
 [b] 如果驱动程序无法确定变量类型的列或参数长度，则返回SQL_NO_TOTAL。  
  
 [c] 此数据类型将忽略**SQLBind 参数**的*列大小*参数。  
  
 [d] 有关间隔数据类型中的列长度的一般规则，请参阅本附录前面段[的间隔数据类型长度](../../../odbc/reference/appendixes/interval-data-type-length.md)。  
  
 为列（或参数）大小返回的值与任何一个描述符字段中的值不对应。 这些值可以来自SQL_DESC_PRECISION或SQL_DESC_LENGTH字段，具体取决于数据类型，如下表所示。  
  
|SQL 类型|与<br /><br /> 列或参数大小|  
|--------------|--------------------------------------------------------------------|  
|所有字符和二进制类型|LENGTH|  
|所有数值类型|PRECISION|  
|所有日期时间和间隔类型|LENGTH|  
|SQL_BIT|LENGTH|
