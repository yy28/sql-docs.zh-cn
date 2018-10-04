---
title: 日期和时间格式 |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- integration-services
ms.topic: conceptual
helpviewer_keywords:
- time data types [Integration Services]
- fast parse [Integration Services]
- date data types
- date and time formats for fast parse
ms.assetid: bed6e2c1-791a-4fa1-b29f-cbfdd1fa8d39
author: douglaslms
ms.author: douglasl
manager: craigg
ms.openlocfilehash: d84f3158b41f2cff79572ad7a65c3033a4d2ca77
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/02/2018
ms.locfileid: "48112737"
---
# <a name="date-and-time-formats"></a>日期和时间格式
  快速分析提供一组快速、简单的数据分析例程。 快速分析支持下列日期和时间数据类型格式。  
  
## <a name="date-data-types"></a>日期数据类型  
 快速分析支持日期数据的下列字符串格式：  
  
-   包含前导空格的日期格式。 例如，值“2004- 02-03”有效。  
  
-   ISO 8601 格式，如下表中所示：  
  
    |“格式”|Description|  
    |------------|-----------------|  
    |YYYYMMDD<br /><br /> YYYY-MM-DD|用四位数表示年、两位数表示月和两位数表示日的基本和扩展格式。 在扩展格式中，日期部分以连字符 (-) 分隔。|  
    |YYYY-MM|用四位数表示年和两位数表示月的基本和扩展简化精度格式。 在扩展格式中，日期部分以连字符 (-) 分隔。|  
    |yyyy|用四位数表示年的简化精度格式。|  
  
 快速分析不支持日期数据的下列格式：  
  
-   用字母表示的月份值。 例如，日期格式 Oct-31-2003 无效。  
  
-   不明确的格式，如 DD-MM-YYYY 和 MM-DD-YYYY。 例如，日期 03-04-1995 和 04-03-1995 都无效。  
  
-   用四位数表示日历年和三位数表示一年中的第几天的基本和扩展截断格式，YYYYDDD 和 YYYY-DDD。  
  
-   用四位数表示年、用两位数表示一年中第几周和一位数表示一周中星期几的基本和扩展格式，YYYYWwwD 和 YYYY-Www-D。  
  
-   年和周日期的基本与扩展截断格式是用四位数表示年和两位数表示周，YYYWww 和 YYYY-Www。  
  
 快速分析将数据输出为 DT_DBDATE。 对截断格式的日期值进行填充。 例如，YYYY 变为 YYYY0101。  
  
 有关详细信息，请参阅 [Integration Services 数据类型](data-flow/integration-services-data-types.md)。  
  
## <a name="time-data-type"></a>时间数据类型  
 快速分析支持时间数据的下列字符串格式：  
  
-   包含前导空格的时间格式。 例如，值“ 10:24”有效。  
  
-   24 小时制格式。 快速分析不支持 AM 和 PM 表示法。  
  
-   ISO 8601 时间格式，如下表中所示：  
  
    |“格式”|Description|  
    |------------|-----------------|  
    |HHMISS<br /><br /> HH:MI:SS|用两位数表示小时、两位数表示分钟和两位数表示秒的基本和扩展格式。 在扩展格式中，时间部分以冒号 (:) 分隔。|  
    |HHMI<br /><br /> HH:MI|用两位数表示小时和两位数表示分钟的基本和扩展截断格式。 在扩展格式中，时间部分以冒号 (:) 分隔。|  
    |HH|用两位数表示小时的截断格式。|  
    |00:00:00<br /><br /> 000000<br /><br /> 0000<br /><br /> 00<br /><br /> 240000<br /><br /> 24:00:00<br /><br /> 2400<br /><br /> 24|午夜的格式。|  
  
