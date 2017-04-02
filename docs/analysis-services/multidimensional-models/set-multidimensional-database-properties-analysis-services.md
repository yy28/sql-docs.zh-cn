---
title: "设置多维数据库属性 (Analysis Services) | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "analysis-services"
  - "analysis-services/multidimensional-tabular"
  - "analysis-services/data-mining"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "属性 [Analysis Services], 数据库"
ms.assetid: a8be5b3f-3148-448a-976c-7222705155d9
caps.latest.revision: 24
author: "Minewiskan"
ms.author: "owend"
manager: "erikre"
caps.handback.revision: 24
---
# 设置多维数据库属性 (Analysis Services)
  可在 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 数据库设计器中配置许多 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] 数据库属性。  
  
 在此设计器中，您可以执行下列任务类型：  
  
-   如果以联机模式连接到 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 数据库，则可以更改 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 数据库的名称。 如果以项目模式进行连接，则可以针对下一个项目部署更改数据库名称。 有关详细信息，请参阅[重命名多维数据库 (Analysis Services)](../../analysis-services/multidimensional-models/rename-a-multidimensional-database-analysis-services.md)和[配置 Analysis Services 项目属性 (SSDT)](../../analysis-services/multidimensional-models/configure-analysis-services-project-properties-ssdt.md)。  
  
-   您可以提供向用户显示的数据库的说明。 还可以查看数据库的名称，但不能进行更改。 若要更改数据库名称，必须编辑项目的属性。  
  
-   您可以提供数据库名称的翻译以及一种或多种语言的说明。 有关详细信息，请参阅[多维数据集转换](../../analysis-services/multidimensional-models-olap-logical-cube-objects/cube-translations.md)、[维度转换](../../analysis-services/multidimensional-models-olap-logical-dimension-objects/dimension-translations.md)和 [Analysis Services 中的转换支持](../../analysis-services/translation-support-in-analysis-services.md)。  
  
-   您可以查看并修改默认的帐户类型映射。 当一个或多个度量值使用 *ByAccount* 聚合函数时，会使用帐户类型映射。 对于每个帐户类型，您可以指定别名并修改与此帐户类型关联的默认聚合函数。 有关修改默认聚合的详细信息，请参阅[定义半累加行为](../../analysis-services/multidimensional-models/define-semiadditive-behavior.md)。  
  
## 数据库属性  
 除了上述属性之外，您还可以在“属性”窗口中配置许多数据库属性。  
  
|属性|Description|  
|--------------|-----------------|  
|聚合前缀|用于数据库中所有分区的聚合名的常用前缀。 有关详细信息，请参阅 [AggregationPrefix 元素 (ASSL)](../../analysis-services/scripting/properties/aggregationprefix-element-assl.md)。|  
|排序规则|将 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 项目部署到 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 实例时，除非在此处提供其他值，否则数据库将继承“排序规则”服务器属性。|  
|DataSourceImpersonationInfo|为数据库中的所有数据源对象指定默认模拟模式。 这是 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 服务在处理对象、同步服务器以及执行 OpenQuery 和 SystemOpenSchema 数据挖掘语句时使用的模式。|  
|估计大小|提供磁盘上数据库文件的估计大小。 如果数据存储在多个位置，此估计值将仅限于数据库文件夹下存储的数据文件。<br /><br /> **EstimatedSize** 也可用作估算内存的基础。 由于将数据库加载到内存时创建的附加数据结构，内存需求通常大于磁盘上的数据大小。<br /><br /> 要进一步估计内存需求，您也可以使用任务管理器查看在处理数据库之前和之后的 Analysis Services 进程内存并查看内存使用率，通过内存使用率来了解数据库的内存需求。|  
|语言|将 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 项目部署到 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 实例时，除非在此处提供其他值，否则数据库将继承“语言”服务器属性。|  
|MasterDataSource ID|用于远程分区。 有关详细信息，请参阅 [Remote Partitions](../Topic/Remote%20Partitions.md)。|  
  
## 另请参阅  
 [“数据库属性”对话框（SSAS - 多维）](../Topic/Database%20Properties%20Dialog%20Box%20\(SSAS%20-%20Multidimensional\).md)   
 [配置 Analysis Services 项目属性 (SSDT)](../../analysis-services/multidimensional-models/configure-analysis-services-project-properties-ssdt.md)  
  
  