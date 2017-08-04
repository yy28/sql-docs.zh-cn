---
title: "SetToStr (MDX) |Microsoft 文档"
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
- SETTOSTR
dev_langs:
- kbMDX
helpviewer_keywords:
- SetToStr function
ms.assetid: b761e002-26cd-460e-b424-fb8e306746fa
caps.latest.revision: 30
author: Minewiskan
ms.author: owend
manager: erikre
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: e0a2db653917d53ac25c290bd6dc14f3afe2cd09
ms.contentlocale: zh-cn
ms.lasthandoff: 08/02/2017

---
# <a name="settostr-mdx"></a>SetToStr (MDX)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx_md](../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  返回多维表达式 (MDX) 格式的字符串，它对应于指定的集合。  
  
## <a name="syntax"></a>语法  
  
```  
  
SetToStr(Set_Expression)  
```  
  
## <a name="arguments"></a>参数  
 *Set_Expression*  
 返回集的有效多维表达式 (MDX)。  
  
## <a name="remarks"></a>備註  
 该函数用于将某集的字符串表示形式传输到外部函数，以进行分析。 返回的字符串以括号 {} 括起，并用逗号分隔集中的每一项。  
  
## <a name="example"></a>示例  
 下面的示例将返回包含 Geography.Country 属性层次结构的所有成员的字符串。  
  
```  
WITH MEMBER Measures.x AS SetToStr (Geography.Geography.Children)  
SELECT Measures.x ON 0  
FROM [Adventure Works]  
```  
  
## <a name="see-also"></a>另请参阅  
 [MDX 函数引用 &#40;MDX &#41;](../mdx/mdx-function-reference-mdx.md)  
  
  

