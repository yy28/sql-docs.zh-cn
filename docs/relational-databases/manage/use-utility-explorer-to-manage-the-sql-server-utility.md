---
title: 使用实用工具资源管理器管理 SQL Server 实用工具 | Microsoft Docs
description: 查看使用实用工具资源管理器管理 SQL Server 实例的各种方法，例如调整策略定义和查看 CPU 以及存储卷利用率。
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
ms.assetid: 74012c90-b42e-4171-b27a-9c30cf69ff98
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: e7fc64fc2c019b69afc603b2cab85044fd639dbb
ms.sourcegitcommit: 04cf7905fa32e0a9a44575a6f9641d9a2e5ac0f8
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/07/2020
ms.locfileid: "91810220"
---
# <a name="use-utility-explorer-to-manage-the-sql-server-utility"></a>使用实用工具资源管理器管理 SQL Server 实用工具
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  实用工具资源管理器是 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]的一个组件，它连接到 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 实例以便提供 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实用工具中所有对象的树视图。 实用工具资源管理器内容窗格提供了几种方法来查看与 SQL Server 的托管实例的运行状态有关的摘要数据和详细数据。 实用工具资源管理器还提供一个用户界面来查看和管理策略定义。 实用工具资源管理器的功能根据 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实用工具中的对象而稍有不同，但通常包括 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实用工具管理的对象、数据和策略。 有关详细信息，请参阅 [SQL Server 实用工具功能和任务](../../relational-databases/manage/sql-server-utility-features-and-tasks.md)。  
  
## <a name="create-utility-control-point"></a>创建实用工具控制点  
 您必须首先创建实用工具控制点，然后才能使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实用工具。 有关详细信息，请参阅 [SQL Server 实用工具功能和任务](../../relational-databases/manage/sql-server-utility-features-and-tasks.md)或[创建 SQL Server 实用工具控制点（SQL Server 实用工具）](../../relational-databases/manage/create-a-sql-server-utility-control-point-sql-server-utility.md)。  
  
## <a name="enroll-an-instance-of-sql-server-or-a-data-tier-application-from-utility-explorer"></a>从实用工具资源管理器注册 SQL Server 的实例或数据层应用程序  
 您可以轻松地将 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的实例注册到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实用工具中。 在实用工具资源管理器中，右键单击 **“托管实例”** 节点，然后单击 **“添加托管实例”** 。 按照向导的步骤完成操作。 有关详细信息，请参阅[注册 SQL Server 的实例（SQL Server 实用工具）](../../relational-databases/manage/enroll-an-instance-of-sql-server-sql-server-utility.md)。  
  
 若要在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实用工具中将数据层应用程序部署到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的托管实例上，请单击“对象资源管理器”选项卡，展开“管理”节点，然后右键单击“数据层应用程序”。 从右键菜单中，选择“部署数据层应用程序”。 有关详细信息，请参阅[部署数据层应用程序](../../relational-databases/data-tier-applications/deploy-a-data-tier-application.md)。  
  
## <a name="viewing-utility-explorer"></a>查看实用工具资源管理器  
 默认情况下，实用工具资源管理器在 [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] 中不可见。 如果您在 [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] 用户界面中看不到实用工具资源管理器，请在 **“视图”** 菜单上，单击 **“实用工具资源管理器”** 。 若要查看实用工具资源管理器内容窗格，请在 **“视图”** 菜单上，单击 **“实用工具资源管理器内容”** 。  
  
## <a name="viewing-objects-in-utility-explorer"></a>在实用工具资源管理器中查看对象  
 实用工具资源管理器导航窗格和实用工具资源管理器内容窗格显示 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实用工具管理的数据、对象和策略。 使用导航窗格可以指定要在面板和视点中显示的信息，然后使用内容窗格和详细信息选项卡访问 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实用工具管理的对象的数据和策略信息。  
  
### <a name="sql-server-utility-navigation-pane"></a>SQL Server 实用工具导航窗格  
 实用工具资源管理器导航窗格在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实用工具中提供对象的树视图，这些对象按实用工具控制点进行分组。 若要展开文件夹，请单击加号 (+) 或在实用工具资源管理器导航窗格中双击 UCP 名称。 右键单击文件夹或对象，以执行常见任务。 树视图中的节点如下所示：  
  
-   树视图中的顶端节点是实用工具控制点 (UCP)。 该节点名的结构为："Utility_Name" (ComputerName\UCP_instance_name)。 如果您没有 UCP，则必须创建一个。 如果您没有连接到某一 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实用工具，则必须连接到一个实用工具。 有关详细信息，请参阅 [SQL Server 实用工具功能和任务](../../relational-databases/manage/sql-server-utility-features-and-tasks.md)。 在树视图中单击该 UCP 名称可以使用面板视图中的数据填充 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实用工具资源管理器内容窗格。 有关详细信息，请参阅[实用工具仪表板（SQL Server 实用工具）](/previous-versions/sql/sql-server-2016/ee210541(v=sql.130))。  
  
     右键单击 UCP 节点可以刷新面板中的数据。  
  
