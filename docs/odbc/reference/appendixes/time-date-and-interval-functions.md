---
title: 时间、 日期和时间间隔函数 |Microsoft Docs
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: e1303ca724ef6790ae7bcf218ab8ed0e5da4ed38
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62735083"
---
# <a name="time-date-and-interval-functions"></a>时间、日期和时间间隔函数
下表列出了 ODBC 标量函数集中包含的日期和时间函数。 应用程序可以确定由驱动程序通过调用支持的日期和时间的函数**SQLGetInfo**与*信息类型*SQL_TIMEDATE_FUNCTIONS。  
  
 参数表示为*timestamp_exp*可以是列，另一个标量函数的结果的名称或*时间的 ODBC 转义*，*日期的 ODBC 转义*，或者*ODBC 时间戳转义*，其中的基础数据类型可以表示为 SQL_CHAR、 SQL_VARCHAR、 SQL_TYPE_TIME、 SQL_TYPE_DATE 或 SQL_TYPE_TIMESTAMP。  
  
 参数表示为*date_exp*可以是列，另一个标量函数的结果的名称或*日期的 ODBC 转义*或*ODBC 时间戳转义*，其中基础数据类型可以表示为 SQL_CHAR、 SQL_VARCHAR、 SQL_TYPE_DATE 或 SQL_TYPE_TIMESTAMP。  
  
 参数表示为*time_exp*可以是列，另一个标量函数的结果的名称或*时间的 ODBC 转义*或*ODBC 时间戳转义*，其中基础数据类型可以表示为 SQL_CHAR、 SQL_VARCHAR、 SQL_TYPE_TIME 或 SQL_TYPE_TIMESTAMP。  
  
 CURRENT_DATE、 CURRENT_TIME 和 CURRENT_TIMESTAMP timedate 标量函数已在 ODBC 3.0 以符合 SQL-92 中添加。  
  
