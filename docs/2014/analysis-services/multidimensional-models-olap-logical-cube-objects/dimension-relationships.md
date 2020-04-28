---
title: 维度关系 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: reference
helpviewer_keywords:
- relationships [Analysis Services]
- member groups [Analysis Services]
- regular dimensions [Analysis Services]
- many-to-many relationships [Analysis Services]
- cubes [Analysis Services], relationships
- reference dimensions
- dimensions [Analysis Services], relationships
- fact dimensions [Analysis Services]
- relationships [Analysis Services], dimensions
ms.assetid: de54c059-cb0f-4f66-bd70-8605af05ec4f
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: c56cd6ee0e2a52ca523a9273e3c705eab2540191
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/27/2020
ms.locfileid: "72797618"
---
# <a name="dimension-relationships"></a>维度关系
  维度用法定义了多维数据集维度与多维数据集中的度量值组之间的关系。 多维数据集维度是在特定多维数据集中使用的数据库维度的实例。 多维数据集可以（并且通常）具有与度量值组不直接相关的多维数据集维度，但是这些维度可以通过另一个维度或度量值组与某度量值组间接相关。 向多维数据集添加数据库维度或度量值组时， [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]将尝试通过检查多维数据集的数据源视图中的维度表和事实数据表之间的关系，并检查维度中各属性之间的关系，从而确定维度的使用情况。 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 可自动为其所检测到的关系设置维度用法设置。  
  
 维度与度量值组之间的关系包括参与该关系的维度和事实数据表以及一个指定特定度量值组中维度粒度的粒度属性。  
  
## <a name="regular-dimension-relationships"></a>常规维度关系  
 当维度的键列与事实数据表直接联接时，多维数据集维度与度量值组之间便会存在常规维度关系。 此直接关系基于基础关系数据库中的主键-外键关系，但也可能基于数据源视图中定义的逻辑关系。 常规维度关系表示传统星型架构设计中维度表与事实数据表之间的关系。 有关常规关系的详细信息，请参阅[定义常规关系和常规关系属性](../multidimensional-models/define-a-regular-relationship-and-regular-relationship-properties.md)。  
  
## <a name="reference-dimension-relationships"></a>引用维度关系  
 当多维数据集维度的键列通过其他维度表中的键与事实数据表间接联接时，该维度与度量值组之间便会存在引用维度关系，如下图所示。  
  
 ![逻辑关系图，引用维度关系](../../analysis-services/dev-guide/media/as-refdimension1.gif "逻辑关系图，引用维度关系")  
  
 引用维度关系表示雪花型架构设计中的维度表与事实数据表之间的关系。 当雪花型架构中的各维度表进行连接时，可以使用多个表中的列定义一个维度，也可以根据单独的维度表定义单独的维度，然后使用引用维度关系设置定义这些维度之间的链接。 下图在雪花型架构中显示一个名为**InternetSales**的事实数据表，以及两个称为**Customer**和**Geography**的维度表。  
  
 ![逻辑架构，引用维度关系](../../analysis-services/dev-guide/media/as-refdim-schema1.gif "逻辑架构，引用维度关系")  
  
 您可以创建一个维度，其中包含**Customer**表作为维度主表和作为相关表包含的**Geography**表。 然后在维度与 InternetSales 度量值组之间定义常规关系。  
  
 另外，您还可以创建两个与 InternetSales 度量值组相关的维度：基于**Customer**表的维度，以及基于**Geography**表的维度。 然后通过使用“客户”维度的引用维度关系将“地域”维度与“Internet 销售”度量值组进行关联。 在这种情况下，当按“地域”维度创建 InternetSales 度量值组中事实数据的维度时，也就是按客户和地域创建这些数据的维度。 如果多维数据集还包含一个名为“分销商销售额”的度量值组，则可能无法按“地域”创建“分销商销售额”度量值组中事实数据的维度，因为“分销商销售额”与“地域”之间没有任何关系。  
  
 对于可相互链接的引用维度的数量没有限制，如下图所示。  
  
 ![逻辑关系图，引用维度关系](../../analysis-services/dev-guide/media/as-refdimension2.gif "逻辑关系图，引用维度关系")  
  
 有关引用关系的详细信息，请参阅[定义引用的关系和引用的关系属性](../multidimensional-models/define-a-referenced-relationship-and-referenced-relationship-properties.md)。  
  
