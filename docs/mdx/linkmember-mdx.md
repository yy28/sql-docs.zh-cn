---
title: LinkMember (MDX) |Microsoft 文档
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 71235953f592572bd7ac0dcb2493d97dd509f8b7
ms.sourcegitcommit: 97bef3f248abce57422f15530c1685f91392b494
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/04/2018
ms.locfileid: "34741496"
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
  
## <a name="remarks"></a>Remarks  
 **LinkMember**函数返回指定层次结构中与每个级别的相关的层次结构中指定的成员键值匹配的成员。 每个级别上的属性必须具有相同的键基数和数据类型。 在非自然层次结构中，如果某属性的键值有多个匹配项，结果将是错误的或不确定。  
  
## <a name="examples"></a>示例  
 下面的示例使用**LinkMember**函数以返回处于日历层次结构中的 Date.Date 属性层次结构的 2002 年 7 月 1 日成员的祖先的 Adventure Works 多维数据集中的默认度量值。  
  
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
 [Hierarchize &#40;MDX&#41;](../mdx/hierarchize-mdx.md)   
 [祖先&#40;MDX&#41;](../mdx/ascendants-mdx.md)   
 [MDX 函数引用&#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
