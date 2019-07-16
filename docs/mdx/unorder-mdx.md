---
title: Unorder (MDX) |Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 954a71c8ca2e96d905892d77ff12b7270deded5f
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/15/2019
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
 **Unorder**函数会删除任何的排序的元组集中包含的任何其他函数或语句，如[顺序](../mdx/order-mdx.md)函数。 返回集中的元组顺序**Unorder**函数是不确定。  
  
 **Unorder**函数用作集处理的查询优化提示。 如果在集内的元组的顺序并不重要到计算或查询，使用**Unorder**函数可提供这种情况下的提高性能。 例如， [NonEmpty (MDX)](../mdx/nonempty-mdx.md)函数可以更好地提供给此函数的集时无序相比[!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]需要保留顺序，尽管与[!INCLUDE[ssASCurrent](../includes/ssascurrent-md.md)]，查询处理器会尝试执行此函数会自动为许多函数，如**总和**并**聚合**。 使用的性能优势**Unorder**才可能会非常大的集包含的元组数以百万计体现出来。  
  
## <a name="example"></a>示例  
 下面的伪代码说明了此函数的语法。  
  
```  
NonEmpty (UnOrder (<set_expression>))  
```  
  
## <a name="see-also"></a>请参阅  
 [MDX 函数引用 (MDX)](../mdx/mdx-function-reference-mdx.md)  
  
  
