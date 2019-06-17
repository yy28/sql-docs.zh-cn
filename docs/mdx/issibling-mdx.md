---
title: IsSibling (MDX) |Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: d86c96686357533aa1217571f3c199ec8ddff508
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/15/2019
ms.locfileid: "63125503"
---
# <a name="issibling-mdx"></a>IsSibling (MDX)


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
  
## <a name="remarks"></a>备注  
 **IsSibling**函数将返回**true**如果指定的第一个成员是第二个指定成员的同级成员。 否则，该函数返回**false**。  
  
## <a name="example"></a>示例  
 如果 Date 维度的 Fiscal 层次结构上的当前成员是 2002 年 7 月的同级，则下面的示例将返回 TRUE：  
  
 `WITH MEMBER MEASURES.ISSIBLINGDEMO AS`  
  
 `IsSibling([Date].[Fiscal].CURRENTMEMBER, [Date].[Fiscal].[Month].&[2002]&[7])`  
  
 `SELECT {MEASURES.ISSIBLINGDEMO} ON 0,`  
  
 `[Date].[Fiscal].MEMBERS ON 1`  
  
 `FROM [Adventure Works]`  
  
## <a name="see-also"></a>请参阅  
 [MDX 函数引用 (MDX)](../mdx/mdx-function-reference-mdx.md)  
  
  
