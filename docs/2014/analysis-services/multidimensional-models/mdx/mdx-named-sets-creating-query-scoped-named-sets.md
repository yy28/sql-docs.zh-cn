---
title: 创建查询作用域的命名集（MDX） |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- query-scoped named sets [MDX]
- WITH keyword
ms.assetid: 78bc1e9a-1bc4-4a5a-ab0b-cf430c8fbfe1
author: minewiskan
ms.author: owend
ms.openlocfilehash: 6eccb4e20fca03079a04a0219b07f6411b80a433
ms.sourcegitcommit: f0772f614482e0b3cde3609e178689ce62ca3a19
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/09/2020
ms.locfileid: "84546309"
---
# <a name="creating-query-scoped-named-sets-mdx"></a>创建查询作用域的命名集 (MDX)
  如果某个命名集仅用于单个多维表达式 (MDX) 查询，则可以使用 WITH 关键字来定义该命名集。 使用 WITH 关键字创建的命名集在执行完查询之后就不再存在。  
  
 如本主题中所述，WITH 关键字的语法非常灵活，甚至允许使用函数来定义命名集。  
  
> [!NOTE]  
>  有关命名集的详细信息，请参阅[在 MDX 中生成命名集 (MDX)](mdx-named-sets-building-named-sets.md)。  
  
## <a name="with-keyword-syntax"></a>WITH 关键字语法  
 可以使用以下语法将 WITH 关键字添加到 MDX SELECT 语句：  
  
```  
[ WITH <SELECT WITH clause> [ , <SELECT WITH clause> ... ] ]   
SELECT [ * | ( <SELECT query axis clause> [ , <SELECT query axis clause> ... ] ) ]  
FROM <SELECT subcube clause>   
[ <SELECT slicer axis clause> ]  
[ <SELECT cell property list clause> ]  
  
<SELECT WITH clause> ::=  
   ( SET Set_Identifier AS 'Set_Expression')  
  
```  
  
 在 WITH 关键字的语法中， `Set_Identifier` 参数包含命名集的别名。 `Set_Expression` 参数包含命名集别名所指代的集表达式。  
  
## <a name="with-keyword-example"></a>WITH 关键字示例  
 下列 MDX 查询将检查 `FoodMart 2000`（Microsoft SQL Server 2000 Analysis Services 示例数据库）中各种 Chardonnay 酒和 Chablis 酒的单位销售额。 尽管就结果集而言此查询相当简单，但是在必须维护这种查询的情况下，它就显得冗长且难处理。  
  
```  
SELECT  
   {[Product].[All Products].[Drink].[Alcoholic Beverages].[Beer and Wine].[Wine].[Good].[Good Chardonnay],   [Product].[All Products].[Drink].[Alcoholic Beverages].[Beer and Wine].[Wine].[Pearl].[Pearl Chardonnay],   [Product].[All Products].[Drink].[Alcoholic Beverages].[Beer and Wine].[Wine].[Portsmouth].[Portsmouth Chardonnay],   [Product].[All Products].[Drink].[Alcoholic Beverages].[Beer and Wine].[Wine].[Top Measure].[Top Measure Chardonnay],   [Product].[All Products].[Drink].[Alcoholic Beverages].[Beer and Wine].[Wine].[Walrus].[Walrus Chardonnay],   [Product].[All Products].[Drink].[Alcoholic Beverages].[Beer and Wine].[Wine].[Good].[Good Chablis Wine],   [Product].[All Products].[Drink].[Alcoholic Beverages].[Beer and Wine].[Wine].[Pearl].[Pearl Chablis Wine],   [Product].[All Products].[Drink].[Alcoholic Beverages].[Beer and Wine].[Wine].[Portsmouth].[Portsmouth Chablis Wine],   [Product].[All Products].[Drink].[Alcoholic Beverages].[Beer and Wine].[Wine].[Top Measure].[Top Measure Chablis Wine],   [Product].[All Products].[Drink].[Alcoholic Beverages].[Beer and Wine].[Wine].[Walrus].[Walrus Chablis Wine]} ON COLUMNS,  
   {Measures.[Unit Sales]} ON ROWS  
FROM Sales  
```  
  
 若要使上述 MDX 更易于维护，可以使用 WITH 关键字为此查询创建一个命名集。 以下代码显示了如何使用 WITH 关键字来创建命名集 `[ChardonnayChablis]`，以及该命名集如何使得 SELECT 语句更简洁、更易于维护。  
  
```  
WITH SET [ChardonnayChablis] AS  
   {[Product].[All Products].[Drink].[Alcoholic Beverages].[Beer and Wine].[Wine].[Good].[Good Chardonnay],  
   [Product].[All Products].[Drink].[Alcoholic Beverages].[Beer and Wine].[Wine].[Pearl].[Pearl Chardonnay],  
   [Product].[All Products].[Drink].[Alcoholic Beverages].[Beer and Wine].[Wine].[Portsmouth].[Portsmouth Chardonnay],  
   [Product].[All Products].[Drink].[Alcoholic Beverages].[Beer and Wine].[Wine].[Top Measure].[Top Measure Chardonnay],  
   [Product].[All Products].[Drink].[Alcoholic Beverages].[Beer and Wine].[Wine].[Walrus].[Walrus Chardonnay],  
   [Product].[All Products].[Drink].[Alcoholic Beverages].[Beer and Wine].[Wine].[Good].[Good Chablis Wine],  
   [Product].[All Products].[Drink].[Alcoholic Beverages].[Beer and Wine].[Wine].[Pearl].[Pearl Chablis Wine],  
   [Product].[All Products].[Drink].[Alcoholic Beverages].[Beer and Wine].[Wine].[Portsmouth].[Portsmouth Chablis Wine],  
   [Product].[All Products].[Drink].[Alcoholic Beverages].[Beer and Wine].[Wine].[Top Measure].[Top Measure Chablis Wine],  
   [Product].[All Products].[Drink].[Alcoholic Beverages].[Beer and Wine].[Wine].[Walrus].[Walrus Chablis Wine]}  
  
SELECT  
   [ChardonnayChablis] ON COLUMNS,  
   {Measures.[Unit Sales]} ON ROWS  
FROM Sales  
```  
  
### <a name="using-functions-together-with-the-with-keyword"></a>将函数与 WITH 关键字一起使用  
 尽管可以显式定义命名集的每个成员，但是这种方法可能会产生过长的语句。 若要使命名集的创建和维护更简单，可以使用 MDX 函数来定义成员。  
  
 例如，下面的 MDX 查询示例使用 [Filter](/sql/mdx/filter-mdx)、 [CurrentMember](/sql/mdx/current-mdx)和 [Name](/sql/mdx/members-string-mdx) MDX 函数以及 InStr VBA 函数创建 `[ChardonnayChablis]` 命名集。 这种版本的 `[ChardonnayChablis]` 命名集与本主题前面所演示的显式定义的命名集相同。  
  
```  
WITH SET [ChardonnayChablis] AS  
   'Filter([Product].Members, (InStr(1, [Product].CurrentMember.Name, "chardonnay") <> 0) OR (InStr(1, [Product].CurrentMember.Name, "chablis") <> 0))'  
  
SELECT  
   [ChardonnayChablis] ON COLUMNS,  
   {Measures.[Unit Sales]} ON ROWS  
FROM Sales  
  
```  
  
## <a name="see-also"></a>另请参阅  
 [SELECT 语句 &#40;MDX&#41;](/sql/mdx/mdx-data-manipulation-select)   
 [创建会话作用域的命名集 (MDX)](mdx-named-sets-creating-session-scoped-named-sets.md)  
  
  