-   在树视图中单击 **“已部署的数据层应用程序”** 节点可以访问 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实用工具内容窗格中的列表视图数据。 该内容窗格底部的详细信息选项卡提供 CPU 和存储使用率数据，并且可以访问 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实用工具中单独数据层应用程序的策略定义和属性详细信息。 有关详细信息，请参阅[已部署数据层应用程序详细信息（SQL Server 实用工具）](/previous-versions/sql/sql-server-2016/ee240857(v=sql.130))。  
  
     在树视图中右键单击“已部署的数据层应用程序”节点可以访问筛选设置或刷新列表视图中的数据。  
  
-   在树视图中单击 **“托管实例”** 节点可以访问 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实用工具内容窗格中的列表视图数据。 该内容窗格底部的详细信息选项卡提供 CPU 和存储卷使用率数据，并且可用于访问 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实用工具中 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的单独托管实例的策略定义和属性详细信息。 有关详细信息，请参阅[托管实例详细信息（SQL Server 实用工具）](./utility-explorer-f1-help.md)。  
  
     右键单击树视图中的“托管实例”节点，可将 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的托管实例添加到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实用工具中，访问筛选器设置，或刷新列表视图中的数据。  
  
-   单击树视图中的“实用工具管理”节点可访问 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的所有托管实例以及 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实用工具中已部署数据层应用程序的全局策略定义，查看 UCP 管理员信息以及访问 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实用工具管理数据仓库的配置设置。 有关详细信息，请参阅[实用工具管理（SQL Server 实用工具）](/previous-versions/sql/sql-server-2016/ee240832(v=sql.130))。 您还可以使用 **“策略”** 选项卡上的控件更改用于报告违反策略的敏感度。 有关详细信息，请参阅[减少 CPU 使用策略中的干扰（SQL Server 实用工具）](../../relational-databases/manage/reduce-noise-in-cpu-utilization-policies-sql-server-utility.md)。  
  
     右键单击树视图中的“实用工具管理”节点，以便刷新内容窗格中的数据。  
  
### <a name="sql-server-utility-dashboard"></a>SQL Server 实用工具面板  
 在实用工具资源管理器树视图中选择 UCP 节点将在实用工具资源管理器内容窗格中填充 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实用工具面板。 该面板在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实用工具中为 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的所有托管实例和数据层应用程序提供一目了然的状态摘要，并且提供 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实用工具托管的对象的整体存储使用率。 有关详细信息，请参阅[实用工具仪表板（SQL Server 实用工具）](/previous-versions/sql/sql-server-2016/ee210541(v=sql.130))。 若要注册或删除 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的实例，请参阅[注册 SQL Server 的实例（SQL Server 实用工具）](../../relational-databases/manage/enroll-an-instance-of-sql-server-sql-server-utility.md)、[部署数据层应用程序](../../relational-databases/data-tier-applications/deploy-a-data-tier-application.md)或[从 SQL Server 实用工具中删除 SQL Server 的实例](../../relational-databases/manage/remove-an-instance-of-sql-server-from-the-sql-server-utility.md)。  
  
### <a name="filtering-the-list-of-objects-in-utility-explorer-contents"></a>在实用工具资源管理器内容中筛选对象列表  
 当某一节点中包含大量对象时，可能会很难找到要查找的对象。 在此类情况下，使用实用工具资源管理器的筛选功能可以减小列表。 例如，你可能想要查找 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的特定实例或者仅查找其文件空间使用不足的计算机。 右键单击要筛选的文件夹，单击筛选按钮，然后单击 **“筛选设置”** 以便打开“实用工具资源管理器筛选设置”对话框。 您可以按名称、计算机 CPU、实例 CPU、文件空间、卷空间、策略覆盖设置或上次报告的时间筛选该列表。 **“运算符”** 和 **“值”** 列在下拉列表中提供附加的筛选运算符。  
  
### <a name="starting-powershell"></a>启动 PowerShell  
 可通过右键单击对象资源管理器树中的大多数文件夹和对象并选择“启动 PowerShell”来启动 PowerShell 会话。 这将启动已启用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] PowerShell 支持的 PowerShell 会话，并将路径设置为在对象资源管理器中右键单击的对象。 然后，您可以在交互式 PowerShell 环境中输入 PowerShell 命令。 有关详细信息，请参阅 [SQL Server PowerShell](../../powershell/sql-server-powershell.md)。  
  
PowerShell 没有 F1 帮助，但包含 Get-Help cmdlet，它提供了有关使用 PowerShell 的信息。 有关使用 Get-Help 的详细信息，请参阅 [获取 SQL Server PowerShell 帮助](../../powershell/sql-server-powershell.md)。  
  
## <a name="see-also"></a>另请参阅  
 [SQL Server 实用工具的功能和任务](../../relational-databases/manage/sql-server-utility-features-and-tasks.md)   
 [配置运行状况策略（SQL Server 实用工具）](../../relational-databases/manage/configure-health-policies-sql-server-utility.md)   
 [对象资源管理器](../../ssms/object/object-explorer.md)  
  
