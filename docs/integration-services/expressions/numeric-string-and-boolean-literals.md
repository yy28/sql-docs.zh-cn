---
title: "文本 (SSIS) | Microsoft Docs"
ms.custom: 
ms.date: 11/16/2016
ms.prod: sql-non-specified
ms.prod_service: integration-services
ms.service: 
ms.component: expressions
ms.reviewer: 
ms.suite: sql
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- string literals
- numeric literals [Integration Services]
- Boolean literals
- expressions [Integration Services], literals
- literals [Integration Services]
- mapping literals [Integration Services]
ms.assetid: a980cd52-54ef-4b9c-b00c-e6807cf8e01f
caps.latest.revision: 
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: a89f9c1fde9d4a14776d37bc648341a5b5fa4aad
ms.sourcegitcommit: 7519508d97f095afe3c1cd85cf09a13c9eed345f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/15/2018
---
# <a name="numeric-string-and-boolean-literals"></a>数值、字符串和布尔型文字
 表达式可以包含数值、字符串和布尔文字。 表达式计算器支持多种数值，例如整数、小数和浮点常量。 表达式计算器还支持数值中包含科学记数法和指定表达式计算器如何处理值的 long 和 float 后缀。  
  
## <a name="numeric-literals"></a>数值  
 表达式计算器支持整型和非整型的数值数据类型。 它还支持包元素的唯一数值标识符 - 沿袭标识符。 沿袭标识符是数字，但不能用于数学运算。  
  
 表达式计算器支持后缀，您可以使用这些后缀来指示表达式计算器处理数值的方式。 例如，可以通过编写 37L 或 37l 来指示将整数 37 作为长整型数据类型处理。  
  
 下表列出了数值的后缀。  
  
|Suffix|Description|  
|------------|-----------------|  
|L 或 l|长整型数值。|  
|U 或 u|无符号数值。|  
|E 或 e|科学记数法中的指数|  
  
 下表列出了数值表达式元素及其正则表达式。  
  