## <a name="fact-dimension-relationships"></a>事实维度关系  
 事实维度（通常称为退化维度）是通过事实数据表而非维度表中的属性列构造的标准维度。 有用的维度数据有时存储在事实数据表中以减少重复。 例如，下面的关系图显示了**FactResellerSales** [!INCLUDE[ssAWDWsp](../../includes/ssawdwsp-md.md)]示例数据库中的 FactResellerSales 事实数据表。  
  
 ![事实数据表中的列可支持维度](../../analysis-services/dev-guide/media/as-factdim.gif "事实数据表中的列可支持维度")  
  
 该表不仅包含分销商所发出订单的每一行的属性信息，而且还包含有关订单本身的属性信息。 上图中带圆圈的属性标识**FactResellerSales**表中的信息，这些信息可用作维度中的属性。 在本例中，CarrierTrackingNumber 和 CustomerPONumber 属性列表示两条附加信息，即承运人跟踪号以及分销商发出的采购订单号。 此信息非常有趣-例如，用户对于在单个跟踪号下发运的所有订单，用户肯定会有兴趣查看聚合信息，如总产品成本。 但是，如果没有维度，则无法组织或聚合这两个属性的数据。  
  
 理论上，您可以创建与 FactResellerSales 表使用相同密钥信息的维度表，并将另外两个属性列 CarrierTrackingNumber 和 CustomerPONumber 移到该维度表。 但是，为了只将这两个属性作为单独的维度表示，您可能会复制大部分数据并为数据仓库增加不必要的复杂性。  
  
> [!NOTE]  
>  事实维度通常用于支持钻取操作。 有关操作的详细信息，请参阅[操作（Analysis Services - 多维数据）](../multidimensional-models/actions-analysis-services-multidimensional-data.md)。  
  
> [!NOTE]  
>  每次对事实关系引用的度量值组进行更新之后，都必须增量更新事实维度。 如果事实维度为 ROLAP 维度，则 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 处理引擎将删除所有缓存并增量处理度量值组。  
  
 有关事实关系的详细信息，请参阅[定义事实关系和事实关系属性](../multidimensional-models/define-a-fact-relationship-and-fact-relationship-properties.md)。  
  
## <a name="many-to-many-dimension-relationships"></a>多对多维度关系  
 在多数维度中，每个与一个且唯一的一个维度成员以及单个维度成员的事实联接都可以与多个事实数据进行关联。 在关系数据库术语中，这称为“一对多关系”。 但是，这种关系通常在将单个事实数据与多个维度成员联接时很有用。 例如，银行客户可能具有多个帐户（现金帐户、储蓄帐户、信用卡帐户以及投资帐户），并且一个帐户也可以有两个所有者或多个所有者。 基于此类关系构造的“客户”维度中，可能会有多个成员与一个帐户事务相关联。  
  
 ![逻辑架构/多对多维度关系](../../analysis-services/dev-guide/media/as-many-dimension1.gif "逻辑架构/多对多维度关系")  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)][!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]允许您在维度和事实数据表之间定义多对多关系。  
  
> [!NOTE]  
>  为了支持多对多维度关系，数据源视图必须在所涉及的所有表之间建立外键关系，如上面的关系图所示。 否则，在维度设计器的 "**维度用法**" 选项卡中建立关系时，将无法选择正确的中间度量值组。  
  
 有关多对多关系的详细信息，请参阅[定义多对多关系和多对多关系属性](../multidimensional-models/define-a-many-to-many-relationship-and-many-to-many-relationship-properties.md)。  
  
## <a name="see-also"></a>另请参阅  
 [维度（Analysis Services - 多维数据）](../multidimensional-models-olap-logical-dimension-objects/dimensions-analysis-services-multidimensional-data.md)  
  
  