|函数|Description|  
|--------------|-----------------|  
|**CURRENT_DATE( )** (ODBC 3.0)|返回当前日期。|  
|**CURRENT_TIME[(** *time-precision* **)]** (ODBC 3.0)|返回当前本地时间。 *时间精度*参数确定返回值的秒精度。|  
|**CURRENT_TIMESTAMP**<br /> **[(** *timestamp-precision* **)]** (ODBC 3.0)|作为时间戳值返回当前本地日期和本地时间。 *时间戳精度*参数确定返回的时间戳的秒精度。|  
|**CURDATE （)** (ODBC 1.0)|返回当前日期。|  
|**CURTIME （)** (ODBC 1.0)|返回当前本地时间。|  
|**DAYNAME(** *date_exp* **)** (ODBC 2.0)|返回一个包含数据源特定名称 （例如，Sunday 到 Saturday 或 Sun 一天中的字符串。 返回 Sunday 到 Saturday 或 Sun. 到 Sat.； 数据源使用德语的数据源使用英语，sonntag 到 Samstag） 有关的日部分*date_exp*。|  
|**DAYOFMONTH(** *date_exp* **)** (ODBC 1.0)|返回日期所处月份字段月份*date_exp*为整数值 1 到 31 范围内。|  
|**DAYOFWEEK(** *date_exp* **)** (ODBC 1.0)|返回根据周字段星期几*date_exp*范围内的一个整数值 1-7，其中 1 表示星期天。|  
|**DAYOFYEAR(** *date_exp* **)** (ODBC 1.0)|返回年份字段基于年的某一天*date_exp*为整数值范围内的 1-366。|  
|**EXTRACT(** *extract-field FROM* *extract-source* **)** (ODBC 3.0)|返回*提取字段*一部分*提取源*。 *提取源*参数是日期时间间隔的表达式。 *提取字段*参数可以是以下关键字之一：<br /><br /> 年月日小时分钟，第二个<br /><br /> 返回的精度是值的实现定义的。 小数位数为 0 指定第二个，则除非这种情况下缩放不小于的秒的小数部分精度*提取源*字段。|  
|**HOUR(** *time_exp* **)** (ODBC 1.0)|返回小时中的小时字段基于*time_exp* 0 到 23 范围内的一个整数值。|  
|**MINUTE(** *time_exp* **)** (ODBC 1.0)|返回分钟中的分钟字段基于*time_exp* 0-59 范围内的一个整数值。|  
|**MONTH(** *date_exp* **)** (ODBC 1.0)|返回所处月份字段月份*date_exp*为整数值 1 到 12 范围内。|  
|**MONTHNAME(** *date_exp* **)** (ODBC 2.0)|返回的月份部分包含的 （例如，一月到十二月或对于使用英语，数据源，返回 Januar 到 Dezember 对于使用德语的数据源） 个月的数据源特定的名称的字符串*date_exp*。|  
|**现在 （)** (ODBC 1.0)|返回当前日期和时间作为时间戳值。|  
|**QUARTER(** *date_exp* **)** (ODBC 1.0)|返回中的每个季度*date_exp*范围内的一个整数值 1-4，其中 1 表示 1 月 1 日到 3 月 31 日结束。|  
|**SECOND(** *time_exp* **)** (ODBC 1.0)|返回根据第二个字段中的第二个*time_exp* 0-59 范围内的一个整数值。|
|**TIMESTAMPADD(** *interval*, *integer_exp*, *timestamp_exp* **)** (ODBC 2.0)|返回通过添加计算的时间戳*integer_exp*类型的时间间隔*间隔*到*timestamp_exp*。 有效值*间隔*是以下关键字：<br /><br /> SQL_TSI_FRAC_SECOND<br /><br /> SQL_TSI_SECOND<br /><br /> SQL_TSI_MINUTE<br /><br /> SQL_TSI_HOUR<br /><br /> SQL_TSI_DAY<br /><br /> SQL_TSI_WEEK<br /><br /> SQL_TSI_MONTH<br /><br /> SQL_TSI_QUARTER<br /><br /> SQL_TSI_YEAR<br /><br /> 其中一秒的十亿分之一中表示秒的小数部分。 例如，以下 SQL 语句返回每个雇员和他或她满一周年日期的名称：<br /><br /> `SELECT NAME, {fn  TIMESTAMPADD(SQL_TSI_YEAR, 1, HIRE_DATE)} FROM  EMPLOYEES`<br /><br /> 如果*timestamp_exp*是一个时间值以及*间隔*指定天、 周、 月、 季度或年的日期部分*timestamp_exp*设置为当前日期之前正在计算生成的时间戳。<br /><br /> 如果*timestamp_exp*是日期值和*间隔*指定小数秒、 秒、 分钟或小时为单位的时间部分*timestamp_exp*设置为 0 之前正在计算生成的时间戳。<br /><br /> 应用程序确定哪些数据源支持通过调用的时间间隔**SQLGetInfo** SQL_TIMEDATE_ADD_INTERVALS 选项。|  
|**TIMESTAMPDIFF(** *interval*, *timestamp_exp1*, *timestamp_exp2* **)** (ODBC 2.0)|返回整数的类型的间隔数*间隔*依据*timestamp_exp2*大于*timestamp_exp1*。 有效值*间隔*是以下关键字：<br /><br /> SQL_TSI_FRAC_SECOND<br /><br /> SQL_TSI_SECOND<br /><br /> SQL_TSI_MINUTE<br /><br /> SQL_TSI_HOUR<br /><br /> SQL_TSI_DAY<br /><br /> SQL_TSI_WEEK<br /><br /> SQL_TSI_MONTH<br /><br /> SQL_TSI_QUARTER<br /><br /> SQL_TSI_YEAR<br /><br /> 其中一秒的十亿分之一中表示秒的小数部分。 例如，以下 SQL 语句返回的名称以及每个雇员的已使用他或她的年数：<br /><br /> `SELECT NAME, {fn  TIMESTAMPDIFF(SQL_TSI_YEAR, {fn CURDATE()}, HIRE_DATE)} FROM EMPLOYEES`<br /><br /> 如果其中任何一个时间戳表达式是一个时间值和*间隔*指定天、 周、 月、 季度或年来，该时间戳的日期部分设置为当前日期之前计算时间戳之间的差异。<br /><br /> 如果其中任何一个时间戳表达式是日期值和*间隔*指定小数秒、 秒、 分钟或小时数，在计算时间戳之间的差异前设置为 0 的该时间戳的时间部分。<br /><br /> 应用程序确定哪些数据源支持通过调用的时间间隔**SQLGetInfo** SQL_TIMEDATE_DIFF_INTERVALS 选项。|  
|**WEEK(** *date_exp* **)** (ODBC 1.0)|返回所处年度中的周字段的一周*date_exp*为整数值 1-53 范围内。|  
|**YEAR(** *date_exp* **)** (ODBC 1.0)|返回根据年份字段中的年份*date_exp*为整数值。 范围是由数据源决定。|
