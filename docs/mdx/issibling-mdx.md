---
title: "IsSibling (MDX) |Microsoft 文档"
ms.custom: 
ms.date: 03/02/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology: analysis-services
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords: ISSIBLING
dev_langs: kbMDX
helpviewer_keywords: IsSibling function
ms.assetid: 12f302f0-141e-4ec0-ad5f-329aade17a4d
caps.latest.revision: "31"
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: Inactive
ms.openlocfilehash: 7c8b3d48ca5be8a1468afcabe37ae98dedf52d4c
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/09/2017
---
# <a name="issibling-mdx"></a>IsSibling (MDX)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx_md](../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  返回一个指定成员是否为另一个指定成员的同级成员。  
  
## <a name="syntax"></a>语法  
  
```  
  
IsSibling(Member_Expression1, Member_Expression2)   
```  
  
## <a name="arguments"></a>参数  
 *Member_Expression1*  
 返回成员的有效多维表达式 (MDX)。  
  
 *Member_Expression2*  
 返回成员的有效多维表达式 (MDX)。  
  
## <a name="remarks"></a>注释  
 **IsSibling**函数返回**true**如果第一个指定成员是第二个指定成员的同级。 否则，该函数返回**false**。  
  
## <a name="example"></a>示例  
 如果 Date 维度的 Fiscal 层次结构上的当前成员是 2002 年 7 月的同级，则下面的示例将返回 TRUE：  
  
 `WITH MEMBER MEASURES.ISSIBLINGDEMO AS`  
  
 `IsSibling([Date].[Fiscal].CURRENTMEMBER, [Date].[Fiscal].[Month].&[2002]&[7])`  
  
 `SELECT {MEASURES.ISSIBLINGDEMO} ON 0,`  
  
 `[Date].[Fiscal].MEMBERS ON 1`  
  
 `FROM [Adventure Works]`  
  
## <a name="see-also"></a>另请参阅  
 [MDX 函数引用 &#40;MDX &#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
