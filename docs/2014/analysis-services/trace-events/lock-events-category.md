---
title: 锁定事件类别 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
ms.topic: conceptual
ms.assetid: 06427f8e-89bb-4710-a0c1-dc5e42b7e95e
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 2153de0275255f55928f10c0d6d21c0350064a1d
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/02/2018
ms.locfileid: "48056357"
---
# <a name="lock-events-category"></a>“锁定事件”类别
  “锁定事件”事件类别具有下表中说明的各事件类。  
  
|Event Class|事件 ID|Description|  
|-----------------|--------------|-----------------|  
|死锁|50|收集跟踪开始后的所有元数据锁死锁事件。|  
|锁超时|51|收集跟踪开始后的所有元数据锁超时事件。|  
|已获取锁|52|收集自开始跟踪后与已获取的锁有关的信息。|  
|已释放锁|53|收集自开始跟踪后与已释放的锁有关的信息。|  
|正在等待的锁|54|收集自开始跟踪后与处于等待状态的锁有关的信息。|  
  
 有关与每个锁事件类关联的列的信息，请参阅 [Lock Events Data Columns](lock-events-data-columns.md)。  
  
## <a name="see-also"></a>请参阅  
 [Analysis Services 跟踪事件](analysis-services-trace-events.md)  
  
  
