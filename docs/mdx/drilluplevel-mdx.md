---
title: "DrillupLevel (MDX) |Microsoft 文档"
ms.custom: 
ms.date: 03/02/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology: analysis-services
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords: DRILLUPLEVEL
dev_langs: kbMDX
helpviewer_keywords: DrillupLevel function
ms.assetid: 63431f79-f3a1-40c4-bf57-2b6bd8991cc3
caps.latest.revision: "32"
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: Inactive
ms.openlocfilehash: 5b17f352e31fe3cb08a2ca2af629cf9cde1bc08f
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/09/2017
---
# <a name="drilluplevel-mdx"></a>DrillupLevel (MDX)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx_md](../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

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
  
## <a name="remarks"></a>注释  
 **DrillupLevel**函数将返回一组的成员按层次结构组织基于包含在指定组的成员。 指定集中的成员顺序将予以保留。  
  
 如果指定一个级别表达式，则**DrillupLevel**函数构造一个集通过检索指定的级别高于那些成员。 如果指定一个级别表达式，并且不存在该指定集内的指定级别的成员，则返回指定的集。  
  
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
 [MDX 函数引用 &#40;MDX &#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
