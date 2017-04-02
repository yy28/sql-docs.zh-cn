---
title: "异类数据库复制 | Microsoft Docs"
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
  - "异类数据库复制, 关于异类数据库复制"
  - "复制 [SQL Server], 异类数据库复制"
  - "异类数据库复制"
ms.assetid: 3fd983ad-e206-45db-9054-417c9b5bb815
caps.latest.revision: 41
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 41
---
# 异类数据库复制
  [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 支持下列异类事务复制和快照复制方案：  
  
-   将数据从 Oracle 发布到 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]。  
  
-   将数据从 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 发布到非 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 订阅服务器。  
  
 不推荐异类复制到非 SQL Server 订阅服务器。 不推荐使用 Oracle 发布。 若要移动数据，请创建使用变更数据捕获和 [!INCLUDE[ssIS](../../../includes/ssis-md.md)]的解决方案。  
  
> [!CAUTION]  
>  [!INCLUDE[ssNoteDepFutureAvoid](../../../includes/ssnotedepfutureavoid-md.md)]  
  
## 从 Oracle 发布数据  
 您可以使用 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 从 Oracle 发布数据，其大多数功能和简单易用性与 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 快照复制和事务复制相同。 从 Oracle 发布数据非常适合于下列情形：  
  
|应用场景|说明|  
|--------------|-----------------|  
|[!INCLUDE[msCoName](../../../includes/msconame-md.md)] .NET Framework 应用程序部署|使用 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] Visual Studio 和 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 开发，用于处理从非 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 数据库复制的数据。|  
|数据仓库临时服务器|保留 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 临时数据库与非同步[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 数据库。|  
|迁移到 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]|针对 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 执行实时应用程序测试，同时复制源系统的更改。 对迁移满意后，切换到 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 。|  
  
 有关详细信息，请参阅 [Oracle 发布概述](../../../relational-databases/replication/non-sql/oracle-publishing-overview.md)。  
  
## 将数据发布到非 SQL Server 订阅服务器  
 支持将下列非 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 数据库作为快照和事务发布的订阅服务器：  
  
-   用于 Oracle 所支持的所有平台的 Oracle。  
  
-   用于 AS400、MVS、Unix、Linux 和 Windows 的 IBM DB2。  
  
 有关详细信息，请参阅 [非 SQL Server 订阅服务器](../../../relational-databases/replication/non-sql/non-sql-server-subscribers.md)。  
  
  