---
title: '- （除外）(MDX) |Microsoft 文档'
ms.custom: ''
ms.date: 03/02/2016
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: ''
ms.component: ''
ms.reviewer: ''
ms.suite: pro-bi
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- '-'
dev_langs:
- kbMDX
helpviewer_keywords:
- Except operator [MDX]
- '- (except operator)'
ms.assetid: 8971a09d-b254-4c4c-a099-103664783589
caps.latest.revision: 39
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: Inactive
ms.openlocfilehash: 4fc33673c259a898d36f54ad6da587a184009352
ms.sourcegitcommit: f486d12078a45c87b0fcf52270b904ca7b0c7fc8
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/08/2018
---
# <a name="except-mdx-operator"></a>除非 (MDX) 运算符
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

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
  
## <a name="remarks"></a>Remarks  
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
  
  
