---
title: SQL Server，内存节点 | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology:
- database-engine
ms.topic: conceptual
ms.assetid: 55b28ba9-b6d5-4ea9-8103-db8a72f42982
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 55c80d333680e40645eab1f643f8a9140781f380
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/01/2018
ms.locfileid: "47677531"
---
# <a name="sql-server-memory-node"></a>SQL Server、内存节点
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  Microsoft **中的** “内存节点” [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 对象在 NUMA 节点上提供监视服务器内存使用情况的计数器。  
  
## <a name="memory-node-counters"></a>内存节点计数  
 下表描述 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] **内存节点** 计数器。  
  
|SQL Server Memory Manager 计数器|描述|  
|----------------------------------------|-----------------|  
|**Database Node Memory (KB)**|指定服务器当前在此节点上用于数据库页面的内存量。|  
|**Free Node Memory (KB)**|指定服务器在此节点上未使用的内存量。|  
|**Foreign Node Memory (KB)**|指定此节点上非 NUMA 本地内存的量。|  
|**Stolen Memory Node (KB)**|指定服务器在此节点上出于数据库页面以外的目的使用的内存量。|  
|**Target Node Memory**|指定此节点的理想内存量。|  
|**Total Node Memory**|指示服务器在此节点上已提交的总内存量。|  
  
## <a name="see-also"></a>另请参阅  
 [监视资源使用情况（系统监视器）](../../relational-databases/performance-monitor/monitor-resource-usage-system-monitor.md)   
 [SQL Server Buffer Manager 对象](../../relational-databases/performance-monitor/sql-server-buffer-manager-object.md)   
 [sys.dm_os_performance_counters (Transact-SQL)](../../relational-databases/system-dynamic-management-views/sys-dm-os-performance-counters-transact-sql.md)  
  
  
