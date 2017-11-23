---
title: "SQL 数据类型 |Microsoft 文档"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: reference
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- SQL data types [ODBC]
- SQL data types [ODBC], about SQL data types
- data types [ODBC], SQL data types
ms.assetid: 1b22f985-f5e4-4779-87eb-e43329a442b1
caps.latest.revision: "7"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: On Demand
ms.openlocfilehash: 1b5ebc2779d005a31f9b93a1cf6ca8fb6e35b346
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/20/2017
---
# <a name="sql-data-types"></a>SQL 数据类型
每个 DBMS 定义其自己的 SQL 类型。 每个 ODBC 驱动程序公开仅关联的 DBMS 定义这些 SQL 数据类型。 有关如何将驱动程序映射信息 DBMS SQL 类型到 ODBC 定义的 SQL 类型标识符和驱动程序将 DBMS SQL 类型映射到其自己的特定于驱动程序的 SQL 类型标识符如何通过调用返回**SQLGetTypeInfo**。 驱动程序也会返回 SQL 数据类型变为描述列和通过对的调用的参数的数据类型时**SQLColAttribute**， **SQLColumns**， **SQLDescribeCol**，**SQLDescribeParam**， **SQLProcedureColumns**，和**SQLSpecialColumns**。  
  
> [!NOTE]  
>  SQL 数据类型包含在实现描述符的 SQL_DESC_ CONCISE_TYPE、 SQL_DESC_TYPE 和 SQL_DESC_DATETIME_INTERVAL_CODE 字段中。 实现描述符的 SQL_DESC_PRECISION、 SQL_DESC_SCALE、 SQL_DESC_LENGTH 和 SQL_DESC_OCTET_LENGTH 字段中包含的 SQL 数据类型的特征。 有关详细信息，请参阅[数据类型标识符和描述符](../../../odbc/reference/appendixes/data-type-identifiers-and-descriptors.md)本附录内容更高版本。  
  
 给定的驱动程序和数据源不一定支持在此附录中定义的所有 SQL 数据类型。 SQL 数据类型的驱动程序的支持取决于与相兼容的驱动程序的 SQL 92 的级别。 若要确定驱动程序支持的 SQL 92 语法的级别，应用程序调用**SQLGetInfo** SQL_SQL_CONFORMANCE 信息类型。 此外，给定的驱动程序和数据源可能支持其他、 特定于驱动程序的 SQL 数据类型。 要确定哪些数据类型的驱动程序支持，应用程序调用**SQLGetTypeInfo**。 有关特定于驱动程序的 SQL 数据类型的信息，请参阅驱动程序的文档。 有关特定数据源中的数据类型的信息，请参阅该数据源的文档。  
  
> [!IMPORTANT]  
>  在此附录整个表是唯一的准则和通常使用的显示名称、 范围和 SQL 数据类型的限制。 给定的数据源可能支持只有某些列出的数据类型，以及支持的数据类型的特征可以与所列出的那些。  
  
 下表列出所有 SQL 数据类型的有效 SQL 类型的标识符。 表还列出的名称和说明的 SQL 92 从相应的数据类型 （如果存在）。  
  
