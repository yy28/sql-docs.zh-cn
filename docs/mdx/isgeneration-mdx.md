---
title: IsGeneration （MDX） |Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 401a11a10f190cda8efeaffa04e1025ef7f4e681
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/27/2020
ms.locfileid: "68105227"
---
# <a name="isgeneration-mdx"></a>IsGeneration (MDX)


  返回指定成员是否处于指定的代中。  
  
## <a name="syntax"></a>语法  
  
```  
  
IsGeneration(Member_Expression, Generation_Number)   
```  
  
## <a name="arguments"></a>参数  
 *Member_Expression*  
 返回成员的有效多维表达式 (MDX)。  
  
 *Generation_Number*  
 指定对指定成员进行计算的代的数值表达式。  
  
## <a name="remarks"></a>备注  
 如果指定的成员处于指定的世代号，则**IsGeneration**函数返回**true** 。 否则，该函数返回**false**。 此外，如果指定成员的计算结果为空成员，则**IsGeneration**函数返回**false**。  
  
 为了创建代索引，叶成员的代索引为 0。 非叶成员的代索引的确定方式为：先从指定成员的所有子成员的并集中获取最高的代索引，然后向该索引添加 1。 由于非叶成员的代索引的确定方式，一个非叶成员可能会属于多个代。  
  
## <a name="example"></a>示例  
 如果 [Date].[Fiscal].CurrentMember 属于第二代，下面的示例将返回 TRUE。  
  
 `WITH MEMBER MEASURES.ISGENERATIONDEMO AS`  
  
 `IsGeneration([Date].[Fiscal].CURRENTMEMBER, 2)`  
  
 `SELECT {MEASURES.ISGENERATIONDEMO} ON 0,`  
  
 `[Date].[Fiscal].MEMBERS ON 1`  
  
 `FROM [Adventure Works]`  
  
## <a name="see-also"></a>另请参阅  
 [MDX 函数引用 (MDX)](../mdx/mdx-function-reference-mdx.md)  
  
  
