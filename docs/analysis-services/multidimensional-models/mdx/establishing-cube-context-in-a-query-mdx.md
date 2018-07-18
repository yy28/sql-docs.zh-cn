---
title: 在查询 (MDX) 中建立多维数据集上下文 |Microsoft 文档
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 2efdfc74bf45f4e8e6b913e651b0be5fa4511034
ms.sourcegitcommit: c12a7416d1996a3bcce3ebf4a3c9abe61b02fb9e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/10/2018
ms.locfileid: "34022084"
---
# <a name="establishing-cube-context-in-a-query-mdx"></a>在查询中建立多维数据集上下文 (MDX)
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
  每个 MDX 查询都是在指定的多维数据集上下文中运行的。 此上下文定义了查询中的表达式求值的成员。  
  
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
 [MDX 查询基础知识 & #40;Analysis Services & #41;](../../../analysis-services/multidimensional-models/mdx/mdx-query-fundamentals-analysis-services.md)  
  
  
