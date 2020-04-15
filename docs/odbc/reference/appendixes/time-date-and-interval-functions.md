---
title: 时间、日期和间隔函数 |微软文档
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- functions [ODBC], time functions
- functions [ODBC], date functions
- interval functions [ODBC]
- functions [ODBC], interval functions
- time functions [ODBC]
- date functions [ODBC]
ms.assetid: bdf054a0-7aba-4e99-a34a-799917376fd5
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: aec3d6b23383edcc9659ff884e8cd71b0595dae1
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/14/2020
ms.locfileid: "81302818"
---
# <a name="time-date-and-interval-functions"></a>时间、日期和时间间隔函数
下表列出了 ODBC 标量函数集中包括的时间和日期函数。 应用程序可以通过使用SQL_TIMEDATE_FUNCTIONS*的信息类型*调用**SQLGetInfo**来确定驱动程序支持哪些时间和日期函数。  
  
 表示为*timestamp_exp*的参数可以是列的名称、另一个标量函数的结果或*ODBC 时间转义**、ODBC-日期转义*或*ODBC 时间戳转义*，其中基础数据类型可以表示为SQL_CHAR、SQL_VARCHAR、SQL_TYPE_TIME、SQL_TYPE_DATE 或SQL_TYPE_TIMESTAMP。  
  
 表示为*date_exp*的参数可以是列的名称、另一个标量函数的结果或*ODBC 日期转义*或*ODBC 时间戳转义*，其中基础数据类型可以表示为SQL_CHAR、SQL_VARCHAR、SQL_TYPE_DATE 或SQL_TYPE_TIMESTAMP。  
  
 表示为*time_exp*的参数可以是列的名称、另一个标量函数的结果或*ODBC 时间转义*或*ODBC 时间戳转义*，其中基础数据类型可以表示为SQL_CHAR、SQL_VARCHAR、SQL_TYPE_TIME 或SQL_TYPE_TIMESTAMP。  
  
 在 ODBC 3.0 中添加了CURRENT_DATE、CURRENT_TIME 和CURRENT_TIMESTAMP时间日期标量函数，以便与 SQL-92 对齐。  
  
