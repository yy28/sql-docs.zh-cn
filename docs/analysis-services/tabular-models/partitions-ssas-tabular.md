---
title: "分区（SSAS 表格） | Microsoft Docs"
ms.custom: ""
ms.date: "03/01/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "analysis-services"
  - "analysis-services/multidimensional-tabular"
  - "analysis-services/data-mining"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 708b9bdf-8c0b-4476-809a-8f616be23a58
caps.latest.revision: 20
author: "Minewiskan"
ms.author: "owend"
manager: "erikre"
caps.handback.revision: 20
---
# 分区（SSAS 表格）
  分区将表分成多个逻辑部分。 然后，每个分区可独立于其他分区进行处理（刷新）。 在模型创建期间使用 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] 中的“分区”对话框创建的分区应用于模型工作区数据库。 部署模型时，在已部署的模型数据库中将复制为模型工作区数据库定义的分区。 您可以使用 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]中的“分区”对话框进一步为已部署的模型数据库创建和管理分区。  本主题中提供的信息描述在模型创建期间使用 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]中的“分区管理器”创建的分区。 有关为已部署的模型创建和管理分区的信息，请参阅[创建和管理表格模型分区（SSAS 表格）](../../analysis-services/tabular-models/create-and-manage-tabular-model-partitions-ssas-tabular.md)。  
  
 本主题的内容：  
  
-   [优势](#bkmk_benefits)  
  
-   [相关任务](#bkmk_related_tasks)  
  
##  <a name="bkmk_benefits"></a> 优势  
 表格模型中的分区将一个表划分为各个逻辑分区对象。 然后，每个分区可独立于其他分区进行处理。 例如，表可能包含某些行集，这些行集的数据很少更改；但是也包含另一些行集，这些行集的数据则经常更改。 在这些情况中，如果您只想处理某一部分数据，没有必要处理所有数据。 通过分区，您可以将需要经常处理的那部分数据与很少处理的那部分数据分开。  
  
 有效的模型设计利用分区来消除 Analysis Services 服务器上不必要的处理和后续处理器负载，而同时可确保以足够的频率处理和刷新数据，以反映数据源中最新的数据。 在模型创建期间如何实现和利用分区可能与如何为已部署的模型实现和利用分区有很大不同。 请记住在模型创建阶段，您可能只使用将最终包含在已部署的模型中的数据的一个子集。  
  
### 处理分区  
 对于已部署的模型，通过使用 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]或运行包含处理命令以及指定处理选项和设置的脚本来执行处理。 在使用 [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)]创建模型时，可以从“模型”菜单或工具栏使用“处理”命令运行处理操作。 可以为分区、表或所有对象指定处理操作。  
  
 运行处理操作时，使用数据连接建立到数据源的连接。 新数据将导入到模型表，并重新构建每个表的关系和层次结构，同时对计算列和度量值中的计算结果重新进行计算。  
  
 通过进一步将表划分为逻辑分区，您可以有选择地确定处理每个分区的哪些数据、何时处理以及如何处理。 部署模型时，可以使用 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]中的“分区”对话框和使用执行处理命令的脚本手动完成分区的处理。  
  
### 模型工作区数据库中的分区  
 您可以使用 [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)]中的分区管理器来创建新分区以及编辑、合并或删除分区。 分区管理器提供两种为分区选择表、行和列的模式：“表预览”模式和 SQL 查询模式。 所有分区都是使用 SQL 查询定义的，但是，通过使用“表预览”模式，您可以预览并选择要在分区中包含的数据。 为您自动创建并验证 SQL 查询。 因为“表预览”模式与“编辑表属性”对话框中和表导入向导的“表预览”页中的表预览模式相同，因此预览中的最大行数为 50。  
  
### 已部署的模型数据库中的分区  
 部署模型时，已部署的模型数据库的分区将显示为 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]中的数据库对象。 您可以使用 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]中的“分区”对话框为已部署的模型创建、编辑、合并和删除分区。 在 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 中管理已部署的模型的分区不在本主题讨论范围内。 若要了解管理 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 中的分区的相关信息，请参阅[创建和管理表格模型分区（SSAS 表格）](../../analysis-services/tabular-models/create-and-manage-tabular-model-partitions-ssas-tabular.md)。  
  
##  <a name="bkmk_related_tasks"></a> 相关任务  
  
|主题|Description|  
|-----------|-----------------|  
|[创建和管理工作区数据库中的分区（SSAS 表格）](../../analysis-services/tabular-models/create-and-manage-partitions-in-the-workspace-database-ssas-tabular.md)|说明如何使用 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]的分区管理器在模型工作区数据库中创建和管理分区。|  
|[在工作区数据库中处理分区（SSAS 表格）](../../analysis-services/tabular-models/process-partitions-in-the-workspace-databse-ssas-tabular.md)|说明如何在模型工作区数据库中处理（刷新）分区。|  
  
## 另请参阅  
 [DirectQuery 模式（SSAS 表格）](../../analysis-services/tabular-models/directquery-mode-ssas-tabular.md)   
 [处理数据（SSAS 表格）](../../analysis-services/tabular-models/process-data-ssas-tabular.md)  
  
  