---
title: 函数（SSIS 表达式）| Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- integration-services
ms.topic: conceptual
helpviewer_keywords:
- functions [Integration Services]
- expressions [Integration Services], functions
- string functions
- SQL Server Integration Services, functions
- SSIS, functions
ms.assetid: e9a41a31-94f4-46a4-b737-c707dd59ce48
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: d4e721c7dfddb953dd82952aa51c20550e5e60eb
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/02/2018
ms.locfileid: "48061247"
---
# <a name="functions-ssis-expression"></a>函数（SSIS 表达式）
  表达式语言包含一组用于表达式的函数。 表达式可以使用单个函数。但是，通常一个表达式可以通过运算符将多个函数组合起来，从而使用多个函数。  
  
 函数可以划分为以下几组：  
  
-   数学函数，根据作为参数提供给函数的数值输入值执行计算并返回数值。  
  
-   字符串函数，对字符串或十六进制输入值执行操作，并返回字符串或数值。  
  
-   日期和时间函数，对日期和时间值执行操作，并返回字符串、数值或日期和时间值。  
  
-   系统函数，返回有关表达式的信息。  
  
 表达式语言提供了下列数学函数。  
  
|函数|Description|  
|--------------|-----------------|  
|[ABS &#40;SSIS 表达式&#41;](abs-ssis-expression.md)|返回数值表达式的绝对值。|  
|[EXP &#40;SSIS 表达式&#41;](exp-ssis-expression.md)|返回指定表达式以 e 为底的指数。|  
|[CEILING &#40;SSIS 表达式&#41;](ceiling-ssis-expression.md)|返回大于或等于数值表达式的最小整数。|  
|[FLOOR &#40;SSIS 表达式&#41;](floor-ssis-expression.md)|返回小于或等于数值表达式的最大整数。|  
|[LN &#40;SSIS 表达式&#41;](ln-ssis-expression.md)|返回数值表达式的自然对数。|  
|[日志&#40;SSIS 表达式&#41;](log-ssis-expression.md)|返回数值表达式以 10 为底的对数。|  
|[POWER &#40;SSIS 表达式&#41;](power-ssis-expression.md)|返回对数值表达式进行幂运算的结果。|  
|[ROUND &#40;SSIS 表达式&#41;](round-ssis-expression.md)|返回舍入到指定长度或精度的数值表达式。 .|  
|[登录&#40;SSIS 表达式&#41;](sign-ssis-expression.md)|返回数值表达式的正号 (+)、负号 (-) 或零 (0)。|  
|[正方形&#40;SSIS 表达式&#41;](square-ssis-expression.md)|返回数值表达式的平方。|  
|[SQRT &#40;SSIS 表达式&#41;](sqrt-ssis-expression.md)|返回数值表达式的平方根。|  
  
 表达式计算器提供了下列字符串函数。  
  
|函数|Description|  
|--------------|-----------------|  
|[码位&#40;SSIS 表达式&#41;](codepoint-ssis-expression.md)|返回字符表达式最左端字符的 Unicode 代码值。|  
|[FINDSTRING &#40;SSIS 表达式&#41;](findstring-ssis-expression.md)|返回表达式中指定出现的字符串从 1 开始的索引。|  
|[HEX &#40;SSIS 表达式&#41;](hex-ssis-expression.md)|返回一个表示整数的十六进制值的字符串。|  
|[LEN &#40;SSIS 表达式&#41;](len-ssis-expression.md)|返回字符表达式中的字符数。|  
|[左&#40;SSIS 表达式&#41;](left-ssis-expression.md)|返回从给定字符表达式最左侧开始的指定数量的字符。|  
|[低&#40;SSIS 表达式&#41;](lower-ssis-expression.md)|返回将大写字符转换为小写字符后得到的字符表达式。|  
|[LTRIM &#40;SSIS 表达式&#41;](trim-ssis-expression.md)|返回删除了前导空格的字符表达式。|  
|[替换为&#40;SSIS 表达式&#41;](replace-ssis-expression.md)|返回用不同字符串或空字符串替换表达式中字符串后的字符表达式。|  
|[复制&#40;SSIS 表达式&#41;](replicate-ssis-expression.md)|返回复制了指定次数后的字符表达式。|  
|[反向&#40;SSIS 表达式&#41;](reverse-ssis-expression.md)|按相反顺序返回字符表达式。|  
|[右&#40;SSIS 表达式&#41;](right-ssis-expression.md)|返回从给定字符表达式最右侧开始的指定数量的字符。|  
|[RTRIM &#40;SSIS 表达式&#41;](rtrim-ssis-expression.md)|返回删除了尾随空格的字符表达式。|  
|[子字符串&#40;SSIS 表达式&#41;](substring-ssis-expression.md)|返回字符表达式的一部分。|  
|[剪裁&#40;SSIS 表达式&#41;](trim-ssis-expression.md)|返回删除了前导空格和尾随空格的字符表达式。|  
|[上限&#40;SSIS 表达式&#41;](upper-ssis-expression.md)|返回将小写字符转换为大写字符后得到的字符表达式。|  
  
 表达式计算器提供了下列日期和时间函数。  
  
|函数|Description|  
|--------------|-----------------|  
|[DATEADD &#40;SSIS 表达式&#41;](dateadd-ssis-expression.md)|通过将指定日期与一个日期或时间间隔相加，返回一个新的 DT_DBTIMESTAMP 值。|  
|[DATEDIFF &#40;SSIS 表达式&#41;](datediff-ssis-expression.md)|返回两个指定日期之间所跨的日期和时间边界的数目。|  
|[DATEPART &#40;SSIS 表达式&#41;](datepart-ssis-expression.md)|返回一个表示日期的日期部分的整数。|  
|[天&#40;SSIS 表达式&#41;](day-ssis-expression.md)|返回表示指定日期的“日”的整数。|  
|[GETDATE &#40;SSIS 表达式&#41;](getdate-ssis-expression.md)|返回系统的当前日期。|  
|[GETUTCDATE &#40;SSIS 表达式&#41;](getutcdate-ssis-expression.md)|返回以 UTC 时间（协调世界时或格林尼治标准时间）表示的系统当前日期。|  
|[月&#40;SSIS 表达式&#41;](month-ssis-expression.md)|返回表示指定日期的月份的整数。|  
|[年&#40;SSIS 表达式&#41;](year-ssis-expression.md)|返回表示指定日期的年份的整数。|  
  
 表达式计算器提供了下列空函数。  
  
|函数|Description|  
|--------------|-----------------|  
|[ISNULL &#40;SSIS 表达式&#41;](null-ssis-expression.md)|根据表达式是否为空，返回一个布尔值结果。|  
|[NULL &#40;SSIS 表达式&#41;](null-ssis-expression.md)|返回请求的数据类型的 Null 值。|  
  
 表达式名称以大写字符显示，但表达式名称并不区分大小写。 例如，使用“null”和使用“NULL”的作用是一样的。  
  
## <a name="see-also"></a>请参阅  
 [运算符&#40;SSIS 表达式&#41;](operators-ssis-expression.md)   
 [高级 Integration Services 表达式的示例](examples-of-advanced-integration-services-expressions.md)   
 [Integration Services (SSIS) 表达式](integration-services-ssis-expressions.md)  
  
  
