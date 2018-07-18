---
title: 创建查询作用域的计算成员 (MDX) |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- WITH keyword
- query-scoped calculated members [MDX]
ms.assetid: c4507149-e67b-4e5d-9192-cc911acd9adc
caps.latest.revision: 28
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 8e5d26eb5ac3e4bb48e16b2ec33fcd2ed98ec60a
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/02/2018
ms.locfileid: "37257663"
---
# <a name="creating-query-scoped-calculated-members-mdx"></a>创建查询作用域的计算成员 (MDX)
  如果某个计算成员仅用于单个多维表达式 (MDX) 查询，则可以使用 WITH 关键字定义该计算成员。 使用 WITH 关键字创建的计算成员在执行完查询之后就不再存在。  
  
 如本主题中所述，WITH 关键字的语法非常灵活，甚至允许一个计算成员基于另一个计算成员。  
  
> [!NOTE]  
>  有关计算成员的详细信息，请参阅[在 MDX 中生成计算成员 (MDX)](mdx-calculated-members-building-calculated-members.md)。  
  
## <a name="with-keyword-syntax"></a>WITH 关键字语法  
 使用以下语法将 WITH 关键字添加到 MDX SELECT 语句：  
  
```  
[ WITH <SELECT WITH clause> [ , <SELECT WITH clause> ... ] ] SELECT [ * | ( <SELECT query axis clause> [ , <SELECT query axis clause> ... ] ) ]FROM <SELECT subcube clause> [ <SELECT slicer axis clause> ][ <SELECT cell property list clause> ]  
<SELECT WITH clause> ::=  
   ( [ CALCULATED ] MEMBER <CREATE MEMBER body clause>) | <CREATE MEMBER body clause> ::= Member_Identifier AS 'MDX_Expression'  
   [ <CREATE MEMBER property clause> [ , <CREATE MEMBER property clause> ... ] ]  
<CREATE MEMBER property clause> ::=  
   ( MemberProperty_Identifier = Scalar_Expression )  
  
```  
  
 在 WITH 关键字的语法中， `Member_Identifier` 值是计算成员的完全限定名称。 此完全限定名称包括计算成员所关联的维度或级别。 对 `MDX_Expression` 表达式求值以后，将返回计算成员的值。 另外，可以通过在 `MemberProperty_Identifier` 值中提供单元属性的名称以及在 `Scalar_Expression` 值中提供单元属性的值，指定计算成员内部单元属性的值。  
  
## <a name="with-keyword-examples"></a>WITH 关键字示例  
 下面的 MDX 查询定义了计算成员 `[Measures].[Special Discount]`，用来基于原始折扣金额来计算特殊折扣。  
  
```  
WITH   
   MEMBER [Measures].[Special Discount] AS  
   [Measures].[Discount Amount] * 1.5  
SELECT   
   [Measures].[Special Discount] on COLUMNS,  
   NON EMPTY [Product].[Product].MEMBERS  ON Rows  
FROM [Adventure Works]  
WHERE [Product].[Category].[Bikes]  
```  
  
 还可以在层次结构中的任意位置创建计算成员。 例如，下面的 MDX 查询为某个假设的“销售额”多维数据集定义计算成员 `[BigSeller]` 。 此计算成员用于确定指定商店的啤酒和葡萄酒的单位销售额是否不少于 100.00。 但是，此查询所创建的 `[BigSeller]` 计算成员不是 `[Product]` 维度的子成员，而是 `[Beer and Wine]` 成员的子成员。  
  
```  
WITH   
   MEMBER [Product].[Beer and Wine].[BigSeller] AS  
  IIf([Product].[Beer and Wine] > 100, "Yes","No")  
SELECT  
   {[Product].[BigSeller]} ON COLUMNS,  
   Store.[Store Name].Members ON ROWS  
FROM Sales  
  
```  
  
 计算成员并非只能依赖于多维数据集中的现有成员。 计算成员还可以基于在同一 MDX 表达式中定义的其他计算成员。 例如，下面的 MDX 查询使用在第一个计算成员 `[Measures].[Special Discount]`中创建的值来生成第二个计算成员 `[Measures].[Special Discounted Amount]`的值。  
  
```  
WITH   
   MEMBER [Measures].[Special Discount] AS  
   [Measures].[Discount Percentage] * 1.5,   
   FORMAT_STRING = 'Percent'  
  
   MEMBER [Measures].[Special Discounted Amount] AS  
   [Measures].[Reseller Average Unit Price] * [Measures].[Special Discount],   
   FORMAT_STRING = 'Currency'  
  
SELECT   
   {[Measures].[Special Discount], [Measures].[Special Discounted Amount]} on COLUMNS,  
   NON EMPTY [Product].[Product].MEMBERS  ON Rows  
FROM [Adventure Works]  
WHERE [Product].[Category].[Bikes]  
  
```  
  
## <a name="see-also"></a>请参阅  
 [MDX 函数引用&#40;MDX&#41;](/sql/mdx/mdx-function-reference-mdx)   
 [SELECT 语句&#40;MDX&#41;](/sql/mdx/mdx-data-manipulation-select)   
 [创建会话作用域的计算成员&#40;MDX&#41;](mdx-calculated-members-session-scoped-calculated-members.md)  
  
  
