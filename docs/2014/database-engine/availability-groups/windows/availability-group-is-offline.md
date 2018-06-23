---
title: 可用性组处于脱机状态 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- dbe-high-availability
ms.tgt_pltfrm: ''
ms.topic: article
f1_keywords:
- sql12.swb.agdashboard.agp2online.issues.f1
helpviewer_keywords:
- Availability Groups [SQL Server], policies
ms.assetid: 093c5208-bf7a-49f4-a546-72b48197cadf
caps.latest.revision: 11
author: rothja
ms.author: jroth
manager: jhubbard
ms.openlocfilehash: 8c2b16b37292956fd5f6c9aec55588e9029798cf
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/19/2018
ms.locfileid: "36016184"
---
# <a name="availability-group-is-offline"></a>可用性组处于脱机状态
    
## <a name="introduction"></a>简介  
  
|||  
|-|-|  
|**策略名称**|可用性组联机状态|  
|**问题**|可用性组处于脱机状态。|  
|**类别**|**严重**|  
|**方面**|可用性组 (availability group)|  
  
## <a name="description"></a>Description  
 此策略检查可用性组的联机或脱机状态。 当可用性组的群集资源处于脱机状态或可用性组不具有主副本时，此策略处于不正常状态并引发警报。  
  
 当可用性组的群集资源处于联机状态并且可用性组具有主副本时，此策略处于正常状态。  
  
> [!NOTE]  
>  对于此版本的 [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)]，与可能原因和解决方法有关的信息位于 TechNet Wiki 上的 [可用性组处于脱机状态](http://go.microsoft.com/fwlink/p/?LinkId=220850) 中。  
  
## <a name="possible-causes"></a>可能的原因  
 此问题可能由承载主副本的服务器实例中的失败或 Windows Server 故障转移群集 (WSFC) 可用性组资源脱机引起。 可用性组脱机可能有以下原因：  
  
-   可用性组未配置为自动故障转移模式。 主副本变为不可用且可用性组中所有副本的角色变为 RESOLVING。  
  
    -   主副本实例服务已关闭或停止响应。  
  
    -   可用性组与群集的连接有问题。  
  
-   可用性组配置为自动故障转移模式，但是未成功完成。  
  
    -   在自动故障转移期间，对目标副本的主副本就绪检查失败，并且没有副本可以变为新的主副本。  
  
-   群集中的可用性组资源变为脱机状态。  
  
    -   任何依赖的群集资源遇到严重问题并变为脱机状态。 可用性组资源还处于脱机状态，直到依赖的资源变为联机状态。  
  
    -   群集中的严重问题导致禁用了可用性组资源。  
  
-   对可用性组存在正在进行的自动、手动或强制故障转移。  
  
## <a name="possible-solutions"></a>可能的解决方法  
 以下是此问题的可能解决方法：  
  
-   如果主副本的 SQL Server 实例关闭，请重新启动服务器，然后验证可用性组恢复到正常状态。  
  
-   如果自动故障转移失败，请验证副本上的数据库与以前已知的主副本同步，然后故障转移到主副本。 如果数据库不同步，请选择数据丢失最少的副本，然后恢复到故障转移模式。  
  
-   如果群集中的资源在 SQL Server 实例处于正常状态时脱机，请使用故障转移群集管理器检查群集运行状况或服务器上的其他群集问题。 您还可以使用故障转移群集管理器尝试将可用性组资源联机。  
  
-   如果正在进行故障转移，请等待故障转移完成。  
  
## <a name="see-also"></a>请参阅  
 [AlwaysOn 可用性组概述&#40;SQL Server&#41;](overview-of-always-on-availability-groups-sql-server.md)   
 [使用 AlwaysOn 面板 (SQL Server Management Studio)](use-the-always-on-dashboard-sql-server-management-studio.md)  
  
  