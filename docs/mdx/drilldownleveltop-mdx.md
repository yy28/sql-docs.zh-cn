---
description: DrilldownLevelTop (MDX)
title: DrilldownLevelTop (MDX) |Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: d0bb64acad5e29ff6eed5570e8764fd6a76a7547
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/17/2020
ms.locfileid: "88500510"
---
# <a name="drilldownleveltop-mdx"></a>DrilldownLevelTop (MDX)


  将集中某一指定级别上最顶端的成员深化到下一个级别。  
  
## <a name="syntax"></a>语法  
  
```  
  
DrilldownLevelTop(<Set_Expression>, <Count> [,[<Level_Expression>] [,[<Numeric_Expression>][,INCLUDE_CALC_MEMBERS]]])  
  
```  
  
## <a name="arguments"></a>参数  
 *Set_Expression*  
 返回集的有效多维表达式 (MDX)。  
  
 *Count*  
 指定要返回的元组数的有效数值表达式。  
  
 *Level_Expression*  
 返回级别的有效多维表达式 (MDX)。  
  
 *Numeric_Expression*  
 返回数字的有效数值表达式，通常为单元坐标的多维表达式 (MDX)。  
  
 *Include_Calc_Members*  
 用于将计算成员添加到深化结果的关键字。  
  
## <a name="remarks"></a>备注  
 如果指定了数值表达式，则 **DrilldownLevelTop** 函数将根据数值表达式的值以降序顺序对指定集内每个成员的子成员进行排序。 如果未指定数值表达式，则此函数根据由查询上下文确定的子成员集所表示的单元值，对指定集中每个成员的子成员按降序排序。  
  
 排序后， **DrilldownLevelTop** 函数将返回一个集，该集包含父成员以及在 *Count* 中指定的具有最高值的子成员数。  
  
 **DrilldownLevelTop**函数类似于[DrilldownLevel](../mdx/drilldownlevel-mdx.md)函数，但**DrilldownLevelTop**函数将返回最顶层的子成员数，而不是将每个成员的所有子级都包含在指定级别。  
  
 通过查询 XMLA 属性 MdpropMdxDrillFunctions，可以验证服务器为钻取函数提供的支持级别;有关详细信息，请参阅 [&#40;xmla&#41;支持的 Xmla 属性 ](https://docs.microsoft.com/analysis-services/xmla/xml-elements-properties/propertylist-element-supported-xmla-properties) 。  
  
## <a name="examples"></a>示例  
 下面的示例根据默认度量值返回产品类别级别的前三个子成员。 在 Adventure Works 示例多维数据集中，Accessories 的前三个子成员是Bike Racks、Bike Stands 和 Bottles and Cages。 在 Management Studio 的 MDX 查询窗口中，你可导航到“产品 | 产品类别 | 成员 | 所有产品 | 附件”查看完整的列表。 你可增加计数参数以返回更多成员。  
  
```  
SELECT DrilldownLevelTop   
   ([Product].[Product Categories].children,  
   3,  
   [Product].[Product Categories].[Category])  
   ON 0  
   FROM [Adventure Works]  
```  
  
 下一个示例演示如何使用 **include_calc_members** 标志，该标志用于在深化级别包含计算成员。 **DrilldownLevelTop**语句中包含度量值 [分销商订单计数]，以确保返回值按该度量值排序。  
  
```  
WITH MEMBER   
[Product].[Product Categories].[Category].&[3].[Premium Clothes] AS  
[Product].[Product Categories].[Subcategory].&[18] +  
[Product].[Product Categories].[Subcategory].&[21]  
SELECT [Measures].[Reseller Order Count] ON 0,  
DRILLDOWNLEVELTOP(  
  [Product].[Product Categories].children ,  
  2,  
  [Product].[Product Categories].[Category] ,  
  [Measures].[Reseller Order Count],  
  INCLUDE_CALC_MEMBERS ) ON 1  
FROM [Adventure Works]  
```  
  
## <a name="see-also"></a>另请参阅  
 [DrilldownLevel &#40;MDX&#41;](../mdx/drilldownlevel-mdx.md)   
 [MDX 函数引用 (MDX)](../mdx/mdx-function-reference-mdx.md)  
  
  
