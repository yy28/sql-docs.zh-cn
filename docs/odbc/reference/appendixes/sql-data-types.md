---
title: SQL 数据类型 |微软文档
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQL data types [ODBC]
- SQL data types [ODBC], about SQL data types
- data types [ODBC], SQL data types
ms.assetid: 1b22f985-f5e4-4779-87eb-e43329a442b1
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 3cc91213533aa39f30be1bc838cc014c20e70884
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/14/2020
ms.locfileid: "81305001"
---
# <a name="sql-data-types"></a>SQL 数据类型
每个 DBMS 定义其自己的 SQL 类型。 每个 ODBC 驱动程序仅公开关联的 DBMS 定义的 SQL 数据类型。 有关驱动程序如何将 DBMS SQL 类型映射到 ODBC 定义的 SQL 类型标识符以及驱动程序如何将 DBMS SQL 类型映射到其自己的特定于驱动程序的 SQL 类型标识符的信息将通过调用**SQLGetTypeInfo**返回。 当通过调用 SQLColattribute、SQLColumns、SQLDescribeCol、SQLDescribeParam、SQL**SQLColAttribute****程序列**和**SQLColumns****SQL 特殊列**来描述列和**SQLDescribeParam**参数的数据类型时，驱动程序也会返回 SQL 数据类型。 **SQLDescribeCol**  
  
> [!NOTE]  
>  SQL 数据类型包含在实现描述符SQL_DESC_CONCISE_TYPE、SQL_DESC_TYPE和SQL_DESC_DATETIME_INTERVAL_CODE字段中。 SQL 数据类型的特征包含在实现描述符的SQL_DESC_PRECISION、SQL_DESC_SCALE、SQL_DESC_LENGTH和SQL_DESC_OCTET_LENGTH字段中。 有关详细信息，请参阅本附录后面的[数据类型标识符和描述符](../../../odbc/reference/appendixes/data-type-identifiers-and-descriptors.md)。  
  
 给定的驱动程序和数据源不一定支持本附录中定义的所有 SQL 数据类型。 驱动程序对 SQL 数据类型的支持取决于驱动程序符合的 SQL-92 级别。 要确定驱动程序支持的 SQL-92 语法级别，应用程序使用SQL_SQL_CONFORMANCE信息类型调用**SQLGetInfo。** 此外，给定的驱动程序和数据源可能支持其他特定于驱动程序的 SQL 数据类型。 要确定驱动程序支持哪些数据类型，应用程序将调用**SQLGetTypeInfo**。 有关特定于驱动程序的 SQL 数据类型的信息，请参阅驱动程序的文档。 有关特定数据源中的数据类型的信息，请参阅该数据源的文档。  
  
> [!IMPORTANT]  
>  本附录中的表只是指南，显示 SQL 数据类型的常用名称、范围和限制。 给定的数据源可能仅支持某些列出的数据类型，并且支持的数据类型的特征可能与列出的数据类型不同。  
  
 下表列出了所有 SQL 数据类型的有效 SQL 类型标识符。 该表还列出了 SQL-92 中相应数据类型的名称和说明（如果存在）。  
  
