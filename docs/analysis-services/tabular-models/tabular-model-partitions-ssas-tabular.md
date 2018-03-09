---
title: "表格模型分区 |Microsoft 文档"
ms.custom: 
ms.date: 03/04/2017
ms.prod: analysis-services
ms.prod_service: analysis-services, azure-analysis-services
ms.service: 
ms.component: data-mining
ms.reviewer: 
ms.suite: pro-bi
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- sql13.asvs.ssms.partitions.partitionmgr.imbi.f1
ms.assetid: 041c269f-a229-4a41-8794-6ba4b014ef83
caps.latest.revision: 
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: On Demand
ms.openlocfilehash: daaca1355790577310419ad5a48395cd9cb8ff34
ms.sourcegitcommit: d8ab09ad99e9ec30875076acee2ed303d61049b7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/23/2018
---
# <a name="tabular-model-partitions"></a>表格模型分区 
[!INCLUDE[ssas-appliesto-sqlas-aas](../../includes/ssas-appliesto-sqlas-aas.md)]
分区将表分成多个逻辑部分。 然后，每个分区可独立于其他分区进行处理（刷新）。 在已部署的模型中将重复在模型创作过程中为模型定义的分区。 部署完成后，您可以通过使用 **中的** “分区” [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 对话框或使用脚本来管理这些分区和创建新分区。 本主题提供的信息描述已部署的表格模型数据库中的分区。 有关创建和管理模型创作期间的分区的详细信息，请参阅[分区](../../analysis-services/tabular-models/partitions-ssas-tabular.md)。  
  
 本主题的内容：  
  
-   [优势](#bkmk_benefits)  
  
-   [Permissions](#bkmk_permissions)  
  
-   [处理分区](#bkmk_process_partitions)  
  
-   [并行处理](#bkmk_parallelProc)  
  
-   [相关任务](#bkmk_related_tasks)  
  
##  <a name="bkmk_benefits"></a> 优势  
 有效的模型设计利用分区来消除 Analysis Services 服务器上不必要的处理和后续处理器负载，而同时可确保以足够的频率处理和刷新数据，以反映数据源中最新的数据。  
  
 例如，表格模型可具有一个 Sales 表，该表包含当前 2011 会计年度和之前每一个会计年度的销售数据。 模型的 Sales 表具有以下三个分区：  
  
|分区|数据来源|  
|---------------|---------------|  
|Sales2011|当前会计年度|  
|Sales2010-2001|会计年度 2001、2002、2003、2004、2005、2006。 2007, 2008, 2009, 2010|  
|SalesOld|过去十年之前的所有会计年度。|  
  
 当为当前 2011 会计年度添加新的销售数据时；该数据必须每天进行处理，以便在当前会计年度销售数据分析中准确得以反映，这样，将每晚处理 Sales2011 分区。  
  
 无需每晚处理 Sales2010-2001 分区中的数据；但是，因为之前十个会计年度的销售数据仍偶尔会因为产品退货和其他调整而发生更改，所以还必须定期进行处理，这样，将每月处理 Sales2010-2001 分区中的数据。 SalesOld 分区中的数据从不会发生变化，因此只是每年处理一次。  
  
 当进入 2012 会计年度时，新的 Sales2012 分区添加到模型的 Sales 表。 然后，Sales2011 分区可以与 Sales2010-2001 分区合并，并重命名为 Sales2011-2002。 从新的 Sales2011-2002 分区中删除 2001 会计年度中的数据，并移入到 SalesOld 分区。 然后，处理所有分区以反映数据更改。  
  
 如何实现组织的表格模型的分区策略在很大程度上取决于特定模型数据处理需求和可用的资源。  
  
##  <a name="bkmk_permissions"></a> Permissions  
 为了在 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]中创建、管理和处理分区，您必须具有在安全角色中定义的适当的 Analysis Services 权限。 每个安全角色都具有以下权限之一：  
  
|权限|操作|  
|----------------|-------------|  
|管理员|读取、处理、创建、复制、合并、删除|  
|处理|读取、处理|  
|只读|读取|  
  
 若要了解有关使用模型创作期间创建角色的详细信息[!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]，请参阅[角色](../../analysis-services/tabular-models/roles-ssas-tabular.md)。 若要深入了解管理角色成员，通过使用部署表格模型角色[!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]，请参阅[表格模型角色](../../analysis-services/tabular-models/tabular-model-roles-ssas-tabular.md)。  
  
##  <a name="bkmk_parallelProc"></a> 并行处理  
Analysis Services 包括对于包含两个或多个分区的表的并行处理，从而提升处理性能。 对于并行处理，没有相应的配置设置（请参阅注释）。 当你处理表或为相同的表和进程选择多个分区时，并行处理会默认发生。 仍可以选择单独处理表的分区。  
  
> [!NOTE]  
>  若要指定刷新操作是按顺序运行还是并行运行，可将 **maxParallism** 属性选项用于 [排序命令 (TMSL)](../../analysis-services/tabular-models-scripting-language-commands/sequence-command-tmsl.md)。

> [!NOTE]  
>  如果检测到重新编码，则并行处理可能会导致系统资源的使用量增加。 这是因为需要中断多个分区操作，并使用并行的新编码重启这些操作。  
  
##  <a name="bkmk_process_partitions"></a> 处理分区  
 可以通过使用 **中的** “分区” [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] 对话框或使用脚本独立于其他分区处理（刷新）分区。 处理具有以下选项：  
  
|模式|Description|  
|----------|-----------------|  
|处理默认值|检测分区对象的处理状态，执行必要的处理，将未处理的分区对象或部分处理的分区对象交付为已完全处理的分区对象。 为空表和分区加载数据；生成或重新生成层次结构、计算列和关系。|  
|处理全部|处理分区对象及其包含的所有对象。 对已处理的对象运行“处理全部”时， [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 将删除该对象中的所有数据，然后再处理该对象。 在对对象进行结构更改后，需要这种类型的处理。|  
|处理数据|将数据加载到分区或表中，而无需重新生成层次结构或关系或重新计算计算列和度量值。|  
|处理清除|删除分区中的所有数据。|  
|处理添加|以增量方式用新数据更新分区。|  
  
##  <a name="bkmk_related_tasks"></a> 相关任务  
  
|任务|Description|  
|----------|-----------------|  
|[创建和管理表格模型分区](../../analysis-services/tabular-models/create-and-manage-tabular-model-partitions-ssas-tabular.md)|描述如何使用 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]在已部署的表格模型中创建和管理分区。|  
|[处理表格模型分区](../../analysis-services/tabular-models/process-tabular-model-partitions-ssas-tabular.md)|描述如何使用 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]在已部署的表格模型中处理分区。|  
  
  
