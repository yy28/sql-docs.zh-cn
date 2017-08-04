---
title: "LinkMember (MDX) |Microsoft 文档"
ms.custom: 
ms.date: 03/02/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- LINKMEMBER
dev_langs:
- kbMDX
helpviewer_keywords:
- LinkMember function
ms.assetid: b9106f07-8ea2-4933-aed3-ee9c63acf7ac
caps.latest.revision: 33
author: Minewiskan
ms.author: owend
manager: erikre
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: c87723c4d7db370b46b2e41cf2d67064f1978f91
ms.contentlocale: zh-cn
ms.lasthandoff: 08/02/2017

---
# <a name="linkmember-mdx"></a>LinkMember (MDX)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx_md](../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  返回相当于指定层次结构中的指定成员的成员。  
  
## <a name="syntax"></a>語法  
  
```  
  
LinkMember(Member_Expression, Hierarchy_Expression)   
```  
  
## <a name="arguments"></a>参数  
 *Member_Expression*  
 返回成员的有效多维表达式 (MDX)。  
  
 *Hierarchy_Expression*  
 返回层次结构的有效多维表达式 (MDX)。  
  
## <a name="remarks"></a>備註  
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
  
## <a name="see-also"></a>另请参阅  
 [Hierarchize &#40;MDX &#41;](../mdx/hierarchize-mdx.md)   
 [祖先 &#40;MDX &#41;](../mdx/ascendants-mdx.md)   
 [MDX 函数引用 &#40;MDX &#41;](../mdx/mdx-function-reference-mdx.md)  
  
  