|SQL 类型标识符 {1}|典型的 SQL 数据<br /><br /> 类型[2]|典型类型描述|  
|------------------------------|------------------------------------|------------------------------|  
|SQL_CHAR|CHAR（*n*）|固定字符串长度 n*的*字符串。|  
|SQL_VARCHAR|瓦尔查尔 （*n*）|具有最大字符串长度*n 的*可变长度字符串。|  
|SQL_LONGVARCHAR|LONG VARCHAR|变长字符数据。 最大长度与数据源相关。[9]|  
|SQL_WCHAR|WCHAR（*n*）|固定字符串长度*n*的单码字符串|  
|SQL_WVARCHAR|瓦尔瓦查尔 （*n*）|具有最大字符串长度*n*的 Unicode 可变长度字符串|  
|SQL_WLONGVARCHAR|朗瓦查尔|Unicode 变长字符数据。 最大长度取决于数据源|  
|SQL_DECIMAL|DECIMAL（*p*，*s*）|签名、精确、数值，精度至少为*p*和刻度*s。* （最大精度为驱动程序定义。（1 <= *p* <= 15;*s* <= *p*。[4]|  
|SQL_NUMERIC|数字 *（p*，*s*）|带精确*p*和刻度*s*的符号、精确、数值（1 <= *p* <= 15;*s* <= *p*。[4]|  
|SQL_SMALLINT|SMALLINT|精度为 5 和刻度 0 的精确数值（签名： -32，768 <= *n* <= 32，767，未签名：0 <= *n* <= 65，535）[3]。|  
|SQL_INTEGER|INTEGER|精度为 10 和刻度 0 的精确数值（签名： -2[31] <= *n* <= 2[31] - 1，未签名：0 <= *n* <= 2[32] - 1）[3]。|  
|SQL_REAL|real|具有二进制精度 24（零或绝对值 10[-38] 到 10[38]）的符号、近似数值。|  
|SQL_FLOAT|浮动（*p*）|签名的、近似的数值，二进制精度至少为*p*。 （最大精度为驱动程序定义。[5]|  
|SQL_DOUBLE|DOUBLE PRECISION|签名、近似、数值，二进制精度 53（零或绝对值 10[-308] 到 10[308]）。|  
|SQL_BIT|BIT|单位二进制数据。[8]|  
|SQL_TINYINT|TINYINT|精度为 3 和刻度 0 的精确数值（签名： -128 <= *n* <= 127，无符号：0 <= *n* <= 255）[3]。|  
|SQL_BIGINT|BIGINT|精度为 19（如果已签名）或 20（如果未签名）和刻度 0（签名：-2[63] <= *n* <= 2[63] - 1，未签名：0 <= *n* <= 2[64] - 1）[3]，[9]。|  
|SQL_BINARY|BINARY（*n*）|固定长度 n*的*二进制数据。[9]|  
|SQL_VARBINARY|瓦尔里数（*n*）|最大长度*n*的可变长度二进制数据。 最大值由用户设置。[9]|  
|SQL_LONGVARBINARY|长瓦二进制|变长二进制数据。 最大长度与数据源相关。[9]|  
|SQL_TYPE_DATE[6]|DATE|年、月和日字段，符合公历的规则。 （请参阅[公历的约束](../../../odbc/reference/appendixes/constraints-of-the-gregorian-calendar.md)，本附录后面的内容。|  
|SQL_TYPE_TIME[6]|时间（*p*）|小时、分钟和第二个字段（有效值为小时为 00 到 23）、分钟为 00 到 59 的有效值以及秒数为 00 到 61 的有效值。 精度*p*表示秒精度。|  
|SQL_TYPE_TIMESTAMP[6]|时间戳（*p*）|年份、月份、日、小时、分钟和第二个字段，为 DATE 和 TIME 数据类型定义有效值。|  
|SQL_TYPE_UTCDATETIME|UTCDATETIME|年、月、日、小时、分钟、秒、utchour 和 utc 分钟字段。 utchour 和 utc 分钟字段具有 1/10 微秒精度。|  
|SQL_TYPE_UTCTIME|UTC时间|小时、分钟、秒、utchour 和 utc 分钟字段。 utchour 和 utc 分钟字段具有 1/10 微秒精度。|  
|SQL_INTERVAL_MONTH[7]|间隔月（*p*）|两个日期之间的月数;*p*是间隔前导精度。|  
|SQL_INTERVAL_YEAR[7]|间隔年（*p*）|两个日期之间的年数;*p*是间隔前导精度。|  
|SQL_INTERVAL_YEAR_TO_MONTH[7]|间隔年（*p*） 到月|两个日期之间的年数和月数;*p*是间隔前导精度。|  
|SQL_INTERVAL_DAY[7]|间隔日（*p*）|两个日期之间的天数;*p*是间隔前导精度。|  
|SQL_INTERVAL_HOUR[7]|间隔小时（*p*）|两个日期/时间之间的小时数;*p*是间隔前导精度。|  
|SQL_INTERVAL_MINUTE[7]|间隔分钟（*p*）|两个日期/时间之间的分钟数;*p*是间隔前导精度。|  
|SQL_INTERVAL_SECOND[7]|间隔秒（*p*，*q*）|两个日期/时间之间的秒数;*p*是间隔前导精度 *，q*是间隔秒精度。|  
|SQL_INTERVAL_DAY_TO_HOUR[7]|间隔日（*p*） 到 HOUR|两个日期/时间之间的天数/小时数;*p*是间隔前导精度。|  
|SQL_INTERVAL_DAY_TO_MINUTE[7]|间隔日（*p*） 到 分钟|两个日期/时间之间的天数/小时/分钟数;*p*是间隔前导精度。|  
|SQL_INTERVAL_DAY_TO_SECOND[7]|间隔日（*p*） 到 秒 （*q*）|两个日期/时间之间的天数/小时/分钟/秒数;*p*是间隔前导精度 *，q*是间隔秒精度。|  
|SQL_INTERVAL_HOUR_TO_MINUTE[7]|间隔小时（*p*） 到 分钟|两个日期/时间之间的小时/分钟数;*p*是间隔前导精度。|  
|SQL_INTERVAL_HOUR_TO_SECOND[7]|间隔小时（*p*） 到 秒 （*q*）|两个日期/时间之间的小时/分钟/秒数;*p*是间隔前导精度 *，q*是间隔秒精度。|  
|SQL_INTERVAL_MINUTE_TO_SECOND[7]|间隔分钟（*p*） 到 秒 （*q*）|两个日期/时间之间的分钟/秒数;*p*是间隔前导精度 *，q*是间隔秒精度。|  
|SQL_GUID|GUID|固定长度 GUID。|  
  
 {1} 这是调用**SQLGetTypeInfo**在DATA_TYPE列中返回的值。  
  
 [2] 这是通过调用**SQLGetTypeInfo**在 NAME 和 CREATE PARAMS 列中返回的值。 NAME 列返回指定（例如，CHAR-而 CREATE PARAMS 列返回创建参数（如精度、比例和长度）的逗号分隔列表。  
  
 [3] 应用程序使用**SQLGetTypeInfo**或**SQLColAttribute**来确定结果集中的特定数据类型或特定列是否未签名。  
  
 [4] SQL_DECIMAL和SQL_NUMERIC数据类型的精度仅不同。 *DECIMAL（p**，s*） 的精度是实现定义的十进制精度，不低于*p，* 而*NUMERIC（p**）* 的精度完全等于*p*。  
  
 [5] 根据实现情况，SQL_FLOAT的精度可以是 24 或 53：如果是 24，则SQL_FLOAT数据类型与SQL_REAL相同;如果是 53，则SQL_FLOAT数据类型与SQL_DOUBLE相同。  
  
 [6] 在 ODBC *3.x*中，SQL 日期、时间和时间戳数据类型分别为SQL_TYPE_DATE、SQL_TYPE_TIME和SQL_TYPE_TIMESTAMP;在 ODBC *2.x*中，数据类型为SQL_DATE、SQL_TIME和SQL_TIMESTAMP。  
  
 [7] 有关间隔 SQL 数据类型的详细信息，请参阅本附录后面的[间隔数据类型](../../../odbc/reference/appendixes/interval-data-types.md)部分。  
  
 [8] SQL_BIT数据类型与 SQL-92 中的 BIT 类型具有不同的特征。  
  
 [9] 此数据类型在 SQL-92 中没有相应的数据类型。  
  
 本节提供以下示例。  
  
-   [示例 SQLGetTypeInfo 结果集](../../../odbc/reference/appendixes/example-sqlgettypeinfo-result-set.md)
