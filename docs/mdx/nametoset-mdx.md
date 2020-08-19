---
description: NameToSet (MDX)
title: NameToSet (MDX) |Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: cd1de5e8c126d9457fda2c7c9545dedea26fd1f3
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/17/2020
ms.locfileid: "88483750"
---
# <a name="nametoset-mdx"></a>NameToSet (MDX)


  返回一个集，该集包含 (MDX) 格式字符串的多维表达式指定的成员。  
  
## <a name="syntax"></a>语法  
  
```  
  
NameToSet(Member_Name)   
```  
  
## <a name="arguments"></a>参数  
 *Member_Name*  
 代表成员名称的有效字符串表达式。  
  
## <a name="remarks"></a>备注  
 如果指定的成员名称存在， **NameToSet** 函数将返回包含该成员的集。 否则，此函数返回空集。  
  
> [!NOTE]  
>  指定的成员名称只能是成员名称，不能是成员表达式。 若要使用成员表达式，请参阅 [StrToSet &#40;MDX&#41;](../mdx/strtoset-mdx.md)。  
  
## <a name="example"></a>示例  
 下例返回指定成员名称的默认度量值。  
  
```  
SELECT NameToSet('[Date].[Calendar].[July 2001]') ON 0  
FROM [Adventure Works]  
```  
  
## <a name="see-also"></a>另请参阅  
 [MDX 函数引用 (MDX)](../mdx/mdx-function-reference-mdx.md)  
  
  
