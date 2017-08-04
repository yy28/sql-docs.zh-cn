---
title: "BottomSum (MDX) |Microsoft 文档"
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
- BOTTOMSUM
dev_langs:
- kbMDX
helpviewer_keywords:
- BottomSum function
ms.assetid: b3b10e68-2a36-4c38-85f4-3bb7917d5ae8
caps.latest.revision: 39
author: Minewiskan
ms.author: owend
manager: erikre
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: 7d36c2567ab73b299cb528430b3ede7d81cf1bc5
ms.contentlocale: zh-cn
ms.lasthandoff: 08/02/2017

---
# <a name="bottomsum-mdx"></a>BottomSum (MDX)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx_md](../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  按升序对指定集进行排序，并返回一个最小值元组集，这些元组的和等于或小于指定值。  
  
## <a name="syntax"></a>語法  
  
```  
  
BottomSum(Set_Expression, Value, Numeric_Expression)  
```  
  
## <a name="arguments"></a>参数  
 *Set_Expression*  
 返回集的有效多维表达式 (MDX)。  
  
 *Value*  
 指定与每个元组相比较的值的有效数值表达式。  
  
 *Numeric_Expression*  
 返回数字的有效数值表达式，通常为单元坐标的多维表达式 (MDX)。  
  
## <a name="remarks"></a>注释  
 **BottomSum**函数计算指定的度量值，计算对指定集，以升序对集进行排序的总和。 然后，此函数返回最小值元素，其指定数值表达式的合计至少为指定值（和）。 此函数返回集的最小子集，其累积合计至少为指定值。 返回的元素按从小到大的顺序排列。  
  
> [!IMPORTANT]  
>  **BottomSum**函数，如[TopSum](../mdx/topsum-mdx.md)函数中，始终中断层次结构。  
  
## <a name="examples"></a>示例  
 以下示例返回 2003 会计年度 Geography 维度 Geography 层次结构中 City 级别的最小成员集（对于 Bike 类别），其使用 Reseller Sales Amount 度量值的累积合计至少是 50,000（从具有最小销售额的集的成员开始）：  
  
 `SELECT`  
  
 `[Product].[Product Categories].Bikes ON 0,`  
  
 `BottomSum`  
  
 `({[Geography].[Geography].[City].Members}`  
  
 `, 50000`  
  
 `, ([Measures].[Reseller Sales Amount],[Product].[Product Categories].Bikes)`  
  
 `) ON 1`  
  
 `FROM [Adventure Works]`  
  
 `WHERE([Measures].[Reseller Sales Amount],[Date].[Fiscal].[Fiscal Year].[FY 2003])`  
  
## <a name="see-also"></a>另請參閱  
 [MDX 函数引用 &#40;MDX &#41;](../mdx/mdx-function-reference-mdx.md)  
  
  

