---
description: Exists (MDX)
title: 存在 (MDX) |Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 9c879d9091c692cfa7a93490b34c70ad84fa81c4
ms.sourcegitcommit: cfa04a73b26312bf18d8f6296891679166e2754d
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/19/2020
ms.locfileid: "92193969"
---
# <a name="exists-mdx"></a>Exists (MDX)


  返回与第二个指定集的一个或多个元组共存的第一个指定集中的元组集。 该函数手动执行自动 Exists 以自动方式执行的操作。 有关 auto exists 的详细信息，请参阅 [MDX 中的重要概念 &#40;Analysis Services&#41;](/analysis-services/multidimensional-models/mdx/key-concepts-in-mdx-analysis-services)。  
  
 如果提供了可选的 \<Measure Group Name> ，则该函数将返回与第二个集合中的一个或多个元组相关的元组，以及在指定度量值组的事实数据表中具有关联行的元组。  
  
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
  
1.  如果指定了 MeasureGroupName 参数，则度量值组中包含空值的度量值会导致 **存在** 。 这种形式的 Exists 和非空函数的不同之处在于：如果将这些度量值的 NullProcessing 属性设置为 "保留"，这意味着当针对多维数据集的该部分运行查询时，度量值将显示 Null 值;非空将始终从具有空度量值的集中删除元组，而 with MeasureGroupName 参数则不会筛选具有关联的度量值组行的元组，即使度量值为 Null 也是如此。  
  
2.  如果使用 *MeasureGroupName* 参数，则结果将取决于所引用的度量值组中是否存在可见度量值;如果被引用的度量值组中没有可见度量值，无论 *Set_Expression1* 和 *Set_Expression2*的值是什么，EXISTS 都将始终返回空集。  
  
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
  
## <a name="see-also"></a>另请参阅  
 [Mdx 函数引用 &#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)   
 [MDX &#40;交叉结合&#41;](../mdx/crossjoin-mdx.md)   
 [NonEmptyCrossjoin &#40;MDX&#41;](../mdx/nonemptycrossjoin-mdx.md)   
 [非空 &#40;MDX&#41;](../mdx/nonempty-mdx.md)   
 [IsEmpty &#40;MDX&#41;](../mdx/isempty-mdx.md)  
  
