---
description: Lag (MDX)
title: " (MDX) 的 Lag |Microsoft Docs"
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: bc9beb8215d8d690f2d4ccdf43c3aaf03096b9d8
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/17/2020
ms.locfileid: "88477039"
---
# <a name="lag-mdx"></a>Lag (MDX)


  返回在成员级别中比指定成员位置靠前且靠前位数为指定位数的成员。  
  
## <a name="syntax"></a>语法  
  
```  
  
Member_Expression.Lag(Index)   
```  
  
## <a name="arguments"></a>参数  
 *Member_Expression*  
 返回成员的有效多维表达式 (MDX)。  
  
 *索引*  
 指定成员位置滞后位数的有效数值表达式。  
  
## <a name="remarks"></a>备注  
 级别内的成员位置由属性层次结构的自然顺序决定。 位置的编号从零开始。  
  
 如果指定的滞后值为零，则 **lag** 函数返回指定的成员本身。  
  
 如果指定的 lag 为负数，则 **lag** 函数返回后续成员。  
  
 `Lag(1)` 等效于 [PrevMember](../mdx/prevmember-mdx.md) 函数。 `Lag(-1)` 等效于 [NextMember](../mdx/nextmember-mdx.md) 函数。  
  
 **Lag**函数类似于[导引](../mdx/lead-mdx.md)函数，但**导引**函数与**Lag**函数的方向相反。 也就是说，`Lag(n)` 等效于 `Lead(-n)`。  
  
## <a name="example"></a>示例  
 下例将返回 2001 年 12 月的值：  
  
```  
SELECT [Date].[Fiscal].[Month].[February 2002].Lag(2) ON 0  
FROM [Adventure Works]  
  
```  
  
 下例将返回 2002 年 3 月的值：  
  
```  
SELECT [Date].[Fiscal].[Month].[February 2002].Lag(-1) ON 0  
FROM [Adventure Works]  
  
```  
  
## <a name="see-also"></a>另请参阅  
 [MDX 函数引用 (MDX)](../mdx/mdx-function-reference-mdx.md)  
  
  
