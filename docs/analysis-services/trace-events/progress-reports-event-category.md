---
title: "进度报告事件类别 |Microsoft 文档"
ms.custom: 
ms.date: 03/01/2017
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: 
ms.component: 
ms.reviewer: 
ms.suite: pro-bi
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: reference
helpviewer_keywords:
- progress events [Analysis Services]
- Progress Reports event category
- event classes [Analysis Services], progress reports
ms.assetid: c130f160-28ef-49bc-9ee6-da47dc9aab2a
caps.latest.revision: "23"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: c90cfbe7e30d0678d13a329737c21f7d45575e22
ms.sourcegitcommit: f486d12078a45c87b0fcf52270b904ca7b0c7fc8
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/08/2018
---
# <a name="progress-reports-event-category"></a>“进度报告”事件类别
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]进度报告事件类别具有下表中说明的事件类。  
  
|Event Class|事件 ID|Description|  
|-----------------|--------------|-----------------|  
|进度报告开始|5|收集启动跟踪后的所有进度报告开始事件。|  
|进度报告结束|6|收集启动跟踪后的所有进度报告结束事件。|  
|进度报告当前状态|7|收集启动跟踪后的所有进度报告当前状态事件。 例如，在处理期间，当前报表包含有关被处理的对象（维度、分区、多维数据集等）的处理信息。|  
|进度报告错误|8|收集启动跟踪后的所有进度报告错误事件。|  
  
 每个进度报告开始事件都以一个处理事件流开始，并以进度报告结束事件终止。 该事件流可以包含任意数量的进度报告当前状态事件和进度报告错误事件。  
  
 有关与每个进度报告事件类关联的列的信息，请参阅 [Progress Reports Data Columns](../../analysis-services/trace-events/progress-reports-data-columns.md)。  
  
## <a name="see-also"></a>另请参阅  
 [Analysis Services 跟踪事件](../../analysis-services/trace-events/analysis-services-trace-events.md)  
  
  
