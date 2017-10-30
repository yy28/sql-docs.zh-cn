---
title: "成员 (Set) (MDX) |Microsoft 文档"
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
- Members
dev_langs:
- kbMDX
helpviewer_keywords:
- Members function
ms.assetid: 0c4d5bb9-500b-47ce-b7fc-f5a10e2400e0
caps.latest.revision: 33
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: 4430d24665eb791b8567fa83e7793c64727fd88f
ms.contentlocale: zh-cn
ms.lasthandoff: 08/02/2017

---
# <a name="members-set-mdx"></a>Members（集）(MDX)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx_md](../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  返回某个维度、级别或层次结构中的成员集。  
  
## <a name="syntax"></a>語法  
  
```  
  
Hierarchy expression syntax  
Hierarchy_Expression.Members  
  
Level expression Syntax  
Level_Expression.Members  
```  
  
## <a name="arguments"></a>参数  
 *Hierarchy_Expression*  
 返回层次结构的有效多维表达式 (MDX)。  
  
 *Level_Expression*  
 返回级别的有效多维表达式 (MDX)。  
  
## <a name="remarks"></a>備註  
 如果指定一个层次结构表达式，则**成员 （设置）**函数将返回指定层次结构，不包括计算的成员内的所有成员组成的集。 若要获取计算的所有成员组成的集或否则，在层次结构上使用[AllMembers &#40;MDX &#41;](../mdx/allmembers-mdx.md)函数  
  
 如果指定一个级别表达式，则**成员 （设置）**函数返回在指定级别的所有成员组成的集。  
  
> [!IMPORTANT]  
>  如果维度仅包含单个可见层次结构，由于在此情况下维度名称将解析为其唯一可见的层次结构，所以既可以通过维度名称也可以通过层次结构名称来引用该层次结构。 例如，因为 Measures.Members 解析为 Measures 维度中唯一的层次结构，所以 Measures.Members 是有效的 MDX 表达式。  
  
## <a name="examples"></a>示例  
 下例返回 Adventure Works 多维数据集中“日历年”层次结构的所有成员的集。  
  
```  
SELECT   
   [Date].[Calendar].[Calendar Year].Members ON 0  
FROM  
   [Adventure Works]  
  
```  
  
 下面的示例将返回 `[Product].[Products].[Product Line]` 级别中每个成员在 2003 年的订单数量。 **成员**函数返回一个表示所有级别中成员集。  
  
```  
SELECT   
   {Measures.[Order Quantity]} ON COLUMNS,  
   [Product].[Product Line].[Product Line].Members ON ROWS  
FROM  
   [Adventure Works]  
WHERE  
   {[Date].[Calendar Year].[Calendar Year].&[2003]}  
```  
  
## <a name="see-also"></a>另请参阅  
 [MDX 函数引用 &#40;MDX &#41;](../mdx/mdx-function-reference-mdx.md)   
 [MDX 函数引用 &#40;MDX &#41;](../mdx/mdx-function-reference-mdx.md)  
  
  

