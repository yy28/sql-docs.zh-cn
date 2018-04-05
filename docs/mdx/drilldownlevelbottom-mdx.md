---
title: DrilldownLevelBottom (MDX) |Microsoft 文档
ms.custom: ''
ms.date: 03/02/2016
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: ''
ms.component: ''
ms.reviewer: ''
ms.suite: pro-bi
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- DRILLDOWNLEVELBOTTOM
dev_langs:
- kbMDX
helpviewer_keywords:
- DrilldownLevelBottom function
ms.assetid: c00a6a02-e618-4713-805a-870e042f2d51
caps.latest.revision: 37
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: Inactive
ms.openlocfilehash: 0811bbd1e0f3cf81ebe87ff200906e2489036092
ms.sourcegitcommit: f486d12078a45c87b0fcf52270b904ca7b0c7fc8
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/08/2018
---
# <a name="drilldownlevelbottom-mdx"></a>DrilldownLevelBottom (MDX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  将集中某一指定级别上的最底层成员深化到下一个级别。  
  
## <a name="syntax"></a>语法  
  
```  
DrilldownLevelBottom(Set_Expression, Count [,[<Level_Expression>] [,[<Numeric_Expression>][,INCLUDE_CALC_MEMBERS]]])  
```  
  
## <a name="arguments"></a>参数  
 *Set_Expression*  
 返回集的有效多维表达式 (MDX)。  
  
 *计数*  
 指定要返回的元组数的有效数值表达式。  
  
 *Level_Expression*  
 返回级别的有效多维表达式 (MDX)。  
  
 *Numeric_Expression*  
 可选。 返回数字的有效数值表达式，通常为单元坐标的多维表达式 (MDX)。  
  
 *Include_Calc_Members*  
 可选。 将计算成员添加到深化结果的关键字。  
  
## <a name="remarks"></a>Remarks  
 如果指定数值表达式，则**DrilldownLevelBottom**函数以升序排序，在指定组中，根据指定的值，每个成员的子级，如对子成员组成的集求值排序。 如果未指定数值表达式，则此函数根据由查询上下文决定的子成员集所表示的单元的值，对指定的集中每个成员的子成员按升序排序。此行为类似于 BottomCount 和 Tail (MDX) 函数，都以自然顺序返回一组成员，没有任何排序。  
  
 排序之后, **DrilldownLevelBottom**函数返回一组包含父成员和中指定的子成员数*计数*，最低值。  
  
 **DrilldownLevelBottom**函数是类似于[DrilldownLevel](../mdx/drilldownlevel-mdx.md)函数，但而不是包含在指定的级别中，每个成员的所有子级**DrilldownLevelBottom**函数返回子成员的最底部的数目。  
  
 查询的 XMLA 属性 MdpropMdxDrillFunctions，您可以验证服务器提供钻函数; 支持的级别请参阅[支持 XMLA 属性 &#40;XMLA &#41;](../analysis-services/xmla/xml-elements-properties/propertylist-element-supported-xmla-properties.md)有关详细信息。  
  
## <a name="examples"></a>示例  
 下面的示例将根据默认度量值返回产品类别级别的最后三个子成员。 在 Adventure Works 示例多维数据集中，Accessories 的最后三个子成员是 Tires and Tubes、Pumps 和 Panniers。 在 Management Studio 的 MDX 查询窗口中，你可导航到“产品 | 产品类别 | 成员 | 所有产品 | 附件”查看完整的列表。 你可增加计数参数以返回更多成员。  
  
```  
SELECT DrilldownLevelBottom   
   ([Product].[Product Categories].children,  
   3,  
   [Product].[Product Categories].[Category])  
   ON 0  
   FROM [Adventure Works]  
```  
  
 下一个示例演示如何使用**include_calc_members**标志，用于在向级别下钻取中包含计算的成员。 度量值 [分销商订单计数] 添加到**DrilldownLevelBottom**语句来确保对结果进行排序由该度量值。 要查看计算成员，必须将计数至少增加到 9。  
  
```  
WITH MEMBER   
[Product].[Product Categories].[Category].&[3].[Premium Clothes] AS  
[Product].[Product Categories].[Subcategory].&[18] +  
[Product].[Product Categories].[Subcategory].&[21]  
SELECT [Measures].[Reseller Order Count] ON 0,  
DRILLDOWNLEVELBOTTOM(  
  [Product].[Product Categories].children ,  
  9,  
  [Product].[Product Categories].[Category] ,  
  [Measures].[Reseller Order Count],  
  INCLUDE_CALC_MEMBERS ) ON 1  
FROM [Adventure Works]  
```  
  
## <a name="see-also"></a>另请参阅  
 [DrilldownLevel &#40;MDX &#41;](../mdx/drilldownlevel-mdx.md)   
 [MDX 函数引用 &#40;MDX &#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
