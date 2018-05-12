---
title: 在简单示例 (MDX) 中使用查询轴和切片器轴 |Microsoft 文档
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: fce95d7e51c17f6e8a0fedbec01eccf7bd8ec8c4
ms.sourcegitcommit: c12a7416d1996a3bcce3ebf4a3c9abe61b02fb9e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/10/2018
---
# <a name="mdx-query-and-slicer-axes---using-axes-in-a-simple-example"></a>MDX 查询轴和切片器轴-在简单的示例中使用轴
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
  本主题中提供的简单示例说明了指定和使用查询轴和切片器轴的基本操作。  
  
## <a name="the-cube"></a>多维数据集  
 名为 TestCube 的多维数据集有两个维度，分别为 Route 和 Time。 每个维度都只有一个用户层次结构，分别为 Route 和 Time。 因为多维数据集的度量值是 Measures 维度的一部分，所以此多维数据集总共有三个维度。  
  
## <a name="the-query"></a>查询  
 查询要提供一个矩阵，可以在该矩阵内跨路线和时间比较 Packages 度量值。  
  
 在下面的 MDX 查询示例中，Route 和 Time 层次结构为查询轴，Measures 维度为切片器轴。 [Members](../../../mdx/members-set-mdx.md) 函数指明 MDX 将使用层次结构或级别的成员来构造一个集。 使用 **Members** 函数意味着不必在 MDX 查询中显式声明特定层次结构或级别的每个成员。  
  
```  
SELECT  
   { Route.nonground.Members } ON COLUMNS,  
   { Time.[1st half].Members } ON ROWS  
FROM TestCube  
WHERE ( [Measures].[Packages] )  
```  
  
## <a name="the-results"></a>结果  
 结果是一个网格，标识 COLUMNS 和 ROWS 轴维度的每个交点处 Packages 度量值的值。 下表显示了此网格。  
  
||air|sea|  
|-|---------|---------|  
|第一季度|60|50|  
|第二季度|45|45|  
  
## <a name="see-also"></a>另请参阅  
 [指定查询轴 & #40; 的内容MDX & #41;](../../../analysis-services/multidimensional-models/mdx/mdx-query-and-slicer-axes-specify-the-contents-of-a-query-axis.md)   
 [指定切片器轴 & #40; 的内容MDX & #41;](../../../analysis-services/multidimensional-models/mdx/mdx-query-and-slicer-axes-specify-the-contents-of-a-slicer-axis.md)  
  
  
