---
title: "VisualTotals (MDX) |Microsoft 文档"
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
f1_keywords: VisualTotals
dev_langs: kbMDX
helpviewer_keywords: VisualTotals function
ms.assetid: 8ec529c2-729a-4a5b-892e-750849ab4013
caps.latest.revision: "36"
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: Inactive
ms.openlocfilehash: 3270bf4f47b4ceafe6d5e1479e870d0492c7c37b
ms.sourcegitcommit: f486d12078a45c87b0fcf52270b904ca7b0c7fc8
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/08/2018
---
# <a name="visualtotals-mdx"></a>VisualTotals (MDX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  返回通过动态计算指定集内子成员的合计而生成的集，可以选择在得到的结果集内为父成员名称应用某种模式。  
  
## <a name="syntax"></a>语法  
  
```  
  
VisualTotals(Set_Expression[,Pattern])  
```  
  
## <a name="arguments"></a>参数  
 *Set_Expression*  
 返回集的有效多维表达式 (MDX)。  
  
 *模式*  
 集中父成员的有效字符串表达式，包含星号 (*) 作为父名称的替代字符。  
  
## <a name="remarks"></a>Remarks  
 指定的集表达式可以指定包含单个维度内任何级别成员（通常是具有祖先-后代关系的成员）的集。 **VisualTotals**函数中指定集的子成员的值进行合计并忽略不在集合中计算结果总计的子成员。 直观地对以层次结构顺序排序的集计算总和。 如果集中成员的顺序违背了层次结构，则结果就不是直观合计了。 例如，VisualTotals (USA, WA, CA, Seattle) 不将 WA 返回为 Seattle，而返回 WA、CA 和 Seattle 的值，然后计算这些值的总和作为 USA 的直观合计，同时计算两次 Seattle 的销售额。  
  
> [!NOTE]  
>  应用**VisualTotals**到不相关的度量值或处于下的度量值组粒度的维度成员函数将导致值替换为 null。  
  
 *模式*，这是可选的指定总计标签的格式。 *模式*需要一个星号 （*），因为父成员和文本字符串中的其余部分的替换字符显示在父名称串接的结果。 若要显示原义星号，使用两个星号 (\*\*)。  
  
## <a name="examples"></a>示例  
 下面的示例根据所指定的一个后代 - 7 月，返回 2001 日历年第三季度的直观合计。  
  
```  
SELECT VisualTotals  
   ({[Date].[Calendar].[Calendar Quarter].&[2001]&[3]  
      ,[Date].[Calendar].[Month].&[2001]&[7]}) ON 0  
FROM [Adventure Works]  
```  
  
 下面的示例返回 Product 维度中 Category 属性层次结构的 [All] 成员及其四个子级中的两个。 对 Internet Sales Amount 度量值的 [All] 成员返回的合计是仅针对 Accessories 和 Clothing 成员的合计。 另外，模式参数用于指定 [All Products] 列的标签。   
  
```  
SELECT  
   VisualTotals  
   ({[Product].[Category].[All Products]  
      ,[Product].[Category].[Accessories]  
      ,[Product].[Category].[Clothing]}  
      , '* - Visual Total'  
   ) ON Columns  
, [Measures].[Internet Sales Amount] ON Rows  
FROM [Adventure Works]  
```  
  
## <a name="see-also"></a>另请参阅  
 [MDX 函数引用 &#40;MDX &#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
