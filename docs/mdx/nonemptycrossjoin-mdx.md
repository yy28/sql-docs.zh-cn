---
title: NonEmptyCrossjoin （MDX） |Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 2d152b51e0c1c996e0bb3309e554a70683937493
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/08/2020
ms.locfileid: "68088354"
---
# <a name="nonemptycrossjoin-mdx"></a>NonEmptyCrossjoin (MDX)


  返回包含一个或多个集的叉积的集，不包括空元组以及无相关事实数据表数据的元组。  
  
## <a name="syntax"></a>语法  
  
```  
  
NonEmptyCrossjoin(Set_Expression1 [ ,Set_Expression2,...] [,Count ] )  
```  
  
## <a name="arguments"></a>参数  
 *Set_Expression1*  
 返回集的有效多维表达式 (MDX)。  
  
 *Set_Expression2*  
 返回集的有效多维表达式 (MDX)。  
  
 *Count*  
 指定返回集的数量的有效数值表达式。  
  
## <a name="remarks"></a>备注  
 **NonEmptyCrossjoin**函数以集的形式返回两个或更多集的叉积，不包括空元组或不包含由基础事实数据表提供的数据的元组。 由于**NonEmptyCrossjoin**函数的工作方式，将自动排除所有计算成员。  
  
 如果未指定*Count* ，则函数将交叉联接所有指定的集，并从结果集中排除空成员。 如果指定了集的数量，该函数将从第一个指定的集开始，交叉联接指定数量的集。 **NonEmptyCrossjoin**函数使用在后续指定集内指定的任何剩余集，但未进行交叉联接来确定生成的交叉联接集中哪些成员被视为非空成员。 **NonEmptyCrossjoin**函数遵循计算度量值的**NON_EMPTY_BEHAVIOR**设置。  
  
> [!IMPORTANT]  
>  不推荐使用此函数并且不应使用它，保留此函数仅是为了维护向后兼容性。 相反，应将[Exists （mdx）](../mdx/exists-mdx.md)函数与度量值组名称参数或非[空（mdx）](../mdx/nonempty-mdx.md)函数一起使用。  
  
## <a name="see-also"></a>另请参阅  
 [Mdx 函数引用 &#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
