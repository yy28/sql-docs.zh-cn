---
title: 高可用性 (Reporting Services) |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
helpviewer_keywords:
- high availability [SQL Server], Reporting Services
- high availability [Reporting Services]
- Reporting Services, high availability
ms.assetid: 50e0813f-f591-4688-9cd1-e6389a3808e5
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 8bc05f1f669597229a3a07d6ce8487eb19a77201
ms.sourcegitcommit: 8d6fb6bbe3491925909b83103c409effa006df88
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/22/2019
ms.locfileid: "59944983"
---
# <a name="high-availability-reporting-services"></a>高可用性 (Reporting Services)
  [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] 报表服务器是一种无状态服务器，它在两个 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 关系数据库中存储应用程序数据、内容、属性和会话信息。 因此，确保 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] 功能的可用性的最佳做法是执行以下操作：  
  
-   使用 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssDE](../includes/ssde-md.md)] 的高可用性功能来最大化报表服务器数据库的正常运行时间。 如果您将某个 [!INCLUDE[ssDE](../includes/ssde-md.md)] 实例配置为在故障转移群集中运行，则在创建报表服务器数据库时可选择该实例。  
  
-   将 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssHADR](../includes/sshadr-md.md)] 用于 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] 数据库并且在可能的情况下用于数据源。 有关详细信息，请参阅 [Reporting Services 与 AlwaysOn 可用性组 (SQL Server)](../database-engine/availability-groups/windows/reporting-services-with-always-on-availability-groups-sql-server.md)。  
  
-   将多个报表服务器配置为在扩展部署下运行，其中所有服务器共享一个报表服务器数据库。 如果在扩展部署中部署多个报表服务器实例（最好在不同的服务器上部署），将有助于在其中一个报表服务器实例出现故障时提供不间断的服务。  
  
 扩展部署提供了一种共享数据库的方法。 如果一台报表服务器出现故障，同一部署下的其他服务器还能继续工作。  
  
 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] 不能识别群集。 扩展部署本身不提供负载平衡；它不会检测报表服务器上的处理负载，也不会将新的处理请求路由到最空闲的服务器。 扩展部署不会重新路由在完成之前失败的处理请求。 若要获取负载平衡功能，必须为承载报表服务器的 Web 服务器配置负载平衡，然后在扩展部署中对报表服务器进行配置以使它们共享同一个报表服务器数据库。  
  
 报表服务器 Web 服务和 Windows 服务紧密集成，并作为一个报表服务器实例一起运行。 您不能单独配置任一服务的可用性。  
  
## <a name="see-also"></a>请参阅  
 [高可用性解决方案 (SQL Server)](../sql-server/failover-clusters/high-availability-solutions-sql-server.md)   
 [配置本机模式报表服务器扩展部署（SSRS 配置管理器）](install-windows/configure-a-native-mode-report-server-scale-out-deployment.md)  
  
  
