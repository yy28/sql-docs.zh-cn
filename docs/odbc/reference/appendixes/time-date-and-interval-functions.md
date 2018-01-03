---
title: "时间、 日期和时间间隔函数 |Microsoft 文档"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: odbc
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- functions [ODBC], time functions
- functions [ODBC], date functions
- interval functions [ODBC]
- functions [ODBC], interval functions
- time functions [ODBC]
- date functions [ODBC]
ms.assetid: bdf054a0-7aba-4e99-a34a-799917376fd5
caps.latest.revision: "7"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: On Demand
ms.openlocfilehash: 49f765c78f6c0b861c56d1299fc90786b6c22b78
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/21/2017
---
# <a name="time-date-and-interval-functions"></a>时间、日期和时间间隔函数
下表列出了 ODBC 标量函数集中包含的日期和时间函数。 应用程序可以确定由驱动程序支持的日期和时间函数，应调用**SQLGetInfo**与*信息类型*SQL_TIMEDATE_FUNCTIONS。  
  
 自变量表示为*timestamp_exp*可以是列，另一个的标量函数的结果的名称或*ODBC 时间转义*， *ODBC 日期转义*，或*ODBC 时间戳转义*，其中基础数据类型无法表示为 SQL_CHAR、 SQL_VARCHAR、 SQL_TYPE_TIME、 SQL_TYPE_DATE 或 SQL_TYPE_TIMESTAMP。  
  
 自变量表示为*date_exp*可以是列，另一个的标量函数的结果的名称或*ODBC 日期转义*或*ODBC 时间戳转义*，其中基础数据类型无法表示为 SQL_CHAR、 SQL_VARCHAR、 SQL_TYPE_DATE 或 SQL_TYPE_TIMESTAMP。  
  
 自变量表示为*time_exp*可以是列，另一个的标量函数的结果的名称或*ODBC 时间转义*或*ODBC 时间戳转义*，其中基础数据类型无法表示为 SQL_CHAR、 SQL_VARCHAR、 SQL_TYPE_TIME 或 SQL_TYPE_TIMESTAMP。  
  
 CURRENT_DATE、 CURRENT_TIME 和 CURRENT_TIMESTAMP timedate 标量函数已在 ODBC 3.0 为了符合 SQL 92 中添加。  
  
