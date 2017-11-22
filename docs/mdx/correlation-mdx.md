---
title: "相关 (MDX) |Microsoft 文档"
ms.custom: 
ms.date: 03/02/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology: analysis-services
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords: CORRELATION
dev_langs: kbMDX
helpviewer_keywords: Correlation function
ms.assetid: 9b3662c9-95a1-4644-b952-9460fe0cf160
caps.latest.revision: "38"
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: Inactive
ms.openlocfilehash: a1a9e2ff1dc496787d0e001a20e9545852904096
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/09/2017
---
# <a name="correlation-mdx"></a>Correlation (MDX)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx_md](../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  返回对集求值的 X-Y 值对的关联系数。  
  
## <a name="syntax"></a>语法  
  
```  
  
Correlation( Set_Expression, Numeric_Expression_y [ ,Numeric_Expression_x ] )  
```  
  
## <a name="arguments"></a>参数  
 *Set_Expression*  
 返回集的有效多维表达式 (MDX)。  
  
 *Numeric_Expression_y*  
 返回表示 Y 轴值的数字的有效数值表达式，通常是单元坐标的多维表达式 (MDX)。  
  
 *Numeric_Expression_x*  
 通常是单元坐标（返回代表 X 轴的值的数字）的多维表达式 (MDX) 的有效数值表达式。  
  
## <a name="remarks"></a>注释  
 **相关**函数通过第一个评估针对可获取 y 轴的值的第一个数值表达式对指定的集来计算的值的两个对相关系数。 然后，此函数根据第二个数值表达式（如果存在）对指定集求值，以获取 X 轴对应的值。 如果未指定第二个数值表达式，则此函数使用指定集中的单元的当前上下文作为 X 轴的值。  
  
> [!NOTE]  
>  **相关**函数将忽略空单元格包含文本或逻辑值。 但是，该函数将包含值为零的单元。  
  
## <a name="see-also"></a>另请参阅  
 [MDX 函数引用 &#40;MDX &#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
