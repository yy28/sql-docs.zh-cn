---
title: "成员 (String) (MDX) |Microsoft 文档"
ms.custom: 
ms.date: 03/02/2016
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: 
ms.component: 
ms.reviewer: 
ms.suite: pro-bi
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords: Members
dev_langs: kbMDX
helpviewer_keywords: Members function
ms.assetid: 21fca354-448b-4b05-93f4-111bde1568f1
caps.latest.revision: "35"
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: Inactive
ms.openlocfilehash: a561739e4a0963b42080e2f27e7ce664d887870d
ms.sourcegitcommit: f486d12078a45c87b0fcf52270b904ca7b0c7fc8
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/08/2018
---
# <a name="members-string-mdx"></a>Members（字符串）(MDX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  返回字符串表达式所指定的成员。  
  
## <a name="syntax"></a>语法  
  
```  
  
Members(Member_Name)   
```  
  
## <a name="arguments"></a>参数  
 *Member_Name*  
 指定成员名称的有效字符串表达式。  
  
## <a name="remarks"></a>Remarks  
 **成员 （字符串）**函数返回其名称指定的单个成员。 通常情况下，使用**成员 （字符串）**具有外部函数，提供到函数**成员 （字符串）**函数标识的成员，将字符串与**成员 （字符串）**函数返回的值为指定的成员。  
  
## <a name="example"></a>示例  
 下面的示例使用**成员 （字符串）**函数将指定的字符串转换为有效的成员，并返回字符串中指定的成员的默认度量值。 指定的字符串用单引号引起来。 默认度量值为 Reseller Sales Amount 度量值。  
  
```  
SELECT Members ('[Geography].[Geography].[Country].&[United States] ') ON 0  
FROM [Adventure Works]  
```  
  
## <a name="see-also"></a>另请参阅  
 [MDX 函数引用 &#40;MDX &#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
