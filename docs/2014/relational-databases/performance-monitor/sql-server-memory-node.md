---
title: SQL Server，内存节点 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- dbe-cross-instance
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 55b28ba9-b6d5-4ea9-8103-db8a72f42982
caps.latest.revision: 9
author: craigg-msft
ms.author: craigg
manager: jhubbard
ms.openlocfilehash: 098eed4d0fd1e8f5dcf0c4fb04f021bb7157e5ae
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/19/2018
ms.locfileid: "36127504"
---
# <a name="sql-server-memory-node"></a>SQL Server、内存节点
  Microsoft **中的** “内存节点” [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 对象在 NUMA 节点上提供监视服务器内存使用情况的计数器。  
  
## <a name="memory-node-counters"></a>内存节点计数  
 下表描述 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] **内存节点** 计数器。  
  
|SQL Server Memory Manager 计数器|Description|  
|----------------------------------------|-----------------|  
|**Database Node Memory (KB)**|指定服务器当前在此节点上用于数据库页面的内存量。|  
|**Free Node Memory (KB)**|指定服务器在此节点上未使用的内存量。|  
|**Foreign Node Memory (KB)**|指定此节点上非 NUMA 本地内存的量。|  
|**Stolen Memory Node (KB)**|指定服务器在此节点上出于数据库页面以外的目的使用的内存量。|  
|**Target Node Memory**|指定此节点的理想内存量。|  
|**Total Node Memory**|指示服务器在此节点上已提交的总内存量。|  
  
## <a name="see-also"></a>请参阅  
 [监视资源使用情况（系统监视器）](monitor-resource-usage-system-monitor.md)   
 [SQL Server Buffer Manager 对象](sql-server-buffer-manager-object.md)   
 [sys.dm_os_performance_counters (Transact-SQL)](/sql/relational-databases/system-dynamic-management-views/sys-dm-os-performance-counters-transact-sql)  
  
  
