---
title: 维度简介（Analysis Services 多维数据） |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: reference
helpviewer_keywords:
- dimensions [Analysis Services], about dimensions
- storage [Analysis Services], dimensions
- dimensions [Analysis Services], examples
- storing data [Analysis Services], dimensions
- storage [Analysis Services]
ms.assetid: ab170fdd-4144-42db-9497-690b9189fc25
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: e1a78735cd5aee5ebc87adaac6fab48bb4e183d6
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/27/2020
ms.locfileid: "81387897"
---
# <a name="introduction-to-dimensions-analysis-services---multidimensional-data"></a>维度简介（Analysis Services - 多维数据）
  所有 Microsoft [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]维度都是基于数据源视图中的表或视图中的列的属性组。 独立于多维数据集存在的维度既可以在多个多维数据集中使用，也可以在一个多维数据集中多次使用，还可以在 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 实例之间链接。 独立于多维数据集存在的维度称为数据库维度，多维数据集中的数据库维度实例称为多维数据集维度。  
  
## <a name="dimension-based-on-a-star-schema-design"></a>基于星型架构设计的维度  
 维度的结构主要由一个或多个基础维度表的结构决定。 最简单的结构称为星型架构，在该架构中，每个维度均基于一个通过主键-外键关系直接链接到事实数据表的维度表。  
  
 下图[!INCLUDE[ssSampleDBDWobject](../../includes/sssampledbdwobject-md.md)]说明了示例数据库的子节，其中， **FactResellerSales**事实数据表与两个维度表**DimReseller**和**DimPromotion**相关联。 **FactResellerSales**事实数据表中的**ResellerKey**列定义了与**DimReseller**维度表中的**ResellerKey**主键列的外键关系。 同样， **FactResellerSales**事实数据表中的**PromotionKey**列定义了与**DimPromotion**维度表中的**PromotionKey**主键列的外键关系。  
  
 ![事实维度关系的逻辑架构](../../analysis-services/dev-guide/media/dimfactrelationship.gif "事实维度关系的逻辑架构")  
  
## <a name="dimension-based-on-a-snowflake-schema-design"></a>基于雪花型架构设计的维度  
 通常，因为需要使用来自多个表的信息才能定义维度，因此将需要一个更为复杂的结构。 在此称为雪花型架构的结构中，每个维度均基于多个通过主键-外键关系相互链接并最终链接到事实数据表的表中的列属性。 例如，下面的关系图说明了在**AdventureWorksDW**示例项目中完整描述 "产品" 维度所需的表：  
  
 ![AdventureWorksAS 产品维度表](../../analysis-services/dev-guide/media/dimproduct.gif "AdventureWorksAS 产品维度表")  
  
 若要完整说明某一产品，则在“产品”维度中必须包含该产品的类别和子类别。 但是，该信息不会直接驻留在**DimProduct**维度的主表中。 从**DimProduct**到**DimProductSubcategory**的外键关系（又与**DimProductCategory**表具有外键关系），因此可以在 "产品" 维度中包含产品类别和子类别的信息。  
  
## <a name="snowflake-schema-versus-reference-relationship"></a>雪花型架构与引用关系  
 有时，您可以选择是使用雪花型架构定义来自多个表的维度中的属性，还是先定义两个单独的维度，然后定义这两个表之间的引用维度关系。 以下关系图阐释了这种方案。  
  
 ![示例引用维度的逻辑架构](../../analysis-services/dev-guide/media/dimindirect.gif "示例引用维度的逻辑架构")  
  
 在上图中， **FactResellerSales**事实数据表与**DimGeography**维度表之间没有外键关系。 但是， **FactResellerSales**事实数据表与**DimReseller**维度表具有外键关系，后者又与**DimGeography**维度表具有外键关系。 若要定义一个包含有关每个分销商的地理信息的分销商维度，则必须从 " **DimGeography** " 和 " **DimReseller** " 维度表中检索这些属性。 但是，在 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 中，通过先创建两个单独的维度，然后通过定义这两个维度之间的引用维度关系将其链接到一个度量值组内，也可以完成上述操作。 有关引用维度关系的详细信息，请参阅[维度关系](../multidimensional-models-olap-logical-cube-objects/dimension-relationships.md)。  
  
 在此方案中使用引用维度关系的一个优点是：可以先创建一个地域维度，然后根据该地域维度创建多个多维数据集维度，而不需要任何额外的存储空间。 例如，可以将其中一个地域多维数据集维度链接到分销商维度，将另一个地域多维数据集维度链接到客户维度。 **相关主题：**[维度关系](../multidimensional-models-olap-logical-cube-objects/dimension-relationships.md)、[定义引用的关系和引用的关系属性](../multidimensional-models/define-a-referenced-relationship-and-referenced-relationship-properties.md)  
  
## <a name="processing-a-dimension"></a>处理维度  
 创建维度之后，必须先处理维度，然后才能查看该维度中属性和层次结构的成员。 更改了维度的结构，或者更新了该维度基础表中的信息之后，必须再次对维度进行处理，然后才能查看更改。 在发生结构更改后对维度进行处理时，还必须处理任何包括该维度的多维数据集，否则无法查看多维数据集。  
  
## <a name="security"></a>安全性  
 维度的所有从属对象（包括层次结构、级别以及成员）都使用 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 中的角色进行保护。 维度安全性可应用于数据库中使用该维度的所有多维数据集，或者只应用于特定的多维数据集。 有关维度安全性的详细信息，请参阅[授予对维度的权限 &#40;Analysis Services&#41;](../multidimensional-models/grant-permissions-on-a-dimension-analysis-services.md)。  
  
## <a name="see-also"></a>另请参阅  
 [维度存储](../multidimensional-models-olap-logical-dimension-objects/dimensions-storage.md)   
 [维度翻译](../multidimensional-models-olap-logical-dimension-objects/dimension-translations.md)   
 [启用写操作的维度](../multidimensional-models-olap-logical-dimension-objects/write-enabled-dimensions.md)  
  
  
