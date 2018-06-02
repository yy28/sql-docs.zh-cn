---
title: MemberToStr (MDX) |Microsoft 文档
ms.date: 05/30/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: ac9998edcf11477a2a4aff1af951d2dc4a17cbbb
ms.sourcegitcommit: 808d23a654ef03ea16db1aa23edab496b73e5072
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/02/2018
ms.locfileid: "34581569"
---
# <a name="membertostr-mdx"></a>MemberToStr (MDX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  返回与指定成员对应的多维表达式 (MDX) 格式的字符串。  
  
## <a name="syntax"></a>语法  
  
```  
  
MemberToStr(Member_Expression)   
```  
  
## <a name="arguments"></a>参数  
 *Member_Expression*  
 返回成员的有效多维表达式 (MDX)。  
  
## <a name="remarks"></a>Remarks  
 此函数返回包含成员的唯一名称的字符串。 它通常用于将某一成员的唯一名称返回到外部函数。  
  
## <a name="example"></a>示例  
 下例返回字符串 [Geography].[Geography].[Country].&[United States]：  
  
 `WITH MEMBER Measures.x AS MemberToStr`  
  
 `([Geography].[Geography].[Country].[United States])`  
  
 `SELECT Measures.x ON 0`  
  
 `FROM [Adventure Works]`  
  
## <a name="see-also"></a>请参阅  
 [MDX 函数引用&#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
