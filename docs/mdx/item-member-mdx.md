---
title: 项（成员） |Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: d7afa88f9d6239c8da7cb9c406ef11f0764f8dcf
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/26/2020
ms.locfileid: "67905912"
---
# <a name="item-member-mdx"></a>Item（成员）(MDX)


  返回指定元组中的成员。  
  
## <a name="syntax"></a>语法  
  
```  
  
Tuple_Expression.Item( Index )  
```  
  
## <a name="arguments"></a>参数  
 *Tuple_Expression*  
 返回元组的有效多维表达式 (MDX)。  
  
 *索引*  
 指定要返回元组中指定特定成员位置的有效数值表达式。  
  
## <a name="remarks"></a>备注  
 **Item**函数返回指定元组中的成员。 函数返回在*Index*指定的从零开始的位置找到的成员。  
  
## <a name="example"></a>示例  
 下面的示例返回各列上的成员 `[2003]`（元组 `[Date].[Calendar Year].&[2003], [Measures].[Internet Sales Amount] ).` 中的第一项）：  
  
 `SELECT`  
  
 `{( [Date].[Calendar Year].&[2003], [Measures].[Internet Sales Amount] ).Item(0)} ON 0`  
  
 `,{[Measures].[Reseller Sales Amount]} ON 1`  
  
 `FROM [Adventure Works]`  
  
## <a name="see-also"></a>另请参阅  
 [MDX 函数引用 (MDX)](../mdx/mdx-function-reference-mdx.md)  
  
  
