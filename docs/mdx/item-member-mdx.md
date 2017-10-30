---
title: "项 （成员） (MDX) |Microsoft 文档"
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
- ITEM
dev_langs:
- kbMDX
helpviewer_keywords:
- Item function
ms.assetid: 71cca249-910b-4ecd-9097-1a17b224e219
caps.latest.revision: 35
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: 4c2649598e6224c3458dfa0b0278df8d6458b7ce
ms.contentlocale: zh-cn
ms.lasthandoff: 08/02/2017

---
# <a name="item-member-mdx"></a>Item（成员）(MDX)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx_md](../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  返回指定元组中的成员。  
  
## <a name="syntax"></a>语法  
  
```  
  
Tuple_Expression.Item( Index )  
```  
  
## <a name="arguments"></a>参数  
 *Tuple_Expression*  
 返回元组的有效多维表达式 (MDX)。  
  
 *索引*  
 指定要返回元组中指定特定成员位置的有效数值表达式。  
  
## <a name="remarks"></a>注释  
 **项**函数返回从指定元组的成员。 该函数将返回指定的从零开始的位置处的成员*索引*。  
  
## <a name="example"></a>示例  
 下面的示例返回各列上的成员 `[2003]`（元组 `[Date].[Calendar Year].&[2003], [Measures].[Internet Sales Amount] ).` 中的第一项）：  
  
 `SELECT`  
  
 `{( [Date].[Calendar Year].&[2003], [Measures].[Internet Sales Amount] ).Item(0)} ON 0`  
  
 `,{[Measures].[Reseller Sales Amount]} ON 1`  
  
 `FROM [Adventure Works]`  
  
## <a name="see-also"></a>另请参阅  
 [MDX 函数引用 &#40;MDX &#41;](../mdx/mdx-function-reference-mdx.md)  
  
  

