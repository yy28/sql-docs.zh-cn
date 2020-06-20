---
title: 异类数据库复制 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- heterogeneous database replication, about heterogeneous database replication
- replication [SQL Server], heterogeneous database replication
- heterogeneous database replication
ms.assetid: 3fd983ad-e206-45db-9054-417c9b5bb815
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: b8e67d65ca316134b4f801cccf9bded31408bb1a
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/18/2020
ms.locfileid: "85049152"
---
# <a name="heterogeneous-database-replication"></a>异类数据库复制
  [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 支持下列异类事务复制和快照复制方案：  
  
-   将数据从 Oracle 发布到 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]。  
  
-   将数据从 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 发布到非[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 订阅服务器。  
  
 不推荐异类复制到非 SQL Server 订阅服务器。 不推荐使用 Oracle 发布。 若要移动数据，请创建使用变更数据捕获和 [!INCLUDE[ssIS](../../../includes/ssis-md.md)]的解决方案。  
  
> [!CAUTION]  
>  [!INCLUDE[ssNoteDepFutureAvoid](../../../includes/ssnotedepfutureavoid-md.md)]  
  
## <a name="publishing-data-from-oracle"></a>从 Oracle 发布数据  
 您可以使用 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 从 Oracle 发布数据，其大多数功能和简单易用性与 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 快照复制和事务复制相同。 从 Oracle 发布数据非常适合于下列情形：  
  
|场景|说明|  
|--------------|-----------------|  
|[!INCLUDE[msCoName](../../../includes/msconame-md.md)] .NET Framework 应用程序部署|使用 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] Visual Studio 和 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 开发，同时还能处理从非[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 数据库复制的数据。|  
|数据仓库临时服务器|使 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 临时数据库与非[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 数据库保持同步。|  
|迁移到 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]|针对 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 执行实时应用程序测试，同时复制源系统的更改。 对迁移满意后，切换到 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 。|  
  
 有关详细信息，请参阅 [Oracle 发布概述](oracle-publishing-overview.md)。  
  
## <a name="publishing-data-to-non-sql-server-subscribers"></a>将数据发布到非 SQL Server 订阅服务器  
 支持将下列非[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 数据库作为快照和事务发布的订阅服务器：  
  
-   用于 Oracle 所支持的所有平台的 Oracle。  
  
-   用于 AS400、MVS、Unix、Linux 和 Windows 的 IBM DB2。  
  
 有关详细信息，请参阅 [Non-SQL Server Subscribers](non-sql-server-subscribers.md)。  
  
  
