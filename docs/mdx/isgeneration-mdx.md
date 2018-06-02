---
title: IsGeneration (MDX) |Microsoft 文档
ms.date: 05/30/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 938ed8cbfab24643ceb1294a3831290c43e1bb5c
ms.sourcegitcommit: 808d23a654ef03ea16db1aa23edab496b73e5072
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/02/2018
ms.locfileid: "34578639"
---
# <a name="isgeneration-mdx"></a>IsGeneration (MDX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

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
  
## <a name="remarks"></a>Remarks  
 **IsGeneration**函数返回**true**如果指定的成员处于指定的生成编号。 否则，该函数返回**false**。 此外，如果指定的成员的计算结果为一个空的成员， **IsGeneration**函数返回**false**。  
  
 为了创建代索引，叶成员的代索引为 0。 非叶成员的代索引的确定方式为：先从指定成员的所有子成员的并集中获取最高的代索引，然后向该索引添加 1。 由于非叶成员的代索引的确定方式，一个非叶成员可能会属于多个代。  
  
## <a name="example"></a>示例  
 如果 [Date].[Fiscal].CurrentMember 属于第二代，下面的示例将返回 TRUE。  
  
 `WITH MEMBER MEASURES.ISGENERATIONDEMO AS`  
  
 `IsGeneration([Date].[Fiscal].CURRENTMEMBER, 2)`  
  
 `SELECT {MEASURES.ISGENERATIONDEMO} ON 0,`  
  
 `[Date].[Fiscal].MEMBERS ON 1`  
  
 `FROM [Adventure Works]`  
  
## <a name="see-also"></a>请参阅  
 [MDX 函数引用&#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
