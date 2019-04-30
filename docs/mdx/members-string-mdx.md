---
title: Members （字符串） (MDX) |Microsoft Docs
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
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63048443"
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
  
## <a name="remarks"></a>备注  
 **Members （字符串）** 函数将返回指定其名称的单个成员。 通常情况下，使用**Members （字符串）** 函数与外部函数，为提供一起**Members （字符串）** 函数标识的成员，将字符串和**Members （字符串）** 函数返回的值，该指定成员。  
  
## <a name="example"></a>示例  
 下面的示例使用**Members （字符串）** 函数将指定的字符串转换为有效成员，然后返回字符串中指定的成员的默认度量值。 指定的字符串用单引号引起来。 默认度量值为 Reseller Sales Amount 度量值。  
  
```  
SELECT Members ('[Geography].[Geography].[Country].&[United States] ') ON 0  
FROM [Adventure Works]  
```  
  
## <a name="see-also"></a>请参阅  
 [MDX 函数引用 (MDX)](../mdx/mdx-function-reference-mdx.md)  
  
  
