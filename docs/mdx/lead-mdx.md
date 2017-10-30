---
title: "导致 (MDX) |Microsoft 文档"
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
- LEAD
dev_langs:
- kbMDX
helpviewer_keywords:
- Lead function
ms.assetid: f3250092-7b98-40b5-8dca-77e3b50734a0
caps.latest.revision: 32
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: 127c84f38fe85453fa3da7ae2b1c9752b05b6ba7
ms.contentlocale: zh-cn
ms.lasthandoff: 08/02/2017

---
# <a name="lead-mdx"></a>Lead (MDX)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx_md](../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  返回在成员级别中比指定成员位置靠后且靠后位数为指定位数的成员。  
  
## <a name="syntax"></a>语法  
  
```  
  
Member_Expression.Lead( Index )  
```  
  
## <a name="arguments"></a>参数  
 *Member_Expression*  
 返回成员的有效多维表达式 (MDX)。  
  
 *索引*  
 指定成员位置位数的有效数值表达式。  
  
## <a name="remarks"></a>注释  
 级别内的成员位置由属性层次结构的自然顺序决定。 位置的编号从零开始。  
  
 如果指定的前导零 (0)，**导致**函数返回指定的成员。  
  
 如果所指定的潜在客户为负，**导致**函数返回之前的成员。  
  
 `Lead(1)`等效于[NextMember](../mdx/nextmember-mdx.md)函数。 `Lead(-1)`等效于[PrevMember](../mdx/prevmember-mdx.md)函数。  
  
 **导致**函数是类似于[延隔时间](../mdx/lag-mdx.md)函数，只不过**延隔时间**函数查找到相反方向**导致**函数。 也就是说，`Lead(n)` 等效于 `Lag(-n)`。  
  
## <a name="example"></a>示例  
 下例将返回 2001 年 12 月的值：  
  
```  
SELECT [Date].[Fiscal].[Month].[February 2002].Lead(-2) ON 0  
FROM [Adventure Works]  
  
```  
  
 下例将返回 2002 年 3 月的值：  
  
```  
SELECT [Date].[Fiscal].[Month].[February 2002].Lead(1) ON 0  
FROM [Adventure Works]  
  
```  
  
## <a name="see-also"></a>另请参阅  
 [MDX 函数引用 &#40;MDX &#41;](../mdx/mdx-function-reference-mdx.md)  
  
  

