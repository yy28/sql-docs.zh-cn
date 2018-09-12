---
title: 实用工具管理 （SQL Server 实用工具） |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: 3e5a00c3-8905-40f0-9ddc-d924df9c2f0d
caps.latest.revision: 5
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 96c81c4f6913c4e355ca368ae67f04c1c5fde12b
ms.sourcegitcommit: 8ae6e6618a7e9186aab3c6a37ea43776aa9a382b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/06/2018
ms.locfileid: "43815273"
---
# <a name="utility-administration-sql-server-utility"></a>实用工具管理（SQL Server 实用工具）
  使用“实用工具管理”选项卡可以管理 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 实用工具的策略、安全性和数据仓库设置。 有关 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 实用工具概念的详细信息，请参阅 [SQL Server 实用工具功能和任务](../relational-databases/manage/sql-server-utility-features-and-tasks.md)。  
  
## <a name="uielement-list"></a>UIElement 列表  
 “策略”选项卡 - 使用“策略”选项卡可查看或指定全局监视策略。  
  
 设置全局数据层应用程序监视策略。 若要展开此选项的值列表，请单击策略名称旁的箭头，或者单击策略标题。  
 何时应用程序会用尽处理器容量？ 若要更改此策略，请使用策略说明右侧的控件，然后单击 **“应用”**。 您还可以使用显示底部的按钮还原默认值或放弃更改。  
  
-   处理器使用率的默认最大值是 70%。  
  
-   处理器使用率的默认最小值是 0%。  
  
 何时应用程序会用尽文件空间？ 若要更改数据文件或日志文件空间使用率的策略，请使用策略说明右侧的控件，然后单击“应用” 。 您还可以使用显示底部的按钮还原默认值或放弃更改。  
  
-   文件空间使用率的默认最大值是 70%。  
  
-   文件空间使用率的默认最小值是 0%。  
  
 设置全局 SQL Server 托管实例应用程序监视策略。 若要展开此选项的值列表，请单击策略名称旁的箭头，或者单击策略标题。  
 何时 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 的托管实例会用尽处理器容量？ 若要更改此策略，请使用策略说明右侧的控件，然后单击 **“应用”**。 您还可以使用显示底部的按钮还原默认值或放弃更改。  
  
-   实例处理器使用率的默认最大值是 70%。  
  
-   实例处理器使用率的默认最小值是 0%。  
  
 何时 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 计算机的托管实例会用尽处理器容量？ 若要更改此策略，请使用策略说明右侧的控件，然后单击 **“应用”**。 您还可以使用显示底部的按钮还原默认值或放弃更改。  
  
-   计算机处理器使用率的默认最大值是 70%。  
  
-   计算机处理器使用率的默认最小值是 0%。  
  
 何时 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 的托管实例会用尽文件空间？ 若要更改数据文件或日志文件空间使用率的策略，请使用策略说明右侧的控件，然后单击 **“应用”**。 您还可以使用显示底部的按钮还原默认值或放弃更改。  
  
-   文件空间使用率的默认最大值是 70%。  
  
-   文件空间使用率的默认最小值是 0%。  
  
 何时 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 计算机的托管实例会用尽存储卷空间？ 若要更改此策略，请使用策略说明右侧的控件，然后单击 **“应用”**。 您还可以使用显示底部的按钮还原默认值或放弃更改。  
  
-   计算机卷空间使用率的默认最大值是 70%。  
  
-   计算机卷空间使用率的默认最小值是 0%。  
  
 减少高度易失性资源中的策略违反干扰。 若要展开此功能的控件，请单击显示右侧的向下箭头。  
 有关详细信息，请参阅[减少 CPU 使用策略中的干扰（SQL Server 实用工具）](../relational-databases/manage/reduce-noise-in-cpu-utilization-policies-sql-server-utility.md)  
  
## <a name="uielement-list"></a>UIElement 列表  
 “安全性”选项卡 - 显示有权管理 UCP 或从 UCP 进行读取的登录名。  
  
 从将添加到实用工具读取者角色的 UCP 选择登录名。  
 实用工具读取者权限允许用户帐户：  
  
-   连接到 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 实用工具。  
  
-   在 SSMS 的实用工具资源管理器中查看所有视点。  
  
-   在 SSMS 的实用工具资源管理器中查看“实用工具管理”节点的设置。  
  
 实用工具管理员可以将 SQL Server 的实例注册到 SQL Server 实用工具中和从 SQL Server 实用工具中删除 SQL Server 的实例，以及修改托管实例上的策略和修改 UCP 上的管理设置。  
  
 要作为实用工具管理员，您必须对 SQL Server 的实例具有 sysadmin 权限。 若要添加或更改 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] UCP 的用户帐户，请使用 SSMS 中的对象资源管理器将该用户添加到 SQL Server 的 UCP 实例的服务器登录名中。 有关详细信息，请参阅 [sp_addlogin (Transact-SQL)](/sql/relational-databases/system-stored-procedures/sp-addlogin-transact-sql)。  
  
## <a name="uielement-list"></a>UIElement 列表  
 “数据仓库”选项卡 - 为实用工具管理数据仓库显示配置详细信息。  
  
 数据保持期  
 针对为 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]的托管实例收集的使用率信息，指定数据保持期。 默认保持期为 1 年。 最小值为 1 个月。 支持的最长的值是 2 年。  
  
 实用工具数据仓库配置信息  
 以下配置设置在此版本的 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]中不可配置：  
  
-   UMDW 名称：Sysutility_mdw_\<GUID>_DATA。  
  
-   收集组上载频率：每隔 15 分钟。  
  
 UMDW 目录是可配置的：\<System drive>:\Program Files\Microsoft SQL Server\MSSQL10_50.<UCP_Name>\MSSQL\Data\\，其中，\<System drive> 通常为 C:\ 驱动器。 日志文件 UMDW_\<GUID>_LOG 位于同一目录中。  
  
> [!NOTE]  
>  可以使用 detach/attach 或 ALTER DATABASE 更改该 UMDW (sysutility_mdw) 文件位置。 我们建议使用 ALTER DATABASE。 有关详细信息，请参阅 [ALTER DATABASE (Transact-SQL)](/sql/t-sql/statements/alter-database-transact-sql)。  
  
 返回到出厂默认值  
 若要将此选项卡上的设置重置为默认值，请单击“还原默认设置”按钮，然后单击“应用”。  
  
## <a name="see-also"></a>请参阅  
 [实用工具仪表板&#40;SQL Server 实用工具&#41;](../../2014/database-engine/utility-dashboard-sql-server-utility.md)   
 [已部署的数据层应用程序详细信息（SQL Server 实用工具）](../../2014/database-engine/deployed-data-tier-application-details-sql-server-utility.md)   
 [托管实例详细信息（SQL Server 实用工具）](../../2014/database-engine/managed-instance-details-sql-server-utility.md)   
 [在 SQL Server 实用工具中监视 SQL Server 的实例](../relational-databases/manage/monitor-instances-of-sql-server-in-the-sql-server-utility.md)  
  
  
