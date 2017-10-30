---
title: "延隔时间 (MDX) |Microsoft 文档"
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
- LAG
dev_langs:
- kbMDX
helpviewer_keywords:
- Lag function
ms.assetid: 08c704ea-35d8-44ee-abe5-93bd24b99906
caps.latest.revision: 34
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: eedeae82c5b7566f0c59a6876fc6743c61794de0
ms.contentlocale: zh-cn
ms.lasthandoff: 08/02/2017

---
# <a name="lag-mdx"></a>Lag (MDX)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx_md](../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  返回在成员级别中比指定成员位置靠前且靠前位数为指定位数的成员。  
  
## <a name="syntax"></a>语法  
  
```  
  
Member_Expression.Lag(Index)   
```  
  
## <a name="arguments"></a>参数  
 *Member_Expression*  
 返回成员的有效多维表达式 (MDX)。  
  
 *索引*  
 指定成员位置滞后位数的有效数值表达式。  
  
## <a name="remarks"></a>備註  
 级别内的成员位置由属性层次结构的自然顺序决定。 位置的编号从零开始。  
  
 如果指定的滞后为零，**延隔时间**函数将返回指定的成员本身。  
  
 如果指定的滞后为负，**延隔时间**函数返回的后续成员。  
  
 `Lag(1)`等效于[PrevMember](../mdx/prevmember-mdx.md)函数。 `Lag(-1)`等效于[NextMember](../mdx/nextmember-mdx.md)函数。  
  
 **延隔时间**函数是类似于[导致](../mdx/lead-mdx.md)函数，只不过**导致**函数查找到相反方向**延隔时间**函数。 也就是说，`Lag(n)` 等效于 `Lead(-n)`。  
  
## <a name="example"></a>示例  
 下例将返回 2001 年 12 月的值：  
  
```  
SELECT [Date].[Fiscal].[Month].[February 2002].Lag(2) ON 0  
FROM [Adventure Works]  
  
```  
  
 下例将返回 2002 年 3 月的值：  
  
```  
SELECT [Date].[Fiscal].[Month].[February 2002].Lag(-1) ON 0  
FROM [Adventure Works]  
  
```  
  
## <a name="see-also"></a>另请参阅  
 [MDX 函数引用 &#40;MDX &#41;](../mdx/mdx-function-reference-mdx.md)  
  
  