|表达式元素|正则表达式|Description|  
|------------------------|------------------------|-----------------|  
|表示为 D 的数字。|[0-9]|任何数字。|  
|表示为 E 的科学记数法。|[Ee][+-]?{D}+|大写 E 或小写 e，+ 或 - 可选，D 根据自身的定义可以为一位数或多位数。|  
|表示为 IS 的整数后缀。|(([lL]?[uU]?)&#124;([uU]?[lL]?))|可以选择使用大写或小写 u 和 l 或 u 和 l 的组合。 U 或 u 指示无符号值。 L 或 l 指示长整型值。|  
|表示为 FS 的 float 后缀。|([f&#124;F]&#124;[l&#124;L])|大写或小写 f 或 l。 F 或 f 指示浮点值（DT_R4 数据类型）。 L 或 l 指示长整型值（DT_R8 数据类型）。|  
|表示为 H 的十六进制数字。|[a-fA-F0-9]|任何十六进制数字。|  
  
 下表介绍了使用正则表达式语言的有效数值。  
  
|正则表达式|Description|  
|------------------------|-----------------|  
|{D}+{IS}|一个整型数值，具有至少一个数字 (D)，还可以包含长整型和/或无符号后缀 (IS)。  示例：457、785u、986L 和 7945ul。|  
|{D}+{E}{FS}|一个非整型数值，具有至少一个数字 (D)、科学计数法和 long 或 float 后缀。  示例：4E8l、13e-2f 和 5E+L。|  
|{D}*"."{D}+{E}?{FS}|一个包含小数位的非整型数值，具有至少有一个数字 (D) 的小数部分、一个指数 (E)（可选）和一个 float 或 long 标识符 (FS)。 此数值的数据类型为 DT_R4 或 DT_R8。  示例：6.45E3f、.89E-2l 和 1.05E+7F。|  
|{D}+"."{D}*{E}?{FS}|一个非整型数值，具有至少一个有效数字 (D)、一个小数位、一个指数 (E) 和一个 float 或 long 标识符 (FS)。 此数值的数据类型为 DT_R4 或 DT_R8。  示例：1.E-4f、4.6E6L 和 8.365E+2f。|  
|{D}*.{D}+|具有一定精度和小数位数的非整型数值。 它具有一个小数位和带有至少一个数字 (D) 的小数部分。 此数值的数据类型为 DT_NUMERIC。  示例：.9、5.8 和 0.346。|  
|{D}+.{D}*|具有一定精度和小数位数的非整型数值。 它至少具有一个有效数字 (D) 和一个小数位。 此数值的数据类型为 DT_NUMERIC。  示例：6.、0.2 和 8.0。|  
|#{D}+|沿袭标识符。 它由井号 (#) 字符和至少一个数字 (D) 组成。 示例：#123。|  
|0[xX]{H}+{uU}|以十六进制格式表示的数值。 其中包含一个零、一个大写或小写 x、至少一个大写 H 和无符号后缀（可选）。 示例：0xFF0A 和 0X000010000U。|  
  
 有关表达式计算器所使用的数据类型的详细信息，请参阅 [Integration Services 数据类型](../../integration-services/data-flow/integration-services-data-types.md)。  
  
 表达式中可以包含具有不同数据类型的数值。 当表达式计算器计算这些表达式时，会将数据转换为兼容的类型。 有关详细信息，请参阅 [Integration Services Data Types in Expressions](../../integration-services/expressions/integration-services-data-types-in-expressions.md)。  
  
 但是，一些数据类型间的转换要求显式转换。 表达式计算器提供了用于执行显式数据类型转换的转换运算符。 有关详细信息，请参阅[转换（SSIS 表达式）](../../integration-services/expressions/cast-ssis-expression.md)。  
  
### <a name="mapping-numeric-literals-to-integration-services-data-types"></a>将数值映射为 Integration Services 数据类型  
 在计算数值时，表达式计算器执行下列转换：  
  
-   将整数数值映射为整数数据类型，如下所示。  
  
    |Suffix|结果类型|  
    |------------|-----------------|  
    |InclusionThresholdSetting|DT_I4|  
    |U|DT_UI4|  
    |L|DT_I8|  
    |UL|DT_UI8|  
  
    > **重要说明！！** 如果没有 long（L 或 l）后缀，表达式计算器会将有符号值映射为 DT_I4 数据类型，将无符号值映射为 DT_UI4 数据类型（即使值溢出了该数据类型）。  
  
-   包含指数的数值将被转换为 DT_R4 或 DT_R8 数据类型。 如果表达式包含 long 后缀，则被转换为 DT_R8；如果包含 float 后缀，则被转换为 DT_R4 数据类型。  
  
-   如果非整型数值包含 F 或 f，则映射为 DT_R4 数据类型。 如果它包含 L 或 l，并且该数字为整数，则映射为 DT_I8 数据类型。 如果为实数，则映射为 DT_R8 数据类型。 如果它包含 long 后缀，则将转换为 DT_R8 数据类型。  
  
-   具有精度和小数位数的非整型数值将映射为 DT_NUMERIC 数据类型。  
  
## <a name="string-literals"></a>字符串文字  
 字符串文字必须用引号引起来。 表达式语言为常用转义字符（如非打印字符和引号）提供了一组转义序列。  
  
 字符串文字由零个或多个被引号引起来的字符组成。 如果字符串中包含引号，则必须将这些引号转义，以便分析表达式。 字符串中允许使用除 \x0000 之外的任何双字节字符，因为 \x0000 字符是字符串的空终止符。  
  
 字符串中可包括需要转义序列的其他字符。 下表列出了字符串文字的转义序列。  
  
|转义序列|Description|  
|---------------------|-----------------|  
|\a|警报|  
|\b|退格键|  
|\f|换页符|  
|\n|换行符|  
|\r|回车符|  
|\t|水平制表符|  
|\v|垂直制表符|  
|\\"|引号|  
|\\\|反斜杠|  
|\xhhhh|十六进制表示的 Unicode 字符|  
  
## <a name="boolean-literals"></a>布尔值文字  
 表达式计算器支持常用的布尔值文字： **True** 和 **False**。 表达式计算器不区分大小写，任何大写和小写字母的组合都是允许的。 例如，TRUE 和 True 的作用是一样的。  
  
> **注意：** 在表达式中，布尔值文字必须用空格分隔。  
  
  
