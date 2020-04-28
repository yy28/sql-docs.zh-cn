---
title: Unorder （MDX） |Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 954a71c8ca2e96d905892d77ff12b7270deded5f
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/27/2020
ms.locfileid: "68097257"
---
# <a name="unorder-mdx"></a>Unorder (MDX)


  从指定集中删除任何强制排序。  
  
## <a name="syntax"></a>语法  
  
```  
  
Unorder(Set_Expression)   
```  
  
## <a name="arguments"></a>参数  
 *Set_Expression*  
 返回集的有效多维表达式 (MDX)。  
  
## <a name="remarks"></a>备注  
 **Unorder**函数删除由任何其他函数或语句（如[Order](../mdx/order-mdx.md)函数）对集中包含的元组施加的任何排序。 **Unorder**函数返回的集中的元组顺序是不确定的。  
  
 **Unorder**函数用作对用于处理集的查询优化的提示。 如果集内的元组顺序对计算或查询不重要，则使用**Unorder**函数可以在这种情况下提高性能。 例如，如果提供给此函数的集的顺序[!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]与需要保留顺序的顺序[!INCLUDE[ssASCurrent](../includes/ssascurrent-md.md)]不同，则非[空（MDX）](../mdx/nonempty-mdx.md)函数的性能可能会更好，查询处理器会尝试自动对许多函数（如**Sum**和**Aggregate**）执行此函数。 使用**Unorder**的性能优势仅在包含数百万元组的超大型集上很有帮助。  
  
## <a name="example"></a>示例  
 下面的伪代码说明了此函数的语法。  
  
```  
NonEmpty (UnOrder (<set_expression>))  
```  
  
## <a name="see-also"></a>另请参阅  
 [MDX 函数引用 (MDX)](../mdx/mdx-function-reference-mdx.md)  
  
  
