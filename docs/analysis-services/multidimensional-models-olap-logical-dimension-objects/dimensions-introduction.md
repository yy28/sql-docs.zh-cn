---
title: "维度 (Analysis Services-多维数据) 简介 |Microsoft 文档"
ms.custom: 
ms.date: 03/14/2017
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: 
ms.component: 
ms.reviewer: 
ms.suite: pro-bi
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: reference
applies_to:
- SQL Server 2016 Preview
helpviewer_keywords:
- dimensions [Analysis Services], about dimensions
- storage [Analysis Services], dimensions
- dimensions [Analysis Services], examples
- storing data [Analysis Services], dimensions
- storage [Analysis Services]
ms.assetid: ab170fdd-4144-42db-9497-690b9189fc25
caps.latest.revision: 
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: On Demand
ms.openlocfilehash: 8e6b39e6f8e91217dbc2de28575571e3043c7358
ms.sourcegitcommit: 7519508d97f095afe3c1cd85cf09a13c9eed345f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/15/2018
---
# <a name="dimensions---introduction"></a>维度-简介
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
所有 Microsoft [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]维度是基于从表或视图中的数据源视图的列的属性的组合。 独立于多维数据集存在的维度既可以在多个多维数据集中使用，也可以在一个多维数据集中多次使用，还可以在 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 实例之间链接。 独立于多维数据集存在的维度称为数据库维度，多维数据集中的数据库维度实例称为多维数据集维度。  
  
## <a name="dimension-based-on-a-star-schema-design"></a>基于星型架构设计的维度  
 维度的结构主要由一个或多个基础维度表的结构决定。 最简单的结构称为星型架构，在该架构中，每个维度均基于一个通过主键-外键关系直接链接到事实数据表的维度表。  
  
 下图说明的子部分的[!INCLUDE[ssSampleDBDWobject](../../includes/sssampledbdwobject-md.md)]示例数据库，在其中**FactResellerSales**事实数据表与两个维度表， **DimReseller**和**DimPromotion**。 **ResellerKey**中的列**FactResellerSales**事实表定义了外的键关系到**ResellerKey**中的主键列**DimReseller**维度表。 同样， **PromotionKey**中的列**FactResellerSales**事实表定义了外的键关系到**PromotionKey** 中的主键列**DimPromotion**维度表。  
  
 ![事实维度关系的逻辑架构](../../analysis-services/multidimensional-models-olap-logical-dimension-objects/media/dimfactrelationship.gif "逻辑架构事实维度关系")  
  
## <a name="dimension-based-on-a-snowflake-schema-design"></a>基于雪花型架构设计的维度  
 通常，因为需要使用来自多个表的信息才能定义维度，因此将需要一个更为复杂的结构。 在此称为雪花型架构的结构中，每个维度均基于多个通过主键-外键关系相互链接并最终链接到事实数据表的表中的列属性。 例如下, 图说明完整地描述中的产品维度所需的表**AdventureWorksDW**示例项目：  
  
 ![为 AdventureWorksAS 产品维度表](../../analysis-services/multidimensional-models-olap-logical-dimension-objects/media/dimproduct.gif "AdventureWorksAS 产品维度的表")  
  
 若要完整说明某一产品，则在“产品”维度中必须包含该产品的类别和子类别。 但是，该信息不驻留在的主表直接**DimProduct**维度。 从外的键关系**DimProduct**到**DimProductSubcategory**，该子元素又具有为外的键关系**DimProductCategory**表，使它可能要包含在产品维度中的产品类别和子类别的信息。  
  
## <a name="snowflake-schema-versus-reference-relationship"></a>雪花型架构与引用关系  
 有时，您可以选择是使用雪花型架构定义来自多个表的维度中的属性，还是先定义两个单独的维度，然后定义这两个表之间的引用维度关系。 以下关系图阐释了这种方案。  
  
 ![示例引用维度的逻辑架构](../../analysis-services/multidimensional-models-olap-logical-dimension-objects/media/dimindirect.gif "逻辑架构示例引用的维度")  
  
 在上图中， **FactResellerSales**事实数据表没有与外的键关系**DimGeography**维度表。 但是， **FactResellerSales**事实表具有外的键关系与**DimReseller**接下来的维度表具有外的键关系与**DimGeography**维度表。 若要定义包含有关每个分销商的地理位置信息的分销商维度，您将不得不检索这些属性从**DimGeography**和**DimReseller**维度表。 但是，在 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 中，通过先创建两个单独的维度，然后通过定义这两个维度之间的引用维度关系将其链接到一个度量值组内，也可以完成上述操作。 有关引用维度关系的详细信息，请参阅[维度关系](../../analysis-services/multidimensional-models-olap-logical-cube-objects/dimension-relationships.md)。  
  
 在此方案中使用引用维度关系的一个优点是：可以先创建一个地域维度，然后根据该地域维度创建多个多维数据集维度，而不需要任何额外的存储空间。 例如，可以将其中一个地域多维数据集维度链接到分销商维度，将另一个地域多维数据集维度链接到客户维度。 **相关主题：**[维度关系](../../analysis-services/multidimensional-models-olap-logical-cube-objects/dimension-relationships.md)，[定义引用关系和引用关系属性](../../analysis-services/multidimensional-models/define-a-referenced-relationship-and-referenced-relationship-properties.md)  
  
## <a name="processing-a-dimension"></a>处理维度  
 创建维度之后，必须先处理维度，然后才能查看该维度中属性和层次结构的成员。 更改了维度的结构，或者更新了该维度基础表中的信息之后，必须再次对维度进行处理，然后才能查看更改。 在发生结构更改后对维度进行处理时，还必须处理任何包括该维度的多维数据集，否则无法查看多维数据集。  
  
## <a name="security"></a>Security  
 维度的所有从属对象（包括层次结构、级别以及成员）都使用 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 中的角色进行保护。 维度安全性可应用于数据库中使用该维度的所有多维数据集，或者只应用于特定的多维数据集。 有关维度安全性的详细信息，请参阅[授予对维度 &#40; 的权限Analysis Services &#41;](../../analysis-services/multidimensional-models/grant-permissions-on-a-dimension-analysis-services.md).  
  
## <a name="see-also"></a>另请参阅  
 [维度存储](../../analysis-services/multidimensional-models-olap-logical-dimension-objects/dimensions-storage.md)   
 [维度翻译](../../analysis-services/multidimensional-models-olap-logical-dimension-objects/dimension-translations.md)   
 [写入的维度](../../analysis-services/multidimensional-models-olap-logical-dimension-objects/write-enabled-dimensions.md)  
  
  
