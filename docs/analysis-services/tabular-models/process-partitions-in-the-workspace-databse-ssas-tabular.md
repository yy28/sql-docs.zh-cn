---
title: "在工作区数据库 (SSAS 表格) 中处理分区 |Microsoft 文档"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-non-specified
ms.prod_service: analysis-services
ms.service: 
ms.component: tabular-models
ms.reviewer: 
ms.suite: sql
ms.technology:
- analysis-services
- analysis-services/multidimensional-tabular
- analysis-services/data-mining
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 3a369705-43fa-4961-9045-32e06fbdde33
caps.latest.revision: "12"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 2ca775614b38765ce52616ac69d98631885715df
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/17/2017
---
# <a name="process-partitions-in-the-workspace-databse-ssas-tabular"></a>在工作区数据库中处理分区（SSAS 表格）
  分区将表分成多个逻辑部分。 然后，每个分区可独立于其他分区进行处理（刷新）。 本主题中的任务说明如何使用 **中的** “处理分区” [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]对话框在模型工作区数据库中处理分区。  
  
 在将模型部署到其他 Analysis Services 实例后，数据库管理员可以使用 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]、脚本或 IS 包在（已部署）模型中创建和管理分区。 有关详细信息，请参阅[创建和管理表格模型分区（SSAS 表格）](../../analysis-services/tabular-models/create-and-manage-tabular-model-partitions-ssas-tabular.md)。  
  
###  <a name="bkmk_create_new"></a> 处理分区  
  
1.  在 [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)] 中，依次单击“模型”菜单、“处理”（“刷新”）和“处理分区”。  
  
2.  在 **“模式”** 列表框中，选择以下处理模式之一：  
  
    |“模式”|Description|  
    |----------|-----------------|  
    |**处理默认值**|检测分区对象的处理状态，执行必要的处理，将未处理的分区对象或部分处理的分区对象交付为已完全处理的分区对象。 为空表和分区加载数据；生成或重新生成层次结构、计算列和关系。|  
    |**处理全部**|处理分区对象及其包含的所有对象。 对已处理的对象运行“处理全部”时， [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 将删除该对象中的所有数据，然后再处理该对象。 在对对象进行结构更改后，需要这种类型的处理。|  
    |**处理数据**|将数据加载到分区或表中，而无需重新生成层次结构或关系或重新计算计算列和度量值。|  
    |**处理清除**|删除分区中的所有数据。|  
    |**处理添加**|以增量方式用新数据更新分区。|  
  
3.  在 **“处理”** 复选框列中，选择要用所选模式处理的分区，然后单击 **“确定”**。  
  
## <a name="see-also"></a>另请参阅  
 [分区（SSAS 表格）](../../analysis-services/tabular-models/partitions-ssas-tabular.md)   
 [创建和管理工作区数据库中的分区（SSAS 表格）](../../analysis-services/tabular-models/create-and-manage-partitions-in-the-workspace-database-ssas-tabular.md)  
  
  
