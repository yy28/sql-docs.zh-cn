---
title: DrilldownLevelTop (MDX) |Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 8d6532998f65625bf3dacd11de2949a3478ba6ea
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63156424"
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
 如果指定了数值表达式，则**DrilldownLevelTop**函数排序，计算出的子降序排序，根据数值表达式的值指定的集中每个成员的子级成员。 如果未指定数值表达式，则此函数根据由查询上下文确定的子成员集所表示的单元值，对指定集中每个成员的子成员按降序排序。  
  
 排序后， **DrilldownLevelTop**函数返回包含父成员的子成员中指定数量的集中*计数，* 最高值。  
  
 **DrilldownLevelTop**函数是类似于[DrilldownLevel](../mdx/drilldownlevel-mdx.md)函数，而不是包括指定级别处每个成员的所有子级，但**DrilldownLevelTop**函数返回的最顶层子成员数。  
  
 查询 XMLA 属性 MdpropMdxDrillFunctions，您可以验证的服务器为钻取功能; 提供的支持级别请参阅[支持的 XMLA 属性&#40;XMLA&#41; ](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/propertylist-element-supported-xmla-properties)有关详细信息。  
  
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
  
 下一步的示例演示如何使用**include_calc_members**标志，用于在深化级别包括计算的成员。 度量值 [Reseller Order Count] 包含在**DrilldownLevelTop**语句以确保返回的值将按该度量值。  
  
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
  
## <a name="see-also"></a>请参阅  
 [DrilldownLevel (MDX)](../mdx/drilldownlevel-mdx.md)   
 [MDX 函数引用 (MDX)](../mdx/mdx-function-reference-mdx.md)  
  
  
