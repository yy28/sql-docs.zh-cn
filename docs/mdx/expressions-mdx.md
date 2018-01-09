---
title: "表达式 (MDX) |Microsoft 文档"
ms.custom: 
ms.date: 03/02/2016
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: 
ms.component: 
ms.reviewer: 
ms.suite: pro-bi
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: language-reference
dev_langs: kbMDX
helpviewer_keywords:
- identifiers [MDX]
- expressions [MDX]
- expressions [MDX], about expressions
- MDX [Analysis Services], expressions
- Multidimensional Expressions [Analysis Services], expressions
ms.assetid: e20c34bc-30fa-4ac5-b896-9d4c9925ef59
caps.latest.revision: "37"
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: On Demand
ms.openlocfilehash: 0fbb0f5d2b1b9699cd468cbcbd81a528c217bd3a
ms.sourcegitcommit: f486d12078a45c87b0fcf52270b904ca7b0c7fc8
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/08/2018
---
# <a name="expressions-mdx"></a>表达式 (MDX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  表达式是标识符、 值和运算符的组合， [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]可以评估用于获取结果。 数据可在多个不同位置时访问或更改数据。 例如，可以将表达式用作查询要检索的数据的一部分，或用作查找满足一组条件的数据的搜索条件。  
  
## <a name="simple-and-complex-expressions"></a>简单表达式和复杂表达式  
 在 MDX 中，表达式可以是简单的，也可以是复杂的：  
  
 简单表达式可以是下列几种表达式之一：  
  
 常量  
 在 MDX 中，常量是表示单个特定值的符号。 字符串、数字和日期值可以呈现为常量。 与数值常量不同，字符串和日期常量必须用单引号 (') 字符分隔开。  
  
 标量函数  
 在 MDX 中，标量函数返回计算上下文内的单个值。 此区别对于理解 MDX 如何解析标量函数很重要，因为不是对单个数据元素计算大多数 MDX 表达式、语句和脚本，而是重复地对一组数据元素（如单元或成员）进行计算。 但在计算标量函数时，函数通常查看单个数据元素。  
  
 对象标识符  
 由于多维数据的本质，因此 MDX 是面向对象的。 在 MDX 中，对象标识符被视为简单表达式。 有关标识符的详细信息，请参阅[标识符 &#40;MDX &#41;](../mdx/identifiers-mdx.md).  
  
 可以从用运算符联接的这些实体的组合生成复杂表达式。  
  
## <a name="expression-results"></a>表达式结果  
 对于生成的单个常量、 变量、 标量函数或列名称的简单表达式，数据类型、 排序规则、 精度、 刻度和表达式的值是数据类型、 排序规则、 精度、 刻度和被引用元素的值。 因为 MDX 仅直接支持 OLE VARIANT 数据类型，所以使用简单表达式时不会发生强制。  
  
 对于复杂表达式，当使用两个或多个不同数据类型的简单表达式时，可以发生强制。  
  
## <a name="expression-examples"></a>表达式示例  
 以下查询说明其定义是简单表达式的计算度量值的示例：  
  
 `WITH`  
  
 `MEMBER MEASURES.CONSTANTVALUE AS 1`  
  
 `MEMBER MEASURES.SCALARFUNCTION AS [Date].[Calendar Year].CURRENTMEMBER.NAME`  
  
 `MEMBER MEASURES.OBJECTIDENTIFIER AS [Measures].[Internet Sales Amount]`  
  
 `SELECT {MEASURES.CONSTANTVALUE,MEASURES.SCALARFUNCTION,MEASURES.OBJECTIDENTIFIER } ON 0,`  
  
 `[Date].[Calendar Year].MEMBERS ON 1`  
  
 `FROM [Adventure Works]`  
  
 表达式还可以是计算，例如 `[Measures].[Discount Amount] * 1.5`。 下面的示例说明如何在 MDX SELECT 语句使用计算来定义成员：  
  
```  
WITH   
   MEMBER [Measures].[Special Discount] AS  
   [Measures].[Discount Amount] * 1.5  
SELECT   
   [Measures].[Special Discount] on COLUMNS,  
   NON EMPTY [Product].[Product].MEMBERS  ON Rows  
FROM [Adventure Works]  
WHERE [Product].[Category].[Bikes]  
```  
  
## <a name="in-this-section"></a>本节内容  
  
|主题|Description|  
|-----------|-----------------|  
|[使用多维数据集表达式和子多维数据集表达式](../mdx/using-cube-and-subcube-expressions.md)|定义多维数据集和子多维数据集表达式。|  
|[使用维度表达式](../mdx/using-dimension-expressions.md)|定义维度表达式。|  
|[使用成员表达式](../mdx/using-member-expressions.md)|定义成员表达式。|  
|[使用元组表达式](../mdx/using-tuple-expressions.md)|定义元组表达式。|  
|[使用集表达式](../mdx/using-set-expressions.md)|定义集表达式。|  
|[使用标量表达式](../mdx/using-scalar-expressions.md)|定义标量表达式。|  
|[处理空值](../mdx/working-with-empty-values.md)|说明什么是空值以及如何处理此类值。|  
  
## <a name="see-also"></a>另请参阅  
 [MDX 语言参考 &#40;MDX &#41;](../mdx/mdx-language-reference-mdx.md)   
 [MDX 查询基础知识 &#40;Analysis Services &#41;](../analysis-services/multidimensional-models/mdx/mdx-query-fundamentals-analysis-services.md)  
  
  
