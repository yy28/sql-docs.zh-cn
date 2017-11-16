---
title: "非 SQL Server 发布服务器 | Microsoft Docs"
ms.custom: 
ms.date: 08/29/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology: replication
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- heterogeneous database replication, non-SQL Server Publishers
- non-SQL Server Publishers
- heterogeneous data sources, non-SQL Server Publishers
- Publishers [SQL Server replication], Oracle
ms.assetid: 08a160a6-33be-46b5-bc7b-d53180d8bdf1
caps.latest.revision: "31"
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 95c9750c86cfe5bb82d37948c24c5e140b2c3187
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/09/2017
---
# <a name="non-sql-server-publishers"></a>非 SQL Server 发布服务器  
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]  

通过从非[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 源发布数据，您可以将数据合并到 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]中。 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 可以订阅从 Oracle 数据库发布的快照或事务数据。 有关从 Oracle 发布的详细信息，请参阅 [Oracle 发布概述](../../../relational-databases/replication/non-sql/oracle-publishing-overview.md)。  
  
[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 支持下列异类事务复制和快照复制方案：  
  
-   将数据从 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 发布到非[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 订阅服务器。  

-   将数据发布到 Oracle 以及从 Oracle 发布数据具有以下限制条件：  
  | |2016 或更早版本 |2017 或更高版本 |
  |-------|-------|--------|
  |从 Oracle 复制 |仅支持 Oracle 10g 或更早版本 |仅支持 Oracle 10g 或更早版本 |
  |复制到 Oracle |最高为 Oracle 12c |不支持 |


 不推荐异类复制到非 SQL Server 订阅服务器。 不推荐使用 Oracle 发布。 若要移动数据，请创建使用变更数据捕获和 [!INCLUDE[ssIS](../../../includes/ssis-md.md)]的解决方案。  
  
  
> [!CAUTION]  
>  [!INCLUDE[ssNoteDepFutureAvoid](../../../includes/ssnotedepfutureavoid-md.md)]  
  
 从非[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 数据库发布适用于下列方案：  
  
|应用场景|说明|  
|--------------|-----------------|  
|[!INCLUDE[msCoName](../../../includes/msconame-md.md)] .NET Framework 应用程序部署|使用 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] Visual Studio 和 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 开发，同时还能处理从非[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 数据库复制的数据。|  
|数据仓库临时服务器|使 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 临时数据库与非[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 数据库保持同步。|  
|迁移到 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]|针对 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 执行实时应用程序测试，同时复制源系统的更改。 对迁移满意后，切换到 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 。|  
  
## <a name="see-also"></a>另请参阅  
 [Heterogeneous Database Replication](../../../relational-databases/replication/non-sql/heterogeneous-database-replication.md)  
  
  
