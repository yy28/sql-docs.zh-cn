---
title: SQL Server XTP 虚拟处理器 | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: performance
ms.topic: conceptual
ms.assetid: 0f691b3d-a8fd-4459-ad21-2cfc8574a8c0
author: julieMSFT
ms.author: jrasnick
ms.openlocfilehash: f9f7f51b2d0ede3bb49bb152ab08cbb2a7eb2732
ms.sourcegitcommit: 58158eda0aa0d7f87f9d958ae349a14c0ba8a209
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/30/2020
ms.locfileid: "68114034"
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
  
  
