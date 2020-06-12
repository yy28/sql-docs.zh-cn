---
title: 实用工具仪表板（SQL Server 实用工具） |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
ms.assetid: 999eb741-4a60-43f6-ab37-2df7dce845c1
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 0ce0c700e7e53ef1b055fa476e1e259fefe6c0aa
ms.sourcegitcommit: 18a7c77be31f9af92ad9d0d3ac5eecebe8eec959
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/26/2020
ms.locfileid: "83857749"
---
# <a name="utility-dashboard-sql-server-utility"></a>实用工具面板（SQL Server 实用工具）
  若要在 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 实用工具仪表板中查看数据，请在标有“Utility<UCP_Name>\\(ComputerName\UCP)”的实用工具资源管理器树中选择顶端节点。 该面板包括来自 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 的所有托管实例和 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 实用工具中所有数据层应用程序的摘要和详细信息数据。 若要刷新仪表板中的数据，请在实用工具资源管理器树中右键单击该顶端节点，然后选择“刷新”****。  
  
 有关如何创建实用工具控制点的详细信息点，请参阅 [创建 SQL Server 实用工具控制点（SQL Server 实用工具）](../relational-databases/manage/create-a-sql-server-utility-control-point-sql-server-utility.md)。 有关如何将 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 实例添加到 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 实用工具的详细信息，请参阅 [注册 SQL Server 实例（SQL Server 实用工具）](../relational-databases/manage/enroll-an-instance-of-sql-server-sql-server-utility.md)。  
  
## <a name="ui-element-list"></a>UI 元素列表  
 托管实例运行状况  
 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 的托管实例的运行状态显示在实用工具资源管理器内容窗格的左侧。  
  
 托管实例的运行状况参数如下所示：  
  
-   [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]实例的 CPU 使用率。  
  
-   数据库文件使用率。  
  
-   存储卷空间使用率。  
  
-   计算机的 CPU 使用率。  
  
-   每个参数的状态划分为三个类别：  
  
-   很好地利用 - 没有违反资源使用策略的 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 托管实例的数目。  
  
-   使用不足 - 违反资源使用不足策略的托管资源的数目。  
  
-   使用过度 - 违反资源使用过度策略的托管资源的数目。  
  
-   没有可用数据 - 数据不可用于 SQL Server 的托管实例，这或者是因为 SQL Server 刚注册并且第一个数据收集操作尚未完成，或者是因为存在与收集数据并将数据上载到 UCP 的 SQL Server 托管实例有关的问题。  
  
 每个运行状况参数的详细状态在滑动指示器中列出。 滑动指示器右侧的部分显示有多少个托管实例处于各状态类别中。  
  
 若要创建 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 的托管实例或数据层应用程序的筛选视图，请在实用工具面板中单击其滑动指示器旁的使用率类别链接。 例如，如果您在 **“实用工具资源管理器内容”** 窗格中单击 **“使用过度的实例 CPU”** ，则 SSMS 将基于当前策略设置创建具有使用过度的 CPU 的 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 托管实例的筛选后列表视图。  
  
 请注意，在你单击某一使用率类别链接时，实用工具资源管理器导航窗格中的相应节点将追加“(已筛选)”****- 也就是说，“托管实例”**** 将标记为“托管实例(已筛选)”****。 若要查看筛选设置，请在导航窗格中右键单击该节点，选择“筛选器”****，然后单击“筛选设置”****。 若要清除筛选设置，请在导航窗格中右键单击该节点，选择“筛选器”****，然后单击“删除筛选器”****。  
  
 有关查看 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 的单独实例的运行状况的详细信息，或者有关查看或更改策略配置设置的详细信息，请参阅[托管实例详细信息（SQL Server 实用工具）](../../2014/database-engine/managed-instance-details-sql-server-utility.md)。  
  
 实用工具摘要  
 显示 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 的托管实例的数目以及 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 实用工具管理的数据层应用程序的数目。  
  
 数据层应用程序运行状况  
 数据层应用程序的运行状态显示在实用工具资源管理器内容窗格的右侧。  
  
 数据层应用程序运行状况参数如下所示：  
  
-   [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]实例的 CPU 使用率。  
  
-   数据库文件使用率。  
  
-   存储卷空间使用率。  
  
-   计算机的 CPU 使用率。  
  
 每个参数的状态划分为三个类别：  
  
-   很好地利用 - 没有违反资源使用策略的数据层应用程序的数目。  
  
-   使用过度 - 违反资源使用过度策略的数据层应用程序的数目。  
  
-   使用过度 - 违反资源使用过度策略的数据层应用程序的数目。  
  
-   没有可用数据 - 数据不可用于数据层应用程序，因为包含数据层应用程序的 SQL Server 托管实例未报告数据。  
  
 每个运行状况参数的详细状态在滑动指示器中列出。 滑动指示器右侧的部分显示有多少个数据层应用程序处于各状态类别中。 有关查看单独数据层应用程序运行状况的详细信息，或者有关查看或更改策略配置设置的详细信息，请参阅[已部署的数据层应用程序详细信息（SQL Server 实用工具）](../../2014/database-engine/deployed-data-tier-application-details-sql-server-utility.md)。  
  
 实用工具存储使用率历史记录  
 实用工具历史记录显示在 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 实用工具面板底部的时间图中。 请注意，时间数据使用 datetime 数据类型显示 UCP 本地日期和时间。 有关详细信息，请参阅 SQL Server 联机丛书中的 [datetime (Transact-SQL)](https://go.microsoft.com/fwlink/?LinkId=164071) 主题。 在使用实用工具对象模型时，请注意 SSMS 使用 datetimeoffset 数据类型。 有关详细信息，请参阅 SQL Server 联机丛书中的 [datetimeoffset (Transact-SQL)](https://go.microsoft.com/fwlink/?LinkId=141713) 主题。  
  
 使用显示区域左侧的单选按钮可以更改图形的报告期间。  
  
 报告间隔选项包括：  
  
-   1 天，以 15 分钟间隔显示。  
  
-   1 周，以 1 天间隔显示。  
  
-   1 个月，以 1 周间隔显示。  
  
-   1 年，以 1 个月间隔显示。  
  
 在对报告间隔进行更改后，数据将自动刷新。  
  
 实用工具存储使用率  
 在面板的右下角中，存储使用率饼图显示在包含 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]的托管实例的计算机上驻留的卷中已用空间与可用空间的比率。 此显示数据每隔 15 分钟刷新一次。  
  
## <a name="see-also"></a>另请参阅  
 [使用实用工具资源管理器管理 SQL Server 实用工具](../relational-databases/manage/use-utility-explorer-to-manage-the-sql-server-utility.md)   
 [SQL Server &#40;SQL Server 实用工具注册实例&#41;](../relational-databases/manage/enroll-an-instance-of-sql-server-sql-server-utility.md)   
 [修改资源运行状况策略定义（SQL Server 实用工具）](../relational-databases/manage/modify-a-resource-health-policy-definition-sql-server-utility.md)  
  
  
