---
title: 多维模型中的数据源 |Microsoft 文档
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: multidimensional-models
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 149ac1e36eb07d40223ffc97fba1646932ab0093
ms.sourcegitcommit: c12a7416d1996a3bcce3ebf4a3c9abe61b02fb9e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/10/2018
ms.locfileid: "34022824"
---
# <a name="data-sources-in-multidimensional-models"></a>多维模型中的数据源
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
  您导入或加载到多维模型中的所有数据都来自外部数据源。 通常源数据来自用于报告目的数据仓库，但它也可以来自可直接访问或通过媒介（如 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 包）间接访问的任意关系数据库。  
  
 **中的** “数据源” [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 对象指定与外部数据源的直接连接。 除了物理位置之外，数据源对象还指定连接字符串、数据访问接口、凭据和控制连接行为的其他属性。  
  
 在下列操作期间使用数据源对象提供的信息：  
  
-   将架构信息和用于生成数据源视图的其他元数据提供给模型。  
  
-   在处理期间查询或将数据加载到模型。  
  
-   对使用 ROLAP 存储模式的多维模型或数据挖掘模型运行查询。  
  
-   读取或写入到远程分区。  
  
-   连接到链接对象，以及从目标同步到源。  
  
-   执行更新存储在关系数据库中的事实数据表数据的写回操作。  
  
 在从头开始生成一个多维模型时，可通过创建数据源对象来开始，然后使用该对象生成下一个对象，即 **“数据源视图”**。 数据源视图是模型中的数据抽象层。 它通常在数据源对象之后创建，并且使用源数据库的架构作为基础。 不过，您可以选择其他方法来生成模型，包括从多维数据集和维度开始，并且生成最好地支持您的设计的架构。  
  
 无论您是以何种方式来生成模型的，每个模型都要求至少一个数据源对象，该对象指定与源数据的连接。 您可以在单个模型中创建多个数据源对象，以便使用来自不同源的数据或者针对特定对象改变连接属性。  
  
 可独立于您的模型中的其他对象来管理数据源对象。 创建一个数据源后，可在以后更改其属性，然后对模型进行预处理以确保正确地检索数据。  
  
## <a name="related-topics-and-tasks"></a>相关主题和任务  
  
|主题|Description|  
|-----------|-----------------|  
|[支持的数据源（SSAS - 多维）](../../analysis-services/multidimensional-models/supported-data-sources-ssas-multidimensional.md)|介绍可以在多维模型中使用的数据源的类型。|  
|[创建数据源 & #40;SSAS 多维 & #41;](../../analysis-services/multidimensional-models/create-a-data-source-ssas-multidimensional.md)|说明如何将数据源对象添加到多维模型。|  
|[删除解决方案资源管理器 & #40; 中的数据源SSAS 多维 & #41;](../../analysis-services/multidimensional-models/delete-a-data-source-in-solution-explorer-ssas-multidimensional.md)|使用此过程可从多维模型中删除数据源对象。|  
|[设置数据源属性 & #40;SSAS 多维 & #41;](../../analysis-services/multidimensional-models/set-data-source-properties-ssas-multidimensional.md)|描述每个属性，并说明如何设置每个属性。|  
|[设置模拟选项 & #40;SSAS-多维 & #41;](../../analysis-services/multidimensional-models/set-impersonation-options-ssas-multidimensional.md)|说明如何在“模拟信息”对话框中配置选项。|  
  
## <a name="see-also"></a>另请参阅  
 [数据库对象 & #40;Analysis Services-多维数据 & #41;](../../analysis-services/multidimensional-models/olap-logical/database-objects-analysis-services-multidimensional-data.md)   
 [逻辑体系结构 & #40;Analysis Services-多维数据 & #41;](../../analysis-services/multidimensional-models/olap-logical/understanding-microsoft-olap-logical-architecture.md)   
 [多维模型中的数据源视图](../../analysis-services/multidimensional-models/data-source-views-in-multidimensional-models.md)   
 [数据源和绑定 & #40;SSAS 多维 & #41;](../../analysis-services/multidimensional-models/data-sources-and-bindings-ssas-multidimensional.md)  
  
  
