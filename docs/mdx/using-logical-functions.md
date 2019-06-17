---
title: 使用逻辑函数 |Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: a63d8cb22a8533cf352acb690f87916e2e9d568d
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/15/2019
ms.locfileid: "63249828"
---
# <a name="using-logical-functions"></a>使用逻辑函数


  逻辑函数对对象和表达式执行逻辑操作或比较并返回布尔值。 在多维表达式 (MDX) 中，逻辑函数对确定成员的位置至关重要。  
  
 最常使用的逻辑函数是**IsEmpty**函数。 有关如何使用的详细信息**IsEmpty**函数中，请参阅[处理空值](../mdx/working-with-empty-values.md)。  
  
 以下查询说明如何使用**IsLeaf**并**IsAncestor**函数：  
  
 `WITH`  
  
 `//Returns true if the CurrentMember on Calendar is a leaf member, ie it has no children`  
  
 `MEMBER MEASURES.[IsLeafDemo] AS IsLeaf([Date].[Calendar].CurrentMember)`  
  
 `//Returns true if the CurrentMember on Calendar is an Ancestor of July 1st 2001`  
  
 `MEMBER MEASURES.[IsAncestorDemo] AS IsAncestor([Date].[Calendar].CurrentMember, [Date].[Calendar].[Date].&[1])`  
  
 `SELECT{MEASURES.[IsLeafDemo],MEASURES.[IsAncestorDemo] } ON 0,`  
  
 `[Date].[Calendar].MEMBERS ON 1`  
  
 `FROM [Adventure Works]`  
  
## <a name="see-also"></a>请参阅  
 [函数&#40;MDX 语法&#41;](../mdx/functions-mdx-syntax.md)  
  
  
