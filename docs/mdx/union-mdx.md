---
title: "联合 (MDX) |Microsoft 文档"
ms.custom: 
ms.date: 03/02/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
ms.tgt_pltfrm: 
ms.topic: language-reference
dev_langs:
- kbMDX
helpviewer_keywords:
- functions [MDX], Union
ms.assetid: cc083455-8b3b-46af-bb55-1e238376f162
caps.latest.revision: 19
author: Minewiskan
ms.author: owend
manager: erikre
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: d68afa2f9c424a0bb745ad2feaf781923eac624a
ms.contentlocale: zh-cn
ms.lasthandoff: 08/02/2017

---
# <a name="union--mdx"></a>联合 (MDX)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx_md](../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  返回两个集的并集，并且可以选择保留重复成员。  
  
## <a name="syntax"></a>語法  
  
```  
  
Standard syntax  
Union(Set_Expression1, Set_Expression2 [,...n][, ALL])  
  
Alternate syntax 1  
Set_Expression1 + Set_Expression2 [+...n]  
  
Alternate syntax 2  
{Set_Expression1 , Set_Expression2 [,...n]}  
```  
  
## <a name="arguments"></a>参数  
 *集表达式 1*  
 返回集的有效多维表达式 (MDX)。  
  
 *集表达式 2*  
 返回集的有效多维表达式 (MDX)。  
  
## <a name="remarks"></a>注释  
 此函数返回的两个联合或多个指定集*。* 与标准语法和备用语法 1，默认情况下将消除重复项。 使用标准语法中，使用**所有**标志将重复项保留在已加入的组。 从该集的尾部删除重复项。 使用替代语法 2 时始终会保留重复项。  
  
## <a name="examples"></a>示例  
 下面的示例演示的行为**联合**函数使用每种语法。  
  
### <a name="standard-syntax-duplicates-eliminated"></a>标准语法，消除重复项  
  
```  
SELECT Union   
   ([Date].[Calendar Year].children  
   , {[Date].[Calendar Year].[CY 2002]}  
   , {[Date].[Calendar Year].[CY 2003]}  
   ) ON 0  
FROM [Adventure Works]  
  
```  
  
### <a name="standard-syntax-duplicates-retained"></a>标准语法，保留重复项  
  
```  
SELECT Union   
   ([Date].[Calendar Year].children  
   , {[Date].[Calendar Year].[CY 2002]}  
   , {[Date].[Calendar Year].[CY 2003]}  
   , ALL  
   ) ON 0  
FROM [Adventure Works]  
  
```  
  
### <a name="alternate-syntax-1-duplicates-eliminated"></a>替代语法 1，消除重复项  
  
```  
SELECT   
   [Date].[Calendar Year].children   
   + {[Date].[Calendar Year].[CY 2002]}   
   + {[Date].[Calendar Year].[CY 2003]} ON 0  
FROM [Adventure Works]  
  
```  
  
### <a name="alternate-syntax-2-duplicates-retained"></a>替代语法 2，保留重复项  
  
```  
SELECT   
   {[Date].[Calendar Year].children  
   , [Date].[Calendar Year].[CY 2002]  
   , [Date].[Calendar Year].[CY 2003]} ON 0  
FROM [Adventure Works]  
  
```  
  
## <a name="see-also"></a>另请参阅  
 [+ &#40;联合 &#41;&#40;MDX &#41;](../mdx/union-mdx-operator-reference.md)   
 [MDX 函数引用 &#40;MDX &#41;](../mdx/mdx-function-reference-mdx.md)  
  
  

