---
title: SQL 数据类型 |Microsoft Docs
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 623ac38791eebc6db84380dfadd499651af938af
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63280915"
---
# <a name="sql-data-types"></a>SQL 数据类型
每个 DBMS 定义其自己的 SQL 类型。 每个 ODBC 驱动程序公开只有关联的 DBMS 定义这些 SQL 数据类型。 DBMS SQL 类型信息驱动程序的将映射到 ODBC 定义的 SQL 类型标识符和驱动程序将 DBMS SQL 类型映射到其自己特定于驱动程序的 SQL 类型标识符的方式通过调用返回**SQLGetTypeInfo**。 驱动程序还返回 SQL 数据类型时描述数据类型的列和参数通过调用**SQLColAttribute**， **SQLColumns**， **SQLDescribeCol**，**SQLDescribeParam**， **SQLProcedureColumns**，并**SQLSpecialColumns**。  
  
> [!NOTE]  
>  实现描述符的 SQL_DESC_ CONCISE_TYPE、 的 SQL_DESC_TYPE、 和 SQL_DESC_DATETIME_INTERVAL_CODE 字段中包含 SQL 数据类型。 SQL 数据类型的特征包含在实现描述符的 SQL_DESC_PRECISION、 SQL_DESC_SCALE、 SQL_DESC_LENGTH 和的 SQL_DESC_OCTET_LENGTH 字段中。 有关详细信息，请参阅[数据类型标识符和描述符](../../../odbc/reference/appendixes/data-type-identifiers-and-descriptors.md)本附录中更高版本。  
  
 给定驱动程序和数据源不一定支持本附录中定义的所有 SQL 数据类型。 驱动程序的支持的 SQL 数据类型取决于驱动程序符合 SQL-92 的级别。 若要确定驱动程序支持的 SQL-92 语法级别，应用程序调用**SQLGetInfo** SQL_SQL_CONFORMANCE 信息类型。 此外，给定的驱动程序和数据源可能支持其他、 特定于驱动程序的 SQL 数据类型。 若要确定哪些数据类型的驱动程序支持，应用程序调用**SQLGetTypeInfo**。 有关特定于驱动程序的 SQL 数据类型的信息，请参阅驱动程序的文档。 有关特定数据源中的数据类型的信息，请参阅该数据源的文档。  
  
> [!IMPORTANT]  
>  在本附录整个表是唯一的指导原则和通常使用的显示名称、 范围和 SQL 数据类型的限制。 给定的数据源可能支持只有一部分列出的数据类型，并且支持的数据类型的特征可以不同于列出的内容。  
  
 下表列出了所有 SQL 数据类型的有效 SQL 类型标识符。 该表还列出的名称和 SQL-92 从相应的数据类型的说明 （如果存在）。  
  
