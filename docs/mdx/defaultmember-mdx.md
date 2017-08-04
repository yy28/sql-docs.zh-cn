---
title: "DefaultMember (MDX) |Microsoft 文档"
ms.custom: 
ms.date: 03/02/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- DefaultMember
dev_langs:
- kbMDX
helpviewer_keywords:
- DefaultMember function
ms.assetid: c1b53b3a-6e73-4c41-a4fe-9f5c96da5463
caps.latest.revision: 32
author: Minewiskan
ms.author: owend
manager: erikre
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: 738d66b3c6486c51978d3a68f5fbca73598c0382
ms.contentlocale: zh-cn
ms.lasthandoff: 08/02/2017

---
# <a name="defaultmember-mdx"></a>DefaultMember (MDX)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx_md](../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  返回层次结构的默认成员。  
  
## <a name="syntax"></a>语法  
  
```  
  
Hierarchy_Expression.DefaultMember  
```  
  
## <a name="arguments"></a>参数  
 *Hierarchy_Expression*  
 返回层次结构的有效多维表达式 (MDX)。  
  
## <a name="remarks"></a>備註  
 特性的默认成员用于在查询中不包括特性的情况下计算表达式。  
  
## <a name="example"></a>示例  
 下面的示例使用**DefaultMember**函数，结合**名称**函数，以在 Adventure Works 多维数据集中返回目标货币维度的默认成员。 此示例将返回**美元**。 **名称**函数用于返回度量值的名称而不是度量值，这是默认属性**值**。  
  
```  
WITH MEMBER Measures.x AS   
   [Destination Currency].[Destination Currency].DefaultMember.Name  
SELECT Measures.x ON 0  
FROM [Adventure Works]  
```  
  
## <a name="see-also"></a>另請參閱  
 [MDX 函数引用 &#40;MDX &#41;](../mdx/mdx-function-reference-mdx.md)   
 [定义默认成员](../analysis-services/multidimensional-models/attribute-properties-define-a-default-member.md)  
  
  

