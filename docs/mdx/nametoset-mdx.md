---
title: "NameToSet (MDX) |Microsoft 文档"
ms.custom: 
ms.date: 03/02/2016
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: 
ms.component: 
ms.reviewer: 
ms.suite: pro-bi
ms.technology: analysis-services
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords: NAMETOSET
dev_langs: kbMDX
helpviewer_keywords: NameToSet function
ms.assetid: e02e17d5-4309-49cb-84c7-5b445ac2bd94
caps.latest.revision: "32"
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: Inactive
ms.openlocfilehash: adf905695fd42a64f4f4705222fcf52f624f509a
ms.sourcegitcommit: 9fbe5403e902eb996bab0b1285cdade281c1cb16
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/27/2017
---
# <a name="nametoset-mdx"></a>NameToSet (MDX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  返回多维表达式 (MDX) 格式的字符串指定的成员组成的集。  
  
## <a name="syntax"></a>语法  
  
```  
  
NameToSet(Member_Name)   
```  
  
## <a name="arguments"></a>参数  
 *Member_Name*  
 代表成员名称的有效字符串表达式。  
  
## <a name="remarks"></a>注释  
 如果指定的成员名称存在， **NameToSet**函数返回一个包含该成员集。 否则，此函数返回空集。  
  
> [!NOTE]  
>  指定的成员名称只能是成员名称，不能是成员表达式。 若要使用一个成员表达式，请参阅[StrToSet &#40;MDX &#41;](../mdx/strtoset-mdx.md).  
  
## <a name="example"></a>示例  
 下例返回指定成员名称的默认度量值。  
  
```  
SELECT NameToSet('[Date].[Calendar].[July 2001]') ON 0  
FROM [Adventure Works]  
```  
  
## <a name="see-also"></a>另请参阅  
 [MDX 函数引用 &#40;MDX &#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
