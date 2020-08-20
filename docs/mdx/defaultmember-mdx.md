---
description: DefaultMember (MDX)
title: DefaultMember (MDX) |Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 6037d5089b9d0fa67599728ce35082432b0a570c
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/17/2020
ms.locfileid: "88456667"
---
# <a name="defaultmember-mdx"></a>DefaultMember (MDX)


  返回层次结构的默认成员。  
  
## <a name="syntax"></a>语法  
  
```  
  
Hierarchy_Expression.DefaultMember  
```  
  
## <a name="arguments"></a>参数  
 *Hierarchy_Expression*  
 返回层次结构的有效多维表达式 (MDX)。  
  
## <a name="remarks"></a>备注  
 特性的默认成员用于在查询中不包括特性的情况下计算表达式。  
  
## <a name="example"></a>示例  
 下面的示例将 **DefaultMember** 函数与 **Name** 函数结合使用，以返回艾德工作多维数据集中目标货币维度的默认成员。 该示例返回 **美元**。 **Name**函数用于返回度量值的名称，而不是度量**值**的默认属性。  
  
```  
WITH MEMBER Measures.x AS   
   [Destination Currency].[Destination Currency].DefaultMember.Name  
SELECT Measures.x ON 0  
FROM [Adventure Works]  
```  
  
## <a name="see-also"></a>另请参阅  
 [Mdx 函数引用 &#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)   
 [定义默认成员](https://docs.microsoft.com/analysis-services/multidimensional-models/attribute-properties-define-a-default-member)  
  
  
