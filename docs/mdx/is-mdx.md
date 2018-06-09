---
title: 是 (MDX) |Microsoft 文档
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 29d251c05639d928f3ea5a9925a4cc21935e0529
ms.sourcegitcommit: 97bef3f248abce57422f15530c1685f91392b494
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/04/2018
ms.locfileid: "34740446"
---
# <a name="is-mdx"></a>IS (MDX)


  对两个对象表达式执行逻辑比较。  
  
## <a name="syntax"></a>语法  
  
```  
  
Expression1 IS ( Expression2 | NULL )  
```  
  
#### <a name="parameters"></a>Parameters  
 *Expression1*  
 返回 MDX 对象引用的有效多维表达式 (MDX) 表达式。  
  
 *Expression2*  
 返回 MDX 对象引用的有效 MDX 表达式。  
  
## <a name="return-value"></a>返回值  
 返回一个布尔值**true**如果这两个自变量引用同一对象; 否则为**false**。 如果**NULL**指定关键字，则该运算符将返回**true**如果*Expression1*是**null**; 否则为**false**。  
  
## <a name="remarks"></a>Remarks  
 **IS**运算符通常用于确定是否元组和成员都是幂等的这意味着它们都已完全等效。  
  
## <a name="examples"></a>示例  
 下面的示例演示如何使用**IS**运算符检查轴上的当前成员是否为特定的成员：  
  
 `With`  
  
 `//Returns TRUE if the currentmember is Bikes`  
  
 `Member [Measures].[IsBikes?] AS`  
  
 `[Product].[Category].CurrentMember IS [Product].[Category].&[1]`  
  
 `SELECT`  
  
 `{[Measures].[IsBikes?]} ON 0,`  
  
 `[Product].[Category].[Category].Members ON 1`  
  
 `FROM`  
  
 `[Adventure Works]`  
  
## <a name="see-also"></a>请参阅  
 [MDX 运算符参考&#40;MDX&#41;](../mdx/mdx-operator-reference-mdx.md)  
  
  
