---
title: TupleToStr （MDX） |Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: d6cde1f60274d1437517d89e48b111e9e7298b9d
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/27/2020
ms.locfileid: "68097373"
---
# <a name="tupletostr-mdx"></a>TupleToStr (MDX)


  返回与指定的元组相对应的多维表达式（MDX）格式的字符串。  
  
## <a name="syntax"></a>语法  
  
```  
  
TupleToStr(Tuple_Expression)   
```  
  
## <a name="arguments"></a>参数  
 *Tuple_Expression*  
 返回元组的有效多维表达式 (MDX)。  
  
## <a name="remarks"></a>备注  
 此函数用于将元组的字符串表示形式传输给外部函数进行分析。 返回的字符串括在大括号{}内，并且每个成员（如果有多个成员在元组中明确定义）用逗号分隔。  
  
## <a name="examples"></a>示例  
 下面的示例返回字符串（[Date]. [日历年]. & [2001]，[Geography]。[Geography]。[Country]. & [美国]）：  
  
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
  
  
