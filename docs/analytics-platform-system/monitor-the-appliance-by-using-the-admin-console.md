---
title: 用管理控制台监视
description: 对于分析平台系统，管理控制台是一个 web 应用程序，用于显示设备状态、运行状况和性能信息。 用户通过 internet 浏览器连接到管理控制台。
author: mzaman1
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.custom: seo-dt-2019
ms.openlocfilehash: 977e38016fbb58356d22ccfc5f783539e5f852d5
ms.sourcegitcommit: d587a141351e59782c31229bccaa0bff2e869580
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/22/2019
ms.locfileid: "74400946"
---
# <a name="monitor-the-appliance-with-the-admin-console---analytics-platform-system"></a>用管理控制台分析平台系统监视设备
管理控制台是一个 SQL Server PDW web 应用程序，用于显示设备状态、运行状况和性能信息。 用户通过 Internet Explorer 连接到管理控制台。  
  
## <a name="About"></a>关于管理控制台  
![工具控制台主页](./media/monitor-the-appliance-by-using-the-admin-console/SQL_Server_PDW_AdminConsol_ApplHome.png "SQL_Server_PDW_AdminConsol_ApplHome")  
  
**本**  
主页  
提供设备状态的快速摘要。  
  
运行状况  
显示设备拓扑，其中显示每个节点内每个受监视组件的运行状况。 允许你查看节点组件的各个节点和属性的当前状态。  
  
显示硬件和软件警报。  
  
性能监视  
显示性能监视器图。  
  
**并行数据仓库**  
主页  
提供 PDW 状态的快速摘要。  
  
会话  
显示活动 PDW 用户会话。 这有助于监视资源争用。  
  
查询  
显示正在运行的查询和最近完成的查询的列表。 它显示相关错误（如果有）。 还可以查看查询执行计划和节点执行信息的详细信息。  
  
加载  
显示加载计划、PDW 加载的当前状态以及相关错误（如果有）。  
  
备份/还原  
显示 PDW 备份和还原操作的日志。  
  
运行状况  
显示 PDW 拓扑，其中显示每个节点内每个受监视组件的运行状况。 允许你查看节点组件的各个节点和属性的当前状态。  
  
显示硬件和软件警报。  
  
资源  
显示 PDW 资源锁及其当前状态的列表。  
  
存储  
总结了 PDW 的存储利用率。  
  
性能监视  
显示 PDW 性能监视器图。  
 
> [!NOTE]  
> 管理控制台的屏幕分辨率为1024x768。 使用 1280 X 1024 或更高版本的屏幕分辨率时，管理控制台显示最佳。  
  
## <a name="Connect"></a>连接到管理控制台  
若要连接到管理控制台，需要：  
  
-   至少为 Internet Explorer 版本10。  
  
-   访问管理控制台的权限。 <!-- MISSING LINKS See [Grant Permissions to Use the Admin Console &#40;SQL Server PDW&#41;](../sqlpdw/grant-permissions-to-use-the-admin-console-sql-server-pdw.md).  -->  
  
-   控制节点群集的 IP 地址。  请从 SQL Server PDW 管理员那里获取此。  
  
若要连接到管理控制台，请使用 Internet Explorer 和 https 浏览到控件节点群集的 IP 地址。 例如，如果控制节点群集的 IP 地址为`10.192.63.102`，则在浏览器`https://10.192.63.102`地址栏中输入。 第一个屏幕将请求您的**登录名**和**密码**。 提供 SQL Server 身份验证登录名和密码，或 Windows 身份验证登录名和 Windows 密码。 如果使用 Windows 身份验证登录名，管理控制台将使用模拟。  
  
## <a name="RelatedTasks"></a>管理控制台任务  
管理员控制台提供了以下功能：  
  
|||  
|-|-|  
|**信息类型**|**如何在管理员控制台中访问**|  
|设备的总体状态|单击顶部菜单中的 "**设备状态**" 或 "**主页**"。|  
|警报|单击 "**警报**"。 有关详细信息，请参阅[了解 &#40;Analytics Platform System&#41;的管理控制台警报](understanding-admin-console-alerts.md)。|  
|设备组件及其状态|单击顶部菜单中的 "**设备状态**" 或 "**主页**"。|  
|监视请求（包括查询、加载、备份和还原）|单击 "**会话**" 以查看当前活动或最新的会话。<br /><br />单击 "**查询**" 以查看当前活动或最近的查询。 为查询显示的信息包括负载、备份和还原。<br /><br />单击 "**锁定**" 查看活动锁。|  
|监视有关加载、备份和还原的其他信息。|单击 "**加载**" 或 "**备份/还原**"。|  
|性能信息|单击 "**性能监视器**"。|  
  
## <a name="see-also"></a>另请参阅  
[设备监视 &#40;分析平台系统&#41;](appliance-monitoring.md)  
  
