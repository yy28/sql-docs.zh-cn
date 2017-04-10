---
title: "函数（SSIS 表达式） | Microsoft Docs"
ms.custom: ""
ms.date: "03/01/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "integration-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "函数 [Integration Services]"
  - "表达式 [Integration Services], 函数"
  - "字符串函数 (string functions)"
  - "SQL Server Integration Services, 函数"
  - "SSIS, 函数"
ms.assetid: e9a41a31-94f4-46a4-b737-c707dd59ce48
caps.latest.revision: 36
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 36
---
# 函数（SSIS 表达式）
  表达式语言包含一组用于表达式的函数。 表达式可以使用单个函数。但是，通常一个表达式可以通过运算符将多个函数组合起来，从而使用多个函数。  
  
 函数可以划分为以下几组：  
  
-   数学函数，根据作为参数提供给函数的数值输入值执行计算并返回数值。  
  
-   字符串函数，对字符串或十六进制输入值执行操作，并返回字符串或数值。  
  
-   日期和时间函数，对日期和时间值执行操作，并返回字符串、数值或日期和时间值。  
  
-   系统函数，返回有关表达式的信息。  
  
 表达式语言提供了下列数学函数。  
  
|函数|Description|  
|--------------|-----------------|  
|[ABS（SSIS 表达式）](../../integration-services/expressions/abs-ssis-expression.md)|返回数值表达式的绝对值。|  
|[EXP（SSIS 表达式）](../../integration-services/expressions/exp-ssis-expression.md)|返回指定表达式以 e 为底的指数。|  
|[CEILING（SSIS 表达式）](../../integration-services/expressions/ceiling-ssis-expression.md)|返回大于或等于数值表达式的最小整数。|  
|[FLOOR（SSIS 表达式）](../../integration-services/expressions/floor-ssis-expression.md)|返回小于或等于数值表达式的最大整数。|  
|[LN（SSIS 表达式）](../../integration-services/expressions/ln-ssis-expression.md)|返回数值表达式的自然对数。|  
|[LOG（SSIS 表达式）](../../integration-services/expressions/log-ssis-expression.md)|返回数值表达式以 10 为底的对数。|  
|[POWER（SSIS 表达式）](../../integration-services/expressions/power-ssis-expression.md)|返回对数值表达式进行幂运算的结果。|  
|[ROUND（SSIS 表达式）](../../integration-services/expressions/round-ssis-expression.md)|返回舍入到指定长度或精度的数值表达式。 。|  
|[SIGN（SSIS 表达式）](../../integration-services/expressions/sign-ssis-expression.md)|返回数值表达式的正号 (+)、负号 (-) 或零 (0)。|  
|[SQUARE（SSIS 表达式）](../../integration-services/expressions/square-ssis-expression.md)|返回数值表达式的平方。|  
|[SQRT（SSIS 表达式）](../../integration-services/expressions/sqrt-ssis-expression.md)|返回数值表达式的平方根。|  
  
 表达式计算器提供了下列字符串函数。  
  
