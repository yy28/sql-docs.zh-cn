---
title: NameToSet (MDX) |Microsoft 文档
ms.date: 05/30/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 766049ff2c285de2b16e1aa67745a98eb22ef05f
ms.sourcegitcommit: 808d23a654ef03ea16db1aa23edab496b73e5072
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/02/2018
ms.locfileid: "34580269"
---
# <a name="nametoset-mdx"></a>NameToSet (MDX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  返回多维表达式 (MDX) 格式的字符串指定的成员组成的集。  
  
## <a name="syntax"></a>语法  
  
```  
  
NameToSet(Member_Name)   
```  
  
## <a name="arguments"></a>参数  
 *Member_Name*  
 代表成员名称的有效字符串表达式。  
  
## <a name="remarks"></a>Remarks  
 如果指定的成员名称存在， **NameToSet**函数返回一个包含该成员集。 否则，此函数返回空集。  
  
> [!NOTE]  
>  指定的成员名称只能是成员名称，不能是成员表达式。 若要使用一个成员表达式，请参阅[StrToSet &#40;MDX&#41;](../mdx/strtoset-mdx.md)。  
  
## <a name="example"></a>示例  
 下例返回指定成员名称的默认度量值。  
  
```  
SELECT NameToSet('[Date].[Calendar].[July 2001]') ON 0  
FROM [Adventure Works]  
```  
  
## <a name="see-also"></a>请参阅  
 [MDX 函数引用&#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
