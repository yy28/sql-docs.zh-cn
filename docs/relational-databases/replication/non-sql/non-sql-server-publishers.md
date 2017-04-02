---
title: "非 SQL Server 发布服务器 | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "replication"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "异类数据库复制, 非 SQL Server 发布服务器"
  - "非 SQL Server 发布服务器"
  - "异类数据源, 非 SQL Server 发布服务器"
  - "发布服务器 [SQL Server 复制], Oracle"
ms.assetid: 08a160a6-33be-46b5-bc7b-d53180d8bdf1
caps.latest.revision: 31
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 31
---
# 非 SQL Server 发布服务器
  将数据从非发布[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 源允许您将合并中的数据 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]。 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 可以订阅从 Oracle 数据库发布的快照或事务数据。 有关从 Oracle 发布的详细信息，请参阅 [Oracle 发布概述](../../../relational-databases/replication/non-sql/oracle-publishing-overview.md)。  
  
 不推荐异类复制到非 SQL Server 订阅服务器。 不推荐使用 Oracle 发布。 若要移动数据，请创建使用变更数据捕获和 [!INCLUDE[ssIS](../../../includes/ssis-md.md)]的解决方案。  
  
> [!CAUTION]  
>  [!INCLUDE[ssNoteDepFutureAvoid](../../../includes/ssnotedepfutureavoid-md.md)]  
  
 从非 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 数据库发布适用于下列方案：  
  
|应用场景|说明|  
|--------------|-----------------|  
|[!INCLUDE[msCoName](../../../includes/msconame-md.md)] .NET Framework 应用程序部署|使用 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] Visual Studio 和 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 开发，用于处理从非 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 数据库复制的数据。|  
|数据仓库临时服务器|保留 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 临时数据库与非同步[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 数据库。|  
|迁移到 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]|针对 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 执行实时应用程序测试，同时复制源系统的更改。 对迁移满意后，切换到 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 。|  
  
## 另请参阅  
 [异类数据库复制](../../../relational-databases/replication/non-sql/heterogeneous-database-replication.md)  
  
  