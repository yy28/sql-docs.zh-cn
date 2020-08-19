---
description: DrillupLevel (MDX)
title: DrillupLevel (MDX) |Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: cfdb8e77fcb92fe208e83f45c32a5c20c5d29615
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/17/2020
ms.locfileid: "88421901"
---
# <a name="drilluplevel-mdx"></a>DrillupLevel (MDX)


  浅化某个集在指定级别以下的成员。  
  
## <a name="syntax"></a>语法  
  
```  
  
DrillupLevel(Set_Expression [ , Level_Expression ] )  
```  
  
## <a name="arguments"></a>参数  
 *Set_Expression*  
 返回集的有效多维表达式 (MDX)。  
  
 *Level_Expression*  
 返回级别的有效多维表达式 (MDX)。  
  
## <a name="remarks"></a>备注  
 **DrillupLevel**函数根据指定集内包含的成员，返回按层次结构组织的一组成员。 指定集中的成员顺序将予以保留。  
  
 如果指定了级别表达式，则 **DrillupLevel** 函数将只检索指定级别以上的成员来构造集。 如果指定了级别表达式，但指定的集中没有表示指定级别的成员，则返回指定的集。  
  
 如果未指定级别表达式，则此函数只检索那些比指定的集所引用的第一个维度的最低级别高一个级别的成员，然后用它们来构造集。  
  
## <a name="example"></a>示例  
 下例将返回位于子类别级别之上第一个集中的成员集。  
  
```  
SELECT DrillUpLevel   
  ({[Product].[Product Categories].[All Products]  
    ,[Product].[Product Categories].[Subcategory].&[32],  
    [Product].[Product Categories].[Product].&[215]},  
  [Product].[Product Categories].[Subcategory]  
    )  
  ON 0  
  FROM [Adventure Works]  
  WHERE [Measures].[Internet Order Quantity]  
```  
  
## <a name="see-also"></a>另请参阅  
 [MDX 函数引用 (MDX)](../mdx/mdx-function-reference-mdx.md)  
  
  
