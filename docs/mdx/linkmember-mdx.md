---
title: LinkMember (MDX) |Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 8a00388e067878d9c2165cbae6844f8020b7c63e
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/15/2019
ms.locfileid: "67905606"
---
# <a name="linkmember-mdx"></a>LinkMember (MDX)


  返回相当于指定层次结构中的指定成员的成员。  
  
## <a name="syntax"></a>语法  
  
```  
  
LinkMember(Member_Expression, Hierarchy_Expression)   
```  
  
## <a name="arguments"></a>参数  
 *Member_Expression*  
 返回成员的有效多维表达式 (MDX)。  
  
 *Hierarchy_Expression*  
 返回层次结构的有效多维表达式 (MDX)。  
  
## <a name="remarks"></a>备注  
 **LinkMember**函数返回从指定的层次结构相匹配的键值相关的层次结构中的指定成员每个级别的成员。 每个级别上的属性必须具有相同的键基数和数据类型。 在非自然层次结构中，如果某属性的键值有多个匹配项，结果将是错误的或不确定。  
  
## <a name="examples"></a>示例  
 下面的示例使用**LinkMember**函数返回日历层次结构中 Date.Date 属性层次结构的 2002 年 7 月 1 日成员的祖先的 Adventure Works 多维数据集的默认度量值。  
  
```  
SELECT  Hierarchize  
   (Ascendants   
      (LinkMember   
         ([Date].[Date].[July 1, 2002], [Date].[Calendar]  
         )  
       )  
    ) ON 0  
FROM [Adventure Works]  
```  
  
## <a name="see-also"></a>请参阅  
 [Hierarchize (MDX)](../mdx/hierarchize-mdx.md)   
 [祖先&#40;MDX&#41;](../mdx/ascendants-mdx.md)   
 [MDX 函数引用 (MDX)](../mdx/mdx-function-reference-mdx.md)  
  
  
