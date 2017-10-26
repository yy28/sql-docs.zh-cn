---
title: "DQS 管理 | Microsoft Docs"
ms.custom: 
ms.date: 10/01/2012
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- data-quality-services
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- dqs administration
- administration
- dqs,adminstration
ms.assetid: 9940ef5d-f6f6-4dec-9414-1077a4d7f12b
caps.latest.revision: 21
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.translationtype: HT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: dab2f79fbd66389684bafcac726bcfe363f50f8e
ms.contentlocale: zh-cn
ms.lasthandoff: 09/09/2017

---
# <a name="dqs-administration"></a>dqs 管理
  使用[!INCLUDE[ssDQSnoversion](../includes/ssdqsnoversion-md.md)] (DQS)，您可以管理在 [!INCLUDE[ssDQSServer](../includes/ssdqsserver-md.md)]上执行的各种 DQS 活动、配置与 DQS 活动有关的服务器级属性、配置 Reference Data Services 设置以及 DQS 日志设置。 通过 **的** 管理 [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)]功能来执行这些操作。 根据您在 DQS 中的安全访问权限（角色），授权/拒绝您在此区域中执行某些功能。  
  
 除了这些管理活动之外，本主题还提供有关备份和还原 DQS 数据库（此管理活动不是使用 [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)]执行的）的信息。  
  
 [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)] 中的管理功能具有以下优点：  
  
-   使数据专员可以从 [!INCLUDE[ssDQSServer](../includes/ssdqsserver-md.md)] 监视 [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)]上的各种 DQS 活动。  
  
-   使 DQS 管理员可以从 [!INCLUDE[ssDQSServer](../includes/ssdqsserver-md.md)] 监视 [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)]上的各种 DQS 活动、根据需要 *终止* 正在运行的活动或 *停止* 活动中某个正在运行的过程。  
  
-   配置引用数据服务设置，如设置与 Windows Azure Marketplace 的连接以及管理直接第三方引用数据服务提供程序。  
  
-   配置清理和匹配活动的阈值。  
  
-   在 [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)]中启用/禁用通知。  
  
-   基于事件的严重级别配置日志记录。  
  
##  <a name="AdminUsingClent"></a> 使用数据质量客户端的管理活动  
 使用 **中的** “管理” [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)]功能执行这些活动。  
  
### <a name="activity-monitoring"></a>活动监视  
 **中的** “活动监视” [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)] 屏幕显示有关在 [!INCLUDE[ssDQSServer](../includes/ssdqsserver-md.md)]上执行的每个活动的详细信息。 此屏幕将主要供数据专员使用，用于对 [!INCLUDE[ssDQSServer](../includes/ssdqsserver-md.md)] 应用程序所连接的 [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)] 上执行的所有活动执行高级监视。 此屏幕不提供任何系统级别的监视。 此外，DQS 管理员还可以使用此屏幕在需要时终止正在运行的活动或停止活动中正在运行的过程，从而控制活动或活动中的过程。 为知识发现、域管理、匹配策略、清理、匹配和基于 SQL Server Integration Services (SSIS) 的清理显示此数据。  
  
### <a name="configuration"></a>配置  
 DQS 管理员使用 **中的** “配置” [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)] 屏幕执行以下操作：  
  
-   **引用数据**：配置引用数据服务提供程序：Windows Azure Marketplace 或直接引用数据服务提供程序。 在设置引用数据服务提供程序后，可以在域管理活动期间在知识库中使用引用数据映射域/复合域，然后将同一知识库用于数据质量项目中的清理活动。 您还可以使用它指定连接到 Internet 的代理设置以使用 Windows Azure Marketplace。  
  
-   **常规设置**：指定数据清理和数据匹配的阈值，以及在 [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)]中是否启用事件探查的通知。 DQS 在执行数据质量项目中的计算机辅助的清理和匹配活动期间使用这些阈值。  
  
-   **日志设置**：DQS 中的日志文件记录在 DQS 中执行的活动，在维护和故障排除期间对于跟踪操作问题很有用。 您可以基于事件的严重级别筛选要为各种 DQS 功能（域管理、知识发现、清理、匹配和 Reference Data Services）记录的消息和 DQS 模块。  
  
> [!NOTE]  
>  **“配置”** 屏幕仅适用于对 DQS_MAIN 数据库具有 dqs_administrator 角色的那些用户。  
  
##  <a name="AdminOutsideClient"></a> 数据质量客户端之外的管理活动  
 下面这些活动在数据质量客户端的外部执行：  
  
-   **备份和还原 DQS 数据库**：备份和还原 DQS 数据库与备份和还原任何 SQL Server 数据库一样，但是针对 DQS 有一些注意事项。  
  
-   **分离和附加 DQS 数据库**：分离和附加 DQS 数据库与分离和附加任何 SQL Server 数据库一样，但是针对 DQS 有一些注意事项。  
  
 有关详细信息，请参阅 [Manage DQS Databases](../data-quality-services/manage-dqs-databases.md)。  
  
## <a name="related-tasks"></a>相关任务  
  
|任务说明|主题|  
|----------------------|-----------|  
|说明如何在 DQS 中监视活动。|[监视 DQS 活动](../data-quality-services/monitor-dqs-activities.md)|  
|说明如何在 DQS 中配置引用数据设置。|[将 DQS 配置为使用引用数据](../data-quality-services/configure-dqs-to-use-reference-data.md)|  
|说明如何配置清理和匹配活动的阈值。|[配置清理和匹配活动的阈值](../data-quality-services/configure-threshold-values-for-cleansing-and-matching.md)|  
|说明如何在 DQS 中启用或禁用通知。|[在 DQS 中启用或禁用事件探查通知](../data-quality-services/enable-or-disable-profiling-notifications-in-dqs.md)|  
|说明如何基于事件的严重级别配置 DQS 日志记录。|[为 DQS 日志文件配置严重级别](../data-quality-services/configure-severity-levels-for-dqs-log-files.md)|  
|说明如何配置 DQS 日志记录的高级设置。|[为 DQS 日志文件配置高级设置](../data-quality-services/configure-advanced-settings-for-dqs-log-files.md)|  
|说明如何备份和还原 DQS 数据库。|[备份和还原 DQS 数据库](../data-quality-services/backing-up-and-restoring-dqs-databases.md)|  
|介绍如何分离和附加 DQS 数据库。|[分离和附加 DQS 数据库](../data-quality-services/detaching-and-attaching-dqs-databases.md)|  
  
## <a name="see-also"></a>另请参阅  
 [DQS 中的 Reference Data Services](../data-quality-services/reference-data-services-in-dqs.md)   
 [管理 DQS 日志文件](../data-quality-services/manage-dqs-log-files.md)   
 [管理 DQS 数据库](../data-quality-services/manage-dqs-databases.md)  
  
  

