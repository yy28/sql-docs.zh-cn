---
title: 上级 (MDX) |Microsoft 文档
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
ms.sourcegitcommit: 97bef3f248abce57422f15530c1685f91392b494
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/04/2018
ms.locfileid: "34740046"
---
# <a name="ancestors-mdx"></a>Ancestors (MDX)


  此函数返回指定成员在指定级别或距离处的所有祖先的集。 与[!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]，返回的集将始终包含的单个成员-[!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]单个成员不支持多个父级。  
  
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
  
## <a name="remarks"></a>Remarks  
 与**上级**函数，该函数提供的 MDX 成员表达式，然后提供的级别，该成员的祖先一个 MDX 表达式，或者表示的上面该成员的级别数的数值表达式。 使用此信息，**上级**函数返回在该级别 （它将是包含的一个成员的集） 的成员组成的集。  
  
> [!NOTE]  
>  若要返回的祖先成员，而不是设置了祖先，则使用[上级](../mdx/ancestor-mdx.md)函数。  
  
 如果指定一个级别表达式，则**上级**函数返回在指定的级别的指定成员的所有祖先构成的集。 如果指定的成员不在指定的级别相同的层次结构内，该函数将返回错误。  
  
 如果指定的距离，则**上级**函数返回多向上指定由成员表达式指定层次结构中的步骤的所有成员组成的集。 成员可以指定为属性层次结构，用户定义的层次结构，或者，在某些情况下，父-子层次结构的成员。 数值 1 返回父级别处的成员集，数值 2 返回祖父级别处（如果存在）的成员集。 数值 0 返回仅包含成员本身的集。  
  
> [!NOTE]  
>  使用这种形式的**上级**情况下在其中的父级别，未知或不能为命名的函数。  
  
## <a name="examples"></a>示例  
 下面的示例使用**上级**函数以返回成员、 其父节点和其祖父的 Internet Sales Amount 度量值。 此例使用级别表达式指定要返回的级别。 这些级别与成员表达式中指定的成员在同一个层次结构中。  
  
```  
SELECT {  
    Ancestors([Product].[Product Categories].[Product].[Mountain-100 Silver, 38],[Product].[Product Categories].[Category]),  
    Ancestors([Product].[Product Categories].[Product].[Mountain-100 Silver, 38],[Product].[Product Categories].[Subcategory]),  
    Ancestors([Product].[Product Categories].[Product].[Mountain-100 Silver, 38],[Product].[Product Categories].[Product])  
    } ON 0,  
[Measures].[Internet Sales Amount] ON 1  
FROM [Adventure Works]  
```  
  
 下面的示例使用**上级**函数以返回成员、 其父节点和其祖父的 Internet Sales Amount 度量值。 此例使用数值表达式指定要返回的级别。 这些级别与成员表达式中指定的成员在同一个层次结构中。  
  
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
 [MDX 函数引用&#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
