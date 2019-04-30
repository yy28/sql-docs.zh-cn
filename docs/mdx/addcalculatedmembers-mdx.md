---
title: AddCalculatedMembers (MDX) |Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 18ccf4ad808c15945d82f1ca05616f0da878a7ca
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63201614"
---
# <a name="addcalculatedmembers-mdx"></a>AddCalculatedMembers (MDX)


  返回通过将计算成员添加到指定集而生成的集。  
  
## <a name="syntax"></a>语法  
  
```  
  
AddCalculatedMembers(Set_Expression)   
```  
  
## <a name="arguments"></a>参数  
 *Set_Expression*  
 返回集的有效多维表达式 (MDX)。  
  
## <a name="remarks"></a>备注  
 默认情况下，MDX 在解析集函数时会排除计算成员。 **AddCalculatedMembers**函数将检查中指定的集表达式*Set_Expression，* 和包括包含该集的作用域内的成员的同级的计算的成员表达式。  
  
> [!NOTE]  
>  此函数只能与一维集表达式一起使用。  
  
## <a name="examples"></a>示例  
 以下示例说明了此函数的用法。  
  
```  
-- This query returns the calculated members for the cube  
-- by retrieving all members, and then excluding non-calculated members.  
SELECT   
   AddCalculatedMembers(  
      {[Measures].Members}  
      )-[Measures].Members ON COLUMNS  
FROM [Adventure Works]   
```  
  
 下面的示例返回`Measures.[Unit Price]`成员中的所有计算成员除了**度量值**维度，从**Adventure Works**多维数据集。  
  
```  
SELECT  
   AddCalculatedMembers({Measures.[Unit Price]}) ON COLUMNS  
FROM   
   [Adventure Works]  
```  
  
## <a name="see-also"></a>请参阅  
 [MDX 函数引用 (MDX)](../mdx/mdx-function-reference-mdx.md)  
  
  
