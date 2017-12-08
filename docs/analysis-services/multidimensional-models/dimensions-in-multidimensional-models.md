---
title: "多维模型中的维度 |Microsoft 文档"
ms.custom: 
ms.date: 03/04/2017
ms.prod: sql-non-specified
ms.prod_service: analysis-services
ms.service: 
ms.component: multidimensional-models
ms.reviewer: 
ms.suite: sql
ms.technology:
- analysis-services
- analysis-services/multidimensional-tabular
- analysis-services/data-mining
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- OLAP [Analysis Services], dimensions
- dimensions [Analysis Services], about dimensions
- OLAP objects [Analysis Services], dimensions
ms.assetid: 2b62b05c-00fd-4e60-b77f-f707ba83a19b
caps.latest.revision: "46"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: On Demand
ms.openlocfilehash: 73d367008bc1b3be6f4e3f6f5885adf79437f4c0
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/17/2017
---
# <a name="dimensions-in-multidimensional-models"></a>多维模型中的维度
  数据库维度是相关对象（称为属性）的集合，用于提供有关一个或多个多维数据集中的事实数据的信息。 例如，产品维度中的典型属性可能是产品名称、产品类别、产品系列、产品规格和产品价格。 这些对象绑定到数据源视图的一个或多个表中的一个或多个列。 默认情况下，这些属性和属性层次结构一样是可见的，可用于了解多维数据集中的事实数据。 可以将属性组织为用户定义层次结构，从而提供导航路径以帮助用户浏览多维数据集中的数据。  
  
 多维数据集包含用户分析事实数据所基于的所有维度。 多维数据集中的数据库维度实例称为多维数据集维度，它与多维数据集中的一个或多个度量值组有关。 数据库维度可以在多维数据集中多次使用。 例如，事实数据表可以具有多个与时间相关的事实数据，并且可以定义单独的多维数据集维度以帮助分析每个与时间相关的事实数据。 但是，只需存在一个与时间相关的数据库维度，这也意味着只需存在一个与时间相关的关系数据库表便可支持多个基于时间的多维数据集维度。  
  
> [!NOTE]  
>  有关与维度设计相关的性能问题，请参阅 [SQL Server 2008 R2 Analysis Services 性能指南](http://go.microsoft.com/fwlink/?LinkId=306717)。  
  
## <a name="defining-dimensions-attributes-and-hierarchies"></a>定义维度、属性和层次结构  
 定义数据库和多维数据集的维度、属性和层次结构的最简单方法是使用多维数据集向导在定义多维数据集的同时创建维度。 多维数据集向导将根据向导在数据源视图中找到的维度表，或您在数据源视图中指定用于多维数据集的维度表来创建维度。 这样，该向导创建数据库维度并将其添加到新的多维数据集中，从而创建多维数据集维度。  
  
 创建多维数据集时，还可以将数据库中已存在的任何维度添加到新的多维数据集中。 这些维度可能在先前已针对其他多维数据集定义，或者已由维度向导定义。 定义数据库维度后，您可以在“维度设计器”中修改并配置数据库维度。 您还可以在“多维数据集设计器”中对多维数据集维度进行有限程度的自定义。  
  
> [!NOTE]  
>  您还可以使用 XMLA 或“分析管理对象”(AMO)，以编程方式来设计并配置维度、属性和层次结构。 有关详细信息，请参阅 [Analysis Services 脚本语言（支持 XMLA 的 ASSL）](../../analysis-services/scripting/analysis-services-scripting-language-assl-for-xmla.md)和[使用分析管理对象 (AMO) 进行开发](../../analysis-services/multidimensional-models/analysis-management-objects/developing-with-analysis-management-objects-amo.md)。  
  
## <a name="in-this-section"></a>本节内容  
 下表对本部分的主题进行了说明：  
  
 [定义数据库维度](../../analysis-services/multidimensional-models/define-database-dimensions.md)  
 说明如何使用维度设计器修改和配置数据库维度。  
  
 [维度特性属性参考](../../analysis-services/multidimensional-models/dimension-attribute-properties-reference.md)  
 说明如何使用维度设计器定义、修改和配置数据库维度属性。  
  
 [定义属性关系](../../analysis-services/multidimensional-models/attribute-relationships-define.md)  
 说明如何使用维度设计器定义、修改和配置属性关系。  
  
 [创建用户定义层次结构](../../analysis-services/multidimensional-models/user-defined-hierarchies-create.md)  
 说明如何使用“维度设计器”定义、修改和配置维度属性的用户定义层次结构。  
  
 [使用商业智能向导增强维度](http://msdn.microsoft.com/library/12d995d1-75ca-4890-bf4b-a2656910b8d0)  
 说明如何使用商业智能向导增强数据库维度。  
  
## <a name="see-also"></a>另请参阅  
 [多维模型中的多维数据集](../../analysis-services/multidimensional-models/cubes-in-multidimensional-models.md)  
  
  
