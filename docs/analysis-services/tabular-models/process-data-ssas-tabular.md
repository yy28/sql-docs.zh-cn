---
title: "处理数据 (SSAS 表格) |Microsoft 文档"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
- analysis-services/multidimensional-tabular
- analysis-services/data-mining
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: d88f2dc9-2933-4be5-9bf3-48ffbc2d0a1a
caps.latest.revision: 14
author: Minewiskan
ms.author: owend
manager: erikre
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 6fc5d0e934ae7fe4d7f9a00594c2f1ffd21bda1c
ms.contentlocale: zh-cn
ms.lasthandoff: 09/01/2017

---
# <a name="process-data-ssas-tabular"></a>处理数据（SSAS 表格）
  在您在缓存模式下将数据导入表格模型时，您在捕获导入时这些数据的快照。 在某些情况下，这些数据可能永远不会更改并且无需在模型中更新。 但可能性更大的情况是，您所导入的数据定期更改，并且为使您的模型反映数据源中的最新数据，需要处理（刷新）数据并且重新计算已计算的数据。 为了更新模型中的数据，您对所有表、单独表、按分区或者按数据源连接执行处理操作。  
  
 在创作您的模型项目时，必须在 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]中手动启动处理操作。 在部署了某一模型之后，可以通过使用 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 执行处理操作，或者使用脚本计划处理操作。 本文所述的任务全都属于在 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]中进行模型创作期间您可以执行的处理操作。 有关已部署模型的处理操作的详细信息，请参阅[处理数据库、表或分区 (Analysis Services)](../../analysis-services/tabular-models/process-database-table-or-partition-analysis-services.md)。  
  
## <a name="related-tasks"></a>相关任务  
  
|主题|Description|  
|-----------|-----------------|  
|[手动处理数据（SSAS 表格）](../../analysis-services/tabular-models/manually-process-data-ssas-tabular.md)|介绍如何手动处理模型工作区数据。|  
|[数据处理故障排除（SSAS 表格）](../../analysis-services/troubleshoot-process-data-ssas-tabular.md)|介绍如何解决处理操作中发生的问题。|  
  
  
