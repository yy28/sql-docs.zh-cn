---
title: NextMember （MDX） |Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: b852564510c6b5918c781e0c75e84e3b30aecd44
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/08/2020
ms.locfileid: "68088366"
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
  
## <a name="remarks"></a>备注  
 **NextMember**函数返回与指定成员位于同一级别的下一个成员。  
  
## <a name="example"></a>示例  
 下例将返回作为 July 2001 成员的下一个成员的 August 2001 成员。  
  
```  
SELECT [Date].[Calendar].[Month].[July 2001].NextMember ON 0  
FROM [Adventure Works]  
```  
  
## <a name="see-also"></a>另请参阅  
 [Mdx 函数引用 &#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
