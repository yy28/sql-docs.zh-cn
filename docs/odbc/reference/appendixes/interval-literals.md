---
title: 间隔文本 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- data types [ODBC], interval data types
- interval literals [ODBC]
- interval data type [ODBC], literals
ms.assetid: f9e6c3c7-4f98-483f-89d8-ebc5680f021b
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: cc5d09bca83724bb956d39512c51c3dc47db1bad
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63188802"
---
# <a name="interval-literals"></a>间隔文本
ODBC 需要的所有驱动程序支持 SQL_CHAR 或 SQL_VARCHAR 数据类型转换为所有的 C 间隔数据类型。 如果基础数据源不支持 interval 数据类型，但是，需要知道 SQL_CHAR 字段中的值的正确格式，才能支持这些转换该驱动程序。 同样，ODBC 要求应具有任何 ODBC C 类型可以转换为 SQL_CHAR 或 SQL_VARCHAR，因此，驱动程序需要知道何种格式存储在字符字段中的时间间隔。 本部分介绍间隔文字，驱动程序编写器需要使用在到或从 C 间隔数据类型转换过程中验证 SQL_CHAR 字段的语法。  
  
> [!NOTE]  
>  间隔文本的完整 BNF 语法节所示[间隔文本语法](../../../odbc/reference/appendixes/interval-literal-syntax.md)附录 c： 驱动器中SQL 语法。  
  
 若要将间隔文本传递作为 SQL 语句的一部分，为间隔文本定义了转义子句语法。 有关详细信息，请参阅[日期、 时间和时间戳文本](../../../odbc/reference/develop-app/date-time-and-timestamp-literals.md)。  
  
 间隔文本的形式：  
  
```  
INTERVAL[<sign>] 'value' <interval qualifier>  
```  
  
 其中"间隔"表示字符文本是一个时间间隔。 符号可以是加号或减号;它是外部的时间间隔字符串，并是可选的。  
  
 间隔限定符可以为单个日期时间字段或窗体中的两个日期时间字段的组合： \<*前导字段*> TO \<*尾部字段*>。  
  
-   当时间间隔由单个字段组成时，单个字段可以是可选的括号中的前导精度可能伴随的非第二个字段。 单个的日期时间字段也可以是可能伴随的可选前导精度、 在括号中的可选小数秒精度或这两者的第二个字段。 如果前导精度和小数秒精度的秒字段存在，它们是逗号分隔。 如果第二个字段具有小数秒精度，它必须还具有前导精度。  
  
-   时间间隔由前导和尾部字段组成，前导字段时，在括号中前导字段精度的时间间隔可能附带的非第二个字段。 尾随的字段可以为非第二个字段或可能伴随时间间隔的秒的小数部分精度在括号中的第二个字段。  
  
 中的时间间隔字符串*值*括在单引号内。 它可以是年-月文字或日期时间文字。 在字符串的格式*值*由以下规则：  
  
-   该字符串包含暗示着每个字段的一个十进制值\<*间隔**限定符*>。  
  
-   如果时间间隔精度包括年份和月份的字段，这些字段的值由负号分隔。  
  
-   如果时间间隔精度包括日期和小时的字段，这些字段的值由空格分隔。  
  
-   如果时间间隔精度包括字段小时和较低的顺序字段 （分钟和秒），这些字段的值由冒号分隔。  
  
-   时间间隔精度包含第二个字段，并且的明示或默示的秒精度为非零值，如果之前的秒的小数部分的第一个数字的字符为句点。  
  
-   没有字段可以是两个以上位数，除外：  
  
    -   前导字段的值可以是只要明示或默示间隔起始精度。  
  
    -   第二个字段的小数部分可以是只要明示或默示的秒精度。  
  
    -   尾部字段按照常用公历的约束。 (请参阅[公历的约束](../../../odbc/reference/appendixes/constraints-of-the-gregorian-calendar.md)。)  
  
 下表列出了有效间隔文本为间隔的 ODBC 转义子句一部分的示例。 Escape 子句的语法如下所示：  
  
