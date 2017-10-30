---
title: "StdevP (MDX) |Microsoft 文档"
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
- STDEVP
dev_langs:
- kbMDX
helpviewer_keywords:
- StdevP function [MDX]
ms.assetid: cd8ae7c9-3cef-49f0-bb41-8f577c7b6f31
caps.latest.revision: 30
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: d72eb148aafccc60aa5097c8c7fed7f8b842a583
ms.contentlocale: zh-cn
ms.lasthandoff: 08/02/2017

---
# <a name="stdevp-mdx"></a>StdevP (MDX)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx_md](../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  返回数值表达式对集求得使用有偏差的总体公式计算总体标准偏差 (除以 *n* )。  
  
## <a name="syntax"></a>语法  
  
```  
  
StdevP(Set_Expression [ ,Numeric_Expression ] )  
```  
  
## <a name="arguments"></a>参数  
 *Set_Expression*  
 返回集的有效多维表达式 (MDX)。  
  
 *Numeric_Expression*  
 返回数字的有效数值表达式，通常为单元坐标的多维表达式 (MDX)。  
  
## <a name="remarks"></a>備註  
 **StdevP**函数使用有偏差的总体公式、 时[Stdev](../mdx/stdev-mdx.md)函数使用无偏差的总体公式。  
  
## <a name="example"></a>示例  
 下面的示例将使用有偏差总体公式返回对 2003 日历年度中前三个月求得的 Internet Order Quantity 的标准偏差。  
  
```  
WITH MEMBER Measures.x AS   
   StdevP   
   ( { [Date].[Calendar].[Month].[January 2003],  
       [Date].[Calendar].[Month].[February 2003],  
       [Date].[Calendar].[Month].[March 2003]},  
    [Measures].[Internet Order Quantity])  
SELECT Measures.x ON 0  
FROM [Adventure Works]  
```  
  
## <a name="see-also"></a>另請參閱  
 [MDX 函数引用 &#40;MDX &#41;](../mdx/mdx-function-reference-mdx.md)  
  
  

