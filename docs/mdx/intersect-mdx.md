---
title: Intersect (MDX) |Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: f253dad526c509edff5c837b61ae2faae07d5758
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/15/2019
ms.locfileid: "68105359"
---
# <a name="intersect-mdx"></a>Intersect (MDX)


  返回两个输入集的交集，可以选择保留重复项。  
  
## <a name="syntax"></a>语法  
  
```  
  
Intersect(Set_Expression1 , Set_Expression2 [ , ALL ] )  
```  
  
## <a name="arguments"></a>参数  
 *Set_Expression1*  
 返回集的有效多维表达式 (MDX)。  
  
 *Set_Expression2*  
 返回集的有效多维表达式 (MDX)。  
  
## <a name="remarks"></a>备注  
 **Intersect**函数将返回两个集的交集。 默认情况下，此函数会先删除两个集合中的重复项，然后再对这两个集合求交集。 指定的两个集合必须具有相同的维度。  
  
 可选**所有**标志来保留重复项。 如果**所有**指定，则**Intersect**函数与不重复的元素相交像往常一样，且还与第二个集中具有匹配重复第一个集中每个重复的相交。 指定的两个集合必须具有相同的维度。  
  
## <a name="example"></a>示例  
 下面的查询将返回 2003 年和 2004 年，这是在指定的两个集合中均出现的成员：  
  
 `SELECT`  
  
 `INTERSECT(`  
  
 `{[Date].[Calendar Year].&[2001], [Date].[Calendar Year].&[2002],[Date].[Calendar Year].&[2003]}`  
  
 `, {[Date].[Calendar Year].&[2002],[Date].[Calendar Year].&[2003], [Date].[Calendar Year].&[2004]})`  
  
 `ON 0`  
  
 `FROM`  
  
 `[Adventure Works]`  
  
 下面的查询将失败，因为指定的两个集合包含来自不同层次结构的成员：  
  
 `SELECT`  
  
 `INTERSECT(`  
  
 `{[Date].[Calendar Year].&[2001]}`  
  
 `, {[Customer].[City].&[Abingdon]&[ENG]})`  
  
 `ON 0`  
  
 `FROM`  
  
 `[Adventure Works]`  
  
## <a name="see-also"></a>请参阅  
 [MDX 函数引用 (MDX)](../mdx/mdx-function-reference-mdx.md)  
  
  
