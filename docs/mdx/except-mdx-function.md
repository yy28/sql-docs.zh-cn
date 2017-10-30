---
title: "除非 (MDX) |Microsoft 文档"
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
- EXCEPT
dev_langs:
- kbMDX
helpviewer_keywords:
- Except function
ms.assetid: 5d832c82-1e6d-4308-9c26-7edb8afe11dd
caps.latest.revision: 37
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: 408d0cc61e2ca182f0549e899242c93994c85449
ms.contentlocale: zh-cn
ms.lasthandoff: 08/02/2017

---
# <a name="except-mdx-function"></a>除非 (MDX) 函数
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx_md](../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  计算两个集并删除第一个集中与第二个集中的元组重复的元组，也可以选择保留重复项。  
  
## <a name="syntax"></a>語法  
  
```  
  
Except(Set_Expression1, Set_Expression2 [, ALL ] )  
```  
  
## <a name="arguments"></a>参数  
 *Set_Expression1*  
 返回集的有效多维表达式 (MDX)。  
  
 *Set_Expression2*  
 返回集的有效多维表达式 (MDX)。  
  
## <a name="remarks"></a>備註  
 如果**所有**是指定的函数将保留在第一组中找到重复项; 第二组中的重复项仍将被删除。 成员的返回顺序与它们在第一个集中出现的顺序相同。  
  
## <a name="examples"></a>示例  
 以下示例说明了此函数的用法。  
  
```  
   //This query shows the quantity of orders for all products,  
   //with the exception of Components, which are not  
   //sold.  
SELECT   
   [Date].[Month of Year].Children  ON COLUMNS,  
   Except  
      ([Product].[Product Categories].[All].Children ,  
         {[Product].[Product Categories].[Components]}  
      ) ON ROWS  
FROM  
   [Adventure Works]  
WHERE  
   ([Measures].[Order Quantity])  
```  
  
## <a name="see-also"></a>另请参阅  
 [-&#40;除 &#41;&#40;MDX &#41;](../mdx/except-mdx-operator.md)   
 [MDX 函数引用 &#40;MDX &#41;](../mdx/mdx-function-reference-mdx.md)  
  
  

