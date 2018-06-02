---
title: AddCalculatedMembers (MDX) |Microsoft 文档
ms.date: 05/30/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 5a9c154588c359c942e6d64a0afdadff981e1bf5
ms.sourcegitcommit: 808d23a654ef03ea16db1aa23edab496b73e5072
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/02/2018
ms.locfileid: "34576929"
---
# <a name="addcalculatedmembers-mdx"></a>AddCalculatedMembers (MDX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  返回通过将计算成员添加到指定集而生成的集。  
  
## <a name="syntax"></a>语法  
  
```  
  
AddCalculatedMembers(Set_Expression)   
```  
  
## <a name="arguments"></a>参数  
 *Set_Expression*  
 返回集的有效多维表达式 (MDX)。  
  
## <a name="remarks"></a>Remarks  
 默认情况下，MDX 在解析集函数时会排除计算成员。 **AddCalculatedMembers**函数将检查中指定的集表达式*值赋，* 和包括包含作用域内的成员的同级的计算的成员的集表达式。  
  
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
  
 下面的示例返回`Measures.[Unit Price]`成员，除了中的所有计算成员**度量值**维度，从**Adventure Works**多维数据集。  
  
```  
SELECT  
   AddCalculatedMembers({Measures.[Unit Price]}) ON COLUMNS  
FROM   
   [Adventure Works]  
```  
  
## <a name="see-also"></a>请参阅  
 [MDX 函数引用&#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
