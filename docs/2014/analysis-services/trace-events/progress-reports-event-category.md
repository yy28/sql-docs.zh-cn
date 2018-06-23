---
title: 进度报告事件类别 |Microsoft 文档
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- progress events [Analysis Services]
- Progress Reports event category
- event classes [Analysis Services], progress reports
ms.assetid: c130f160-28ef-49bc-9ee6-da47dc9aab2a
caps.latest.revision: 22
author: Minewiskan
ms.author: owend
manager: mblythe
ms.openlocfilehash: 8bcfa530f87d7a8caaee6814c2e2e2282e2783ed
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/19/2018
ms.locfileid: "36014627"
---
# <a name="progress-reports-event-category"></a>“进度报告”事件类别
  “进度报告事件”类别包含下表中说明的事件类。  
  
|Event Class|事件 ID|Description|  
|-----------------|--------------|-----------------|  
|进度报告开始|5|收集启动跟踪后的所有进度报告开始事件。|  
|进度报告结束|6|收集启动跟踪后的所有进度报告结束事件。|  
|进度报告当前状态|7|收集启动跟踪后的所有进度报告当前状态事件。 例如，在处理期间，当前报表包含有关被处理的对象（维度、分区、多维数据集等）的处理信息。|  
|进度报告错误|8|收集启动跟踪后的所有进度报告错误事件。|  
  
 每个进度报告开始事件都以一个处理事件流开始，并以进度报告结束事件终止。 该事件流可以包含任意数量的进度报告当前状态事件和进度报告错误事件。  
  
 有关与每个进度报告事件类关联的列的信息，请参阅 [Progress Reports Data Columns](progress-reports-data-columns.md)。  
  
## <a name="see-also"></a>请参阅  
 [Analysis Services 跟踪事件](analysis-services-trace-events.md)  
  
  