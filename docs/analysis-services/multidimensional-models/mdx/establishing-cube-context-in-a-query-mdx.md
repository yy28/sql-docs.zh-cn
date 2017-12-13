---
title: "在查询 (MDX) 中建立多维数据集上下文 |Microsoft 文档"
ms.custom: 
ms.date: 03/13/2017
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: 
ms.component: 
ms.reviewer: 
ms.suite: pro-bi
ms.technology:
- analysis-services
- analysis-services/multidimensional-tabular
- analysis-services/data-mining
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- cubes [Analysis Services], MDX
- MDX [Analysis Services], cube context
- SELECT statement [MDX]
- Multidimensional Expressions [Analysis Services], cube context
- queries [MDX], cube context
ms.assetid: 79d6a1e8-2825-4eb9-97df-5071aecae8f0
caps.latest.revision: "29"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 1b8d97b906a0ef1121daac5379f4938dfe4b2466
ms.sourcegitcommit: f1a6944f95dd015d3774a25c14a919421b09151b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/08/2017
---
# <a name="establishing-cube-context-in-a-query-mdx"></a>在查询中建立多维数据集上下文 (MDX)
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]在指定的多维数据集的上下文中运行的每个 MDX 查询。 此上下文定义了查询中的表达式求值的成员。  
  
 在 SELECT 语句中，FROM 子句用于确定多维数据集上下文。 此上下文可以是整个多维数据集，也可以只是该多维数据集的一个子多维数据集。 如果通过 FROM 子句指定了多维数据集上下文，就可以使用其他函数来扩展或限制该上下文。  
  
> [!NOTE]  
>  也可以使用 SCOPE 和 CALCULATE 语句在 MDX 脚本中管理多维数据集上下文。 有关详细信息，请参阅 [MDX 脚本编写基础知识 (Analysis Services)](../../../analysis-services/multidimensional-models/mdx/mdx-scripting-fundamentals-analysis-services.md)。  
  
## <a name="from-clause-syntax"></a>FROM 子句的语法  
 以下语法说明了 FROM 子句：  
  
```  
<SELECT subcube clause> ::=  
   Cube_Identifier |   
   (SELECT [  
      * |   
      ( <SELECT query axis clause> [ , <SELECT query axis clause> ... ] ) ]   
   FROM <SELECT subcube clause> <SELECT slicer axis clause> )  
```  
  
 请注意，在此语法中， `<SELECT subcube clause>` 子句说明了执行 SELECT 语句时所在的多维数据集或子多维数据集。  
  
 FROM 子句的一个简单例子为针对整个 Adventure Works 示例多维数据集执行的子句。 这样的 FROM 子句将具有以下格式：  
  
```  
FROM [Adventure Works]  
```  
  
 有关 MDX SELECT 语句中的 FROM 子句的详细信息，请参阅 [SELECT 语句 (MDX)](../../../mdx/mdx-data-manipulation-select.md)。  
  
## <a name="refining-the-context"></a>完善上下文  
 虽然 FROM 子句指定的多维数据集上下文在单个多维数据集中，但这并不会造成您无法一次处理多个多维数据集中的数据。  
  
 您可以使用 MDX [LookupCube](../../../mdx/lookupcube-mdx.md) 函数从多维数据集上下文以外的多维数据集中检索数据。 另外，可以使用诸如 [Filter](../../../mdx/filter-mdx.md) 之类的函数在对查询求值时对上下文进行临时限制。  
  
## <a name="see-also"></a>另请参阅  
 [MDX 查询基础知识 (Analysis Services)](../../../analysis-services/multidimensional-models/mdx/mdx-query-fundamentals-analysis-services.md)  
  
  
