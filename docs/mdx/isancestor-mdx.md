---
title: "IsAncestor (MDX) |Microsoft 文档"
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
- ISANCESTOR
dev_langs:
- kbMDX
helpviewer_keywords:
- IsAncestor function
ms.assetid: 49d2fcdf-8d9a-4c79-bd00-4910ea149141
caps.latest.revision: 32
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: eb2d6dcfb4e5d0992a522c060947d942a5b48a53
ms.contentlocale: zh-cn
ms.lasthandoff: 08/02/2017

---
# <a name="isancestor-mdx"></a>IsAncestor (MDX)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx_md](../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  返回一个指定成员是否为另一个指定成员的祖先。  
  
## <a name="syntax"></a>语法  
  
```  
  
IsAncestor(Member_Expression1, Member_Expression2)   
```  
  
## <a name="arguments"></a>参数  
 *Member_Expression1*  
 返回成员的有效多维表达式 (MDX)。  
  
 *Member_Expression2*  
 返回成员的有效多维表达式 (MDX)。  
  
## <a name="remarks"></a>備註  
 **IsAncestor**函数返回**true**如果指定的第一个成员为指定的第二个成员的祖先。 否则，该函数返回**false**。  
  
## <a name="example"></a>示例  
 下面的示例返回**true**如果 [Date]。 [会计]。CurrentMember 是 2003 年 1 月的祖先：  
  
 `WITH MEMBER MEASURES.ISANCESTORDEMO AS`  
  
 `IsAncestor([Date].[Fiscal].CurrentMember, [Date].[Fiscal].[Month].&[2003]&[1])`  
  
 `SELECT MEASURES.ISANCESTORDEMO ON 0,`  
  
 `[Date].[Fiscal].MEMBERS ON 1`  
  
 `FROM [Adventure Works]`  
  
## <a name="see-also"></a>另請參閱  
 [上级 &#40;MDX &#41;](../mdx/ancestor-mdx.md)   
 [MDX 函数引用 &#40;MDX &#41;](../mdx/mdx-function-reference-mdx.md)  
  
  

