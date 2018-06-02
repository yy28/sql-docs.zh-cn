---
title: 存在 (MDX) |Microsoft 文档
ms.date: 05/30/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 98f07985b83ae32f02bd3da68d382c8f3fceb0cf
ms.sourcegitcommit: 808d23a654ef03ea16db1aa23edab496b73e5072
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/02/2018
ms.locfileid: "34578249"
---
# <a name="exists-mdx"></a>Exists (MDX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  返回与第二个指定集的一个或多个元组共存的第一个指定集中的元组集。 该函数手动执行自动 Exists 以自动方式执行的操作。 存在自动有关的详细信息，请参阅[在 MDX 中的关键概念&#40;Analysis Services&#41;](../analysis-services/multidimensional-models/mdx/key-concepts-in-mdx-analysis-services.md)。  
  
 如果可选\<度量值组名称 > 提供该函数通过第二个集和具有关联的行的事实数据表中指定的度量值组的这些元组返回的元组存在与一个或多个元组。  
  
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
  
## <a name="remarks"></a>Remarks  
  
1.  包含 null 值的度量值的度量值组行贡献**Exists**指定 MeasureGroupName 自变量时。 下面是此形式的 Exists 和 Nonempty 函数之间的差异：如果这些度量值的 NullProcessing 属性设置为 Preserve，则意味着在对该部分的多维数据集运行查询时这些度量值将显示 Null 值；NonEmpty 始终从集中删除具有 Null 度量值的元组，而具有 MeasureGroupName 参数的 Exists 将不筛选具有关联的度量值组行的元组，甚至在度量值为 Null 时也是如此。  
  
2.  如果*MeasureGroupName*参数时，结果将取决于引用的度量值组中是否存在可见的度量值; 如果被引用的度量值组中不有任何可见的度量值则 EXISTS 将始终返回空集，而不考虑的值*Set_Expression1*和*Set_Expression2*。  
  
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
 [MDX 函数引用&#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)   
 [叉积&#40;MDX&#41;](../mdx/crossjoin-mdx.md)   
 [NonEmptyCrossjoin &#40;MDX&#41;](../mdx/nonemptycrossjoin-mdx.md)   
 [非空&#40;MDX&#41;](../mdx/nonempty-mdx.md)   
 [IsEmpty &#40;MDX&#41;](../mdx/isempty-mdx.md)  
  
  
