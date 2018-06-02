---
title: 父 (MDX) |Microsoft 文档
ms.date: 05/30/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 32922aebffd9704725e534742656b86348f5e1ee
ms.sourcegitcommit: 808d23a654ef03ea16db1aa23edab496b73e5072
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/02/2018
ms.locfileid: "34580639"
---
# <a name="parent-mdx"></a>Parent (MDX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  返回成员的父成员。  
  
## <a name="syntax"></a>语法  
  
```  
  
Member_Expression.Parent   
```  
  
## <a name="arguments"></a>参数  
 *Member_Expression*  
 返回成员的有效多维表达式 (MDX)。  
  
## <a name="remarks"></a>Remarks  
 **父**函数将返回指定成员的父成员。  
  
## <a name="examples"></a>示例  
 以下例返回“July 1, 2001”成员的父成员。 第一个示例在日期属性层次结构的上下文中指定了该成员并返回“所有时期”成员。  
  
```  
SELECT [Date].[Date].[July 1, 2001].Parent ON 0  
FROM [Adventure Works]  
```  
  
 下例在日历层次结构的上下文中指定了“July 1, 2001”成员。  
  
```  
SELECT [Date].[Calendar].[July 1, 2001].Parent ON 0  
FROM [Adventure Works]  
```  
  
## <a name="see-also"></a>请参阅  
 [MDX 函数引用&#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
