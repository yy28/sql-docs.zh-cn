---
title: 处理数据库、 表或分区 (Analysis Services) |Microsoft 文档
ms.date: 05/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.component: tabular-models
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 7ae87c71ed58cf557dbf6c1b8bf0627127ea72ff
ms.sourcegitcommit: 38f8824abb6760a9dc6953f10a6c91f97fa48432
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/10/2018
---
# <a name="process-database-table-or-partition-analysis-services"></a>处理数据库、表或分区 (Analysis Services)
[!INCLUDE[ssas-appliesto-sqlas-aas](../../includes/ssas-appliesto-sqlas-aas.md)]
  本主题中的任务说明如何通过使用手动处理表格模型数据库、 表或分区**过程\<对象 >** 中的对话框[!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]。  
  
 有关表格模型处理的详细信息，请参阅[处理数据](../../analysis-services/tabular-models/process-data-ssas-tabular.md)。  
  
##  <a name="bkmk_process_tasks"></a> “任务”  
  
###  <a name="bkmk_process_db"></a> 处理数据库  
  
1.  在 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 中，右键单击要处理的数据库，然后单击“处理数据库”。  
  
2.  在 **“处理数据库”** 对话框的 **“模式”** 列表框中，选择下列处理模式之一：  
  
    |“模式”|Description|  
    |----------|-----------------|  
    |**处理默认值**|检测数据库对象的处理状态，进行必要的处理，将未处理对象或部分处理的对象转变成为已完全处理的对象。 为空表和分区加载数据；生成或重新生成（重新计算）层次结构、计算列和关系。|  
    |**处理全部**|处理数据库及其包含的所有对象。 对已处理的对象运行“处理全部”时， [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 将删除该对象中的所有数据，然后再处理该对象。 在对对象进行结构更改后，需要这种类型的处理。 此选项需要的资源最多。|  
    |**处理清除**|从数据库对象中删除所有数据。|  
    |**处理重新计算**|更新并重新计算层次结构、关系和计算列。|  
  
3.  在 **“处理”** 复选框列中，选择要用所选模式处理的分区，然后单击 **“确定”**。  
  
###  <a name="bkmk_process_table"></a> 处理表  
  
1.  在 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 中，在包含要处理的表的表格模型数据库中，展开“表”节点，再右键单击要处理的表，然后单击“处理表”。  
  
2.  在 **“处理表”** 对话框的 **“模式”** 列表框中，选择下列处理模式之一：  
  
    |“模式”|Description|  
    |----------|-----------------|  
    |**处理默认值**|检测表对象的处理状态，进行必要的处理，将未处理对象或部分处理的对象转变成为已完全处理的对象。 为空表和分区加载数据；生成或重新生成（重新计算）层次结构、计算列和关系。|  
    |**处理全部**|处理表对象及其包含的所有对象。 对已处理的对象运行“处理全部”时， [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 将删除该对象中的所有数据，然后再处理该对象。 在对对象进行结构更改后，需要这种类型的处理。 此选项需要的资源最多。|  
    |**处理数据**|将数据加载到表中，而无需重新生成层次结构或关系或重新计算计算列和度量值。|  
    |**处理清除**|从表和所有表分区中删除所有数据。|  
    |**处理碎片整理**|对辅助表索引进行碎片整理。|  
  
3.  在表复选框列中，确认表并（可选）选择要处理的任何其他表，然后单击 **“确定”**。  
  
###  <a name="bkmk_process_partition"></a> 处理一个或多个分区  
  
1.  在 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 中，右键单击包含要处理的分区的表，然后单击“分区”。  
  
2.  在 **“分区”** 对话框的 **“分区”**中，单击“处理”按钮。  
  
3.  在 **“处理分区”** 对话框的 **“模式”** 列表框中，选择下列处理模式之一：  
  
    |“模式”|Description|  
    |----------|-----------------|  
    |**处理默认值**|检测分区对象的处理状态，执行必要的处理，将未处理的分区对象或部分处理的分区对象交付为已完全处理的分区对象。 为空表和分区加载数据；生成或重新生成（重新计算）层次结构、计算列和关系。|  
    |**处理全部**|处理分区对象及其包含的所有对象。 对已处理的对象运行“处理全部”时， [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 将删除该对象中的所有数据，然后再处理该对象。 在对对象进行结构更改后，需要这种类型的处理。|  
    |**处理数据**|将数据加载到分区或表中，而无需重新生成层次结构或关系或重新计算计算列和度量值。|  
    |**处理清除**|删除分区中的所有数据。|  
    |**处理添加**|以增量方式用新数据更新分区。|  
  
4.  在 **“处理”** 复选框列中，选择要用所选模式处理的分区，然后单击 **“确定”**。  
  
## <a name="see-also"></a>另请参阅  
 [表格模型分区](../../analysis-services/tabular-models/tabular-model-partitions-ssas-tabular.md)   
 [创建和管理表格模型分区](../../analysis-services/tabular-models/create-and-manage-tabular-model-partitions-ssas-tabular.md)  
  
  
