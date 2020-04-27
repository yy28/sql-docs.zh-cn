---
title: 为（MDX） |Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: aaf4151d8291ccd4249892c6ef8fce8a3d280f6b
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/26/2020
ms.locfileid: "67905981"
---
# <a name="is-mdx"></a>IS (MDX)


  对两个对象表达式执行逻辑比较。  
  
## <a name="syntax"></a>语法  
  
```  
  
Expression1 IS ( Expression2 | NULL )  
```  
  
#### <a name="parameters"></a>参数  
 *Expression1*  
 返回 MDX 对象引用的有效多维表达式 (MDX) 表达式。  
  
 Expression2**  
 返回 MDX 对象引用的有效 MDX 表达式。  
  
## <a name="return-value"></a>返回值  
 一个布尔值，如果两个参数引用同一个对象，则返回**true** ;否则**为 false**。 如果指定了**null**关键字，则运算符将返回**True** （如果*表达式*1 为**null**）;否则**为 false**。  
  
## <a name="remarks"></a>备注  
 **IS**运算符通常用于确定元组和成员是否是幂等的，这意味着它们完全相等。  
  
## <a name="examples"></a>示例  
 下面的示例演示如何使用**IS**运算符来检查轴上的当前成员是否为特定成员：  
  
 `With`  
  
 `//Returns TRUE if the currentmember is Bikes`  
  
 `Member [Measures].[IsBikes?] AS`  
  
 `[Product].[Category].CurrentMember IS [Product].[Category].&[1]`  
  
 `SELECT`  
  
 `{[Measures].[IsBikes?]} ON 0,`  
  
 `[Product].[Category].[Category].Members ON 1`  
  
 `FROM`  
  
 `[Adventure Works]`  
  
## <a name="see-also"></a>另请参阅  
 [Mdx 运算符引用 &#40;MDX&#41;](../mdx/mdx-operator-reference-mdx.md)  
  
  
