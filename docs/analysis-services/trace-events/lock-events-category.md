---
title: 锁定事件类别 |Microsoft 文档
ms.custom: ''
ms.date: 03/01/2017
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.component: ''
ms.reviewer: ''
ms.suite: pro-bi
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: reference
ms.assetid: 06427f8e-89bb-4710-a0c1-dc5e42b7e95e
caps.latest.revision: 6
author: Minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: fe7c4c743e8a111f4a489ee47c8a1fd8ef865663
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
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
  
  
