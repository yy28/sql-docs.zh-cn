---
title: 成员 (String) (MDX) |Microsoft 文档
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 302445cadc829de35eca28db2888aaa01673ca75
ms.sourcegitcommit: 97bef3f248abce57422f15530c1685f91392b494
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/04/2018
ms.locfileid: "34741896"
---
# <a name="members-string-mdx"></a>Members（字符串）(MDX)


  返回字符串表达式所指定的成员。  
  
## <a name="syntax"></a>语法  
  
```  
  
Members(Member_Name)   
```  
  
## <a name="arguments"></a>参数  
 *Member_Name*  
 指定成员名称的有效字符串表达式。  
  
## <a name="remarks"></a>Remarks  
 **成员 （字符串）** 函数返回其名称指定的单个成员。 通常情况下，使用**成员 （字符串）** 具有外部函数，提供到函数**成员 （字符串）** 函数标识的成员，将字符串与**成员 （字符串）** 函数返回的值为指定的成员。  
  
## <a name="example"></a>示例  
 下面的示例使用**成员 （字符串）** 函数将指定的字符串转换为有效的成员，并返回字符串中指定的成员的默认度量值。 指定的字符串用单引号引起来。 默认度量值为 Reseller Sales Amount 度量值。  
  
```  
SELECT Members ('[Geography].[Geography].[Country].&[United States] ') ON 0  
FROM [Adventure Works]  
```  
  
## <a name="see-also"></a>请参阅  
 [MDX 函数引用&#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