|函数|Description|  
|--------------|-----------------|  
|**CURRENT_DATE （)** (ODBC 3.0)|返回当前日期。|  
|**CURRENT_TIME [(** *时间精度* **)]** (ODBC 3.0)|返回当前本地时间。 *时间精度*参数确定返回值的秒精度。|  
|**CURRENT_TIMESTAMP**<br /> **[(** *时间戳精度* **)]** (ODBC 3.0)|返回当前日期和本地时间时间戳值。 *时间戳精度*参数确定返回的时间戳的秒精度。|  
|**CURDATE （)** (ODBC 1.0)|返回当前日期。|  
|**CURTIME （)** (ODBC 1.0)|返回当前本地时间。|  
|**DAYNAME (** *date_exp* **)** (ODBC 2.0)|返回包含 （例如星期日至星期六或者 Sun 一天数据源 – 特定名称字符串。 返回 Sunday 到 Saturday 或 Sun. 到 Sat.； 使用英语或通过 Samstag Sonntag 使用德语的数据源的数据源） 有关的日部分*date_exp*。|  
|**DAYOFMONTH (** *date_exp* **)** (ODBC 1.0)|返回月会根据月字段中的天*date_exp*为整数值 1-31 范围内。|  
|**DAYOFWEEK (** *date_exp* **)** (ODBC 1.0)|返回根据周字段星期几*date_exp*为范围内的一个整数值 1 – 7，其中 1 表示星期日。|  
|**DAYOFYEAR (** *date_exp* **)** (ODBC 1.0)|返回根据年份字段的年度的天*date_exp*为 1-366 的范围中的整数值。|  
|**提取 (** *提取字段 FROM* *提取源* **)** (ODBC 3.0)|返回*提取字段*部分*提取源*。 *提取源*参数是一个日期时间或间隔的表达式。 *提取字段*自变量可以是以下关键字之一：<br /><br /> 年月天、 每天小时分钟秒<br /><br /> 返回的精度是值的实现定义的。 刻度为 0 指定第二个，则除非在这种情况下缩放不小于的秒的小数部分精度*提取源*字段。|  
|**小时 (** *time_exp* **)** (ODBC 1.0)|返回根据小时字段表示小时*time_exp*为整数值在 0-23 的范围内。|  
|**分钟 (** *time_exp* **)** (ODBC 1.0)|返回基于分钟字段分钟*time_exp*范围是 0-59 以整数值形式。|  
|**月 (** *date_exp* **)** (ODBC 1.0)|返回基于月字段中的月份*date_exp*为整数值 1 到 12 范围内。|  
|**月份名称 (** *date_exp* **)** (ODBC 2.0)|返回的月份部分包含的 （例如，一月至 12 月或年 1 月 12 月的数据源，使用英语，为通过或通过使用德语的数据源的 Dezember Januar） 的月份的数据源 – 特定名称的字符串*date_exp*。|  
|**现在 （)** (ODBC 1.0)|返回当前日期和时间戳值的时间。|  
|**季度 (** *date_exp* **)** (ODBC 1.0)|返回此季度中的*date_exp*为范围内的一个整数值 1-4，其中 1 表示月年 1 月 1 日到 3 月 31 日。|  
|**第二个 (** *time_exp* **)** (ODBC 1.0)|返回根据第二个字段中的第二个*time_exp*范围是 0-59 以整数值形式。|
|**TIMESTAMPADD (** *间隔*， *integer_exp*， *timestamp_exp* **)** (ODBC 2.0)|返回通过将计算出的时间戳*integer_exp*间隔类型*间隔*到*timestamp_exp*。 有效值*间隔*都是以下关键字：<br /><br /> SQL_TSI_FRAC_SECOND<br /><br /> SQL_TSI_SECOND<br /><br /> SQL_TSI_MINUTE<br /><br /> SQL_TSI_HOUR<br /><br /> SQL_TSI_DAY<br /><br /> SQL_TSI_WEEK<br /><br /> SQL_TSI_MONTH<br /><br /> SQL_TSI_QUARTER<br /><br /> SQL_TSI_YEAR<br /><br /> 其中用在第二个 billionths 表示秒的小数部分。 例如，以下 SQL 语句返回的每个员工和他或她一年周年日的名称：<br /><br /> `SELECT NAME, {fn  TIMESTAMPADD(SQL_TSI_YEAR, 1, HIRE_DATE)} FROM  EMPLOYEES`<br /><br /> 如果*timestamp_exp*是时间值和*间隔*指定日、 周、 月、 季度或年的日期部分*timestamp_exp*设置为当前日期之前计算的结果的时间戳。<br /><br /> 如果*timestamp_exp*日期值和*间隔*指定小数秒、 秒、 分钟或小时数的时间部分的*timestamp_exp*设置为 0 之前计算的结果的时间戳。<br /><br /> 应用程序确定数据源支持通过调用哪些间隔**SQLGetInfo** SQL_TIMEDATE_ADD_INTERVALS 选项。|  
|**TIMESTAMPDIFF (** *间隔*， *timestamp_exp1*， *timestamp_exp2* **)** (ODBC 2.0)|返回整数的类型的间隔数*间隔*依据*timestamp_exp2*大于*timestamp_exp1*。 有效值*间隔*都是以下关键字：<br /><br /> SQL_TSI_FRAC_SECOND<br /><br /> SQL_TSI_SECOND<br /><br /> SQL_TSI_MINUTE<br /><br /> SQL_TSI_HOUR<br /><br /> SQL_TSI_DAY<br /><br /> SQL_TSI_WEEK<br /><br /> SQL_TSI_MONTH<br /><br /> SQL_TSI_QUARTER<br /><br /> SQL_TSI_YEAR<br /><br /> 其中用在第二个 billionths 表示秒的小数部分。 例如，以下 SQL 语句返回的每个员工和已使用他或她的年数的名称：<br /><br /> `SELECT NAME, {fn  TIMESTAMPDIFF(SQL_TSI_YEAR, {fn CURDATE()}, HIRE_DATE)} FROM EMPLOYEES`<br /><br /> 如果其中任何一个时间戳表达式是一个时间值和*间隔*指定天、 周、 月、 季度或年，该时间戳的日期部分设置为当前日期之前计算时间戳之间的差异。<br /><br /> 如果其中任何一个时间戳表达式是一个日期值和*间隔*指定小数秒、 秒、 分钟或小时数，在计算时间戳之间的差异之前设置为 0 的时间部分的该时间戳。<br /><br /> 应用程序确定数据源支持通过调用哪些间隔**SQLGetInfo** SQL_TIMEDATE_DIFF_INTERVALS 选项。|  
|**一周 (** *date_exp* **)** (ODBC 1.0)|返回基于周字段的年度的某一周*date_exp*为整数值 1 – 53 范围内。|  
|**年 (** *date_exp* **)** (ODBC 1.0)|返回根据年份字段的年度*date_exp*为一个整数值。 范围是数据源而定。|
