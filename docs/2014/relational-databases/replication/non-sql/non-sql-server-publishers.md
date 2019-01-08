---
title: 非 SQL Server 发布服务器 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- heterogeneous database replication, non-SQL Server Publishers
- non-SQL Server Publishers
- heterogeneous data sources, non-SQL Server Publishers
- Publishers [SQL Server replication], Oracle
ms.assetid: 08a160a6-33be-46b5-bc7b-d53180d8bdf1
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 19db106c43007259754bace7f0e9d2938ad9cf1e
ms.sourcegitcommit: ceb7e1b9e29e02bb0c6ca400a36e0fa9cf010fca
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/03/2018
ms.locfileid: "52752569"
---
# <a name="non-sql-server-publishers"></a>非 SQL Server 发布服务器
  通过从非[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 源发布数据，您可以将数据合并到 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]中。 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 可以订阅从 Oracle 数据库发布的快照或事务数据。 有关从 Oracle 发布的详细信息，请参阅 [Oracle 发布概述](oracle-publishing-overview.md)。  
  
 不推荐异类复制到非 SQL Server 订阅服务器。 不推荐使用 Oracle 发布。 若要移动数据，请创建使用变更数据捕获和 [!INCLUDE[ssIS](../../../includes/ssis-md.md)]的解决方案。  
  
> [!CAUTION]  
>  [!INCLUDE[ssNoteDepFutureAvoid](../../../includes/ssnotedepfutureavoid-md.md)]  
  
 从非[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 数据库发布适用于下列方案：  
  
|应用场景|Description|  
|--------------|-----------------|  
|[!INCLUDE[msCoName](../../../includes/msconame-md.md)] .NET Framework 应用程序部署|使用 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] Visual Studio 和 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 开发，同时还能处理从非[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 数据库复制的数据。|  
|数据仓库临时服务器|使 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 临时数据库与非[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 数据库保持同步。|  
|迁移到 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]|针对 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 执行实时应用程序测试，同时复制源系统的更改。 对迁移满意后，切换到 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 。|  
  
## <a name="see-also"></a>请参阅  
 [Heterogeneous Database Replication](heterogeneous-database-replication.md)  
  
  
