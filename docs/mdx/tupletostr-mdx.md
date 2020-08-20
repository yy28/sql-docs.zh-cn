---
description: TupleToStr (MDX)
title: TupleToStr (MDX) |Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 69e81156b26d4becb05390c8684b433584793697
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/17/2020
ms.locfileid: "88487620"
---
# <a name="tupletostr-mdx"></a>TupleToStr (MDX)


  返回与指定元组相对应 (MDX) 格式字符串的多维表达式。  
  
## <a name="syntax"></a>语法  
  
```  
  
TupleToStr(Tuple_Expression)   
```  
  
## <a name="arguments"></a>参数  
 *Tuple_Expression*  
 返回元组的有效多维表达式 (MDX)。  
  
## <a name="remarks"></a>备注  
 此函数用于将元组的字符串表示形式传输给外部函数进行分析。 返回的字符串括在大括号内， {} 并且每个成员（如果有多个成员在元组中明确定义）用逗号分隔。  
  
## <a name="examples"></a>示例  
 下面的示例返回字符串 ( [Date]。[日历年]. & [2001]，[Geography]。[Geography]。[Country]. & [美国] ) ：  
  
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
 [MDX 函数引用 (MDX)](../mdx/mdx-function-reference-mdx.md)  
  
  
