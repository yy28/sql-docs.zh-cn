---
title: IF 语句（MDX） |Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 41bd34fbd3d296f4aa38877e6d26e25eba9ae726
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/08/2020
ms.locfileid: "68138692"
---
# <a name="mdx-scripting---if"></a>MDX 脚本 - IF


  如果条件为真，则执行语句。  
  
## <a name="syntax"></a>语法  
  
```  
  
IF expression THEN assignment END IF  
```  
  
## <a name="arguments"></a>参数  
 *表达式*  
 计算结果为返回 True 或 False 的布尔值的多维表达式 (MDX)。  
  
 *#a1*  
 为子多维数据集或计算属性赋值的 MDX 表达式。  
  
## <a name="remarks"></a>备注  
 对控制流使用 IF 语句，该语句不同于[IIf &#40;mdx&#41;](../mdx/iif-mdx.md)函数和[CASE 语句 &#40;mdx&#41;](../mdx/case-statement-mdx.md) ，它们只能用于返回值或对象。  
  
## <a name="examples"></a>示例  
 在以下示例中，作用域限制在 Customers 维度中 Customers Geography 层次结构的 Country 级别。 如果当前度量值为 Internet Sales Amount，则 Internet Sales Amount 设置为 10：  
  
 `SCOPE ([Customer].[Customer Geography].[Country].MEMBERS);`  
  
 `IF Measures.CurrentMember IS [Measures].[Internet Sales Amount] THEN this = 10 END IF;`  
  
 `END SCOPE`;  
  
## <a name="see-also"></a>另请参阅  
 [Mdx 函数引用 &#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
