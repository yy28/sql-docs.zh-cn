---
title: CurrentMember (MDX) |Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 03583c9af74bd21511dfe871b229d03370a7b436
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/15/2019
ms.locfileid: "68047108"
---
# <a name="currentmember-mdx"></a>CurrentMember (MDX)


  在遍历过程中返回当前成员以及指定层次结构。  
  
## <a name="syntax"></a>语法  
  
```  
  
Hierarchy_Expression.CurrentMember  
```  
  
## <a name="arguments"></a>参数  
 *Hierarchy_Expression*  
 返回层次结构的有效多维表达式 (MDX)。  
  
## <a name="remarks"></a>备注  
 遍历一组层次结构成员时，在遍历过程的每一步，所操作的成员就是当前成员。 **CurrentMember**函数将返回该成员。  
  
> [!IMPORTANT]  
>  如果维度只包含一个可见的层次结构，则可以通过此维度的名称或此层次结构的名称引用此层次结构，原因是此维度的名称会解析为它唯一可见的层次结构。 例如，`Measures.CurrentMember` 是一个有效的 MDX 表达式，这是因为它会解析为 Measures 维度中唯一的层次结构。  
  
## <a name="examples"></a>示例  
 以下查询说明如何**Currentmember**可用于查找列、 行和切片轴上层次结构中的当前成员：  
  
 `WITH MEMBER MEASURES.CURRENTDATE AS`  
  
 `[Date].[Calendar].CURRENTMEMBER.NAME`  
  
 `MEMBER MEASURES.CURRENTPRODUCT AS`  
  
 `[Product].[Product Categories].CURRENTMEMBER.NAME`  
  
 `MEMBER MEASURES.CURRENTMEASURE AS`  
  
 `MEASURES.CURRENTMEMBER.NAME`  
  
 `MEMBER MEASURES.CURRENTCUSTOMER AS`  
  
 `[Customer].[Customer Geography].CURRENTMEMBER.NAME`  
  
 `SELECT`  
  
 `[Product].[Product Categories].[Category].MEMBERS`  
  
 `*`  
  
 `{MEASURES.CURRENTDATE, MEASURES.CURRENTPRODUCT,MEASURES.CURRENTMEASURE, MEASURES.CURRENTCUSTOMER}`  
  
 `ON 0,`  
  
 `[Date].[Calendar].MEMBERS`  
  
 `ON 1`  
  
 `FROM [Adventure Works]`  
  
 `WHERE([Customer].[Customer Geography].[Country].&[Australia])`  
  
 当前成员在查询中的轴上使用的层次结构上进行更改。 因此，还可以更改同一维度上未使用的轴上的其他层次结构上的当前成员;此行为称为自动共存并且可以在中找到更多详细信息[MDX 中的重要概念&#40;Analysis Services&#41;](../analysis-services/multidimensional-models/mdx/key-concepts-in-mdx-analysis-services.md)。 例如，下面的查询说明当 Calendar 层次结构上的当前成员显示在行轴上时，Date 维度的 Calendar Year 层次结构上的当前成员如何随 Calendar 层次结构上的当前成员更改：  
  
 `WITH MEMBER MEASURES.CURRENTYEAR AS`  
  
 `[Date].[Calendar Year].CURRENTMEMBER.NAME`  
  
 `SELECT`  
  
 `{MEASURES.CURRENTYEAR}`  
  
 `ON 0,`  
  
 `[Date].[Calendar].MEMBERS`  
  
 `ON 1`  
  
 `FROM [Adventure Works]`  
  
 **CurrentMember**对于使计算能够识别它们的使用中的查询的上下文是非常重要。 下面的示例返回每个产品的订单数量和订单数量百分比按类别和型号，从**Adventure Works**多维数据集。 **CurrentMember**函数标识其订单数量来计算过程中使用的产品。  
  
```  
WITH   
   MEMBER [Measures].[Order Percent by Category] AS  
   CoalesceEmpty  
(   
      ([Product].[Product Categories].CurrentMember,  
        Measures.[Order Quantity]) /   
          (  
           Ancestor  
           ( [Product].[Product Categories].CurrentMember,   
             [Product].[Product Categories].[Category]  
           ), Measures.[Order Quantity]  
       ), 0  
   ), FORMAT_STRING='Percent'  
SELECT   
   {Measures.[Order Quantity],  
      [Measures].[Order Percent by Category]} ON COLUMNS,  
{[Product].[Product].Members} ON ROWS  
FROM [Adventure Works]  
WHERE {[Date].[Calendar Year].[Calendar Year].&[2003]}  
```  
  
## <a name="see-also"></a>请参阅  
 [MDX 函数引用 (MDX)](../mdx/mdx-function-reference-mdx.md)  
  
  
