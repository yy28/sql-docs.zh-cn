---
title: "项 （元组） (MDX) |Microsoft 文档"
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
f1_keywords: ITEM
dev_langs: kbMDX
helpviewer_keywords: Item function
ms.assetid: 9ee7af55-d5b5-47c8-a480-ef23878306af
caps.latest.revision: "37"
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: Inactive
ms.openlocfilehash: 9c7e727908bbd2265cab05b9d1aa2f55cc7b9ebd
ms.sourcegitcommit: f486d12078a45c87b0fcf52270b904ca7b0c7fc8
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/08/2018
---
# <a name="item-tuple-mdx"></a>Item（元组）(MDX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  返回某个集中的元组。  
  
## <a name="syntax"></a>语法  
  
```  
  
Index syntax  
Set_Expression.Item(Index)  
  
String expression syntax  
Set_Expression.Item(String_Expression1 [ ,String_Expression2,...n])  
```  
  
## <a name="arguments"></a>参数  
 *Set_Expression*  
 返回集的有效多维表达式 (MDX)。  
  
 *String_Expression1*  
 通常是以字符串表示的元组的有效字符串表达式。  
  
 *String_Expression2*  
 通常是以字符串表示的元组的有效字符串表达式。  
  
 *Index*  
 根据集中位置指定要返回的特定元组的有效数值表达式。  
  
## <a name="remarks"></a>Remarks  
 **项**函数返回指定集的元组。 有三个可能的方法来调用**项**函数：  
  
-   如果指定单个字符串表达式，则**项**函数将返回指定元组。 例如，"([2005].Q3, [Store05])"。  
  
-   如果指定多个字符串表达式，则**项**函数返回由指定的坐标定义的元组。 字符串数必须与轴数一致，而且每个字符串都必须标识一个唯一的层次结构。 例如，"[2005].Q3", "[Store05]"。  
  
-   如果指定一个整数，则**项**函数返回的从零开始的位置指定的元组*索引*。  
  
## <a name="examples"></a>示例  
 下面的示例返回 ([1996],Sales)：  
  
 `{([1996],Sales), ([1997],Sales), ([1998],Sales)}.Item(0)`  
  
 下面的示例使用一个级别表达式，并返回 Australia 中每个 State-Province 的 Internet Sales Amount 及其占 Australia 总 Internet Sales Amount 的百分比。 此示例使用 Item 函数以返回集中提取的第一个 （和仅元组）**上级**函数。  
  
```  
WITH MEMBER Measures.x AS [Measures].[Internet Sales Amount] /   
   ( [Measures].[Internet Sales Amount],    
      Ancestors   
      ( [Customer].[Customer Geography].CurrentMember,  
        [Customer].[Customer Geography].[Country]  
      ).Item (0)  
   ), FORMAT_STRING = '0%'  
SELECT {[Measures].[Internet Sales Amount], Measures.x} ON 0,  
{ Descendants   
   ( [Customer].[Customer Geography].[Country].&[Australia],  
     [Customer].[Customer Geography].[State-Province], SELF   
   )   
} ON 1  
FROM [Adventure Works]  
```  
  
## <a name="see-also"></a>另请参阅  
 [MDX 函数引用 &#40;MDX &#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
