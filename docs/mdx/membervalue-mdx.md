---
title: "MemberValue (MDX) |Microsoft 文档"
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
- MEMBERVALUE
dev_langs:
- kbMDX
helpviewer_keywords:
- MemberValue function
ms.assetid: f9b2af16-2b81-48e4-ae81-99f64e4bbc98
caps.latest.revision: 15
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: 2ede5ef1aa5903095bc990ed6871682ce341e77b
ms.contentlocale: zh-cn
ms.lasthandoff: 08/02/2017

---
# <a name="membervalue-mdx"></a>MemberValue (MDX)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx_md](../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  返回成员的值。  
  
## <a name="syntax"></a>语法  
  
```  
  
Member_Expression.MemberValue  
```  
  
## <a name="arguments"></a>参数  
 *Member_Expression*  
 计算结果为成员的有效多维表达式 (MDX)。  
  
## <a name="return-value"></a>返回值  
 返回的成员值包含以下信息（按这些信息在返回值中出现的顺序列出）：  
  
-   值绑定（如果已定义）。  
  
-   原始数据类型的键（如果不存在名称绑定，或者键和标题绑定到同一列）。  
  
-   成员的标题。  
  
## <a name="example"></a>示例  
 下例将返回 Adventure Works 多维数据集 Date 维度中的第一个日期的值绑定、成员键和标题。  
  
```  
WITH MEMBER Measures.ValueColumn as [Date].[Calendar].[July 1, 2001].MemberValue  
MEMBER Measures.KeyColumn as [Date].[Calendar].[July 1, 2001].Member_Key  
MEMBER Measures.NameColumn as [Date].[Calendar].[July 1, 2001].Member_Name  
  
SELECT {Measures.ValueColumn, Measures.KeyColumn, Measures.NameColumn}  ON 0  
from [Adventure Works]  
```  
  
## <a name="see-also"></a>另请参阅  
 [MDX 函数引用 &#40;MDX &#41;](../mdx/mdx-function-reference-mdx.md)  
  
  

