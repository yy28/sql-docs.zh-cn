---
title: 进度报告事件类别 |Microsoft 文档
ms.date: 05/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.component: tabular-models
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 6ffc1030149040ed56855cd837c1e4664e64e4c9
ms.sourcegitcommit: 1aedef909f91dc88dc741748f36eabce3a04b2b1
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/08/2018
---
# <a name="progress-reports-event-category"></a>“进度报告”事件类别
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
  “进度报告事件”类别包含下表中说明的事件类。  
  
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
  
  
