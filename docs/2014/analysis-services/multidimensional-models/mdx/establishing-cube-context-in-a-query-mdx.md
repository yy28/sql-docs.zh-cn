---
title: 在查询中建立多维数据集上下文（MDX） |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- cubes [Analysis Services], MDX
- MDX [Analysis Services], cube context
- SELECT statement [MDX]
- Multidimensional Expressions [Analysis Services], cube context
- queries [MDX], cube context
ms.assetid: 79d6a1e8-2825-4eb9-97df-5071aecae8f0
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: f9f0f960c531fac8bae8f03479bacd507ffc3078
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/08/2020
ms.locfileid: "66074602"
---
# <a name="establishing-cube-context-in-a-query-mdx"></a>在查询中建立多维数据集上下文 (MDX)
  每个 MDX 查询都是在指定的多维数据集上下文中运行的。 此上下文定义了查询中的表达式求值的成员。  
  
 在 SELECT 语句中，FROM 子句用于确定多维数据集上下文。 此上下文可以是整个多维数据集，也可以只是该多维数据集的一个子多维数据集。 如果通过 FROM 子句指定了多维数据集上下文，就可以使用其他函数来扩展或限制该上下文。  
  
> [!NOTE]  
>  也可以使用 SCOPE 和 CALCULATE 语句在 MDX 脚本中管理多维数据集上下文。 有关详细信息，请参阅 [MDX 脚本编写基础知识 (Analysis Services)](mdx-scripting-fundamentals-analysis-services.md)。  
  
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
  
 有关 MDX SELECT 语句中的 FROM 子句的详细信息，请参阅 [SELECT 语句 (MDX)](/sql/mdx/mdx-data-manipulation-select)。  
  
## <a name="refining-the-context"></a>完善上下文  
 虽然 FROM 子句指定的多维数据集上下文在单个多维数据集中，但这并不会造成您无法一次处理多个多维数据集中的数据。  
  
 您可以使用 MDX [LookupCube](/sql/mdx/lookupcube-mdx) 函数从多维数据集上下文以外的多维数据集中检索数据。 另外，可以使用诸如 [Filter](/sql/mdx/filter-mdx) 之类的函数在对查询求值时对上下文进行临时限制。  
  
## <a name="see-also"></a>另请参阅  
 [MDX 查询基础知识 &#40;Analysis Services&#41;](mdx-query-fundamentals-analysis-services.md)  
  
  
