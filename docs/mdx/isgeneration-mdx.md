---
title: "IsGeneration (MDX) |Microsoft 文档"
ms.custom: 
ms.date: 03/02/2016
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: 
ms.component: 
ms.reviewer: 
ms.suite: pro-bi
ms.technology: analysis-services
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords: ISGENERATION
dev_langs: kbMDX
helpviewer_keywords: IsGeneration function
ms.assetid: fd11d2e0-d81d-45af-ac45-c98634d05550
caps.latest.revision: "32"
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: Inactive
ms.openlocfilehash: a4bdcf4847d11284dc2901cc44f5daffc2ec5816
ms.sourcegitcommit: 9fbe5403e902eb996bab0b1285cdade281c1cb16
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/27/2017
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
  
## <a name="remarks"></a>注释  
 **IsGeneration**函数返回**true**如果指定的成员处于指定的生成编号。 否则，该函数返回**false**。 此外，如果指定的成员的计算结果为一个空的成员， **IsGeneration**函数返回**false**。  
  
 为了创建代索引，叶成员的代索引为 0。 非叶成员的代索引的确定方式为：先从指定成员的所有子成员的并集中获取最高的代索引，然后向该索引添加 1。 由于非叶成员的代索引的确定方式，一个非叶成员可能会属于多个代。  
  
## <a name="example"></a>示例  
 如果 [Date].[Fiscal].CurrentMember 属于第二代，下面的示例将返回 TRUE。  
  
 `WITH MEMBER MEASURES.ISGENERATIONDEMO AS`  
  
 `IsGeneration([Date].[Fiscal].CURRENTMEMBER, 2)`  
  
 `SELECT {MEASURES.ISGENERATIONDEMO} ON 0,`  
  
 `[Date].[Fiscal].MEMBERS ON 1`  
  
 `FROM [Adventure Works]`  
  
## <a name="see-also"></a>另请参阅  
 [MDX 函数引用 &#40;MDX &#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
