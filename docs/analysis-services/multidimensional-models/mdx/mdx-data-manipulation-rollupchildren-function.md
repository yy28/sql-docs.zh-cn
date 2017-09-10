---
title: "使用 RollupChildren 函数 (MDX) |Microsoft 文档"
ms.custom: 
ms.date: 03/16/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
- analysis-services/multidimensional-tabular
- analysis-services/data-mining
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- queries [MDX], RollupChildren function
- RollupChildren function
- custom member properties [MDX]
- IIf function
ms.assetid: 03c624d4-f277-451d-9995-623a07ea2f86
caps.latest.revision: 27
author: Minewiskan
ms.author: owend
manager: erikre
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: aa1200dd746dcb1ffc7ae7372b0d85a3d60d49f2
ms.contentlocale: zh-cn
ms.lasthandoff: 09/01/2017

---
# <a name="mdx-data-manipulation---rollupchildren-function"></a>MDX 数据操作-RollupChildren 函数
  多维表达式 (MDX) [RollupChildren](../../../mdx/rollupchildren-mdx.md) 函数可以汇总某个成员的子级（对每个子级应用不同的一元运算符），并以数字的形式返回此汇总值。 一元运算符可通过与子成员关联的成员属性提供，也可以是直接提供给函数的字符串表达式。  
  
## <a name="rollupchildren-function-examples"></a>RollupChildren 函数示例  
 **RollupChildren** 函数在多维表达式 (MDX) 语句中的用法很容易理解，但它对 MDX 查询的影响十分广泛。  
  
 **RollupChildren** 函数的影响体现在为对现有多维数据集数据执行选择性分析而设计的 MDX 查询中。 例如，下表包含“净销售额”父成员的子成员列表，子成员的一元运算符（由 **UNARY_OPERATOR** 成员属性表示）显示在括号内。  
  
|父成员|子成员 (Child member)|  
|-------------------|------------------|  
|净销售额|国内销售额 (+)<br /><br /> 国内盈利 (-)<br /><br /> 国外销售额 (+)<br /><br /> 国外盈利 (-)|  
  
 “净销售额”父成员当前等于总净销售额减去国内和国外总销售额，并在汇总过程中减去国内和国外盈利。  
  
 但是，您希望提供国内和国外总销售额加 10% 的快速预测（忽略国内盈利和国外盈利）。 若要计算此值，可以按下列两种方式之一使用 **RollupChildren** 函数：使用自定义成员属性或使用 **IIf** 函数。  
  
### <a name="using-a-custom-member-property"></a>使用自定义成员属性  
 如果经常要进行汇总计算，一种方法是创建一个成员属性，以存储特定函数的每个子级要使用的运算符。 下表显示了有效的一元运算符并说明了预期的结果。  
  
|运算符|结果|  
|--------------|------------|  
|+|total = total + current child|  
|-|总额 = 总额 - 当前子级|  
|*|total = total * current child|  
|/|total = total / current child|  
|~|不在汇总中使用子级。 子级的值将被忽略。|  
  
 例如，可以创建名为 **SALES_OPERATOR** 的成员属性并为其分配下列一元运算符，如下表所示。  
  
|父成员|子成员 (Child member)|  
|-------------------|------------------|  
|净销售额|国内销售额 (+)<br /><br /> 国内盈利 (~)<br /><br /> 国外销售额 (+)<br /><br /> 国外盈利 (~)|  
  
 通过这个新的成员属性，可使用下列 MDX 语句快速有效地估算出总销售额（忽略国内盈利和国外盈利）：  
  
```  
RollupChildren([Net Sales], [Net Sales].CurrentMember.Properties("SALES_OPERATOR")) * 1.1  
```  
  
 当调用函数时，使用该成员属性中存储的运算符将每个子级的值应用于总数。 将忽略国内盈利和国外盈利的成员，并将 **RollupChildren** 函数返回的汇总总数乘以 1.1。  
  
### <a name="using-the-iif-function"></a>使用 IIf 函数  
 如果示例操作不常发生或者只适用于一个 MDX 查询，则可以将 [IIf](../../../mdx/iif-mdx.md) 函数与 **RollupChildren** 函数一起使用，以提供相同的结果。 下列 MDX 查询提供的结果与前面的 MDX 示例相同，但这里没有使用自定义成员属性：  
  
```  
RollupChildren([Net Sales], IIf([Net Sales].CurrentMember.Properties("UNARY_OPERATOR") = "-", "~", [Net Sales].CurrentMember.Properties("UNARY_OPERATOR))) * 1.1  
```  
  
 MDX 语句检查子成员的一元运算符。 如果一元运算符用于减法（正如在考虑国内盈利和国外盈利成员的情况下）， **IIf** 函数将替代一元运算符 (~)。 否则， **IIf** 函数将使用子成员的一元运算符。 最后，将所返回的汇总总数乘以 1.1，得出国内和国外总销售额的预测值。  
  
## <a name="see-also"></a>另请参阅  
 [操作数据 (MDX)](../../../analysis-services/multidimensional-models/mdx/mdx-data-manipulation-manipulating-data.md)  
  
  
