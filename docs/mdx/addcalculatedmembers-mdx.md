---
title: AddCalculatedMembers （MDX） |Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 982484b729b59a7106b6195e361110c1d4012653
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/08/2020
ms.locfileid: "68017181"
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
 默认情况下，MDX 在解析集函数时会排除计算成员。 **AddCalculatedMembers**函数检查在 Set_Expression 中指定的集表达式 *，* 并包括作为该集表达式作用域内包含的成员的同级成员的计算成员。  
  
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
  
 下面的示例从`Measures.[Unit Price]` **艾德工作**多维数据集中返回除了**度量值**维度中的所有计算成员之外的成员。  
  
```  
SELECT  
   AddCalculatedMembers({Measures.[Unit Price]}) ON COLUMNS  
FROM   
   [Adventure Works]  
```  
  
## <a name="see-also"></a>另请参阅  
 [Mdx 函数引用 &#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
