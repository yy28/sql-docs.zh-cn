---
title: 断开可用性副本的连接 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
f1_keywords:
- sql12.swb.agdashboard.arp2connected.issues.f1
helpviewer_keywords:
- Availability Groups [SQL Server], policies
ms.assetid: 1a2162d3-54fb-4356-b349-effbdc15a5a4
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 51004cf91b039ccdd83eda91425b3aea0764d237
ms.sourcegitcommit: 9ee72c507ab447ac69014a7eea4e43523a0a3ec4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/17/2020
ms.locfileid: "84937066"
---
# <a name="availability-replica-is-disconnected"></a>断开可用性副本的连接
    
## <a name="introduction"></a>简介  
  
|||  
|-|-|  
|**策略名称**|可用性副本连接状态|  
|**问题**|断开可用性副本的连接。|  
|**类别**|**严重**|  
|**多**|可用性副本|  
  
## <a name="description"></a>说明  
 此策略检查可用性副本之间的连接状态。 当可用性副本的连接状态为 DISCONNECTED 时，此策略处于不正常状态。 否则，该策略处于正常状态。  
  
> [!NOTE]  
>   对于此版本的 [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)]，与可能原因和解决方法有关的信息位于 TechNet Wiki 上的 [断开可用性副本的连接](https://go.microsoft.com/fwlink/p/?LinkId=220857) 中。  
  
## <a name="possible-causes"></a>可能的原因  
 辅助副本未连接到主副本。 连接状态为 DISCONNECTED。 此问题可能由以下原因导致：  
  
-   连接端口可能与另一个应用程序冲突。  
  
-   加密类型或算法不匹配。  
  
-   连接端点已被删除或尚未启动。  
  
-   传输已断开连接。  
  
## <a name="possible-solutions"></a>可能的解决方法  
 以下是此问题的可能解决方法：  
  
-   检查主副本和辅助副本实例的数据库镜像端点配置，并更新不匹配的配置。  
  
-   检查端口是否冲突，如果冲突，请更改端口号。  
  
## <a name="see-also"></a>另请参阅  
 [AlwaysOn 可用性组 &#40;SQL Server 概述&#41;](overview-of-always-on-availability-groups-sql-server.md)   
 [使用 AlwaysOn 面板 (SQL Server Management Studio)](use-the-always-on-dashboard-sql-server-management-studio.md)  
  
  
