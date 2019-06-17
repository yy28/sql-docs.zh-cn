---
title: 上级 (MDX) |Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 0c108ea102e03000481d18bfc69f657e6bd8a0ce
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/15/2019
ms.locfileid: "63313727"
---
# <a name="ancestors-mdx"></a>Ancestors (MDX)


  此函数返回指定成员在指定级别或距离处的所有祖先的集。 与[!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]，返回的集将始终包含的单个成员[!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]不支持多个父级的单个成员。  
  
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
  
 *距离*  
 指定与指定成员距离的有效数值表达式。  
  
## <a name="remarks"></a>备注  
 与**上级**函数，该函数提供 MDX 成员表达式，然后提供该成员的祖先所在级别的 MDX 表达式，或者表示的级别数的数值表达式该成员之上。 使用此信息，**上级**函数返回在该级别成员 （它将是一个成员的集） 的集合。  
  
> [!NOTE]  
>  若要返回祖先成员，而不是祖先集，使用[祖先](../mdx/ancestor-mdx.md)函数。  
  
 如果指定了级别表达式，则**上级**函数返回指定成员在指定级别处的所有祖先构成的集。 如果指定的成员不是指定的级别相同的层次结构中，该函数将返回错误。  
  
 如果指定了距离，则**上级**函数返回的所有成员在层次结构指定成员表达式高出指定步骤数集。 成员可以指定为属性层次结构，用户定义层次结构，或者在某些情况下，父-子层次结构的成员。 数值 1 返回父级别处的成员集，数值 2 返回祖父级别处（如果存在）的成员集。 数值 0 返回仅包含成员本身的集。  
  
> [!NOTE]  
>  使用这种形式的**上级**函数的情况下是未知的或不能为命名的父级别。  
  
## <a name="examples"></a>示例  
 下面的示例使用**上级**函数返回成员、 其父节点和其祖父的 Internet Sales Amount 度量值。 此例使用级别表达式指定要返回的级别。 这些级别与成员表达式中指定的成员在同一个层次结构中。  
  
```  
SELECT {  
    Ancestors([Product].[Product Categories].[Product].[Mountain-100 Silver, 38],[Product].[Product Categories].[Category]),  
    Ancestors([Product].[Product Categories].[Product].[Mountain-100 Silver, 38],[Product].[Product Categories].[Subcategory]),  
    Ancestors([Product].[Product Categories].[Product].[Mountain-100 Silver, 38],[Product].[Product Categories].[Product])  
    } ON 0,  
[Measures].[Internet Sales Amount] ON 1  
FROM [Adventure Works]  
```  
  
 下面的示例使用**上级**函数返回成员、 其父节点和其祖父的 Internet Sales Amount 度量值。 此例使用数值表达式指定要返回的级别。 这些级别与成员表达式中指定的成员在同一个层次结构中。  
  
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
  
 下面的示例使用**上级**函数返回的属性层次结构成员的父级的 Internet Sales Amount 度量值。 此示例使用数值表达式指定要返回的级别。 由于成员表达式中的成员是属性层次结构的成员，因此其父成员是“(全部)”级别。  
  
```  
SELECT {  
   Ancestors(  
      [Product].[Product].[Mountain-100 Silver, 38],1  
      )  
   } ON 0,  
[Measures].[Internet Sales Amount] ON 1  
FROM [Adventure Works]  
```  
  
## <a name="see-also"></a>请参阅  
 [MDX 函数引用 (MDX)](../mdx/mdx-function-reference-mdx.md)  
  
  
