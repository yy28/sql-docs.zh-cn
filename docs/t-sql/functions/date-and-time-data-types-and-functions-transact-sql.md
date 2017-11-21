---
title: "日期和时间数据类型和函数 (Transact SQL) |Microsoft 文档"
ms.custom: 
ms.date: 09/01/2017
ms.prod: sql-non-specified
ms.prod_service: sql-database
ms.service: 
ms.component: t-sql|functions
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
dev_langs:
- TSQL
helpviewer_keywords:
- dates [SQL Server], functions
- dates [SQL Server]
- date and time [SQL Server], all data types and functions
- date and time [SQL Server]
- functions [SQL Server], time
- functions [SQL Server], date and time
- time [SQL Server], functions
ms.assetid: 83e378a2-6e89-4c80-bc4f-644958d9e0a9
caps.latest.revision: 79
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Active
ms.translationtype: MT
ms.sourcegitcommit: 60272ce672c0a32738b0084ea86f8907ec7fc0a5
ms.openlocfilehash: 7ce3baac7ec87ff3cad771234ab1196fb0a3855e
ms.contentlocale: zh-cn
ms.lasthandoff: 09/06/2017

---
# <a name="date-and-time-data-types-and-functions-transact-sql"></a>日期和时间数据类型及函数 (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

