---
title: 处理数据 (SSAS 表格) |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: d88f2dc9-2933-4be5-9bf3-48ffbc2d0a1a
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 0a0ca45681866e0ba96edaa81c21445a89f94275
ms.sourcegitcommit: f40fa47619512a9a9c3e3258fda3242c76c008e6
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/23/2019
ms.locfileid: "66070701"
---
# <a name="process-data-ssas-tabular"></a>处理数据（SSAS 表格）
  在您在缓存模式下将数据导入表格模型时，您在捕获导入时这些数据的快照。 在某些情况下，这些数据可能永远不会更改并且无需在模型中更新。 但可能性更大的情况是，您所导入的数据定期更改，并且为使您的模型反映数据源中的最新数据，需要处理（刷新）数据并且重新计算已计算的数据。 为了更新模型中的数据，您对所有表、单独表、按分区或者按数据源连接执行处理操作。  
  
 在创作您的模型项目时，必须在 [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]中手动启动处理操作。 在部署了某一模型之后，可以通过使用 [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] 执行处理操作，或者使用脚本计划处理操作。 本文所述的任务全都属于在 [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]中进行模型创作期间您可以执行的处理操作。 处理操作的已部署的模型的详细信息，请参阅[处理数据库、 表或分区](tabular-models/process-database-table-or-partition-analysis-services.md)。  
  
## <a name="related-tasks"></a>Related Tasks  
  
|主题|Description|  
|-----------|-----------------|  
|[手动处理数据（SSAS 表格）](manually-process-data-ssas-tabular.md)|介绍如何手动处理模型工作区数据。|  
|[数据处理故障排除（SSAS 表格）](troubleshoot-process-data-ssas-tabular.md)|介绍如何解决处理操作中发生的问题。|  
  
  
