---
title: 存在 (MDX) |Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 781c03283c39ab5ec100ba7f7d83b3cbe19a7c19
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/15/2019
ms.locfileid: "68139176"
---
# <a name="exists-mdx"></a>Exists (MDX)


  返回与第二个指定集的一个或多个元组共存的第一个指定集中的元组集。 该函数手动执行自动 Exists 以自动方式执行的操作。 存在有关自动的详细信息，请参阅[MDX 中的重要概念&#40;Analysis Services&#41;](../analysis-services/multidimensional-models/mdx/key-concepts-in-mdx-analysis-services.md)。  
  
 如果可选\<度量值组名称 > 提供该函数将返回从第二个集和具有关联的事实数据表中指定的度量值组的行的元组的存在元组与一个或多个元组。  
  
## <a name="syntax"></a>语法  
  
```  
  
Exists( Set_Expression1 , Set_Expression2 [, MeasureGroupName] )  
```  
  
## <a name="arguments"></a>参数  
 *Set_Expression1*  
 返回集的有效多维表达式 (MDX)。  
  
 *Set_Expression2*  
 返回集的有效多维表达式 (MDX)。  
  
 *MeasureGroupName*  
 指定度量值组名称的有效字符串表达式。  
  
## <a name="remarks"></a>备注  
  
1.  包含 null 值的度量值的度量值组行贡献**Exists**时指定了 MeasureGroupName 参数。 这是这种形式的 Exists 和 Nonempty 函数之间的差异： 如果这些度量值的 NullProcessing 属性设置为保留，这意味着根据多维数据集; 该部分运行查询时，度量值将显示 Null 值而具有 MeasureGroupName 参数的 Exists 将不会筛选具有关联的度量值组行的元组，即使度量值均为 Null，nonEmpty 始终将从一组具有 Null 度量值的删除元组。  
  
2.  如果*MeasureGroupName*参数，结果将取决于引用的度量值组中是否具有可见度量值; 如果引用的度量值组中有无可见度量值，则将始终返回 EXISTS空集，而不考虑的值*Set_Expression1*并*Set_Expression2*。  
  
## <a name="examples"></a>示例  
 居住在加利福尼亚的客户：  
  
```  
SELECT [Measures].[Internet Sales Amount] ON 0,  
EXISTS(  
[Customer].[Customer].[Customer].MEMBERS  
, {[Customer].[State-Province].&[CA]&[US]}  
) ON 1   
FROM [Adventure Works]  
  
```  
  
 居住在加利福尼亚并且有销售额的客户：  
  
```  
SELECT [Measures].[Internet Sales Amount] ON 0,  
EXISTS(  
[Customer].[Customer].[Customer].MEMBERS  
, {[Customer].[State-Province].&[CA]&[US]}  
, "Internet Sales") ON 1   
FROM [Adventure Works]  
  
```  
  
 有销售额的客户：  
  
```  
SELECT [Measures].[Internet Sales Amount] ON 0,  
EXISTS(  
[Customer].[Customer].[Customer].MEMBERS  
, , "Internet Sales") ON 1   
FROM [Adventure Works]  
  
```  
  
 购买了自行车的客户：  
  
```  
SELECT [Measures].[Internet Sales Amount] ON 0,  
EXISTS(  
[Customer].[Customer].[Customer].MEMBERS  
, {[Product].[Product Categories].[Category].&[1]}  
, "Internet Sales") ON 1   
FROM [Adventure Works]  
```  
  
## <a name="see-also"></a>请参阅  
 [MDX 函数引用 (MDX)](../mdx/mdx-function-reference-mdx.md)   
 [叉积&#40;MDX&#41;](../mdx/crossjoin-mdx.md)   
 [NonEmptyCrossjoin &#40;MDX&#41;](../mdx/nonemptycrossjoin-mdx.md)   
 [非空&#40;MDX&#41;](../mdx/nonempty-mdx.md)   
 [IsEmpty &#40;MDX&#41;](../mdx/isempty-mdx.md)  
  
  
