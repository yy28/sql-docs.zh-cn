---
title: 使用成员函数 |Microsoft 文档
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 1c9979b6b9fcb04115695cbe8d9c224e1c6c1f57
ms.sourcegitcommit: 97bef3f248abce57422f15530c1685f91392b494
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/04/2018
ms.locfileid: "34743636"
---
# <a name="using-member-functions"></a>使用成员函数


  成员函数是返回成员的多维表达式 (MDX) 函数。 与元组函数和集函数一样，成员函数对协商 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 中的多维结构至关重要。  
  
 在 MDX 中的许多成员函数，最重要是**CurrentMember**函数，用于确定层次结构上的当前成员。 下面的查询演示如何使用它，连同**父**，**上级**，和**Prevmember**函数：  
  
 `WITH`  
  
 `//Returns the name of the currentmember on the Calendar hierarchy`  
  
 `MEMBER MEASURES.[CurrentMemberDemo] AS [Date].[Calendar].CurrentMember.Name`  
  
 `//Returns the name of the parent of the currentmember on the Calendar hierarchy`  
  
 `MEMBER MEASURES.[ParentDemo] AS [Date].[Calendar].CurrentMember.Parent.Name`  
  
 `//Returns the name of the ancestor of the currentmember on the Calendar hierarchy at the Year level`  
  
 `MEMBER MEASURES.[AncestorDemo] AS ANCESTOR([Date].[Calendar].CurrentMember, [Date].[Calendar].[Calendar Year]).Name`  
  
 `//Returns the name of the member before the currentmember on the Calendar hierarchy`  
  
 `MEMBER MEASURES.[PrevMemberDemo] AS [Date].[Calendar].CurrentMember.Prevmember.Name`  
  
 `SELECT{MEASURES.[CurrentMemberDemo],MEASURES.[ParentDemo],MEASURES.[AncestorDemo],MEASURES.[PrevMemberDemo] } ON 0,`  
  
 `[Date].[Calendar].MEMBERS ON 1`  
  
 `FROM [Adventure Works]`  
  
## <a name="see-also"></a>请参阅  
 [函数&#40;MDX 语法&#41;](../mdx/functions-mdx-syntax.md)   
 [使用元组函数](../mdx/using-tuple-functions.md)   
 [使用集函数](../mdx/using-set-functions.md)  
  
  
