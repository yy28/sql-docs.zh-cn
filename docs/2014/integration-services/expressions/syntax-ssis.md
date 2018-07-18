---
title: 语法 (SSIS) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- integration-services
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- expressions [Integration Services], syntax
- syntax [Integration Services]
ms.assetid: 61c053c5-1182-4ad0-b804-51cbd19aa0ba
caps.latest.revision: 46
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 8678b9909756d89a3a5bb11c2691aaacfc828f09
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/02/2018
ms.locfileid: "37269375"
---
# <a name="syntax-ssis"></a>语法 (SSIS)
  [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 表达式语法与 C 和 C# 语言使用的语法类似。 表达式可包括多种元素，例如标识符（列和变量）、文字、运算符和函数。 本主题概述了表达式计算器语法在应用于不同的表达式元素时的特殊要求。  
  
> [!NOTE]  
>  在以前版本的 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]中，如果某表达式的计算结果具有 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 数据类型 DT_WSTR 或 DT_STR，则结果将具有 4000 个字符的限制。 这一限制已被取消。  
  
 有关使用特定运算符和函数的示例表达式，请参阅以下主题中关于每个运算符和函数的主题：[运算符（SSIS 表达式）](operators-ssis-expression.md)和[函数（SSIS 表达式）](functions-ssis-expression.md)。  
  
 有关使用多个运算符和函数以及标识符和文本的示例表达式，请参阅[高级 Integration Services 表达式的示例](examples-of-advanced-integration-services-expressions.md)。  
  
 有关要在属性表达式中使用的示例表达式，请参阅 [在包中使用属性表达式](use-property-expressions-in-packages.md)。  
  
## <a name="identifiers"></a>标识符  
 表达式可包含列和变量标识符。 列可以源自数据源或由数据流中的转换创建。 表达式可以使用沿袭标识符来引用列。 沿袭标识符是唯一地标识包元素的数字。 表达式中引用的沿袭标识符必须包含井号 (#) 前缀。 例如，使用 #138 引用沿袭标识符 138。  
  
 表达式可包含 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 提供的系统变量和自定义变量。 在表达式中引用的变量必须包含 @ 前缀。 例如，使用 @Counter 引用 `Counter` 变量。 @ 字符不是变量名的一部分，它仅向表达式计算器指示该标识符是一个变量。 有关详细信息，请参阅[标识符 (SSIS)](identifiers-ssis.md)。  
  
## <a name="literals"></a>文字  
 表达式可以包含数值、字符串和布尔文字。 表达式中使用的字符串文字必须用引号引起来。 数值和布尔文字不使用引号。 表达式语言包含用于常用转义字符的转义序列。 有关详细信息，请参阅[文字 (SSIS)](numeric-string-and-boolean-literals.md)。  
  
## <a name="operators"></a>运算符  
 表达式计算器提供了一组运算符，这些运算符可提供与 Transact-SQL、C++ 和 C# 等语言中的运算符集类似的功能。 但是，表达式语言还包含其他运算符，并使用您可能不熟悉的其他符号。 有关详细信息，请参阅[运算符（SSIS 表达式）](operators-ssis-expression.md)。  
  
### <a name="namespace-resolution-operator"></a>命名空间解析运算符  
 表达式使用命名空间解析运算符 (::) 来消除同名变量的歧义。 通过使用命名空间解析运算符，您可以用变量的命名空间来限定变量，从而可以在一个包中使用多个同名变量。  
  
#### <a name="cast-operator"></a>转换运算符  
 转换运算符将表达式结果、列值、变量值和常量从一种数据类型转换为另一种数据类型。 表达式语言提供的转换运算符与 C 和 C# 语言提供的运算符类似。 在 Transact-SQL 中，CAST 和 CONVERT 函数提供了此功能。 转换运算符语法与 CAST 和 CONVERT 使用的语法在下列方面存在差别：  
  
-   可将表达式用作参数。  
  
-   其语法不包含 CAST 关键字。  
  
-   其语法不包含 AS 关键字。  
  
##### <a name="conditional-operator"></a>条件运算符  
 条件运算符基于布尔表达式的值返回两个表达式之一。 表达式语言提供的条件运算符与 C 和 C# 语言提供的运算符类似。 在多维表达式 (MDX) 中，IIF 函数提供类似的功能。  
  
###### <a name="logical-operators"></a>逻辑运算符  
 表达式语言支持逻辑非运算符的 ! 字符。 在 Transact-SQL 中，! 运算符 内置于关系运算符集中。 例如，Transact-SQL 提供 > 和 !> 运算符。 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 表达式语言不支持 ! 运算符与 其他运算符的组合。 例如，将 ! 和 > 组合为 !> 是 无效的。 但是，表达式语言支持用于“不等于”比较的内置 != 字符组合。  
  
###### <a name="equality-operators"></a>相等运算符  
 表达式计算器语法提供 == 相等运算符。 此运算符等价于 Transact-SQL 中的 = 运算符和 C# 中的 == 运算符。  
  
## <a name="functions"></a>函数  
 表达式语言包含类似于 Transact-SQL 函数和 C# 方法的日期和时间函数、数学函数及字符串函数。  
  
 一些函数具有与 Transact-SQL 函数相同的名称，但在表达式计算器中，功能稍有不同。  
  
-   在 Transact-SQL 中，ISNULL 函数将 Null 值替换为指定值，而表达式计算器的 ISNULL 函数则根据表达式是否为 Null 返回布尔值。  
  
-   在 Transact-SQL 中，ROUND 函数提供截断结果集的选项，而表达式计算器的 ROUND 函数则不提供。  
  
 有关详细信息，请参阅[函数（SSIS 表达式）](functions-ssis-expression.md)。  
  
## <a name="related-tasks"></a>Related Tasks  
 [在数据流组件中使用表达式](../use-an-expression-in-a-data-flow-component.md)  
  
## <a name="related-content"></a>相关内容  
  
-   pragmaticworks.com 上的技术文章 [SSIS 表达式小抄表](http://go.microsoft.com/fwlink/?LinkId=217683)。  
  
-   social.technet.microsoft.com 上的技术文章 [SSIS 表达式示例](http://go.microsoft.com/fwlink/?LinkId=220761)  
  
  
