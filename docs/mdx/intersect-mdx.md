---
description: Intersect (MDX)
title: " (MDX) 的交集 |Microsoft Docs"
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 9216b334caf67191e231c3ec0389da3fb7493b24
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/17/2020
ms.locfileid: "88471839"
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
 **Intersect**函数返回两个集的交集。 默认情况下，此函数会先删除两个集合中的重复项，然后再对这两个集合求交集。 指定的两个集合必须具有相同的维度。  
  
 可选的 **ALL** 标志保留重复项。 如果指定了 **ALL** ，则 **Intersect** 函数会照常与照常元素相交，还会将第一个集中的每个重复项与第二个集中具有匹配重复项的副本相交。 指定的两个集合必须具有相同的维度。  
  
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
  
## <a name="see-also"></a>另请参阅  
 [MDX 函数引用 (MDX)](../mdx/mdx-function-reference-mdx.md)  
  
  
