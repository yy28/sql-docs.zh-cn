---
description: Root (MDX)
title: 根 (MDX) |Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: a408250de53e3d77750d6ea9a87aa679152a86d8
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/17/2020
ms.locfileid: "88341303"
---
# <a name="root-mdx"></a>Root (MDX)


  返回一个元组，该元组由多维数据集、维度或元组中的当前范围内的每个属性层次结构中的 **所有** 成员组成。 有关范围的详细信息，请参阅 [Scope 语句 &#40;MDX&#41;](../mdx/mdx-scripting-scope.md)。  
  
> [!NOTE]  
>  如果属性层次结构中没有 " **全部** " 成员，则元组将包含该层次结构的默认成员。  
  
## <a name="syntax"></a>语法  
  
```  
  
Cube syntax  
Root ()  
Dimension syntax  
Root( Dimension_Name )  
Tuple syntax  
Root( Tuple_Expression )  
```  
  
## <a name="arguments"></a>参数  
 *Dimension_Name*  
 指定维度名称的有效字符串表达式。  
  
 *Tuple_Expression*  
 返回元组的有效多维表达式 (MDX)。  
  
## <a name="remarks"></a>备注  
 如果维度名称和元组表达式均未指定，则 **Root** 函数将返回一个元组，该元组包含 " **全部** 成员" (或默认成员（如果不存在 **所有** 成员）) 多维数据集的每个属性层次结构中。 成员在元组中的顺序基于多维数据集中定义属性层次结构的顺序。  
  
 如果指定了维度名称，则**根**函数将返回一个元组，该元组包含从指定维度的每个属性层次结构中的每个属性层次结构**中的每**个属性层次结构中的每个属性层次结构中的每个属性层次结构中**的所有成员** (或) 默认 成员在元组中的顺序基于维度中定义属性层次结构的顺序。  
  
> [!NOTE]  
>  如果指定了层次结构名称， **元组** 函数将从指定的层次结构名称中选取维度名称。  
  
 如果指定了元组表达式，则 **根** 函数将返回一个元组，该元组包含指定元组的交集和所有其他维度属性的 **所有** 成员（未显式包括在指定元组中）。  
  
## <a name="examples"></a>示例  
 下面的示例返回包含 " **全部** 成员" (的元组，或者，如果 " **所有** 成员") 从艾德工作多维数据集中的每个层次结构都不存在，则返回默认值。  
  
```  
SELECT Root()ON 0  
FROM [Adventure Works]  
```  
  
 下面的示例返回包含 " **全部** 成员" (的元组，或者，如果 " **所有** 成员") 来自艾德工作多维数据集的 "日期" 维度中的每个层次结构，以及与这些默认成员相交的 "度量值" 维度的指定成员的值，则为默认值。  
  
```  
SELECT Root([Date]) ON 0  
FROM [Adventure Works]  
WHERE [Measures].[Order Count]  
```  
  
 下面的示例返回包含指定的元组成员 (的元组，同时包含2001年7月1日与 **all** 成员 (或默认值（) 如果从 Date 维度艾德作品多维 **数据集中的** 每个非指定层次结构到与这些成员相交的度量值维度的指定成员的值）。  
  
```  
SELECT Root([Date].[July 1, 2001]) ON 0  
FROM [Adventure Works]  
WHERE [Measures].[Order Count]  
```  
  
## <a name="see-also"></a>另请参阅  
 [MDX 函数引用 (MDX)](../mdx/mdx-function-reference-mdx.md)  
  
  
