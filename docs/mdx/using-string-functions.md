---
title: 使用字符串函数 |Microsoft 文档
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 6e151d06d086569b16fcdf1dc3570f9b220dfcd6
ms.sourcegitcommit: 97bef3f248abce57422f15530c1685f91392b494
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/04/2018
ms.locfileid: "34743818"
---
# <a name="using-string-functions"></a>使用字符串函数


  可以对多维表达式 (MDX) 中的几乎所有对象使用字符串函数。 在存储过程中，字符串函数主要用于将对象转换为字符串表示形式。 还可以使用字符串函数为对象计算字符串表达式，以返回一个值。  
  
 使用最广泛的字符串函数是**名称**和**Uniquename**。 这两个函数分别返回对象的名称和唯一名称。 它们通常用于调试计算以发现函数正在返回哪个成员。  
  
## <a name="examples"></a>示例  
 以下示例查询说明如何使用这两个函数：  
  
 `WITH`  
  
 `//Returns the name of the current Product on rows`  
  
 `MEMBER [Measures].[ProductName] AS [Product].[Product].CurrentMember.Name`  
  
 `//Returns the uniquename of the current Product on rows`  
  
 `MEMBER [Measures].[ProductUniqueName] AS [Product].[Product].CurrentMember.Uniquename`  
  
 `//Returns the name of the Product dimension`  
  
 `MEMBER [Measures].[ProductDimensionName] AS [Product].Name`  
  
 `SELECT  {[Measures].[ProductName],[Measures].[ProductUniqueName],[Measures].[ProductDimensionName]}`  
  
 `ON COLUMNS,`  
  
 `[Product].[Product].MEMBERS  ON ROWS`  
  
 `FROM [Adventure Works]`  
  
 **生成**函数可用来在一组的每个成员上执行的字符串函数，并将结果串联起来。 由于此函数允许您对集的内容进行可视化，因此它在调试计算时也很有用。 以下示例说明如何以这种方式使用此函数：  
  
 `WITH`  
  
 `//Returns the names of the current Product and its ancestors up to the All Member`  
  
 `MEMBER [Measures].[AncestorNames] AS`  
  
 `GENERATE(`  
  
 `ASCENDANTS([Product].[Product Categories].CurrentMember)`  
  
 `, [Product].[Product Categories].CurrentMember.Name, ", ")`  
  
 `SELECT`  
  
 `{[Measures].[AncestorNames]}`  
  
 `ON COLUMNS,`  
  
 `[Product].[Product Categories].MEMBERS  ON ROWS`  
  
 `FROM [Adventure Works]`  
  
 另一组广泛使用的字符串函数能够转换字符串，该字符串包含对象的唯一名称或将该对象解析到对象本身的表达式。 下面的示例查询演示如何**StrToMember**和**StrToSet**函数执行此操作：  
  
 `SELECT`  
  
 `{StrToMember("[Measures].[Inter" + "net Sales Amount]")}`  
  
 `ON COLUMNS,`  
  
 `StrToSet("{`  
  
 `[Product].[Product Categories].[Category].&[3],`  
  
 `[Product].[Product Categories].[Product].&[477],`  
  
 `[Product].[Product Categories].[Product].&[788],`  
  
 `[Product].[Product Categories].[Product].&[708],`  
  
 `[Product].[Product Categories].[Product].&[711]`  
  
 `}")`  
  
 `ON ROWS`  
  
 `FROM [Adventure Works]`  
  
> [!NOTE]  
>  **StrToMember**和**StrToSet**应多加小心使用函数。 如果在计算定义中使用这些函数，则可能会导致查询性能较差。  
  
## <a name="see-also"></a>请参阅  
 [生成&#40;MDX&#41;](../mdx/generate-mdx.md)   
 [名称&#40;MDX&#41;](../mdx/name-mdx.md)   
 [UniqueName &#40;MDX&#41;](../mdx/uniquename-mdx.md)   
 [函数&#40;MDX 语法&#41;](../mdx/functions-mdx-syntax.md)   
 [使用存储的过程&#40;MDX&#41;](../mdx/using-stored-procedures-mdx.md)   
 [StrToMember &#40;MDX&#41;](../mdx/strtomember-mdx.md)   
 [StrToSet &#40;MDX&#41;](../mdx/strtoset-mdx.md)  
  
  
