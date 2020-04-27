---
title: 暂停和恢复共享计划 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
helpviewer_keywords:
- pausing schedules
- report-specific schedules [Reporting Services]
- shared schedules [Reporting Services], resuming
- resuming schedules
- continuing schedules
- schedules [Reporting Services], resuming
- schedules [Reporting Services], pausing
ms.assetid: e416be75-5234-4aa6-a3de-77f60f25169a
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: c30dfdd78ed6f420bee7c6bbba449ba40a2a137a
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/26/2020
ms.locfileid: "66100793"
---
# <a name="pause-and-resume-shared-schedules"></a>暂停和恢复共享计划
  您可以暂停和恢复正在使用的共享计划。 通过暂停共享计划，可以暂时冻结用于触发报表处理和订阅的计划。 您只能暂停和恢复共享计划。 不能暂停报表特定计划。  
  
 您不能暂停和恢复正在进行的报表处理。 您只能暂停和恢复处于 SQL Server 代理服务计划队列中的计划。 正在进行的作业不在计划引擎的管理范围内。 有关详细信息，请参阅 [管理运行中的进程](manage-a-running-process.md)  
  
 暂停共享计划时，可以取消将要发生的任何操作。 恢复共享计划后，报表和订阅处理将使用服务器的本地时间，在计划的下一次执行时间进行。 假如未暂停计划，本机模式报表服务器或 SharePoint 服务应用程序不会虚构出一些本来将要发生的计划操作。  
  
 本主题内容：  
  
-   [暂停和恢复共享计划（本机模式）](#bkmk_native)  
  
-   [暂停和恢复共享计划（SharePoint 模式）](#bkmk_sharepoint)  
  
##  <a name="pause-and-resume-shared-schedules-native-mode"></a><a name="bkmk_native"></a> 暂停和恢复共享计划（本机模式）  
 要暂停和恢复共享计划，请使用报表管理器中的“计划”页。 不能使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)][!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]；它没有提供用于暂停和恢复计划的选项。 有关详细信息，请参阅 [Create, Modify, and Delete Schedules](create-modify-and-delete-schedules.md)。  
  
#### <a name="to-pause-or-resume-a-shared-schedule"></a>暂停或恢复共享计划  
  
1.  从报表管理器单击 **“站点设置”** 。  
  
2.  单击 **“计划”** 。  
  
3.  选择计划，在功能区中单击 **“暂停”** 或 **“恢复”** 。 如果计划当前已暂停， **“状态”** 列将包含 **“已暂停”** 。  
  
##  <a name="pause-and-resume-shared-schedules-sharepoint-mode"></a><a name="bkmk_sharepoint"></a> 暂停和恢复共享计划（SharePoint 模式）  
 要暂停和恢复共享计划，请使用“站点设置”页或 PowerShell。 针对每个 SharePoint 站点管理计划。  
  
#### <a name="to-pause-or-resume-a-shared-schedule"></a>暂停或恢复共享计划  
  
1.  单击 **“网站操作”** 。  
  
2.  单击 **“网站设置”** 。  
  
3.  在 Reporting Services 部分中，单击 **“管理共享计划”** 。  
  
4.  选择计划，并单击 **“暂停所选计划”** 或 **“运行所选计划”** 。 如果计划当前已暂停， **“状态”** 列将包含 **“已暂停”** 。  
  
## <a name="see-also"></a>另请参阅  
 [“计划”](schedules.md)   
 [创建、修改和删除计划](create-modify-and-delete-schedules.md)   
 [更改报表服务器上的时区和时钟设置](change-time-zones-and-clock-settings-on-a-report-server.md)   
 [管理运行中的进程](manage-a-running-process.md)  
  
  
