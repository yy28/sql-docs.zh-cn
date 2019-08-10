---
title: 多维数据集单元 (Analysis Services 多维数据) |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: reference
helpviewer_keywords:
- storing data [Analysis Services], cells
- hierarchies [Analysis Services], cells
- OLAP objects [Analysis Services], cells
- data members [Analysis Services]
- cubes [Analysis Services], cells
- empty cells [Analysis Services]
- nonleaf members
- cubes [Analysis Services], examples
- storage [Analysis Services], cells
- nonleaf cells
- calculated cells [Analysis Services]
- dimensions [Analysis Services], cells
- cells [Analysis Services]
- leaf members
- leaf cells
ms.assetid: 9945773c-a43b-40d4-91cf-3d2ebc90bca5
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 9d9ca444c4e889c68f90abf4cf76c07d1c2d574a
ms.sourcegitcommit: a1adc6906ccc0a57d187e1ce35ab7a7a951ebff8
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/09/2019
ms.locfileid: "68887917"
---
# <a name="cube-cells-analysis-services---multidimensional-data"></a>多维数据集单元（Analysis Services - 多维数据）
  多维数据集由单元组成，单元按度量值组和维度进行组织。 单元表示多维数据集中来自多维数据集内每个维度的一个成员的唯一逻辑交集。 例如，以下关系图说明的多维数据集包含了一个有两个度量值的度量值组，它们通过三个名为“源”、“路线”和“时间”的维度组织在一起。  
  
 ![标识单个单元格的多维数据集关系图](https://docs.microsoft.com/analysis-services/analysis-services/dev-guide/media/as-cubeintro5.gif "标识单个单元格的多维数据集关系图")  
  
 此关系图中的单个带阴影的单元是下列成员的交集：  
  
-   “路线”维度的空运成员。  
  
-   “源”维度的非洲成员。  
  
-   “时间”维度的第四季度成员。  
  
-   包度量值。  
  
## <a name="leaf-and-nonleaf-cells"></a>叶和非叶单元  
 可以用几种方式获得多维数据集中的单元的值。 在上面的示例中, 可以从多维数据集的事实数据表中直接检索单元中的值, 因为用于标识该单元的所有成员均为*叶成员*。 从层次结构上看，叶成员没有子成员，并且通常引用维度表中的单个记录。 这种形式的单元格称为*叶单元格*。  
  
 但是, 还可以使用*非叶成员*识别单元。 非叶成员是有一个或多个子成员的成员。 在这种情况下，通常基于与非叶成员关联的子成员的聚合派生单元的值。 例如，下列成员和维度的交集是指其值由聚合提供的单元：  
  
-   “路线”维度的空运成员。  
  
-   “源”维度的非洲成员。  
  
-   “时间”维度的下半年成员。  
  
-   包成员。  
  
 “时间”维度的下半年成员是非叶成员。 因此，与它关联的所有值必须都是聚合值，如以下关系图所示。  
  
 第![二个半个成员的第三个和第四个季度单元]第(https://docs.microsoft.com/analysis-services/analysis-services/dev-guide/media/as-cubeintro6.gif "二个半个成员的第三个和第四个季度单元")  
  
 假定“第三季度”和“第四季度”成员的聚合就是汇总，则指定单元的值是 400，即上面关系图中所有带阴影叶单元的总和。 由于该单元的值是从其他单元的聚合派生的, 因此指定的单元格被视为*非叶单元*。  
  
 除了自定义成员以外，为使用自定义汇总和成员组的成员所派生的单元值将以相似方式进行处理。 但是，为计算成员而派生的单元值将完全基于用来定义计算成员的多维表达式 (MDX)；在某些情况下，可能不涉及实际的单元数据。 有关详细信息, 请参阅[父子维度中的自定义汇总运算符](../multidimensional-models/parent-child-dimension-attributes-custom-rollup-operators.md)、[定义自定义成员公式](../multidimensional-models/attribute-properties-define-custom-member-formulas.md)和[计算](../multidimensional-models-olap-logical-cube-objects/calculations.md)。  
  
## <a name="empty-cells"></a>空单元  
 并不是多维数据集中的每个单元都必须要包含值；多维数据集中可以有没有数据的交集。 这些称为空单元的交集经常出现在多维数据集中，因为并非多维数据集中带有度量值的维度属性的每个交集都在事实数据表中包含一个相应的记录。 多维数据集中的空单元格与多维数据集中的单元总数的比值经常称为多维数据集的*稀疏度*。  
  
 例如，下列关系图中所示的多维数据集的结构与本主题中的其他示例类似。 但是，在本示例中，在第三季度没有到非洲的空运或者在第四季度没有到澳大利亚的空运。 由于事实数据表中无数据支持这些维度和度量值的交集，所以这些交集的单元为空。  
  
 ![标识空单元格的多维数据集关系图](https://docs.microsoft.com/analysis-services/analysis-services/dev-guide/media/as-cubeintro7.gif "标识空单元格的多维数据集关系图")  
  
 在[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 中[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)], 空单元格是具有特殊质量的单元格。 因为空单元可扭曲交叉联接、计数等的结果，因此为了进行计算，许多 MDX 函数都提供了忽略空单元的功能。 有关详细信息, 请参阅[多维&#40;表达式&#41; mdx 参考](/sql/mdx/multidimensional-expressions-mdx-reference)和[mdx &#40;中的重要概念&#41;Analysis Services](../multidimensional-models/key-concepts-in-mdx-analysis-services.md)。  
  
## <a name="security"></a>安全性  
 对单元数据的访问是在角色级别通过 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 来进行管理的，并且可以使用 MDX 表达式进行严格控制。 有关详细信息, 请参阅[授予对维度数据&#40;的自&#41;定义访问权限 Analysis Services](../multidimensional-models/grant-custom-access-to-dimension-data-analysis-services.md), 以及向[单元&#40;数据&#41;Analysis Services 授予自定义访问权限](../multidimensional-models/grant-custom-access-to-cell-data-analysis-services.md)。  
  
## <a name="see-also"></a>请参阅  
 [多维数据&#40;集存储 Analysis Services-多维数据&#41;](../multidimensional-models-olap-logical-cube-objects/cube-storage-analysis-services-multidimensional-data.md)   
 [聚合和聚合设计](../multidimensional-models-olap-logical-cube-objects/aggregations-and-aggregation-designs.md)  
  
  