|函数|Description|  
|--------------|-----------------|  
|[CODEPOINT（SSIS 表达式）](../../integration-services/expressions/codepoint-ssis-expression.md)|返回字符表达式最左端字符的 Unicode 代码值。|  
|[FINDSTRING（SSIS 表达式）](../../integration-services/expressions/findstring-ssis-expression.md)|返回表达式中指定出现的字符串从 1 开始的索引。|  
|[HEX（SSIS 表达式）](../../integration-services/expressions/hex-ssis-expression.md)|返回一个表示整数的十六进制值的字符串。|  
|[LEN（SSIS 表达式）](../../integration-services/expressions/len-ssis-expression.md)|返回字符表达式中的字符数。|  
|[LEFT（SSIS 表达式）](../../integration-services/expressions/left-ssis-expression.md)|返回从给定字符表达式最左侧开始的指定数量的字符。|  
|[LOWER（SSIS 表达式）](../../integration-services/expressions/lower-ssis-expression.md)|返回将大写字符转换为小写字符后得到的字符表达式。|  
|[LTRIM（SSIS 表达式）](../../integration-services/expressions/ltrim-ssis-expression.md)|返回删除了前导空格的字符表达式。|  
|[REPLACE（SSIS 表达式）](../../integration-services/expressions/replace-ssis-expression.md)|返回用不同字符串或空字符串替换表达式中字符串后的字符表达式。|  
|[REPLICATE（SSIS 表达式）](../../integration-services/expressions/replicate-ssis-expression.md)|返回复制了指定次数后的字符表达式。|  
|[REVERSE（SSIS 表达式）](../../integration-services/expressions/reverse-ssis-expression.md)|按相反顺序返回字符表达式。|  
|[RIGHT（SSIS 表达式）](../../integration-services/expressions/right-ssis-expression.md)|返回从给定字符表达式最右侧开始的指定数量的字符。|  
|[RTRIM（SSIS 表达式）](../../integration-services/expressions/rtrim-ssis-expression.md)|返回删除了尾随空格的字符表达式。|  
|[SUBSTRING（SSIS 表达式）](../../integration-services/expressions/substring-ssis-expression.md)|返回字符表达式的一部分。|  
|[TRIM（SSIS 表达式）](../../integration-services/expressions/trim-ssis-expression.md)|返回删除了前导空格和尾随空格的字符表达式。|  
|[UPPER（SSIS 表达式）](../../integration-services/expressions/upper-ssis-expression.md)|返回将小写字符转换为大写字符后得到的字符表达式。|  
  
 表达式计算器提供了下列日期和时间函数。  
  
|函数|Description|  
|--------------|-----------------|  
|[DATEADD（SSIS 表达式）](../../integration-services/expressions/dateadd-ssis-expression.md)|通过将指定日期与一个日期或时间间隔相加，返回一个新的 DT_DBTIMESTAMP 值。|  
|[DATEDIFF（SSIS 表达式）](../../integration-services/expressions/datediff-ssis-expression.md)|返回两个指定日期之间所跨的日期和时间边界的数目。|  
|[DATEPART（SSIS 表达式）](../../integration-services/expressions/datepart-ssis-expression.md)|返回一个表示日期的日期部分的整数。|  
|[DAY（SSIS 表达式）](../../integration-services/expressions/day-ssis-expression.md)|返回表示指定日期的“日”的整数。|  
|[GETDATE（SSIS 表达式）](../../integration-services/expressions/getdate-ssis-expression.md)|返回系统的当前日期。|  
|[GETUTCDATE（SSIS 表达式）](../../integration-services/expressions/getutcdate-ssis-expression.md)|返回以 UTC 时间（协调世界时或格林尼治标准时间）表示的系统当前日期。|  
|[MONTH（SSIS 表达式）](../../integration-services/expressions/month-ssis-expression.md)|返回表示指定日期的月份的整数。|  
|[YEAR（SSIS 表达式）](../../integration-services/expressions/year-ssis-expression.md)|返回表示指定日期的年份的整数。|  
  
 表达式计算器提供了下列空函数。  
  
|函数|Description|  
|--------------|-----------------|  
|[ISNULL（SSIS 表达式）](../../integration-services/expressions/isnull-ssis-expression.md)|根据表达式是否为空，返回一个布尔值结果。|  
|[NULL（SSIS 表达式）](../../integration-services/expressions/null-ssis-expression.md)|返回请求的数据类型的 Null 值。|  
  
 表达式名称以大写字符显示，但表达式名称并不区分大小写。 例如，使用“null”和使用“NULL”的作用是一样的。  
  
## 另请参阅  
 [运算符（SSIS 表达式）](../../integration-services/expressions/operators-ssis-expression.md)   
 [高级 Integration Services 表达式的示例](../../integration-services/expressions/examples-of-advanced-integration-services-expressions.md)   
 [Integration Services (SSIS) 表达式](../../integration-services/expressions/integration-services-ssis-expressions.md)  
  
  