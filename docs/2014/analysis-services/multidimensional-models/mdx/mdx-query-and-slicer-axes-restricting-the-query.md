---
title: 限制查询中的使用查询轴和切片器轴 (MDX) |Microsoft 文档
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- Multidimensional Expressions [Analysis Services], axes
- queries [MDX], axes
- axes [MDX]
- MDX [Analysis Services], axes
ms.assetid: a64b8172-cd73-42f9-8847-52e967b9697a
caps.latest.revision: 29
author: Minewiskan
ms.author: owend
manager: mblythe
ms.openlocfilehash: e727b432afec1f42a6a111442c2263d6c48784de
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/19/2018
ms.locfileid: "36127991"
---
# <a name="restricting-the-query-with-query-and-slicer-axes-mdx"></a>用查询轴和切片器轴限定查询 (MDX)
  在设计多维表达式 (MDX) SELECT 语句时，应用程序通常检查多维数据集并将层次结构集分为两个子集：  
  
-   **查询轴**- 从此层次结构集中检索多个成员的数据。 有关查询轴的详细信息，请参阅[指定查询轴的内容 (MDX)](mdx-query-and-slicer-axes-specify-the-contents-of-a-query-axis.md)。  
  
-   **切片器轴**- 从此层次结构集中检索单个成员的数据。 有关切片器轴的详细信息，请参阅[指定切片器轴的内容 (MDX)](mdx-query-and-slicer-axes-specify-the-contents-of-a-slicer-axis.md)。  
  
 由于查询轴和切片器轴可以从要查询的多维数据集的多个层次结构中构造，因此这些术语可用于将要查询的多维数据集所使用的层次结构与在由 MDX 查询所返回的多维数据集中创建的层次结构区分开。  
  
 若要查看使用查询轴和切片器轴的简单示例，请参阅[在简单示例中使用查询轴和切片器轴 (MDX)](mdx-query-and-slicer-axes-using-axes-in-a-simple-example.md)。  
  
## <a name="see-also"></a>请参阅  
 [使用成员、 元组和集&#40;MDX&#41;](working-with-members-tuples-and-sets-mdx.md)   
 [MDX 查询基础知识&#40;Analysis Services&#41;](mdx-query-fundamentals-analysis-services.md)  
  
  