|SQL type identifier[1]|典型的 SQL 数据<br /><br /> type[2]|典型的类型说明|  
|------------------------------|------------------------------------|------------------------------|  
|SQL_CHAR|CHAR(*n*)|字符固定的长度的字符串*n*。|  
|SQL_VARCHAR|VARCHAR(*n*)|最大字符串长度的可变长度字符串*n*。|  
|SQL_LONGVARCHAR|LONG VARCHAR|变长字符数据。 最大长度因数据源决定。[9]|  
|SQL_WCHAR|WCHAR(*n*)|固定的长度的 Unicode 字符串*n*|  
|SQL_WVARCHAR|VARWCHAR(*n*)|Unicode 变长字符串，最大字符串长度*n*|  
|SQL_WLONGVARCHAR|LONGWVARCHAR|Unicode 变长字符数据。 最大长度是由数据源决定|  
|SQL_DECIMAL|DECIMAL(*p*,*s*)|有符号的精确数值的精度至少*p*和规模*s。* （最大精度是驱动程序定义的。）(1 < = *p* < = 15;*s* <= *p*)。 [4]|  
|SQL_NUMERIC|NUMERIC(*p*,*s*)|有符号的精确数值，其精度*p*和规模*s* (1 < = *p* < = 15;*s* <= *p*)。 [4]|  
|SQL_SMALLINT|SMALLINT|精确数值精度为 5，小数位数为 0 (签名:-32,768 < = *n* < = 32767，无符号：0 < = *n* < = 65535) [3]。|  
|SQL_INTEGER|整数|精确数值精度为 10 和小数位数为 0 (签名:-2 [31] < = *n* < = 2 [31]-1，无符号：0 < = *n* < = 2 [32]-1) [3]。|  
|SQL_REAL|real|有符号的近似数值，其二进制精度为 24 （零或绝对值为 10 [-38] 到 10[38])。|  
|SQL_FLOAT|FLOAT(*p*)|有符号的近似数值二进制精度为至少*p*。 （最大精度是驱动程序定义的。）[5]|  
|SQL_DOUBLE|DOUBLE PRECISION|有符号的近似数值，其二进制精度为 53 （零或绝对值为 10 [-308] 到 10[308])。|  
|SQL_BIT|BIT|位的二进制数据。[8]|  
|SQL_TINYINT|TINYINT|精确数值精度为 3 和小数位数为 0 (签名:-128 < = *n* < = 127，无符号：0 < = *n* < = 255) [3]。|  
|SQL_BIGINT|bigint|精确数值，其精度为 19 （有符号） 或 20 （如果无符号） 和小数位数为 0 (签名:-2 [63] < = *n* < = 2 [63]-1，无符号：0 < = *n* < = 2 [64]-1) [3] [9]。|  
|SQL_BINARY|BINARY(*n*)|固定长度的二进制数据*n*。 [9]|  
|SQL_VARBINARY|VARBINARY(*n*)|可变长度二进制数据的最大长度*n*。 用户设置的最大。[9]|  
|SQL_LONGVARBINARY|长 VARBINARY|可变长度二进制数据。 最大长度因数据源决定。[9]|  
|SQL_TYPE_DATE[6]|DATE|年、 月和天字段，符合公历的规则。 (请参阅[公历的约束](../../../odbc/reference/appendixes/constraints-of-the-gregorian-calendar.md)、 本附录中更高版本。)|  
|SQL_TYPE_TIME[6]|TIME(*p*)|小时、 分钟和具有有效的值为 00 到 23，有效的值的小时为 00 到 59 的分钟数和有效的值为 00 到 61 秒的第二个字段。 精度*p*指示的秒精度。|  
|SQL_TYPE_TIMESTAMP[6]|TIMESTAMP(*p*)|年、 月、 日、 小时、 分钟和第二个字段，使用有效的日期和时间数据类型定义的值。|  
|SQL_TYPE_UTCDATETIME|UTCDATETIME|年、 月、 日、 小时、 分钟、 秒、 utchour 和 utcminute 字段。 Utchour 和 utcminute 字段具有 1/10 微秒精度。|  
|SQL_TYPE_UTCTIME|UTCTIME|小时、 分钟、 秒、 utchour 和 utcminute 字段。 Utchour 和 utcminute 字段具有 1/10 微秒精度...|  
|SQL_INTERVAL_MONTH[7]|间隔月 (*p*)|两个日期; 之间的月数*p*为间隔起始精度。|  
|SQL_INTERVAL_YEAR[7]|INTERVAL YEAR(*p*)|两个日期; 之间的年数*p*为间隔起始精度。|  
|SQL_INTERVAL_YEAR_TO_MONTH[7]|间隔年 (*p*) 给月份|年和两个日期; 之间的月数*p*为间隔起始精度。|  
|SQL_INTERVAL_DAY[7]|INTERVAL DAY(*p*)|两个日期; 之间的天数*p*为间隔起始精度。|  
|SQL_INTERVAL_HOUR[7]|间隔小时 (*p*)|两个之间的小时数日期/时间;*p*为间隔起始精度。|  
|SQL_INTERVAL_MINUTE[7]|间隔分钟 (*p*)|两个之间的分钟数日期/时间;*p*为间隔起始精度。|  
|SQL_INTERVAL_SECOND[7]|INTERVAL SECOND(*p*,*q*)|两个之间的秒数日期/时间;*p*为间隔起始精度和*q*是时间间隔的秒精度。|  
|SQL_INTERVAL_DAY_TO_HOUR[7]|INTERVAL DAY(*p*) TO HOUR|天/之间的小时数两个日期/时间;*p*为间隔起始精度。|  
|SQL_INTERVAL_DAY_TO_MINUTE[7]|INTERVAL DAY(*p*) TO MINUTE|天/小时/之间的分钟数两个日期/时间;*p*为间隔起始精度。|  
|SQL_INTERVAL_DAY_TO_SECOND[7]|INTERVAL DAY(*p*) TO SECOND(*q*)|天/小时/分钟/之间的秒数两个日期/时间;*p*为间隔起始精度和*q*是时间间隔的秒精度。|  
|SQL_INTERVAL_HOUR_TO_MINUTE[7]|间隔小时 (*p*) 为分钟|小时/之间的分钟数两个日期/时间;*p*为间隔起始精度。|  
|SQL_INTERVAL_HOUR_TO_SECOND[7]|INTERVAL HOUR(*p*) TO SECOND(*q*)|小时/分钟/之间的秒数两个日期/时间;*p*为间隔起始精度和*q*是时间间隔的秒精度。|  
|SQL_INTERVAL_MINUTE_TO_SECOND[7]|间隔分钟 (*p*) 到第二个 (*q*)|分钟/之间的秒数两个日期/时间;*p*为间隔起始精度和*q*是时间间隔的秒精度。|  
|SQL_GUID|GUID|固定的长度的 GUID。|  
  
 [1] 这是通过调用在 DATA_TYPE 列中返回的值**SQLGetTypeInfo**。  
  
 [2] 这是通过调用返回的名称以及创建参数列中的值**SQLGetTypeInfo**。 名称列将返回指定-例如，CHAR-而创建 PARAMS 列将返回一列以逗号分隔的创建参数，例如精度、 小数位数和长度。  
  
 [3] 应用程序使用**SQLGetTypeInfo**或**SQLColAttribute**以确定特定的数据类型或结果集中的特定列是否为无符号。  
  
 [4] SQL_DECIMAL 和 SQL_NUMERIC 数据类型的区别只在于其精度。 某小数的精度 (*p*，*s*) 是实现定义的小数精度小于*p*，而数字的精度 (*p*，*s*) 完全相等*p*。  
  
 [5] 具体取决于实现的 SQL_FLOAT 精度可以为 24 或 53： 如果它为 24，SQL_FLOAT 数据类型是 SQL_REAL; 相同如果它是 53，SQL_FLOAT 数据类型是 SQL_DOUBLE 相同。  
  
 [6] 在 ODBC 3 *.x*，SQL 日期、 时间和时间戳数据类型为 SQL_TYPE_DATE、 SQL_TYPE_TIME 和 SQL_TYPE_TIMESTAMP，ODBC 2 中分别;。*x*，数据类型为 SQL_DATE、 SQL_TIME 和 SQL_TIMESTAMP。  
  
 [7] 的间隔 SQL 数据类型的详细信息，请参阅[Interval 数据类型](../../../odbc/reference/appendixes/interval-data-types.md)部分中的，稍后在本附录中。  
  
 [8] SQL_BIT 数据类型具有不同特征的位类型与 SQL-92 中。  
  
 [9] 此数据类型具有 SQL-92 中没有相应的数据类型。  
  
 本部分提供下面的示例。  
  
-   [示例 SQLGetTypeInfo 结果集](../../../odbc/reference/appendixes/example-sqlgettypeinfo-result-set.md)
