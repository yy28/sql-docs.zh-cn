---
title: 限制用查询轴和切片器轴 (MDX) 查询 |Microsoft 文档
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.component: mdx
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: b5a72e3ecb9afa0b345e3b1c74c7a220f517841a
ms.sourcegitcommit: 38f8824abb6760a9dc6953f10a6c91f97fa48432
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/10/2018
---
# <a name="mdx-query-and-slicer-axes---restricting-the-query"></a>MDX 查询轴和切片器轴-限定查询
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
  在设计多维表达式 (MDX) SELECT 语句时，应用程序通常检查多维数据集并将层次结构集分为两个子集：  
  
-   **查询轴**- 从此层次结构集中检索多个成员的数据。 有关查询轴的详细信息，请参阅[指定查询轴的内容 (MDX)](../../../analysis-services/multidimensional-models/mdx/mdx-query-and-slicer-axes-specify-the-contents-of-a-query-axis.md)。  
  
-   **切片器轴**- 从此层次结构集中检索单个成员的数据。 有关切片器轴的详细信息，请参阅[指定切片器轴的内容 (MDX)](../../../analysis-services/multidimensional-models/mdx/mdx-query-and-slicer-axes-specify-the-contents-of-a-slicer-axis.md)。  
  
 由于查询轴和切片器轴可以从要查询的多维数据集的多个层次结构中构造，因此这些术语可用于将要查询的多维数据集所使用的层次结构与在由 MDX 查询所返回的多维数据集中创建的层次结构区分开。  
  
 若要查看使用查询轴和切片器轴的简单示例，请参阅[在简单示例中使用查询轴和切片器轴 (MDX)](../../../analysis-services/multidimensional-models/mdx/mdx-query-and-slicer-axes-using-axes-in-a-simple-example.md)。  
  
## <a name="see-also"></a>另请参阅  
 [使用成员、 元组，和集 & #40;MDX & #41;](../../../analysis-services/multidimensional-models/mdx/working-with-members-tuples-and-sets-mdx.md)   
 [MDX 查询基础知识 & #40;Analysis Services & #41;](../../../analysis-services/multidimensional-models/mdx/mdx-query-fundamentals-analysis-services.md)  
  
  