本主题的以下各节对所有 [!INCLUDE[tsql](../../includes/tsql-md.md)] 日期和时间数据类型及函数作了概述。
-   [日期和时间数据类型](#DateandTimeDataTypes)  
-   [日期和时间函数](#DateandTimeFunctions)  
    -   [函数获取系统日期和时间值](#GetSystemDateandTimeValues)  
    -   [函数可以获取日期和时间部分](#GetDateandTimeParts)  
    -   [从其部分中获取日期和时间值的函数](#fromParts)  
    -   [函数可以获取日期和时间差异](#GetDateandTimeDifference)  
    -   [函数修改日期和时间值](#ModifyDateandTimeValues)  
    -   [设置或获取会话格式函数的函数](#SetorGetSessionFormatFunctions)  
    -   [函数验证日期和时间值](#ValidateDateandTimeValues)  
-   [日期和时间的相关主题](#DateandTimeRelatedTopics)  
  
##  <a name="DateandTimeDataTypes"></a>日期和时间数据类型
[!INCLUDE[tsql](../../includes/tsql-md.md)]下表中列出了日期和时间数据类型：
  
|数据类型|格式|范围|精确度|存储大小 （字节）|用户定义的秒的小数部分精度|时区偏移量|  
|---|---|---|---|---|---|---|
|[time](../../t-sql/data-types/time-transact-sql.md)|hh:mm:ss[.nnnnnnn]|00:00:00.0000000 到 23:59:59.9999999|100 纳秒|3 到 5|是|是|  
|[date](../../t-sql/data-types/date-transact-sql.md)|YYYY-MM-DD|0001-01-01 到 31.12.99|1 天|3|是|是|  
|[smalldatetime](../../t-sql/data-types/smalldatetime-transact-sql.md)|YYYY-MM-DD hh:mm:ss|1900-01-01 到 2079-06-06|1 分钟|4|是|是|  
|[datetime](../../t-sql/data-types/datetime-transact-sql.md)|YYYY-MM-DD hh:mm:ss[.nnn]|1753-01-01 到 9999-12-31|0.00333 秒|8|是|是|  
|[datetime2](../../t-sql/data-types/datetime2-transact-sql.md)|YYYY-MM-DD hh:mm:ss[.nnnnnnn]|0001-01-01 00:00:00.0000000 到 9999-12-31 23:59:59.9999999|100 纳秒|6 到 8|是|是|  
|[datetimeoffset](../../t-sql/data-types/datetimeoffset-transact-sql.md)|YYYY MM DD hh: mm: [.nnnnnnn] [+ &#124;-] hh: mm|0001-01-01 00:00:00.0000000 到 9999-12-31 23:59:59.9999999（以 UTC 时间表示）|100 纳秒|8 到 10|是|是|  
  
> [!NOTE]  
>  [!INCLUDE[tsql](../../includes/tsql-md.md)] [Rowversion](../../t-sql/data-types/rowversion-transact-sql.md)数据类型不是日期或时间数据类型。 **时间戳**是不推荐使用的同义词**rowversion**。  
  
##  <a name="DateandTimeFunctions"></a>日期和时间函数  
以下各表列出了 [!INCLUDE[tsql](../../includes/tsql-md.md)] 的日期和时间函数。 有关确定性的详细信息，请参阅[Deterministic and Nondeterministic Functions](../../relational-databases/user-defined-functions/deterministic-and-nondeterministic-functions.md)。
  
###  <a name="GetSystemDateandTimeValues"></a>获取系统日期和时间值的函数 
所有系统日期和时间值均得自运行 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实例的计算机的操作系统。
  
#### <a name="higher-precision-system-date-and-time-functions"></a>精度较高的系统日期和时间函数  
[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]通过使用 GetSystemTimeAsFileTime() Windows API 中获取日期和时间值。 精确程度取决于运行 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实例的计算机硬件和 Windows 版本。 此 API 的精度固定为 100 纳秒。 可以使用 GetSystemTimeAdjustment() Windows API 确定准确性。
  
|函数|语法|返回值|返回数据类型|确定性|  
|---|---|---|---|---|
|[SYSDATETIME](../../t-sql/functions/sysdatetime-transact-sql.md)|SYSDATETIME ()|返回**datetime2 （7)**值，该值包含的日期和时间的计算机上的实例[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]正在运行。 时区偏移量未包含在内。|**datetime2(7)**|不具有确定性|  
|[SYSDATETIMEOFFSET](../../t-sql/functions/sysdatetimeoffset-transact-sql.md)|SYSDATETIMEOFFSET ( )|返回**datetimeoffset(7)**值，该值包含的日期和时间的计算机上的实例[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]正在运行。 时区偏移量包含在内。|**datetimeoffset(7)**|不具有确定性|  
|[SYSUTCDATETIME](../../t-sql/functions/sysutcdatetime-transact-sql.md)|SYSUTCDATETIME ( )|返回**datetime2 （7)**值，该值包含的日期和时间的计算机上的实例[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]正在运行。 日期和时间作为 UTC 时间（通用协调时间）返回。|**datetime2(7)**|不具有确定性|  
  
#### <a name="lower-precision--system-date-and-time-functions"></a>较低的精度系统日期和时间函数
  
|函数|语法|返回值|返回数据类型|确定性|  
|---|---|---|---|---|
|[CURRENT_TIMESTAMP](../../t-sql/functions/current-timestamp-transact-sql.md)|CURRENT_TIMESTAMP|返回**datetime**值，该值包含的日期和时间的计算机上的实例[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]正在运行。 时区偏移量未包含在内。|**datetime**|不具有确定性|  
|[GETDATE](../../t-sql/functions/getdate-transact-sql.md)|GETDATE ( )|返回**datetime**值，该值包含的日期和时间的计算机上的实例[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]正在运行。 时区偏移量未包含在内。|**datetime**|不具有确定性|  
|[GETUTCDATE](../../t-sql/functions/getutcdate-transact-sql.md)|GETUTCDATE ( )|返回**datetime**值，该值包含的日期和时间的计算机上的实例[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]正在运行。 日期和时间作为 UTC 时间（通用协调时间）返回。|**datetime**|不具有确定性|  
  
###  <a name="GetDateandTimeParts"></a>获取日期和时间部分的函数
  
|函数|语法|返回值|返回数据类型|确定性|  
|--------------|------------|------------------|----------------------|-----------------|  
|[DATENAME](../../t-sql/functions/datename-transact-sql.md)|DATENAME ( *datepart* ，*日期*)|返回表示指定的字符字符串*datepart*的指定日期。|**nvarchar**|不具有确定性|  
|[DATEPART](../../t-sql/functions/datepart-transact-sql.md)|DATEPART ( *datepart* ，*日期*)|返回一个整数，表示指定*datepart*指定*日期*。|**int**|不具有确定性|  
|[一天](../../t-sql/functions/day-transact-sql.md)|一天 (*日期*)|返回一个整数，表示指定的日部分*日期*。|**int**|具有确定性|  
|[月](../../t-sql/functions/month-transact-sql.md)|月 (*日期*)|返回一个整数，表示指定的月份部分*日期*。|**int**|具有确定性|  
|[年](../../t-sql/functions/year-transact-sql.md)|年 (*日期*)|返回一个整数，表示指定的年份部分*日期*。|**int**|具有确定性|  
  
###  <a name="fromParts"></a>从其部分获取日期和时间值的函数
  
|函数|语法|返回值|返回数据类型|确定性|  
|---|---|---|---|---|
|[DATEFROMPARTS](../../t-sql/functions/datefromparts-transact-sql.md)|DATEFROMPARTS (*年*，*月*，*天*)|返回**日期**指定的年、 月和日的值。|**date**|具有确定性|  
|[DATETIME2FROMPARTS](../../t-sql/functions/datetime2fromparts-transact-sql.md)|DATETIME2FROMPARTS (*年*，*月*，*天*，*小时*，*分钟*，*秒*，*分数 （竖式)*，*精度*)|返回**datetime2**值的指定的日期和时间并使用指定的精度。|**datetime2 (** *精度* **)**|具有确定性|  
|[DATETIMEFROMPARTS](../../t-sql/functions/datetimefromparts-transact-sql.md)|DATETIMEFROMPARTS (*年*，*月*，*天*，*小时*，*分钟*，*秒*，*毫秒*)|返回**datetime**值的指定的日期和时间。|**datetime**|具有确定性|  
|[DATETIMEOFFSETFROMPARTS](../../t-sql/functions/datetimeoffsetfromparts-transact-sql.md)|DATETIMEOFFSETFROMPARTS (*年*，*月*，*天*，*小时*，*分钟*， *秒*，*分数 （竖式)*， *hour_offset*， *minute_offset*，*精度*)|返回**datetimeoffset**值的指定的日期和时间并使用指定的偏移量和精度。|**datetime (** *精度* **)**|具有确定性|  
|[SMALLDATETIMEFROMPARTS](../../t-sql/functions/smalldatetimefromparts-transact-sql.md)|SMALLDATETIMEFROMPARTS (*年*，*月*，*天*，*小时*，*分钟*)|返回**smalldatetime**值的指定的日期和时间。|**smalldatetime**|具有确定性|  
|[TIMEFROMPARTS](../../t-sql/functions/timefromparts-transact-sql.md)|TIMEFROMPARTS (*小时*，*分钟*，*秒*，*分数 （竖式)*，*精度*)|返回**时间**值指定的时间并使用指定的精度。|**时间 (** *精度* **)**|具有确定性|  
  
###  <a name="GetDateandTimeDifference"></a>获取日期和时间差异的函数
  
|函数|语法|返回值|返回数据类型|确定性|  
|---|---|---|---|---|
|[DATEDIFF](../../t-sql/functions/datediff-transact-sql.md)|DATEDIFF ( *datepart* ， *startdate* ， *enddate* )|返回的日期或时间数*datepart*超过两个指定日期之间的边界。|**int**|具有确定性|  
|[DATEDIFF_BIG](../../t-sql/functions/datediff-big-transact-sql.md)|DATEDIFF_BIG ( *datepart* ， *startdate* ， *enddate* )|返回的日期或时间数*datepart*超过两个指定日期之间的边界。|**bigint**|具有确定性|  
  
###  <a name="ModifyDateandTimeValues"></a>修改日期和时间值的函数
  
|函数|语法|返回值|返回数据类型|确定性|  
|---|---|---|---|---|
|[DATEADD](../../t-sql/functions/dateadd-transact-sql.md)|DATEADD (*datepart* ，*数*，*日期*)|返回一个新**datetime**通过将间隔添加到指定的值*datepart*指定*日期*。|数据类型*日期*自变量|具有确定性|  
|[EOMONTH](../../t-sql/functions/eomonth-transact-sql.md)|EOMONTH ( *start_date* [， *month_to_add* ])|返回包含指定日期的月份的最后一天（具有可选偏移量）。|返回类型是一种*start_date*或**日期**。|具有确定性|  
|[SWITCHOFFSET](../../t-sql/functions/switchoffset-transact-sql.md)|交换机*偏移量*(*DATETIMEOFFSET* ， *time_zone*)|交换机*偏移量*更改 DATETIMEOFFSET 值的时区偏移量，并保留 UTC 值。|**datetimeoffset**使用的小数部分精度*DATETIMEOFFSET*|具有确定性|  
|[TODATETIMEOFFSET](../../t-sql/functions/todatetimeoffset-transact-sql.md)|TODATETIMEOFFSET (*表达式*， *time_zone*)|TODATETIMEOFFSET 将 datetime2 值转换为 datetimeoffset 值。 datetime2 值被解释为指定 time_zone 的本地时间。|**datetimeoffset**使用的小数部分精度*datetime*自变量|具有确定性|  
  
###  <a name="SetorGetSessionFormatFunctions"></a>获取或设置会话格式的函数
  
|函数|语法|返回值|返回数据类型|确定性|  
|---|---|---|---|---|
|[@@DATEFIRST](../../t-sql/functions/datefirst-transact-sql.md)|@@DATEFIRST|返回对会话进行 SET DATEFIRST 操作所得结果的当前值。|**tinyint**|不具有确定性|  
|[SET DATEFIRST](../../t-sql/statements/set-datefirst-transact-sql.md)|SET DATEFIRST {*数*&#124; **@**  *number_var* }|将一周的第一天设置为从 1 到 7 的一个数字。|不适用|不适用|  
|[集 DATEFORMAT](../../t-sql/statements/set-dateformat-transact-sql.md)|SET DATEFORMAT {*格式*&#124; **@**  *format_var* }|用于输入设置的日期部分 （月/日/年） 的顺序**datetime**或**smalldatetime**数据。|不适用|不适用|  
|[@@LANGUAGE](../../t-sql/functions/language-transact-sql.md)|@@LANGUAGE|返回当前使用的语言的名称。 @@LANGUAGE不是日期或时间的函数。 但是，语言设置会影响日期函数的输出。|不适用|不适用|  
|[设置语言](../../t-sql/statements/set-language-transact-sql.md)|SET LANGUAGE {[N] *语言* &#124; **@**  *language_var* }|设置会话和系统消息的语言环境。 SET LANGUAGE 不是日期或时间函数。 但是，语言设置会影响日期函数的输出。|不适用|不适用|  
|[sp_helplanguage](../../relational-databases/system-stored-procedures/sp-helplanguage-transact-sql.md)|**sp_helplanguage** [[  **@language =** ] *语言* ]|返回有关所有支持语言的日期格式的信息。 **sp_helplanguage**日期或时间不是存储过程。 但是，语言设置会影响日期函数的输出。|不适用|不适用|  
  
###  <a name="ValidateDateandTimeValues"></a>验证日期和时间值的函数
  
|函数|语法|返回值|返回数据类型|确定性|  
|---|---|---|---|---|
|[ISDATE](../../t-sql/functions/isdate-transact-sql.md)|ISDATE (*表达式*)|确定是否**datetime**或**smalldatetime**输入的表达式是有效的日期或时间值。|**int**|只有与 CONVERT 函数一起使用，同时指定了 CONVERT 样式参数且样式不等于 0、100、9 或 109 时，ISDATE 才是确定的。|  
  
##  <a name="DateandTimeRelatedTopics"></a>日期和时间相关的主题 
  
|主题|Description|  
|-----------|-----------------|  
|[CAST 和 CONVERT (Transact-SQL)](../../t-sql/functions/cast-and-convert-transact-sql.md)|提供有关在日期和时间值与字符串文字及其他日期和时间格式之间进行相互转换的信息。|  
|[编写国际化 Transact-SQL 语句](../../relational-databases/collations/write-international-transact-sql-statements.md)|提供的数据库和数据库应用程序使用可移植性的指南[!INCLUDE[tsql](../../includes/tsql-md.md)]从一种语言到另一个，或该语句支持多种语言。|  
|[ODBC 标量函数 &#40;Transact SQL &#41;](../../t-sql/functions/odbc-scalar-functions-transact-sql.md)|提供有关可以在中使用的 ODBC 标量函数的信息[!INCLUDE[tsql](../../includes/tsql-md.md)]语句。 这包括 ODBC 日期和时间函数。|  
|[时区 &AMP; #40;Transact SQL &#41;](../../t-sql/queries/at-time-zone-transact-sql.md)|提供时区转换。|  
  
## <a name="see-also"></a>另请参阅
[函数](../../t-sql/functions/functions.md)  
[数据类型 (Transact-SQL)](../../t-sql/data-types/data-types-transact-sql.md)
  
  

