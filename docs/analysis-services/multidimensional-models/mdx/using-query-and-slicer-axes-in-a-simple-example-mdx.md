---
title: "在简单示例中使用查询轴和切片器轴 (MDX) | Microsoft Docs"
ms.custom: ""
ms.date: "03/04/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "analysis-services"
  - "analysis-services/multidimensional-tabular"
  - "analysis-services/data-mining"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "切片器轴"
  - "查询轴 [MDX]"
ms.assetid: 85bcb26f-5971-4153-b334-61f8d8b475b5
caps.latest.revision: 11
author: "Minewiskan"
ms.author: "owend"
manager: "erikre"
---
# 在简单示例中使用查询轴和切片器轴 (MDX)
  本主题中提供的简单示例说明了指定和使用查询轴和切片器轴的基本操作。  
  
## 多维数据集  
 名为 TestCube 的多维数据集有两个维度，分别为 Route 和 Time。 每个维度都只有一个用户层次结构，分别为 Route 和 Time。 因为多维数据集的度量值是 Measures 维度的一部分，所以此多维数据集总共有三个维度。  
  
## 查询  
 查询要提供一个矩阵，可以在该矩阵内跨路线和时间比较 Packages 度量值。  
  
 在下面的 MDX 查询示例中，Route 和 Time 层次结构为查询轴，Measures 维度为切片器轴。 [Members](../../../mdx/members-set-mdx.md) 函数指明 MDX 将使用层次结构或级别的成员来构造一个集。 使用 **Members** 函数意味着不必在 MDX 查询中显式声明特定层次结构或级别的每个成员。  
  
```  
SELECT  
   { Route.nonground.Members } ON COLUMNS,  
   { Time.[1st half].Members } ON ROWS  
FROM TestCube  
WHERE ( [Measures].[Packages] )  
```  
  
## 结果  
 结果是一个网格，标识 COLUMNS 和 ROWS 轴维度的每个交点处 Packages 度量值的值。 下表显示了此网格。  
  
||air|sea|  
|-|---------|---------|  
|第一季度|60|50|  
|第二季度|45|45|  
  
## 另请参阅  
 [指定查询轴的内容 (MDX)](../../../analysis-services/multidimensional-models/mdx/specifying-the-contents-of-a-query-axis-mdx.md)   
 [指定切片器轴的内容 (MDX)](../../../analysis-services/multidimensional-models/mdx/specifying-the-contents-of-a-slicer-axis-mdx.md)  
  
  