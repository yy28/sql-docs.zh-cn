---
title: Wtd (MDX) |Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: eee40829c72394bf95a1bc06540a434a1c74e166
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/15/2019
ms.locfileid: "68125811"
---
# <a name="wtd-mdx"></a>Wtd (MDX)


  按照时间维度中的周级别的约束，从给定成员所在的级别返回一组同级成员，从第一个同级成员开始到给定成员为止。  
  
## <a name="syntax"></a>语法  
  
```  
  
Wtd( [ Member_Expression ] )  
```  
  
## <a name="arguments"></a>参数  
 *Member_Expression*  
 返回成员的有效多维表达式 (MDX)。  
  
## <a name="remarks"></a>备注  
 如果未指定成员表达式，默认值是第一个层次结构的当前成员级别类型为时间类型的第一个维度中的周数 (**Time.CurrentMember**) 度量值组中。  
  
 **Wtd**的快捷函数技术支持部门[PeriodsToDate](../mdx/periodstodate-mdx.md)函数，其中的级别设置为*周*。 也就是说，`Wtd(Member_Expression)` 等效于 `PeriodsToDate(Week_Level_Expression,Member_Expression)`。  
  
## <a name="see-also"></a>请参阅  
 [Qtd &#40;MDX&#41;](../mdx/qtd-mdx.md)   
 [Mtd &#40;MDX&#41;](../mdx/mtd-mdx.md)   
 [Ytd &#40;MDX&#41;](../mdx/ytd-mdx.md)   
 [MDX 函数引用 (MDX)](../mdx/mdx-function-reference-mdx.md)  
  
  
