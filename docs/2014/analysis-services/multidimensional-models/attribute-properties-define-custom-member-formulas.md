---
title: 定义自定义成员公式 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
ms.topic: conceptual
helpviewer_keywords:
- members [Analysis Services], custom
- custom rollup formulas [Analysis Services]
- MDX [Analysis Services], custom rollup formulas
- custom member formulas [Analysis Services]
ms.assetid: 258304e2-d900-4013-97e3-871f51dfdce2
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 83c864fc3af588b2dbf78346af1ddf1cd8430a01
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/02/2018
ms.locfileid: "48186017"
---
# <a name="define-custom-member-formulas"></a>定义自定义成员公式
  可以定义称为自定义成员公式的多维表达式 (MDX) 表达式，以便为指定属性的成员提供值。 数据源视图内表中的列为属性中的每个成员提供了用于为其提供值的表达式。  
  
 自定义成员公式确定与成员相关的单元值，并替代度量值的聚合函数。 自定义成员公式是以 MDX 编写的。 每个自定义成员公式应用于一个成员。 自定义成员公式存储在维度表中，或者存储在与维度表具有外键关系的其他表中。  
  
 特性的 `CustomRollupColumn` 属性指定包含该特性成员的自定义成员公式的列。 如果列中的某行为空，则通常返回成员的单元值。 如果列中的公式无效，则每当检索使用该成员的单元值时，都会出现运行时错误。  
  
 在为特性指定自定义成员公式前，请确保包含该特性的维度表或直接相关的表具有用于存储自定义成员公式的字符串列。 如果是这样，则可以设置`CustomRollupColumn`特性的属性手动或使用商业智能向导的设置自定义成员公式增强功能启用特性的自定义成员公式。 有关如何使用此增强功能的详细信息，请参阅 [为维度中的属性设置自定义成员公式](bi-wizard-custom-member-formulas-for-attributes-in-a-dimension.md)。  
  
## <a name="evaluating-custom-member-formulas"></a>对自定义成员公式求值  
 自定义成员公式不同于计算成员。 自定义成员公式应用于维度表中存在的成员，并且仅提供成员的值。 相反，计算成员并未存储在维度表中，并且计算成员表达式可定义维度或层次结构中包含的其他成员的数据和元数据。  
  
 自定义成员公式替代与度量值相关的聚合函数。 例如，在指定自定义成员公式之前，使用 `Sum` 聚合函数的度量值对“时间”维度的下列成员产生下列值：  
  
-   2003: 2100  
  
    -   第一季度：700  
  
    -   第二季度：500  
  
    -   第三季度：100  
  
    -   第四季度：800  
  
-   2004: 1500  
  
    -   第一季度：600  
  
    -   第二季度：200  
  
    -   第三季度：300  
  
    -   第四季度：400  
  
 使用自定义成员公式时，成员的值可改由自定义汇总公式提供。 例如，以下自定义成员公式可用来为“时间”维度中 2004 成员的“第四季度”子成员提供值 450。  
  
```  
Time.[Quarter 3] * 1.5  
```  
  
 自定义成员公式存储在维度表的一列中。 通过设置启用自定义汇总公式`CustomRollupColumn`特性的属性。  
  
 若要将单个 MDX 表达式应用于属性的所有成员，请在维度表中创建可将 MDX 表达式作为文字字符串返回的命名计算。 然后，使用要配置的特性的 `CustomRollupColumn` 属性设置指定命名计算。 命名计算是数据源视图表中的一列，可返回由 SQL 表达式定义的行值。 有关构造命名计算的详细信息，请参阅[在数据源视图中定义命名计算 (Analysis Services)](define-named-calculations-in-a-data-source-view-analysis-services.md)  
  
> [!NOTE]  
>  若要将 MDX 表达式应用于基于特定属性的特定级别的成员（而不是所有级别的成员），您可以将表达式定义为该级别中的 MDX 脚本。 有关详细信息，请参阅 [MDX 脚本编写基础知识 (Analysis Services)](mdx/mdx-scripting-fundamentals-analysis-services.md)。  
  
 如果对属性成员同时使用计算成员和自定义汇总公式，则应当注意计算顺序。 系统会先解析计算成员，然后再解析自定义汇总公式。  
  
## <a name="see-also"></a>请参阅  
 [属性和属性层次结构](../multidimensional-models-olap-logical-dimension-objects/attributes-and-attribute-hierarchies.md)   
 [为维度中的属性设置自定义成员公式](bi-wizard-custom-member-formulas-for-attributes-in-a-dimension.md)  
  
  
