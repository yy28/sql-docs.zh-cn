---
title: "属性关系 |Microsoft 文档"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: analysis-services
ms.service: 
ms.component: multidimensional-models
ms.reviewer: 
ms.suite: sql
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
applies_to:
- SQL Server 2016 Preview
helpviewer_keywords:
- member properties [Analysis Services], attribute relationships
- security [Analysis Services], properties
- PROPERTIES keyword
- storage [Analysis Services], attribute relationships
- natural hierarchies [Analysis Services]
- dimensions [Analysis Services], member properties
- queries [MDX], attribute relationships
- user-defined hierarchies [Analysis Services]
- attributes [Analysis Services], relationships
- member properties [Analysis Services]
- members [Analysis Services], attribute relationships
- storing data [Analysis Services], attribute relationships
- relationships [Analysis Services], attributes
ms.assetid: 2491422a-4cf5-4b23-b6ab-289222b22ce8
caps.latest.revision: 45
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: f2fc6db2abf6c23ae4b265255b2cc9d191632e7f
ms.contentlocale: zh-cn
ms.lasthandoff: 09/01/2017

---
# <a name="attribute-relationships"></a>属性关系
  在[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]，维度中的属性将始终与直接或间接的键属性。 当您基于星型架构（在该架构中，所有维度属性都派生自同一关系表）定义维度时，维度的键属性和每个非键属性之间会自动定义属性关系。 当您基于雪花架构（在该架构中，维度属性派生自多个相关的表）定义维度时，会自动按如下方式定义属性关系：  
  
-   在键属性与绑定到主维度表中各列的每个非键属性之间定义。  
  
-   在键属性与绑定到辅助表中链接基础维度表的外键的属性之间定义。  
  
-   在绑定到辅助表中外键的属性与绑定到辅助表中各列的每个非键属性之间定义。  
  
 但是，由于多种原因您可能需要更改这些默认的属性关系。 例如，您可能需要定义自然层次结构、自定义排序顺序或基于非键属性的维度粒度。 有关详细信息，请参阅[维度特性属性参考](../../analysis-services/multidimensional-models/dimension-attribute-properties-reference.md)。  
  
> [!NOTE]  
>  特性关系在多维表达式 (MDX) 中称作成员属性。  
  
## <a name="natural-hierarchy-relationships"></a>自然层次结构关系  
 当用户定义层次结构中包含的每个属性都与其下直接属性具有一对多关系时，层次结构就是自然层次结构。 例如，请参考基于具有八列的关系源表的“客户”维度：  
  
-   CustomerKey  
  
-   CustomerName  
  
-   年龄  
  
-   性别  
  
-   电子邮件  
  
-   City  
  
-   Country  
  
-   地区  
  
 相应的 Analysis Services 维度具有七个属性：  
  
-   客户（基于 CustomerKey，其中 CustomerName 提供成员名称）  
  
-   年龄、性别、电子邮件、市县、地区、国家(地区)  
  
 通过在某级别的属性和此级别下面的级别的属性之间创建属性关系，强制执行表示自然层次结构的关系。 对于 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]，这可指定自然关系和潜在聚合。 在“客户”维度中，“国家(地区)”、“区域”、“市县”和“客户”属性具有自然层次结构。 通过添加下列属性关系来说明 `{Country, Region, City, Customer}` 的自然层次结构：  
  
-   与“区域”属性具有属性关系的“国家(地区)”属性。  
  
-   与“市县”属性具有属性关系的“区域”属性。  
  
-   与“客户”属性具有属性关系的“市县”属性。  
  
 有关导航多维数据集中的数据，你还可以创建用户定义层次结构，不表示自然层次结构数据中的 (这种行为称为*即席*或*reporting*层次结构)。 例如，您可以基于 `{Age, Gender}` 创建用户定义层次结构。 尽管自然层次结构是在聚合结构和索引结构（这两种结构对源数据中的自然关系进行了解释，并且对用户隐藏）的基础上形成，但是用户无法看到两种层次结构的行为差异。  
  
 **SourceAttribute**级别的属性确定哪些属性用于描述级别。 **KeyColumns**属性上的属性提供成员数据源视图中指定的列。 **NameColumn**属性上的属性可以指定不同的名称列的成员。  
  
 若要使用的用户定义的层次结构中定义级别[!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]、**维度设计器**允许你选择相关表中的数据源视图包含中的维度属性、 维度表中的列多维数据集。 有关创建用户定义的层次结构的详细信息，请参阅[Create User-Defined 层次结构](../../analysis-services/multidimensional-models/user-defined-hierarchies-create.md)。  
  
 在 Analysis Services 中，通常对成员的内容进行假定。 叶成员没有后代，并且包含派生自基础数据源的数据。 非叶成员则具有后代，并且包含派生自对子成员执行的聚合的数据。 在聚合级别中，各成员基于其从属级别的聚合。 因此，当**IsAggregatable**属性设置为**False**上级别的源属性，没有可聚合属性应添加为与其上级别。  
  
## <a name="defining-an-attribute-relationship"></a>定义属性关系  
 创建属性关系时的主要约束是确保，对于属性关系引用的属性，属性关系所属的属性中的任何成员的值不超过一个。 例如，如果您在“市县”属性与“省市自治区”属性之间定义了关系，则每个市县只能与单个省市自治区相关。  
  
## <a name="attribute-relationship-queries"></a>属性关系查询  
 你可以使用 MDX 查询要从中检索数据属性关系，成员属性的形式与**属性**MDX 关键字**选择**语句。 有关如何使用 MDX 来检索成员属性的详细信息，请参阅[使用成员属性 &#40;MDX &#41;](../../analysis-services/multidimensional-models/mdx/mdx-member-properties.md).  
  
## <a name="see-also"></a>另请参阅  
 [属性和属性层次结构](../../analysis-services/multidimensional-models-olap-logical-dimension-objects/attributes-and-attribute-hierarchies.md)   
 [维度特性属性参考](../../analysis-services/multidimensional-models/dimension-attribute-properties-reference.md)   
 [用户层次结构](../../analysis-services/multidimensional-models-olap-logical-dimension-objects/user-hierarchies.md)   
 [用户层次结构属性](../../analysis-services/multidimensional-models-olap-logical-dimension-objects/user-hierarchies-properties.md)  
  
  

