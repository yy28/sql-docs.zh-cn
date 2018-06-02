---
title: Unorder (MDX) |Microsoft 文档
ms.date: 05/30/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 9fe8d86b322aaf753f1ce45be2332095e2b85af9
ms.sourcegitcommit: 808d23a654ef03ea16db1aa23edab496b73e5072
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/02/2018
ms.locfileid: "34581329"
---
# <a name="unorder-mdx"></a>Unorder (MDX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  从指定集中删除任何强制排序。  
  
## <a name="syntax"></a>语法  
  
```  
  
Unorder(Set_Expression)   
```  
  
## <a name="arguments"></a>参数  
 *Set_Expression*  
 返回集的有效多维表达式 (MDX)。  
  
## <a name="remarks"></a>Remarks  
 **Unorder**函数中删除任何对排序集中包含的任何其他函数或语句，如元组[顺序](../mdx/order-mdx.md)函数。 返回集中的元组的顺序**Unorder**函数是不确定。  
  
 **Unorder**函数用作提示[!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]集处理的查询优化。 如果在集内的元组的顺序并不重要到计算或查询，使用**Unorder**函数可提供这种情况下的提高性能。 例如， [NonEmpty (MDX)](../mdx/nonempty-mdx.md)函数可以更好地提供对此函数的集时与无序[!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]需要保留顺序，尽管与[!INCLUDE[ssASCurrent](../includes/ssascurrent-md.md)]，查询处理器会尝试执行此函数会自动为许多函数，如**总和**和**聚合**。 使用的性能优势**Unorder**才，可能需要明显包含的元组数以百万计的非常大集。  
  
## <a name="example"></a>示例  
 下面的伪代码说明了此函数的语法。  
  
```  
NonEmpty (UnOrder (<set_expression>))  
```  
  
## <a name="see-also"></a>请参阅  
 [MDX 函数引用&#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