|SQL 类型标识符 [1]|典型的 SQL 数据<br /><br /> 类型 [2]|典型的类型说明|  
|------------------------------|------------------------------------|------------------------------|  
|SQL_CHAR|CHAR (*n*)|字符的固定的字符串长度的字符串 *n* 。|  
|SQL_VARCHAR|VARCHAR (*n*)|最大字符串长度的可变长度字符串 *n* 。|  
|SQL_LONGVARCHAR|LONG VARCHAR|可变长度的字符数据。 最大长度为数据源而定。[9]|  
|SQL_WCHAR|WCHAR (*n*)|Unicode 字符的固定的字符串长度的字符串*n*|  
|SQL_WVARCHAR|VARWCHAR (*n*)|Unicode 可变长度字符串，最大字符串长度*n*|  
|SQL_WLONGVARCHAR|LONGWVARCHAR|Unicode 长度可变的字符数据。 最大长度是数据源而定|  
|SQL_DECIMAL|十进制 (*p*，*s*)|已签名，精确数值的值的精度至少*p*和小数位数*s。* （最大精度是驱动程序定义的。）(1 < = *p* < = 15;*s* <= *p*)。 [4]|  
|SQL_NUMERIC|数字 (*p*，*s*)|有符号的确切数字，其精度*p*和小数位数*s* (1 < = *p* < = 15;*s* <= *p*)。 [4]|  
|SQL_SMALLINT|SMALLINT|确切数字值，该值精度为 5，小数位数为 0 (签名:-32768 < =  *n*  < = 32,767，未签名： 0 < =  *n*  < = 65535) [3]。|  
_INTEGER|整数|确切数字值，该值精度为 10，小数位数为 0 (签名:-2 [31] < =  *n*  < = 2 [31] – 1，未签名： 0 < =  *n*  < = 2 [32] – 1) [3]。|  
|SQL_REAL|REAL|已签名，其二进制精度为 24 的近似的数字值 （0 或绝对值 10 [–38] 到 10[38])。|  
|SQL_FLOAT|FLOAT (*p*)|有符号，近似数值二进制精度为至少*p*。 （最大精度是驱动程序定义的。）[5]|  
|SQL_DOUBLE|DOUBLE PRECISION|有符号的近似数值，其二进制精度 53 （零或绝对值 10 [–308] 到 10[308])。|  
|SQL_BIT|BIT|一个位的二进制数据。[8]|  
|SQL_TINYINT|TINYINT|确切其精度为 3 的数字值，小数位数为 0 (签名: – 128 < =  *n*  < = 127，未签名： 0 < =  *n*  < = 255) [3]。|  
_BIGINT|bigint|确切数字值，该值精度为 19 （如果有符号） 或 20 （如果无符号），小数位数为 0 (签名:-2 [63] < =  *n*  < = 2 [63] – 1，未签名： 0 < =  *n*  < = 2 [64] – 1) [3] [9]。|  
|SQL_BINARY|二进制 (*n*)|固定长度的二进制数据 *n* 。 [9]|  
|SQL_VARBINARY|VARBINARY (*n*)|可变长度的最大长度的二进制数据 *n* 。 用户设置的最大。[9]|  
|SQL_LONGVARBINARY|长 VARBINARY|可变长度的二进制数据。 最大长度为数据源而定。[9]|  
|SQL_TYPE_DATE [6]|DATE|年、 月和天字段，符合规则的公历。 (请参阅[约束的公历](../../../odbc/reference/appendixes/constraints-of-the-gregorian-calendar.md)、 本附录内容更高版本。)|  
|SQL_TYPE_TIME [6]|时间 (*p*)|小时、 分钟和具有有效的值为小时的 00 到 23 有效的值为 00 到 59 分钟和秒 00 到 61 的有效值的第二个字段。 精度*p*指示秒精度。|  
|SQL_TYPE_TIMESTAMP [6]|时间戳 (*p*)|年、 月、 日、 小时、 分钟、 和第二个字段，用日期和时间数据类型定义的有效值。|  
_TYPE_UTCDATETIME|UTCDATETIME|年、 月、 日、 小时、 分钟、 秒、 utchour 和 utcminute 字段。 Utchour 和 utcminute 字段具有 1/10 微秒精度。|  
|SQL_TYPE_UTCTIME|UTCTIME|小时、 分钟、 秒、 utchour 和 utcminute 字段。 Utchour 和 utcminute 字段具有 1/10 微秒精度...|  
|SQL_INTERVAL_MONTH [7]|INTERVAL MONTH (*p*)|两个日期; 间隔的月数*p*前导精度的时间间隔。|  
|SQL_INTERVAL_YEAR [7]|INTERVAL YEAR (*p*)|两个日期; 之间的年数*p*前导精度的时间间隔。|  
|SQL_INTERVAL_YEAR_TO_MONTH [7]|INTERVAL YEAR (*p*) 到月份|年和两个日期; 之间的月数*p*前导精度的时间间隔。|  
|SQL_INTERVAL_DAY [7]|INTERVAL DAY (*p*)|两个日期; 之间的天数*p*前导精度的时间间隔。|  
|SQL_INTERVAL_HOUR [7]|INTERVAL HOUR (*p*)|两个之间的小时数日期/时间;*p*前导精度的时间间隔。|  
|SQL_INTERVAL_MINUTE [7]|间隔分钟 (*p*)|两个之间的分钟数日期/时间;*p*前导精度的时间间隔。|  
|SQL_INTERVAL_SECOND [7]|间隔第二个 (*p*，*q*)|两个之间的秒数日期/时间;*p*前导精度的时间间隔和*q*的间隔秒精度。|  
_INTERVAL_DAY_TO_HOUR [7]|INTERVAL DAY (*p*) 到小时|天/之间的小时数两个日期/时间;*p*前导精度的时间间隔。|  
|SQL_INTERVAL_DAY_TO_MINUTE [7]|INTERVAL DAY (*p*) 为分钟|天数/小时/之间的分钟数两个日期/时间;*p*前导精度的时间间隔。|  
|SQL_INTERVAL_DAY_TO_SECOND [7]|INTERVAL DAY (*p*) 到第二个 (*q*)|天数/小时/分钟数/秒数之间两个日期/时间;*p*前导精度的时间间隔和*q*的间隔秒精度。|  
|SQL_INTERVAL_HOUR_TO_MINUTE [7]|INTERVAL HOUR (*p*) 为分钟|小时/之间的分钟数两个日期/时间;*p*前导精度的时间间隔。|  
|SQL_INTERVAL_HOUR_TO_SECOND [7]|INTERVAL HOUR (*p*) 到第二个 (*q*)|小时数/分钟数/秒数之间两个日期/时间;*p*前导精度的时间间隔和*q*的间隔秒精度。|  
_INTERVAL_MINUTE_TO_SECOND [7]|间隔分钟 (*p*) 到第二个 (*q*)|分钟数/秒数之间两个日期/时间;*p*前导精度的时间间隔和*q*的间隔秒精度。|  
|SQL_GUID|GUID|固定的长度 GUID。|  
  
 [1] 这是通过调用 DATA_TYPE 列中返回的值**SQLGetTypeInfo**。  
  
 [2] 这是通过调用返回到名称以及创建参数列中的值**SQLGetTypeInfo**。 名称列返回的设定 — 例如，CHAR — 而创建 PARAMS 列返回如精度、 小数位数和长度的创建参数的以逗号分隔列表。  
  
 [3] 应用程序使用**SQLGetTypeInfo**或**SQLColAttribute**若要确定特定的数据类型或结果集中的特定列是否为无符号。  
  
 [4] SQL_DECIMAL 和 SQL_NUMERIC 数据类型的区别只在于其精度。 某小数的精度 (*p*，*s*) 是实现定义的小数精度小于*p*，而数字精度 (*p*，*s*) 完全等于*p*。  
  
 [5] 具体取决于实现，SQL_FLOAT 的精度可以为 24 或 53： 如果它为 24，SQL_FLOAT 数据类型等同于 SQL_REAL;如果它是 53，SQL_FLOAT 数据类型是 SQL_DOUBLE 相同。  
  
 [6] ODBC 3 中*.x*，SQL 日期、 时间和时间戳数据类型是 SQL_TYPE_DATE、 SQL_TYPE_TIME 和 SQL_TYPE_TIMESTAMP，分别; 在 ODBC 2。*x*，数据类型是 SQL_DATE、 SQL_TIME 和 SQL_TIMESTAMP。  
  
 [7] 有关间隔 SQL 数据类型的详细信息，请参阅[Interval 数据类型](../../../odbc/reference/appendixes/interval-data-types.md)本附录后面的部分。  
  
 [8] SQL_BIT 数据类型在 SQL 92 中有特征与位类型不同。  
  
 [9] 此数据类型在 SQL 92 中有相应的数据类型。  
  
 本部分提供下面的示例。  
  
-   [示例 SQLGetTypeInfo 结果集](../../../odbc/reference/appendixes/example-sqlgettypeinfo-result-set.md)
