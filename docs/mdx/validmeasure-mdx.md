---
title: "ValidMeasure (MDX) |Microsoft 文档"
ms.custom: 
ms.date: 03/02/2016
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: 
ms.component: 
ms.reviewer: 
ms.suite: pro-bi
ms.technology: analysis-services
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords: VALIDMEASURE
dev_langs: kbMDX
helpviewer_keywords: ValidMeasure function
ms.assetid: ecf20a86-c45e-4521-84ce-3a466e0c1136
caps.latest.revision: "36"
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: Inactive
ms.openlocfilehash: 9309b0b62994e6d3199a7aa565d9edd2e88c5f73
ms.sourcegitcommit: 9fbe5403e902eb996bab0b1285cdade281c1cb16
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/27/2017
---
# <a name="validmeasure-mdx"></a>ValidMeasure (MDX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  在返回指定元组的结果时，通过将不适用的维度强制到“全部”级别（如果是不可聚合的，则为默认成员）来返回多维数据集中的度量值。  
  
## <a name="syntax"></a>语法  
  
```  
  
ValidMeasure(Tuple_Expression)   
```  
  
## <a name="arguments"></a>参数  
 *Tuple_Expression*  
 返回元组的有效多维表达式 (MDX)。  
  
## <a name="remarks"></a>注释  
 **ValidMeasure**函数返回的元组的值，忽略具有其值的度量值的度量值组没有关系的属性元组返回。 出于以下两个原因，属性可与度量值无关：  
  
-   属性的维度与元组中度量值的度量值组无关。  
  
-   属性的维度与度量值的度量值组无关，但粒度属性不是键属性，并且粒度属性与元组中的属性没有直接关系。  
  
 指定此函数的行为是默认服务器端行为，并由控制**IgnoreUnrelatedDimensions**度量值组对象的属性。  
  
 对于具有粒度的指定元组中的每个属性（也就是说，元组中的成员不是“全部”成员），其当前坐标按如下方式移动：  
  
-   与指定属性成员相关的属性移动至与当前成员共存的成员。  
  
-   与指定属性成员相关的属性移动至“全部”成员（如果层次结构是不可聚合的，则为默认成员）。  
  
-   不相关的属性移动至“全部”成员（根据度量值）。  
  
## <a name="example"></a>示例  
 下面的查询显示如何使用 ValidMeasure 函数来覆盖 IgnoreUnrelatedDimensions 属性的行为。 在 Adventure Works 多维数据集中，Sales Targets 度量值组将 IgnoreUnrelatedDimensions 设置为 False；因为 Date 维度在 Calendar Quarter 粒度联接到此度量值组，所以这意味着，Sales Quota 度量值默认情况下将在 Calendar Quarter 下返回 Null（尽管在 MDX 脚本中也存在将值向下分配给 Month 级别的计算）。 在计算度量值中使用 ValidMeasure 函数可用于使 Sales Quota 度量值的行为就像 IgnoreUnrelatedDimensions 设置为 True 一样并且强制 Sales Quota 显示当前 Calendar Quarter 的值。  
  
```  
WITH MEMBER MEASURES.VTEST AS VALIDMEASURE([Measures].[Sales Amount Quota])  
SELECT {[Measures].[Sales Amount Quota], MEASURES.VTEST} ON 0,  
[Date].[Calendar].MEMBERS ON 1  
FROM [Adventure Works]  
```  
  
 同样，Sales Targets 度量值组与 Promotion 维度完全没有任何关系，因此，在 Promotion 上任何层次结构的“全部”成员之下，它将返回 Null。 此外，可以通过使用 ValidMeasure 更改此行为：  
  
 `WITH MEMBER MEASURES.VTEST AS VALIDMEASURE([Measures].[Sales Amount Quota])`  
  
 `SELECT {[Measures].[Sales Amount Quota], MEASURES.VTEST} ON 0,`  
  
 `[Promotion].[Promotions].members ON 1`  
  
 `FROM [Adventure Works]`  
  
## <a name="see-also"></a>另请参阅  
 [MDX 函数引用 &#40;MDX &#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
