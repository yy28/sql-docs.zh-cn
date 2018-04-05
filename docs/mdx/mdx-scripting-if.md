---
title: IF 语句 (MDX) |Microsoft 文档
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
dev_langs:
- kbMDX
helpviewer_keywords:
- statements [MDX], IF
ms.assetid: 8830cce5-9e06-4f89-a555-295bb0d0a8a1
caps.latest.revision: 13
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: Inactive
ms.openlocfilehash: 67376067c26a3eae41d0c090a141367fcf5cc396
ms.sourcegitcommit: f486d12078a45c87b0fcf52270b904ca7b0c7fc8
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/08/2018
---
# <a name="mdx-scripting---if"></a>MDX 脚本编写-如果
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  如果条件为真，则执行语句。  
  
## <a name="syntax"></a>语法  
  
```  
  
IF expression THEN assignment END IF  
```  
  
## <a name="arguments"></a>参数  
 *expression*  
 计算结果为返回 True 或 False 的布尔值的多维表达式 (MDX)。  
  
 *分配*  
 为子多维数据集或计算属性赋值的 MDX 表达式。  
  
## <a name="remarks"></a>Remarks  
 IF 语句用于控制流，这是与不同[IIf &#40;MDX &#41;](../mdx/iif-mdx.md)函数和[CASE 语句 &#40;MDX &#41;](../mdx/case-statement-mdx.md) ，仅可用于返回值或对象。  
  
## <a name="examples"></a>示例  
 在以下示例中，作用域限制在 Customers 维度中 Customers Geography 层次结构的 Country 级别。 如果当前度量值为 Internet Sales Amount，则 Internet Sales Amount 设置为 10：  
  
 `SCOPE ([Customer].[Customer Geography].[Country].MEMBERS);`  
  
 `IF Measures.CurrentMember IS [Measures].[Internet Sales Amount] THEN this = 10 END IF;`  
  
 `END SCOPE`;  
  
## <a name="see-also"></a>另请参阅  
 [MDX 函数引用 &#40;MDX &#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
