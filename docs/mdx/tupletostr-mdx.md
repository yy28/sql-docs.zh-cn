---
title: TupleToStr (MDX) |Microsoft 文档
ms.custom: ''
ms.date: 03/02/2016
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: ''
ms.component: ''
ms.reviewer: ''
ms.suite: pro-bi
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- TUPLETOSTR
dev_langs:
- kbMDX
helpviewer_keywords:
- TupletoStr function
ms.assetid: ad12347c-d1c4-4d8b-a910-3116bd6b68e0
caps.latest.revision: 32
author: Minewiskan
ms.author: owend
manager: erikre
ms.openlocfilehash: 9a3a17d50ac15f7f59b41881d95a6e0c5fc2a3a6
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
---
# <a name="tupletostr-mdx"></a>TupleToStr (MDX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  返回多维表达式 (MDX) 格式的字符串，它对应于指定的元组。  
  
## <a name="syntax"></a>语法  
  
```  
  
TupleToStr(Tuple_Expression)   
```  
  
## <a name="arguments"></a>参数  
 *Tuple_Expression*  
 返回元组的有效多维表达式 (MDX)。  
  
## <a name="remarks"></a>注释  
 此函数用于将元组的字符串表示形式传输给外部函数进行分析。 返回的字符串括在大括号{}和用逗号分隔每个成员，如果多个明确定义的元组。  
  
## <a name="examples"></a>示例  
 下面的示例返回字符串 ([Date].[Calendar Year].&[2001],[Geography].[Geography].[Country].&[United States])：  
  
```  
WITH MEMBER Measures.x AS TupleToStr   
   (   
      ([Date].[Calendar Year].&[2001]  
         , [Geography].[Geography].[Country].&[United States]  
      )  
   )     
SELECT Measures.x ON 0  
FROM [Adventure Works]  
```  
  
 下面的示例与上面的示例返回相同的字符串。  
  
```  
WITH SET s AS   
   {  
      ([Date].[Calendar Year].&[2001],  
         [Geography].[Geography].[Country].&[United States]  
      )   
   }  
MEMBER Measures.x AS TupleToStr ( s.Item(0) )  
SELECT Measures.x ON 0  
FROM [Adventure Works]  
```  
  
## <a name="see-also"></a>另请参阅  
 [MDX 函数引用 & #40;MDX & #41;](../mdx/mdx-function-reference-mdx.md)  
  
  
