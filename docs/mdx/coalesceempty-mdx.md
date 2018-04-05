---
title: CoalesceEmpty (MDX) |Microsoft 文档
ms.custom: ''
ms.date: 03/02/2016
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: ''
ms.component: ''
ms.reviewer: ''
ms.suite: pro-bi
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- COALESCEEMPTY
dev_langs:
- kbMDX
helpviewer_keywords:
- CoalesceEmpty function
ms.assetid: c00dd739-44bc-4af6-9871-c7e1e3f3e5ba
caps.latest.revision: 39
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: Inactive
ms.openlocfilehash: d02d253d39a605405df747b49fd0a762913030f1
ms.sourcegitcommit: f486d12078a45c87b0fcf52270b904ca7b0c7fc8
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/08/2018
---
# <a name="coalesceempty-mdx"></a>CoalesceEmpty (MDX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  将空单元值转换为指定的非空单元值，该值可以是数字或字符串。  
  
## <a name="syntax"></a>语法  
  
```  
  
Numeric syntax  
CoalesceEmpty( Numeric_Expression1 [ ,Numeric_Expression2,...n] )  
  
String syntax  
CoalesceEmpty(String_Expression1 [ ,String_Expression2,...n] )  
```  
  
## <a name="arguments"></a>参数  
 *Numeric_Expression1*  
 返回数字的有效数值表达式，通常为单元坐标的多维表达式 (MDX)。  
  
 *Numeric_Expression2*  
 有效数值表达式，通常为指定的数值。  
  
 *String_Expression1*  
 有效字符串表达式，通常为返回字符串的单元坐标的多维表达式 (MDX)。  
  
 *String_Expression2*  
 有效字符串表达式，通常为指定的字符串值（该值被第一个字符串表达式返回的 NULL 代替）。  
  
## <a name="remarks"></a>Remarks  
 如果指定一个或多个数值表达式， **CoalesceEmpty**函数返回的第一个数值表达式 （从左到右） 可被解析为一个非空值的数值。 如果指定的所有数值表达式都不能被解析为非空值，则此函数返回空单元值。 通常情况下，第二个数值表达式的值是被第一个数值表达式返回的 NULL 代替的数值。  
  
 如果指定了一个或多个字符串表达式，此函数将返回可被解析为非空值的第一个（从左向右）字符串表达式的值。 如果指定的所有字符串表达式都不能被解析为非空值，则此函数返回空单元值。 通常情况下，第二个字符串表达式的值是被第一个字符串表达式返回的 NULL 代替的字符串值。  
  
 **CoalesceEmpty**函数只能采用相同的类型的值。 也就是说，指定的所有值表达式的值都必须为数值数据类型或空单元值，或者，指定的所有值表达式的值都必须为字符串数据类型或空单元值。 对此函数的一次调用不能同时包括数值表达式和字符串表达式。  
  
 有关空单元的详细信息，请参阅 OLE DB 文档。  
  
## <a name="example"></a>示例  
 下面的示例查询**Adventure Works**多维数据集。 此示例将返回每个产品的订单数量以及按类别排列的订单数量百分比。 **CoalesceEmpty**函数会确保设置格式的计算的成员时，将 null 值表示为零 (0)。  
  
```  
WITH   
   MEMBER [Measures].[Order Percent by Category] AS  
   CoalesceEmpty(   
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
  
## <a name="see-also"></a>另请参阅  
 [MDX 函数引用 &#40;MDX &#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
