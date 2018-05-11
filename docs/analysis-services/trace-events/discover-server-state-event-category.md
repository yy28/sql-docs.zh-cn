---
title: 发现服务器状态事件类别 |Microsoft 文档
ms.date: 05/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.component: trace-events
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 83bad9f141c0da4918f7558f0b34b7816e51d737
ms.sourcegitcommit: 38f8824abb6760a9dc6953f10a6c91f97fa48432
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/10/2018
---
# <a name="discover-server-state-event-category"></a>“发现服务器状态”事件类别
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
  “发现服务器状态”事件类别包含下表中说明的事件类。  
  
|Event Class|事件 ID|Description|  
|-----------------|--------------|-----------------|  
|服务器状态发现开始|33|收集启动跟踪后的所有服务器状态 XMLA 发现开始事件。|  
|服务器状态发现数据|34|收集启动跟踪后的所有服务器状态 XMLA 发现数据事件。 这些事件可以捕获对发现请求的响应内容。|  
|服务器状态发现结束|35|收集启动跟踪后的所有服务器状态 XMLA 发现结束事件。|  
  
 有关与每个“查询事件”事件类关联的列的信息，请参阅 [Discover Server State Events Data Columns](../../analysis-services/trace-events/discover-server-state-events-data-columns.md)。  
  
## <a name="see-also"></a>另请参阅  
 [Analysis Services 跟踪事件](../../analysis-services/trace-events/analysis-services-trace-events.md)  
  
  
