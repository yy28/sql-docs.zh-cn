---
description: Leaves (MDX)
title: 离开 (MDX) |Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 7beab859a2953b3eba52e74d97bed5718c59ea90
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/17/2020
ms.locfileid: "88387303"
---
# <a name="leaves-mdx"></a>Leaves (MDX)


  返回由所有属性（或者限制为属于特定维度的属性）组成的集。 对于返回集中的每个属性 x，如果 x 是粒度属性或者直接或间接与粒度属性相关，则在属性 x 上设置粒度而不会影响切片。 **叶子**函数旨在在 SCOPE 语句或赋值的左侧使用。  
  
## <a name="syntax"></a>语法  
  
```  
  
Leaves( [ Dimension_expression ] )  
```  
  
## <a name="arguments"></a>参数  
 *Dimension_Expression*  
 返回维度的有效多维表达式 (MDX)。  
  
## <a name="remarks"></a>备注  
 叶成员是由所有属性层次结构中的最低级别交叉联接构成的元组。 已排除了计算成员。  
  
-   如果指定了维度名称，则 **叶子** 函数将返回包含指定维度的键属性的叶成员的集。  
  
-   如果维度与多个度量值组相关联，将使用当前作用域中度量值的维度。  
  
-   如果未指定维度名称，则此函数返回的集中将包含整个多维数据集的叶成员。  
  
    > [!NOTE]  
    >  如果维度表达式解析为层次结构，并且层次结构的唯一名称与维度的唯一名称相同（多维数据集维度属性 HierarchyUniqueNameStyle=ExcludeDimensionName，并且层次结构名称 = 维度名称），则已经使用该维度。  
  
    > [!IMPORTANT]  
    >  如果并非所有属性在当前范围内的度量值组中均具备相同的粒度，则会产生错误。  
  
## <a name="see-also"></a>另请参阅  
 [MDX 函数引用 (MDX)](../mdx/mdx-function-reference-mdx.md)  
  
  
