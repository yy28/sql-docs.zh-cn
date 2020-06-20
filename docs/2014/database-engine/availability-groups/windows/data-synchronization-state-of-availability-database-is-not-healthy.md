---
title: 可用性数据库的数据同步状态不正常 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
f1_keywords:
- sql12.swb.agdashboard.arp3datasynchealthy.issues.f1
helpviewer_keywords:
- Availability Groups [SQL Server], policies
ms.assetid: 4fd003e7-808e-4b0e-b28a-47d9f2616f06
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 7ed541e86bf531dd9681e9926e4acb6d1bdc6042
ms.sourcegitcommit: 9ee72c507ab447ac69014a7eea4e43523a0a3ec4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/17/2020
ms.locfileid: "84936859"
---
# <a name="data-synchronization-state-of-availability-database-is-not-healthy"></a>可用性数据库的数据同步状态不正常
    
## <a name="introduction"></a>简介  
  
|||  
|-|-|  
|**策略名称**|可用性数据库数据同步状态|  
|**问题**|可用性数据库的数据同步状态不正常。|  
|**类别**|**警告**|  
|**多**|可用性数据库|  
  
## <a name="description"></a>说明  
 此策略汇总可用性副本中所有可用性数据库（也称为“数据库副本”）的数据同步状态。 当有数据库副本不处于要求的数据同步状态时，此策略处于不正常状态。 否则，该策略处于正常状态。  
  
> [!NOTE]  
>  对于此版本的 [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)]，与可能原因和解决方法有关的信息位于 TechNet Wiki 上的 [一些可用性数据库的数据同步状态不正常](https://go.microsoft.com/fwlink/p/?LinkId=220858) 中。  
  
## <a name="possible-causes"></a>可能的原因  
 此可用性数据库的数据同步状态不正常。 在异步-提交可用性副本上，每个可用性数据库都应该处于“正在同步”状态。 在同步提交副本上，每个可用性数据库必须处于 SYNCHRONIZED 状态。  
  
## <a name="possible-solution"></a>可能的解决方法  
 使用数据库副本策略查找具有不正常数据同步状态的数据库副本，然后解决该数据库副本上的问题。  
  
## <a name="see-also"></a>另请参阅  
 [AlwaysOn 可用性组 &#40;SQL Server 概述&#41;](overview-of-always-on-availability-groups-sql-server.md)   
 [使用 AlwaysOn 面板 (SQL Server Management Studio)](use-the-always-on-dashboard-sql-server-management-studio.md)  
  
  
