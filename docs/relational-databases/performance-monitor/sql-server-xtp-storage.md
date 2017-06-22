---
title: "SQL Server XTP 存储 | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 4070580b-880d-4f4c-abcc-626a4fe0c9a2
caps.latest.revision: 6
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: ca13381f6cc2d2b9af6286f28d25791522118a72
ms.contentlocale: zh-cn
ms.lasthandoff: 06/22/2017

---
# <a name="sql-server-xtp-storage"></a>SQL Server XTP 存储
[!INCLUDE[tsql-appliesto-ss2016-xxxx-xxxx-xxx_md](../../includes/tsql-appliesto-ss2016-xxxx-xxxx-xxx-md.md)]

  SQL Server XTP 存储性能对象包含与 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]中的内存中 OLTP 的磁盘存储相关的计数器。  
  
 下表介绍了 **SQL Server XTP 存储** 计数器。  
  
|计数器|说明|  
|-------------|-----------------|  
|**Checkpoints Closed**|联机代理执行的已关闭检查点的计数。|  
|**Checkpoints Completed**|脱机检查点线程处理的检查点计数。|  
|**Core Merges Completed**|合并工作线程完成的核心合并数。 仍需要安装这些合并。|  
|**Merge Policy Evaluations**|自服务器启动以来的合并策略评估数。|  
|**Merge Requests Outstanding**|自服务器启动以来未完成的合并请求数。|  
|**Merges Abandoned**|因失败而放弃的合并数。|  
|**Merges Installed**|成功安装的合并数。|  
|**Total Files Merged**|已合并的源文件总数。 此计数可用于查找合并中源文件的平均数目。|  
  
## <a name="see-also"></a>另请参阅  
 [SQL Server XTP（内存中 OLTP）性能计数器](../../relational-databases/performance-monitor/sql-server-xtp-in-memory-oltp-performance-counters.md)  
  
  