-   指定时区的时间格式，如下表所示：  
  
    |“格式”|Description|  
    |------------|-----------------|  
    |+HH:MI<br /><br /> +HHMI|指示为得出本地时间而在协调世界时 (UTC) 基础上加上的小时和分钟数的基本和扩展格式。|  
    |-HH:MI<br /><br /> -HHMI|指示为得出本地时间而从 UTC 减去的小时和分钟数的基本和扩展格式。|  
    |+HH|指示为得出本地时间而在 UTC 基础上加上的小时数的截断格式。|  
    |-HH|指示为得出本地时间而从 UTC 减去的小时数的截断格式。|  
    |Z|值为 0 表示采用 UTC 表示时间。|  
  
     所有时间和日期/时间数据的格式都可以包括时区元素。 不过，如果数据的类型不是 DT_DBTIMESTAMPOFFSET，系统将忽略该时区值。 有关详细信息，请参阅 [Integration Services 数据类型](data-flow/integration-services-data-types.md)。  
  
     在包括时区元素的格式中，时间元素和时区元素之间没有空格，如下面的示例所示：  
  
     HH:MI:SS[+HH:MI]  
  
     上例中的括号表明时区值是可选的。  
  
-   包含小数的时间格式，如下表所示：  
  
    |“格式”|Description|  
    |------------|-----------------|  
    |HH[.nnnnnnn]|n 是介于 0 和 9999999 之间的值，表示小时的小数部分。 方括号表明该值是可选的。<br /><br /> 例如，值 12.750 表示 12:45。|  
    |HHMI[.nnnnnnn]<br /><br /> HH:MI[.nnnnnnn]|n 是介于 0 和 9999999 之间的值，表示分钟的小数部分。 方括号表明该值是可选的。<br /><br /> 例如，值 1220.500 表示 12:20:30。|  
    |HHMISS[.nnnnnnn]<br /><br /> HH:MI:SS[.nnnnnnn]|n 是介于 0 和 9999999 之间的值，表示秒的小数部分。 方括号表明该值是可选的。<br /><br /> 例如，值 122040.250 表示 12:20:40.15。|  
  
    > [!NOTE]  
    >  上表中时间格式的小数分隔符可以是小数点或逗号。  
  
-   包括闰秒的时间值，如下例所示：  
  
     23:59:60[.0000000]  
  
     235960[.0000000]  
  
 快速分析将字符串输出为 DT_DBTIME 和 DT_DBTIME2。 对截断格式的时间值进行填充。 例如，HH:MI 变为 HH:MM:00.000。  
  
 有关详细信息，请参阅 [Integration Services 数据类型](data-flow/integration-services-data-types.md)。  
  
## <a name="datetime-data-type"></a>日期/时间数据类型  
 快速分析支持日期/时间数据的下列字符串格式：  
  
-   包含前导空格的格式。 例如，值“  2003-01-10T203910”有效。  
  
-   以大写字母 T 分隔的有效日期格式与有效时间格式以及有效时区格式的组合，例如 YYYYMMDDT[HHMISS][+HH:MI]。 时间和时区值不是必需的。 例如，“2003-10-14”有效。  
  
 快速分析不支持时间间隔。 例如，无法分析起始和结束日期和时间以 YYYYMMDDThhmmss/YYYYMMDDThhmmss 格式标识的时间间隔。  
  
 快速分析将字符串输出为 DT_DATE、DT_DBTIMESTAMP、DT_DBTIMESTAMP2 和 DT_DBTIMESTAMPOFFSET。 对截断格式的日期/时间值进行填充。 下表列出为缺少的日期和时间部分添加的值。  
  
|日期/时间部分|填充|  
|---------------------|-------------|  
|Seconds|添加 00。|  
|Minutes|添加 00:00。|  
|Hour|添加 00:00:00。|  
|Day|添加 01，表示一个月中的第几天。|  
|Month|添加 01，表示一年中的第几个月。|  
  
 有关详细信息，请参阅 [Integration Services 数据类型](data-flow/integration-services-data-types.md)。  
  
  
