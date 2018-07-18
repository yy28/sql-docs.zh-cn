---
title: 使用成员、 元组和集 (MDX) |Microsoft Docs
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
- MDX [Analysis Services], tuples
- member keys [MDX]
- MDX [Analysis Services], sets
- calculated members [MDX]
- members [MDX]
- Multidimensional Expressions [Analysis Services], members
- named sets [MDX]
- Multidimensional Expressions [Analysis Services], tuples
- member functions [MDX]
- sets [MDX]
- MDX [Analysis Services], members
- member names [MDX]
- Multidimensional Expressions [Analysis Services], sets
- tuple functions
- tuples
- set functions [MDX]
ms.assetid: b6ec2439-caef-46d3-9fd7-5f4526cee334
caps.latest.revision: 41
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: fbd4fa53eb870bc8422dcb80fe019083e773e638
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/02/2018
ms.locfileid: "37153258"
---
# <a name="working-with-members-tuples-and-sets-mdx"></a>使用成员、元组和集 (MDX)
  MDX 提供多个可返回一个或多个成员、元组或集的函数，或对成员、元组或集进行操作的函数。  
  
## <a name="member-functions"></a>成员函数  
 MDX 提供多个用于从其他 MDX 实体（如从维度、级别、集或元组）检索成员的函数。 例如， [FirstChild](/sql/mdx/firstchild-mdx) 函数是一个对成员进行操作的函数，该函数返回一个成员。  
  
 若要获得时间维度的第一个子成员，可以显式标示该成员，如下面的示例所示。  
  
```  
SELECT [Date].[Calendar Year].[CY 2001] on 0  
FROM [Adventure Works]  
  
```  
  
 此外可以使用`FirstChild`函数以返回成员，如以下示例所示。  
  
```  
SELECT [Date].[Calendar Year].FirstChild on 0  
FROM [Adventure Works]  
  
```  
  
 有关 MDX 成员函数的详细信息，请参阅 [MDX 函数引用 (MDX)](/sql/mdx/mdx-function-reference-mdx)。  
  
## <a name="tuple-functions"></a>元组函数  
 MDX 提供多个返回元组的函数，它们可在任何接受元组的地方使用。 例如，[Item (Tuple) (MDX)](/sql/mdx/item-tuple-mdx) 函数可用于从集中提取第一个元组，当你知道某个集是由单个元组组成，并且要向需要元组的函数提供该元组时，此函数非常有用。  
  
 下面的示例返回列轴上元组集中的第一个元组。  
  
```  
SELECT {  
   ([Measures].[Reseller Sales Amount]  
      ,[Date].[Calendar Year].[CY 2003]  
   )  
, ([Measures].[Reseller Sales Amount]  
      ,[Date].[Calendar Year].[CY 2004]  
   )  
}.Item(0)  
ON COLUMNS   
FROM [Adventure Works]  
```  
  
 有关元组函数的详细信息，请参阅 [MDX 函数引用 (MDX)](/sql/mdx/mdx-function-reference-mdx)。  
  
## <a name="set-functions"></a>集函数  
 MDX 提供多个返回集的函数。 显式键入元组并将它们括在大括号内并不是检索集的唯一方法。 有关返回集的成员函数的详细信息，请参阅 [MDX 中的重要概念 (Analysis Services)](../key-concepts-in-mdx-analysis-services.md)。 还有很多其他集函数。  
  
 冒号运算符允许您使用成员的自然顺序创建集。 例如，下面的示例中显示的集包含 2002 日历年第一季度到第四季度的元组。  
  
```  
SELECT   
   {[Calendar Quarter].[Q1 CY 2002]:[Calendar Quarter].[Q4 CY 2002]}   
ON 0  
FROM [Adventure Works]  
```  
  
 如果不使用冒号运算符创建集，则可以通过指定下面示例中的元组来创建相同的成员集。  
  
```  
SELECT {  
   [Calendar Quarter].[Q1 CY 2002],   
   [Calendar Quarter].[Q2 CY 2002],   
   [Calendar Quarter].[Q3 CY 2002],   
   [Calendar Quarter].[Q4 CY 2002]  
   } ON 0  
FROM [Adventure Works]  
  
```  
  
 冒号运算符起到包含作用。 生成的集中包含冒号运算符两侧的成员。  
  
 有关集函数的详细信息，请参阅 [MDX 函数引用 (MDX)](/sql/mdx/mdx-function-reference-mdx)。  
  
## <a name="array-functions"></a>数组函数  
 数组函数对集进行操作并返回一个数组。 有关数组函数的详细信息，请参阅 [MDX 函数引用 (MDX)](/sql/mdx/mdx-function-reference-mdx)。  
  
## <a name="hierarchy-functions"></a>层次结构函数  
 通过对成员、级别、层次结构或字符串进行操作，层次结构函数返回一个层次结构。 有关层次结构函数的详细信息，请参阅 [MDX 函数引用 (MDX)](/sql/mdx/mdx-function-reference-mdx)。  
  
## <a name="level-functions"></a>级别函数  
 通过对成员、级别或字符串进行操作，级别函数返回一个级别。 有关级别函数的详细信息，请参阅 [MDX 函数引用 (MDX)](/sql/mdx/mdx-function-reference-mdx)。  
  
## <a name="logical-functions"></a>逻辑函数  
 逻辑函数对 MDX 表达式进行操作，返回表达式中有关元组、成员或集的信息。 例如，[IsEmpty (MDX)](/sql/mdx/isempty-mdx) 函数评估表达式是否返回了空单元值。 有关逻辑函数的详细信息，请参阅 [MDX 函数引用 (MDX)](/sql/mdx/mdx-function-reference-mdx)。  
  
## <a name="numeric-functions"></a>数值函数  
 数值函数对 MDX 表达式进行操作，返回一个标量值。 例如，[Aggregate (MDX)](/sql/mdx/aggregate-mdx) 函数返回一个标量值，该值由对指定集中元组的度量值聚合而得。 有关数值函数的详细信息，请参阅 [MDX 函数引用 (MDX)](/sql/mdx/mdx-function-reference-mdx)。  
  
## <a name="string-functions"></a>字符串函数  
 字符串函数对 MDX 表达式进行操作，返回一个字符串。 例如，[UniqueName (MDX)](/sql/mdx/uniquename-mdx) 函数返回一个字符串值，该字符串包含维度、层次结构、级别或成员的唯一名称。 有关字符串函数的详细信息，请参阅 [MDX 函数引用 (MDX)](/sql/mdx/mdx-function-reference-mdx)。  
  
## <a name="see-also"></a>请参阅  
 [MDX 中的重要概念&#40;Analysis Services&#41;](../key-concepts-in-mdx-analysis-services.md)   
 [MDX 查询基础知识&#40;Analysis Services&#41;](mdx-query-fundamentals-analysis-services.md)   
 [MDX 函数引用&#40;MDX&#41;](/sql/mdx/mdx-function-reference-mdx)  
  
  
