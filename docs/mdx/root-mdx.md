---
title: Root (MDX) | Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 2c2301f44cbdac4505bef95d590ce206c8b6b509
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/15/2019
ms.locfileid: "63150240"
---
# <a name="root-mdx"></a>Root (MDX)


  返回一个元组组成**所有**多维数据集、 维度或元组中的当前作用域内每个属性层次结构中的成员。 有关作用域的详细信息，请参阅[SCOPE 语句&#40;MDX&#41;](../mdx/mdx-scripting-scope.md)。  
  
> [!NOTE]  
>  如果属性层次结构不具有**所有**成员、 元组包含该层次结构的默认成员。  
  
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
 如果指定了维度名称既不是元组表达式，则**根**函数返回包含一个元组**所有**成员 (或默认成员如果**所有**成员不存在） 的多维数据集中各个属性层次结构。 成员在元组中的顺序基于多维数据集中定义属性层次结构的顺序。  
  
 如果指定了维度名称，则**根**函数返回包含一个元组**所有**成员 (或默认成员如果**所有**成员不存在) 从每个基于上下文的当前成员的指定维中的属性层次结构。 成员在元组中的顺序基于维度中定义属性层次结构的顺序。  
  
> [!NOTE]  
>  如果指定层次结构名称，则**元组**函数将选取维度名称从指定的层次结构名称。  
  
 如果指定元组表达式，则**根**函数将返回包含指定元组的交集的元组并**所有**的所有其他成员未显式维度属性包含指定元组中。  
  
## <a name="examples"></a>示例  
 下面的示例返回元组包含**所有**成员 (默认值或如果**所有**成员不存在) 从 Adventure Works 多维数据集中每个层次结构。  
  
```  
SELECT Root()ON 0  
FROM [Adventure Works]  
```  
  
 下面的示例返回元组包含**所有**成员 (默认值或如果**所有**成员不存在) 从 Adventure Works 多维数据集和的值中的日期维度中的每个层次结构这些默认成员与指定的成员的相交的度量值维度。  
  
```  
SELECT Root([Date]) ON 0  
FROM [Adventure Works]  
WHERE [Measures].[Order Count]  
```  
  
 下面的示例返回包含指定元组成员的元组 (2001 年 7 月 1 日，连同**所有**成员 (默认值或如果**所有**成员不存在) 从每个非指定层次结构中日期维度 Adventure Works 多维数据集和这些成员与指定的相交的度量值维度成员的值。  
  
```  
SELECT Root([Date].[July 1, 2001]) ON 0  
FROM [Adventure Works]  
WHERE [Measures].[Order Count]  
```  
  
## <a name="see-also"></a>请参阅  
 [MDX 函数引用 (MDX)](../mdx/mdx-function-reference-mdx.md)  
  
  
