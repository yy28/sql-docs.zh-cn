---
title: 分区 |Microsoft 文档
ms.date: 05/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.component: tabular-models
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: dadc8572085ff93d2e6e1ec09a15874089a324f4
ms.sourcegitcommit: 38f8824abb6760a9dc6953f10a6c91f97fa48432
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/10/2018
---
# <a name="partitions"></a>分区
[!INCLUDE[ssas-appliesto-sqlas-aas](../../includes/ssas-appliesto-sqlas-aas.md)]
  分区将表分成多个逻辑部分。 然后，每个分区可独立于其他分区进行处理（刷新）。 通过使用 SSDT 中的分区对话框在模型创作期间创建的分区将应用于模型工作区数据库。 部署模型时，在已部署的模型数据库中将复制为模型工作区数据库定义的分区。 你可以进一步创建并管理通过使用 SSMS 中的分区对话框为已部署的模型数据库的分区。  本主题中提供的信息描述使用 SSDT 中的分区管理器对话框模型创作期间创建的分区。 有关创建和管理为部署的模型的分区的信息，请参阅[创建和管理表格模型分区](../../analysis-services/tabular-models/create-and-manage-tabular-model-partitions-ssas-tabular.md)。  
  
##  <a name="bkmk_benefits"></a> 优点  
 表格模型中的分区将一个表划分为各个逻辑分区对象。 然后，每个分区可独立于其他分区进行处理。 例如，表可能包含某些行集，这些行集的数据很少更改；但是也包含另一些行集，这些行集的数据则经常更改。 在这些情况中，如果您只想处理某一部分数据，没有必要处理所有数据。 通过分区，您可以将需要经常处理的那部分数据与很少处理的那部分数据分开。  
  
 有效的模型设计利用分区来消除 Analysis Services 服务器上不必要的处理和后续处理器负载，而同时可确保以足够的频率处理和刷新数据，以反映数据源中最新的数据。 在模型创建期间如何实现和利用分区可能与如何为已部署的模型实现和利用分区有很大不同。 请记住在模型创建阶段，您可能只使用将最终包含在已部署的模型中的数据的一个子集。  
  
### <a name="processing-partitions"></a>处理分区  
 对于已部署的模型，使用 SSMS，或通过运行包含处理命令并指定处理选项和设置的脚本，将进行处理。 在创作模型时使用 SSDT，你可以通过使用模型菜单或工具栏中的进程命令运行处理操作。 可以为分区、表或所有对象指定处理操作。  
  
 运行处理操作时，使用数据连接建立到数据源的连接。 新数据将导入到模型表，并重新构建每个表的关系和层次结构，同时对计算列和度量值中的计算结果重新进行计算。  
  
 通过进一步将表划分为逻辑分区，您可以有选择地确定处理每个分区的哪些数据、何时处理以及如何处理。 在部署模型时，可以使用 SSMS 中的分区对话框手动完成分区的处理或使用脚本的执行过程命令。  
  
### <a name="partitions-in-the-model-workspace-database"></a>模型工作区数据库中的分区  
 你可以创建新分区、 编辑、 合并，或删除分区在 SSDT 中使用分区管理器。 具体取决于你正创作的模型的兼容性级别，分区管理器所提供的用于选择表、 行和分区的列的两种模式： 表格 1400年模型中，为分区定义使用 M 查询，或者可以使用设计模式下打开查询编辑器。 对于表格 1100、 1103，1200年模型，使用表预览模式和 SQL 查询模式。 
  
### <a name="partitions-in-a-deployed-model-database"></a>已部署的模型数据库中的分区  
 在部署模型时，部署的模型数据库的分区将显示为在 SSMS 中的数据库对象。 可以创建、 编辑、 合并，并使用 SSMS 中的分区对话框删除已部署的模型的分区。 管理为部署的模型，在 SSMS 中的分区不在本主题的范围。 若要了解有关管理在 SSMS 中的分区，请参阅[创建和管理表格模型分区](../../analysis-services/tabular-models/create-and-manage-tabular-model-partitions-ssas-tabular.md)。  
  
##  <a name="bkmk_related_tasks"></a> Related tasks  
  
|主题|Description|  
|-----------|-----------------|  
|[创建和管理工作区数据库中的分区](../../analysis-services/tabular-models/create-and-manage-partitions-in-the-workspace-database-ssas-tabular.md)|描述如何创建和管理在 SSDT 中使用分区管理器的模型工作区数据库中的分区。|  
|[在工作区数据库中处理分区](../../analysis-services/tabular-models/process-partitions-in-the-workspace-databse-ssas-tabular.md)|说明如何在模型工作区数据库中处理（刷新）分区。|  
  
## <a name="see-also"></a>另请参阅  
 [DirectQuery 模式](../../analysis-services/tabular-models/directquery-mode-ssas-tabular.md)   
 [处理数据](../../analysis-services/tabular-models/process-data-ssas-tabular.md)  
  
  
