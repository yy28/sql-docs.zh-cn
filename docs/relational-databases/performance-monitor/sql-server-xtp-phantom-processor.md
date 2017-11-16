---
title: "SQL Server XTP 虚拟处理器 | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: performance-monitor
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 0f691b3d-a8fd-4459-ad21-2cfc8574a8c0
caps.latest.revision: 7
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 722137db4fdddd79f8ed4bfe8d5a7c3ed4531738
ms.contentlocale: zh-cn
ms.lasthandoff: 06/22/2017

---
# <a name="sql-server-xtp-phantom-processor"></a>SQL Server XTP 虚拟处理器
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

  SQL Server XTP 虚拟处理器性能对象包含与内存中 OLTP 引擎的虚拟处理子系统相关的计数器。 此组件用于检测在 SERIALIZABLE 隔离级别运行的事务中的虚拟行和并发方案中的约束验证。  
  
 下表介绍了 **SQL Server XTP 虚拟处理器** 计数器。  
  
|计数器|说明|  
|-------------|-----------------|  
|**灰尘角扫描重试次数/秒（虚拟发出）**|在虚拟处理器发出的灰尘角扫描期间，由于写冲突而进行的每秒扫描重试次数（平均值）。 此为非常低级的计数器，不适合客户使用。|  
|**删除的虚拟过期行数/秒**|虚拟扫描每秒删除的过期行数（平均值）。|  
|**接触的虚拟过期行数/秒**|虚拟扫描每秒接触的过期行数（平均值）。|  
|**接触的即将到期的虚拟行数/秒**|虚拟扫描每秒接触的即将到期的行数（平均值）。|  
|**接触的虚拟行数/秒**|虚拟扫描每秒接触的行数（平均值）。|  
|**启动的虚拟扫描数/秒**|每秒启动的虚拟扫描数（平均值）。|  
  
## <a name="see-also"></a>另请参阅  
 [SQL Server XTP（内存中 OLTP）性能计数器](../../relational-databases/performance-monitor/sql-server-xtp-in-memory-oltp-performance-counters.md)  
  
  

