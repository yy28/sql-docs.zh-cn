---
title: IsGeneration (MDX) |Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: a726470f89f2d3ea1677259e849735a09909a42d
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62629402"
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
 **IsGeneration**函数将返回**true**如果指定的成员在指定的生成编号。 否则，该函数返回**false**。 此外，如果指定的成员的计算结果为空成员，则**IsGeneration**函数将返回**false**。  
  
 为了创建代索引，叶成员的代索引为 0。 非叶成员的代索引的确定方式为：先从指定成员的所有子成员的并集中获取最高的代索引，然后向该索引添加 1。 由于非叶成员的代索引的确定方式，一个非叶成员可能会属于多个代。  
  
## <a name="example"></a>示例  
 如果 [Date].[Fiscal].CurrentMember 属于第二代，下面的示例将返回 TRUE。  
  
 `WITH MEMBER MEASURES.ISGENERATIONDEMO AS`  
  
 `IsGeneration([Date].[Fiscal].CURRENTMEMBER, 2)`  
  
 `SELECT {MEASURES.ISGENERATIONDEMO} ON 0,`  
  
 `[Date].[Fiscal].MEMBERS ON 1`  
  
 `FROM [Adventure Works]`  
  
## <a name="see-also"></a>请参阅  
 [MDX 函数引用 (MDX)](../mdx/mdx-function-reference-mdx.md)  
  
  
