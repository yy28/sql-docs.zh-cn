---
description: Ancestors (MDX)
title: " (MDX) 的上级 |Microsoft Docs"
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: d92f15f20c872fbe63db09a55356b5d1e35ff0d6
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/17/2020
ms.locfileid: "88461679"
---
# <a name="ancestors-mdx"></a>Ancestors (MDX)


  此函数返回指定成员在指定级别或距离处的所有祖先的集。 对于 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] ，返回的集始终包含一个成员-不 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 支持单个成员的多个父项。  
  
## <a name="syntax"></a>语法  
  
```  
  
Level syntax  
Ancestors(Member_Expression, Level_Expression)  
  
Numeric syntax  
Ancestors(Member_Expression, Distance)  
```  
  
## <a name="arguments"></a>参数  
 *Member_Expression*  
 返回成员的有效多维表达式 (MDX)。  
  
 *Level_Expression*  
 返回级别的有效多维表达式 (MDX)。  
  
 *长途*  
 指定与指定成员距离的有效数值表达式。  
  
## <a name="remarks"></a>备注  
 使用 **上级** 函数时，为函数提供一个 mdx 成员表达式，然后提供一个级别的 mdx 表达式，该表达式是该成员的上级，或是表示该成员之上的级别数的数值表达式。 使用此信息时， **上级** 函数将返回一组成员 (，这将是一个由该级别的一个成员) 组成的集合。  
  
> [!NOTE]  
>  若要返回祖先成员而不是祖先集，请使用 [祖先](../mdx/ancestor-mdx.md) 函数。  
  
 如果指定了级别表达式， **上级** 函数将返回指定成员在指定级别上的所有祖先的集。 如果指定的成员与指定的级别不在同一层次结构中，则该函数将返回错误。  
  
 如果指定了距离， **上级** 函数将返回所有成员的集合，这些成员是在成员表达式指定的层次结构中指定的步骤数。 成员可以指定为属性层次结构、用户定义的层次结构的成员，也可以指定为父子层次结构。 数值 1 返回父级别处的成员集，数值 2 返回祖父级别处（如果存在）的成员集。 数值 0 返回仅包含成员本身的集。  
  
> [!NOTE]  
>  对于父级别未知或无法命名的情况，请使用此窗体的 **上级** 函数。  
  
## <a name="examples"></a>示例  
 下面的示例使用 **祖先** 函数返回成员、其父项和祖父的 "Internet 销售额" 度量值。 此例使用级别表达式指定要返回的级别。 这些级别与成员表达式中指定的成员在同一个层次结构中。  
  
```  
SELECT {  
    Ancestors([Product].[Product Categories].[Product].[Mountain-100 Silver, 38],[Product].[Product Categories].[Category]),  
    Ancestors([Product].[Product Categories].[Product].[Mountain-100 Silver, 38],[Product].[Product Categories].[Subcategory]),  
    Ancestors([Product].[Product Categories].[Product].[Mountain-100 Silver, 38],[Product].[Product Categories].[Product])  
    } ON 0,  
[Measures].[Internet Sales Amount] ON 1  
FROM [Adventure Works]  
```  
  
 下面的示例使用 **祖先** 函数返回成员、其父项和祖父的 "Internet 销售额" 度量值。 此例使用数值表达式指定要返回的级别。 这些级别与成员表达式中指定的成员在同一个层次结构中。  
  
```  
SELECT {  
   Ancestors(  
      [Product].[Product Categories].[Product].[Mountain-100 Silver, 38],2  
      ),  
   Ancestors(  
      [Product].[Product Categories].[Product].[Mountain-100 Silver, 38],1  
      ),  
   Ancestors(  
      [Product].[Product Categories].[Product].[Mountain-100 Silver, 38],0  
      )  
   } ON 0,  
[Measures].[Internet Sales Amount] ON 1  
FROM  [Adventure Works]  
```  
  
 下面的示例使用 **祖先** 函数为属性层次结构的成员的父成员返回 "Internet 销售额" 度量值。 此示例使用数值表达式指定要返回的级别。 由于成员表达式中的成员是属性层次结构的成员，因此其父成员是“(全部)”级别。  
  
```  
SELECT {  
   Ancestors(  
      [Product].[Product].[Mountain-100 Silver, 38],1  
      )  
   } ON 0,  
[Measures].[Internet Sales Amount] ON 1  
FROM [Adventure Works]  
```  
  
## <a name="see-also"></a>另请参阅  
 [MDX 函数引用 (MDX)](../mdx/mdx-function-reference-mdx.md)  
  
  
