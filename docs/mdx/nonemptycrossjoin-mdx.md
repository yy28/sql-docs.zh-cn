---
title: NonEmptyCrossjoin (MDX) |Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 7da56ac658f57d6eb664762f9dd94351df39fe0f
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/15/2019
ms.locfileid: "63456565"
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
 **NonEmptyCrossjoin**函数返回两个或多个集的叉积为一组，而无需提供基础事实数据表的数据中排除空元组或元组。 由于如何**NonEmptyCrossjoin**函数的工作，所有计算成员将自动排除。  
  
 如果*计数*未指定，则该函数将交叉联接所有指定的集，并在结果集中排除空成员。 如果指定了集的数量，该函数将从第一个指定的集开始，交叉联接指定数量的集。 **NonEmptyCrossjoin**函数使用后续的指定集合中指定，但尚未交叉联接以确定哪些成员被视为非空交叉联接集生成任何剩余的集。 **NonEmptyCrossjoin**函数不影响**NON_EMPTY_BEHAVIOR**设置的计算度量值。  
  
> [!IMPORTANT]  
>  不推荐使用此函数并且不应使用它，保留此函数仅是为了维护向后兼容性。 相反，应使用[Exists (MDX)](../mdx/exists-mdx.md)具有度量值组名称参数函数或[NonEmpty (MDX)](../mdx/nonempty-mdx.md)函数。  
  
## <a name="see-also"></a>请参阅  
 [MDX 函数引用 (MDX)](../mdx/mdx-function-reference-mdx.md)  
  
  
