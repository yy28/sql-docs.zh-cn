---
title: NextMember (MDX) |Microsoft 文档
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 4535b837d81db10f41f1445a7051678ce4fdd688
ms.sourcegitcommit: 97bef3f248abce57422f15530c1685f91392b494
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/04/2018
ms.locfileid: "34742176"
---
# <a name="nextmember-mdx"></a>NextMember (MDX)


  返回指定成员所在级别的下一个成员。  
  
## <a name="syntax"></a>语法  
  
```  
  
Member_Expression.NextMember   
```  
  
## <a name="arguments"></a>参数  
 *Member_Expression*  
 返回成员的有效多维表达式 (MDX)。  
  
## <a name="remarks"></a>Remarks  
 **NextMember**函数返回的下一个成员，在同一级别中，包含指定的成员。  
  
## <a name="example"></a>示例  
 下例将返回作为 July 2001 成员的下一个成员的 August 2001 成员。  
  
```  
SELECT [Date].[Calendar].[Month].[July 2001].NextMember ON 0  
FROM [Adventure Works]  
```  
  
## <a name="see-also"></a>请参阅  
 [MDX 函数引用&#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