> [!NOTE]  
>  *{间隔登录时间间隔字符串间隔限定符}*  
  
|文字的转义子句|指定时间间隔|  
|---------------------------|------------------------|  
|{INTERVAL '326' YEAR(4)}|指定 326 年的时间间隔。 间隔起始精度为 4。|  
|{INTERVAL '326' MONTH(3)}|指定 326 几个月的时间间隔。 间隔起始精度为 3。|  
|{INTERVAL '3261' DAY(4)}|指定 3261 天的间隔。 间隔起始精度为 4。|  
|{INTERVAL '163' HOUR(3)}|指定 163 天的间隔。 间隔起始精度为 3。|  
|{间隔"163"MINUTE(3)}|指定 163 分钟的间隔。 间隔起始精度为 3。|  
|{INTERVAL '223.16' SECOND(3,2)}|指定 223.16 秒的间隔。 时间间隔前导精度为 3，并且秒精度为 2。|  
|{为月间隔"163-11 YEAR(3)}|指定 163 年 11 个月的时间间隔。 间隔起始精度为 3。|  
|{INTERVAL '163 12' DAY(3) TO HOUR}|指定 163 天 12 小时的间隔。 间隔起始精度为 3。|  
|{INTERVAL '163 12:39' DAY(3) TO MINUTE}|指定 163 天，12 小时和 39 分钟的间隔。 间隔起始精度为 3。|  
|{INTERVAL '163 12:39:59.163' DAY(3) TO SECOND(3)}|指定 163 天，12 小时，39 分和 59.163 秒的间隔。 时间间隔前导精度为 3，并且秒精度为 3。|  
|{INTERVAL '163:39' HOUR(3) TO MINUTE}|指定 163 小时 39 分钟的间隔。 间隔起始精度为 3。|  
|{INTERVAL '163:39:59.163' HOUR(3) TO SECOND(4)}|指定 163 小时，39 分钟和 59.163 秒的间隔。 间隔前导精度为 3，而秒的精度为 4。|  
|{INTERVAL '163:59.163' MINUTE(3) TO SECOND(5)}|指定 163 分钟 59.163 秒的间隔。 时间间隔前导精度为 3，和秒的精度为 5。|  
|{间隔-"16 23:39:56.23"一天到第二个}|指定减去 16 天，23 小时，39 分和 56.23 秒的间隔。 隐含的前导精度为 2，并暗示的秒的精度是 6。|  
  
 下表列出了无效的间隔文本的示例：  
  
|文字的转义子句|原因无效的原因|  
|---------------------------|------------------------|  
|{INTERVAL '163' HOUR(2)}|间隔前导精度为 2，但 163 前导字段的值。|  
|{INTERVAL '223.16' SECOND(2,2)}<br /><br /> {INTERVAL '223.16' SECOND(3,1)}|在第一个示例中，前导精度为太小，并且在第二个示例中，秒的精度太小。|  
|{INTERVAL '223.16' SECOND}<br /><br /> {INTERVAL '223' YEAR}|前导精度未指定，因为它默认为 2，这是太小而无法保存指定的文本。|  
|{INTERVAL '22.1234567' SECOND}|秒的精度是未指定的因此它将默认为 6。 文本在小数点后具有 7 位。|  
|{为月间隔"163-13' YEAR(3)}<br /><br /> {INTERVAL '163 65' DAY(3) TO HOUR}<br /><br /> {INTERVAL '163 62:39' DAY(3) TO MINUTE}<br /><br /> {INTERVAL '163 12:125:59.163' DAY(3) TO SECOND(3)}<br /><br /> {INTERVAL '163:144' HOUR(3) TO MINUTE}<br /><br /> {INTERVAL '163:567:234.163' HOUR(3) TO SECOND(4)}<br /><br /> {间隔"163:591.163"到 SECOND(5) MINUTE(3)}|尾随的字段不遵循公历日历以来的规则。|
