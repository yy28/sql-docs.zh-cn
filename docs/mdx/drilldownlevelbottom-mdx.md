---
title: DrilldownLevelBottom (MDX) |Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 14b0b2dfd3e4578558e49cc305c37821e208c65d
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/15/2019
ms.locfileid: "62516026"
---
# <a name="drilldownlevelbottom-mdx"></a>DrilldownLevelBottom (MDX)


  将集中某一指定级别上的最底层成员深化到下一个级别。  
  
## <a name="syntax"></a>语法  
  
```  
DrilldownLevelBottom(Set_Expression, Count [,[<Level_Expression>] [,[<Numeric_Expression>][,INCLUDE_CALC_MEMBERS]]])  
```  
  
## <a name="arguments"></a>参数  
 *Set_Expression*  
 返回集的有效多维表达式 (MDX)。  
  
 *Count*  
 指定要返回的元组数的有效数值表达式。  
  
 *Level_Expression*  
 返回级别的有效多维表达式 (MDX)。  
  
 *Numeric_Expression*  
 可选。 返回数字的有效数值表达式，通常为单元坐标的多维表达式 (MDX)。  
  
 *Include_Calc_Members*  
 可选。 将计算成员添加到深化结果的关键字。  
  
## <a name="remarks"></a>备注  
 如果指定了数值表达式，则**DrilldownLevelBottom**函数排序的子成员集求得升序排序，在指定的组，根据指定的值，每个成员的子级。 如果未指定数值表达式，则此函数根据由查询上下文决定的子成员集所表示的单元的值，对指定的集中每个成员的子成员按升序排序。此行为类似于 BottomCount 和 Tail (MDX) 函数，都以自然顺序返回一组成员，没有任何排序。  
  
 排序后， **DrilldownLevelBottom**函数返回包含父成员的子成员中指定数量的集中*计数*，具有最小值。  
  
 **DrilldownLevelBottom**函数是类似于[DrilldownLevel](../mdx/drilldownlevel-mdx.md)函数，而不是包括指定级别处每个成员的所有子级，但**DrilldownLevelBottom**函数返回的最底层子成员数。  
  
 查询 XMLA 属性 MdpropMdxDrillFunctions，您可以验证的服务器为钻取功能; 提供的支持级别请参阅[支持的 XMLA 属性&#40;XMLA&#41; ](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/propertylist-element-supported-xmla-properties)有关详细信息。  
  
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
  
 下一步的示例演示如何使用**include_calc_members**标志，用于在深化级别包括计算的成员。 度量值 [Reseller Order Count] 添加到**DrilldownLevelBottom**语句以确保结果将按该度量值。 要查看计算成员，必须将计数至少增加到 9。  
  
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
  
## <a name="see-also"></a>请参阅  
 [DrilldownLevel (MDX)](../mdx/drilldownlevel-mdx.md)   
 [MDX 函数引用 (MDX)](../mdx/mdx-function-reference-mdx.md)  
  
  
