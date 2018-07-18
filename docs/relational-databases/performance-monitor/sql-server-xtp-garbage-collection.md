---
title: SQL Server XTP 垃圾收集 | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.component: performance-monitor
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: 64ae91e5-b420-44b4-af1a-f8bca83d7f41
caps.latest.revision: 8
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: b234fb7a34449bf7ba4af0a77b4a72c5f44a0310
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
ms.locfileid: "32951152"
---
# <a name="sql-server-xtp-garbage-collection"></a>SQL Server XTP 垃圾收集
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

  SQL Server XTP 垃圾回收性能对象包含与内存中 OLTP 引擎的垃圾回收器相关的计数器。  
  
 下表介绍了 **SQL Server XTP 垃圾回收** 计数器。  
  
|计数器|Description|  
|-------------|-----------------|  
|**灰尘角扫描重试次数/秒（垃圾收集器发出）**|在垃圾收集器发出的灰尘角扫描期间，由于写冲突而进行的每秒扫描重试次数（平均值）。 此为非常低级的计数器，不适合客户使用。|  
|**主垃圾收集器工作项数/秒**|主垃圾收集器线程处理的工作项数。|  
|**并行垃圾收集器工作项数/秒**|并行线程执行垃圾收集器工作项的次数。|  
|**处理的行数/秒**|垃圾收集器每秒处理的行数（平均值）。|  
|**处理的行数/秒（桶中的第一行并能删除）**|垃圾收集器每秒处理的、在相应哈希桶中是第一行并能立即删除的行数（平均值）。|  
|**处理的行数/秒（桶中的第一行）**|垃圾收集器每秒处理的、在相应哈希桶中是第一行的行数（平均值）。|  
|**处理的行数/秒（标记为取消链接）**|垃圾收集器每秒处理的、已标记为取消链接的行数（平均值）。|  
|**处理的行数/秒（无需扫描）**|垃圾收集器每秒处理的、无需灰尘角扫描的行数（平均值）。|  
|**扫描中删除的过期行数/秒**|灰尘角扫描期间每秒删除的过期行数（平均值）。|  
|**扫描中接触的过期行数/秒**|灰尘角扫描期间每秒接触的过期行数（平均值）。|  
|**扫描中接触的即将到期的行数/秒**|灰尘角扫描期间每秒接触的即将到期的行数（平均值）。|  
|**扫描中接触的行数/秒**|灰尘角扫描期间每秒接触的行数（平均值）。|  
|**启动的扫描数/秒**|每秒启动的灰尘角扫描数（平均值）。|  
  
## <a name="see-also"></a>另请参阅  
 [SQL Server XTP（内存中 OLTP）性能计数器](../../relational-databases/performance-monitor/sql-server-xtp-in-memory-oltp-performance-counters.md)  
  
  
