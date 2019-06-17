---
title: 使用管理控制台的分析平台系统监视 |Microsoft Docs
description: Analytics Platform system 管理员控制台是一个 web 应用程序，它会显示设备状态、 运行状况和性能信息。 用户连接到 internet 浏览器通过在管理控制台。
author: mzaman1
manager: craigg
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.openlocfilehash: d094f809052222238806e679e38c6578422fd9aa
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/15/2019
ms.locfileid: "63027552"
---
# <a name="monitor-the-appliance-with-the-admin-console---analytics-platform-system"></a>监视设备，但在管理控制台的分析平台系统
在管理控制台是一个 SQL Server PDW web 应用程序，它会显示设备状态、 运行状况和性能信息。 用户连接到 Internet 资源管理器通过在管理控制台。  
  
## <a name="About"></a>有关在管理控制台  
![工具控制台主页](./media/monitor-the-appliance-by-using-the-admin-console/SQL_Server_PDW_AdminConsol_ApplHome.png "SQL_Server_PDW_AdminConsol_ApplHome")  
  
**Appliance**  
主页  
提供的设备状态的快速摘要。  
  
运行状况  
显示的指示器，显示每个节点中每个受监视组件的运行状况工具拓扑。 可以查看各个节点的当前状态和节点组件的属性。  
  
显示硬件和软件的警报。  
  
性能监视器  
显示性能监视器关系图。  
  
**并行数据仓库**  
主页  
提供的 PDW 状态的快速摘要。  
  
会话  
显示活动 PDW 用户会话。 这可以帮助进行监视的资源争用。  
  
查询  
显示正在运行的查询和最近完成的查询的列表。 如果有的话，它会显示相关的错误。 此外提供了查看查询执行计划和节点执行信息的详细信息的能力。  
  
加载  
如果有，显示加载计划、 PDW 加载和相关的错误的当前状态。  
  
Backups/Restores  
显示日志的 PDW 备份和还原操作。  
  
运行状况  
显示的指示器，显示每个节点中每个受监视组件的运行状况 PDW 拓扑。 可以查看各个节点的当前状态和节点组件的属性。  
  
显示硬件和软件的警报。  
  
资源  
显示 PDW 资源锁及其当前状态的列表。  
  
存储  
总结了 PDW 存储使用率。  
  
性能监视器  
显示 PDW 性能监视器关系图。  
 
> [!NOTE]  
> 管理员控制台具有 1024 x 768 屏幕分辨率。 管理员控制台会显示最适合于的屏幕分辨率 1280 X 1024 或更高版本。  
  
## <a name="Connect"></a>连接到管理员控制台  
若要连接到管理控制台中，需要：  
  
-   在最低 Internet Explorer 版本 10。  
  
-   若要访问管理控制台的权限。 <!-- MISSING LINKS See [Grant Permissions to Use the Admin Console &#40;SQL Server PDW&#41;](../sqlpdw/grant-permissions-to-use-the-admin-console-sql-server-pdw.md).  -->  
  
-   控制节点群集的 IP 地址。  从 SQL Server PDW 管理员处获取这。  
  
若要连接到管理控制台，使用 Internet Explorer 和 https，以浏览到控制节点群集的 IP 地址。 例如，如果是群集的控制节点的 IP 地址`10.192.63.102`，输入`https://10.192.63.102`在浏览器地址栏中。 第一个屏幕将请求你**登录名**并**密码**。 提供的 SQL Server 身份验证登录名和密码，或 Windows 身份验证登录名和 Windows 密码。 如果使用 Windows 身份验证登录名，在管理控制台将使用模拟。  
  
## <a name="RelatedTasks"></a>管理员控制台任务  
在管理控制台提供了监视以下功能：  
  
|||  
|-|-|  
|**信息类型**|**如何在管理控制台中的访问权限**|  
|设备的总体状态|单击**设备状态**在顶部菜单中，或**主页**。|  
|警报|单击**警报**。 有关详细信息，请参阅[了解管理员控制台警报&#40;Analytics Platform System&#41;](understanding-admin-console-alerts.md)。|  
|设备组件和它们的状态|单击**设备状态**在顶部菜单中，或**主页**。|  
|监视器请求 （包括查询、 加载、 备份和还原）|单击**会话**若要查看当前活动会话或新会话。<br /><br />单击**查询**若要查看当前活动或最新的查询。 显示查询的信息包括加载、 备份和还原。<br /><br />单击**锁**若要查看活动锁。|  
|监视负载、 备份和还原的其他信息。|单击**负载**或**备份/还原**。|  
|性能信息|单击**性能监视器**。|  
  
## <a name="see-also"></a>请参阅  
[设备监视&#40;分析平台系统&#41;](appliance-monitoring.md)  
  
