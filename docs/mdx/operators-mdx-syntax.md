---
title: 运算符 (MDX 语法) |Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 5067793ae0f5533a889973e18f7b300914df9092
ms.sourcegitcommit: a1adc6906ccc0a57d187e1ce35ab7a7a951ebff8
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/09/2019
ms.locfileid: "68892116"
---
# <a name="operators-mdx-syntax"></a>运算符（MDX 语法）


  在多维表达式 (MDX) 中，可以使用运算符执行下列操作：  
  
-   永久或临时更改数据。  
  
-   搜索满足指定条件的值或对象。  
  
-   在值或表达式之间进行判断。  
  
-   在开始或提交事务之前，或在执行特定语句之前测试特定条件。  
  
 MDX 支持下表中列出的运算符：  
  
|若要执行这种运算|改用|  
|---------------------------------------|---------|  
|将一个值赋给变量, 或将结果集列与别名相关联。|[赋值运算符](../mdx/assignment-operators.md)|  
|加法、减法、乘法、除法。|[算术运算符](../mdx/arithmetic-operators.md)|  
|测试某个条件（如 AND、OR、NOT 和 XOR）的真实性。|[位运算符](../mdx/bitwise-operators.md)|  
|将一个值与另一个值或表达式进行比较。|[比较运算符](../mdx/comparison-operators.md)|  
|永久或临时将两个字符串合并成一个字符串。|[串联运算符](../mdx/concatenation-operators.md)|  
|永久或临时将两个集表达式合并成一个集。|[集运算符](../mdx/set-operators.md)|  
|对一个操作数执行操作。|[一元运算符](../mdx/unary-operators.md)|  
  
> [!NOTE]  
>  在查询中，任何人只要能够查看多维数据集中要与某种运算符一起使用的数据，就可以执行操作。 但是，需要具有相应的权限才能成功更改数据。  
  
 同时使用多个运算符时，MDX 计算运算符的顺序非常重要。 同样，运算符的用户可能需要在计算运算符之前将一个数据类型转换为另一个数据类型。  
  
## <a name="evaluating-complex-expressions"></a>计算复杂表达式  
 可以通过使用运算符合并几个较小的表达式来生成一个表达式。 在这些复杂的表达式中, MDX 根据所使用[!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]的运算符优先级的定义, 按顺序计算运算符。 MDX 先计算具有较高优先级的运算符，后计算具有较低优先级的运算符。  
  
### <a name="understanding-operator-precedence"></a>了解运算符优先级  
 以下列表显示了运算符优先级，按从最高到最低的顺序排列。 位于同一行中的运算符具有相同的优先级，按从左到右的顺序进行计算，除非使用括号进行强制：  
  
-   IS  
  
-   方式  
  
-   DISTINCT  
  
-   :  
  
-   ^  
  
-   /, *  
  
-   +, -  
  
-   EXISTING  
  
-   <>, >=, =, \<=, >, <  
  
-   NOT  
  
-   和  
  
-   XOR  
  
-   或  
  
 有关 MDX 中的运算符的详细信息, 请参阅[Mdx &#40;运算符&#41;参考 mdx](../mdx/mdx-operator-reference-mdx.md)。  
  
### <a name="determining-results"></a>确定结果  
 将简单的表达式合并成复杂的表达式时，运算符的规则与数据类型优先级的规则一起决定结果值的数据类型。  
  
 如果结果是一个字符或 Unicode 值，则结果的排序规则由运算符的规则和排序优先级的规则一起决定。 有关排序规则的详细信息, 请参阅[语言&#40;和&#41;排序规则 Analysis Services](https://docs.microsoft.com/analysis-services/languages-and-collations-analysis-services)。  
  
 另外还有一些规则，根据简单表达式的精度、小数位数和长度来确定结果的精度、小数位数和长度。  
  
## <a name="converting-data-types"></a>转换数据类型  
 当在需要另一种对象类型的表达式中使用某种对象时，MDX 将把该对象隐式转换为另一种类型。 下表定义了每种对象的转换规则。  
  
|原始类型|所需类型|转换|  
|-------------------|-----------------|----------------|  
|级别|将|\<级别 > 成员|  
|层次结构|成员|\<层次结构 > defaultmember|  
|成员|Tuple|(\<成员 >)|  
|Tuple|成员|\<元组 > 项 (0)|  
|Tuple|Scalar|\<tuple>.value|  
  
## <a name="see-also"></a>请参阅  
 [MDX 运算符引用&#40;mdx&#41;](../mdx/mdx-operator-reference-mdx.md)   
 [MDX 语法元素&#40;mdx&#41;](../mdx/mdx-syntax-elements-mdx.md)  
  
  