|函数|说明|  
|--------------|-----------------|  
|**CURRENT_DATE（** ODBC 3.0）|返回当前日期。|  
|**CURRENT_TIME[（***时间精度***）]** （ODBC 3.0）|返回当前本地时间。 *时间精度*参数确定返回值的秒精度。|  
|**CURRENT_TIMESTAMP**<br /> **[（***时间戳精度***）]** （ODBC 3.0）|将当前本地日期和本地时间作为时间戳值返回。 *时间戳精度*参数确定返回的时间戳的秒精度。|  
|**（ODBC** 1.0）|返回当前日期。|  
|**CURTIME（ （ODBC** 1.0）|返回当前本地时间。|  
|**天名（** *date_exp* **）** （ODBC 2.0）|返回包含当天数据源特定名称的字符串（例如，星期日到星期六或周日）。 返回 Sunday 到 Saturday 或 Sun. 到 Sat.； 对于使用英语的数据源，或 Sonntag 通过 Samstag 的数据源，使用德语）的*date_exp*日部分。|  
|**月日（** *date_exp* **）** （ODBC 1.0）|根据*date_exp*中的月份字段返回月份中的天，作为 1-31 范围内的整数值。|  
|**周日（date_exp** *date_exp* **）** （ODBC 1.0）|根据*date_exp*中的周字段返回星期数，作为 1-7 范围内的整数值，其中 1 表示星期日。|  
|**日 （date_exp** *date_exp* **）** （ODBC 1.0）|根据*date_exp*中的年份字段将一年中的天作为 1-366 范围内的整数值返回。|  
|**提取（***从提取物来源提取字段**extract-source* **）（ODBC** 3.0）|返回*提取源*的*提取字段*部分。 *提取源*参数是日期时间或间隔表达式。 *提取字段*参数可以是以下关键字之一：<br /><br /> 年月小时分钟秒<br /><br /> 返回值的精度是实现定义的。 除非指定了"秒"，否则比例为 0，在这种情况下，比例不小于*提取源*字段的小数秒精度。|  
|**小时（time_exp** *time_exp* **）** （ODBC 1.0）|根据*time_exp*中的小时字段返回小时，作为 0-23 范围内的整数值。|  
|**分钟（time_exp** *time_exp* **）** （ODBC 1.0）|返回基于*time_exp*中的分钟字段的分钟，作为 0-59 范围内的整数值。|  
|**月（date_exp** *date_exp* **）** （ODBC 1.0）|基于*date_exp*中的月份字段返回月份，作为 1-12 范围内的整数值。|  
|**月名（** *date_exp* **）** （ODBC 2.0）|返回包含该月特定于数据源名称的字符串（例如，1 月至 12 月或 1 月到 12 月，对于使用英语的数据源，或使用德语的数据源的 Januar 通过 Dezember）返回 date_exp*的月份*部分。|  
|**现在（** （ODBC 1.0）|将当前日期和时间作为时间戳值返回。|  
|**零（date_exp** *date_exp* **）** （ODBC 1.0）|*将 date_exp*中的季度作为 1-4 范围内的整数值返回，其中 1 表示 1 月 1 日至 3 月 31 日。|  
|**秒（** *time_exp* **）** （ODBC 1.0）|返回基于*time_exp*中的第二个字段，作为 0-59 范围内的整数值。|
|**时间戳（***间隔*， *integer_exp*， *timestamp_exp* **）** （ODBC 2.0）|通过将*integer_exp**类型间隔间隔*添加到*timestamp_exp，* 返回计算的时间戳。 *间隔*的有效值如下关键字：<br /><br /> SQL_TSI_FRAC_SECOND<br /><br /> SQL_TSI_SECOND<br /><br /> SQL_TSI_MINUTE<br /><br /> SQL_TSI_HOUR<br /><br /> SQL_TSI_DAY<br /><br /> SQL_TSI_WEEK<br /><br /> SQL_TSI_MONTH<br /><br /> SQL_TSI_QUARTER<br /><br /> SQL_TSI_YEAR<br /><br /> 其中分数秒以十亿分之一秒表示。 例如，以下 SQL 语句返回每个员工的姓名及其一周年日期：<br /><br /> `SELECT NAME, {fn  TIMESTAMPADD(SQL_TSI_YEAR, 1, HIRE_DATE)} FROM  EMPLOYEES`<br /><br /> 如果*timestamp_exp*是时间值，*并且间隔*指定了天、周、月、季度或年，则*timestamp_exp*的日期部分在计算结果的时间戳之前设置为当前日期。<br /><br /> 如果*timestamp_exp*是日期值，*并且间隔*指定分数秒、秒、分钟或小时，则在计算结果的时间戳之前 *，timestamp_exp*的时间部分设置为 0。<br /><br /> 应用程序通过使用SQL_TIMEDATE_ADD_INTERVALS选项调用**SQLGetInfo**来确定数据源支持哪个间隔。|  
|**时间戳（***间隔**，timestamp_exp1，timestamp_exp2）*（ODBC 2.0） *timestamp_exp2* **)**|返回*timestamp_exp2*大于*timestamp_exp1*的类型*间隔*的整数。 *间隔*的有效值如下关键字：<br /><br /> SQL_TSI_FRAC_SECOND<br /><br /> SQL_TSI_SECOND<br /><br /> SQL_TSI_MINUTE<br /><br /> SQL_TSI_HOUR<br /><br /> SQL_TSI_DAY<br /><br /> SQL_TSI_WEEK<br /><br /> SQL_TSI_MONTH<br /><br /> SQL_TSI_QUARTER<br /><br /> SQL_TSI_YEAR<br /><br /> 其中分数秒以十亿分之一秒表示。 例如，以下 SQL 语句返回每个员工的姓名及其雇用的年数：<br /><br /> `SELECT NAME, {fn  TIMESTAMPDIFF(SQL_TSI_YEAR, {fn CURDATE()}, HIRE_DATE)} FROM EMPLOYEES`<br /><br /> 如果时间戳表达式是时间值，*并且间隔*指定日期、周、月、季度或年，则该时间戳的日期部分在计算时间戳之间的差异之前设置为当前日期。<br /><br /> 如果时间戳表达式是日期值，*并且间隔*指定分数秒、秒、分钟或小时，则在计算时间戳之间的差异之前，该时间戳的时间部分设置为 0。<br /><br /> 应用程序通过使用SQL_TIMEDATE_DIFF_INTERVALS选项调用**SQLGetInfo**来确定数据源支持哪个间隔。|  
|**周（date_exp** *date_exp* **）** （ODBC 1.0）|根据*date_exp*中的周字段返回一年中的周，作为 1-53 范围内的整数值。|  
|**年份（date_exp** *date_exp* **）** （ODBC 1.0）|基于*date_exp*中的年份字段作为整数值返回年份。 范围与数据源相关。|
