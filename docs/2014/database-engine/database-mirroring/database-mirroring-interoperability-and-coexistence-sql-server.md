---
title: 数据库镜像：互操作性和共存 (SQL Server) |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
helpviewer_keywords:
- high availability [SQL Server], interoperability and coexistence
- Database Engine [SQL Server], high availability
ms.assetid: 89fef397-e0cf-4e08-b598-25b8d4170523
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 2f38e7bac91c4d65e9c6209d693a598466096069
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62807286"
---
# <a name="database-mirroring-interoperability-and-coexistence-sql-server"></a>数据库镜像：互操作性和共存 (SQL Server)
  数据库镜像可以与 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]的下列功能或组件一起使用：  
  
-   [AlwaysOn 故障转移群集实例 （SQL Server 故障转移群集）](database-mirroring-and-sql-server-failover-cluster-instances.md)  
  
-   [变更数据捕获（和更改跟踪）](../../relational-databases/track-changes/change-data-capture-and-other-sql-server-features.md)  
  
-   [数据库快照](../../relational-databases/databases/database-snapshots-sql-server.md)  
  
-   [全文目录](database-mirroring-and-full-text-catalogs-sql-server.md)  
  
-   [日志传送](database-mirroring-and-log-shipping-sql-server.md)  
  
-   [复制](database-mirroring-and-replication-sql-server.md)  
  
 数据库镜像与以下功能不能共存：  
  
-   跨数据库事务/分布式事务  
  
     有关不支持此类事务原因的信息，请参阅[数据库镜像或 AlwaysOn 可用性组 (SQL Server) 不支持跨数据库事务](../availability-groups/windows/transactions-always-on-availability-and-database-mirroring.md)。  
  
-   [!INCLUDE[ssHADR](../../includes/sshadr-md.md)]  
  
## <a name="see-also"></a>请参阅  
 [数据库镜像 (SQL Server)](database-mirroring-sql-server.md)  
  
  
