---
title: "- （除外）(MDX) |Microsoft 文档"
ms.custom: 
ms.date: 03/02/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology: analysis-services
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords: '-'
dev_langs: kbMDX
helpviewer_keywords:
- Except operator [MDX]
- '- (except operator)'
ms.assetid: 8971a09d-b254-4c4c-a099-103664783589
caps.latest.revision: "39"
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: Inactive
ms.openlocfilehash: 600b9135825aa7e7363c3a3b62db3c19ddc23a31
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/09/2017
---
# <a name="except-mdx-operator"></a>除非 (MDX) 运算符
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx_md](../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  执行一个集运算，以返回两个集之间的不同项并删除重复成员。  
  
## <a name="syntax"></a>语法  
  
```  
  
Set_Expression - Set_Expression  
```  
  
#### <a name="parameters"></a>Parameters  
 *Set_Expression*  
 返回集的有效多维表达式 (MDX)。  
  
## <a name="return-value"></a>返回值  
 由两个指定集的非共享成员组成的集。  
  
## <a name="remarks"></a>注释  
 **-（除外）**运算符在功能上等效于[除](../mdx/except-mdx-function.md)函数。  
  
## <a name="examples"></a>示例  
 以下示例演示此运算符的用法：  
  
```  
// This query shows the quantity of orders for all product categories  
// with the exception of Components.  
SELECT   
   [Measures].[Order Quantity] ON COLUMNS,  
   [Product].[Product Categories].[All].Children   
   - [Product].[Product Categories].[Components] ON ROWS  
FROM  
    [Adventure Works]  
```  
  
## <a name="see-also"></a>另请参阅  
 [MDX 运算符参考 &#40;MDX &#41;](../mdx/mdx-operator-reference-mdx.md)  
  
  
