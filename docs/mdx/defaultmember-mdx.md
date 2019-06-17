---
title: DefaultMember (MDX) |Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 3a0c11acadcbdcadfd9398baff09db9292c87eb2
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/15/2019
ms.locfileid: "63248133"
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
 下面的示例使用**DefaultMember**函数，结合**名称**函数，返回 Adventure Works 多维数据集中的 Destination Currency 维度的默认成员。 该示例将返回**美元**。 **名称**函数用于返回的度量值名称，而不是默认属性的度量值是**值**。  
  
```  
WITH MEMBER Measures.x AS   
   [Destination Currency].[Destination Currency].DefaultMember.Name  
SELECT Measures.x ON 0  
FROM [Adventure Works]  
```  
  
## <a name="see-also"></a>请参阅  
 [MDX 函数引用 (MDX)](../mdx/mdx-function-reference-mdx.md)   
 [定义默认成员](../analysis-services/multidimensional-models/attribute-properties-define-a-default-member.md)  
  
  
