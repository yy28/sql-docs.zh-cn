---
title: 锁定事件类别 |Microsoft 文档
ms.date: 05/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.component: trace-events
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 7885e7dd6090a1877ca40337b6aae1abde886132
ms.sourcegitcommit: 38f8824abb6760a9dc6953f10a6c91f97fa48432
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/10/2018
---
# <a name="lock-events-category"></a>“锁定事件”类别
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
  “锁定事件”事件类别具有下表中说明的各事件类。  
  
|Event Class|事件 ID|Description|  
|-----------------|--------------|-----------------|  
|死锁|50|收集跟踪开始后的所有元数据锁死锁事件。|  
|锁超时|51|收集跟踪开始后的所有元数据锁超时事件。|  
|已获取锁|52|收集自开始跟踪后与已获取的锁有关的信息。|  
|已释放锁|53|收集自开始跟踪后与已释放的锁有关的信息。|  
|正在等待的锁|54|收集自开始跟踪后与处于等待状态的锁有关的信息。|  
  
 有关与每个锁事件类关联的列的信息，请参阅 [Lock Events Data Columns](../../analysis-services/trace-events/lock-events-data-columns.md)。  
  
## <a name="see-also"></a>另请参阅  
 [Analysis Services 跟踪事件](../../analysis-services/trace-events/analysis-services-trace-events.md)  
  
  
