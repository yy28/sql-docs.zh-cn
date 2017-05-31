---
title: "实用工具资源管理器的 F1 帮助 | Microsoft Docs"
ms.custom: 
ms.date: 08/19/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: reference
f1_keywords:
- sql13.swb.ue.navigation.f1
- sql13.SWB.UE.dac.details.F1
- sql13.SQB.UE.dac.details.F1
- utility details
helpviewer_keywords:
- Utility
- management
- data-tier application
ms.assetid: 8697e4a4-4f59-4cda-af71-7de86005bd4a
caps.latest.revision: 8
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: 46b3d92d8c1f6a720eb39a701aca50a8bc2733b9
ms.contentlocale: zh-cn
ms.lasthandoff: 04/11/2017

---
# <a name="utility-explorer-f1-help"></a>实用工具资源管理器的 F1 帮助
  下面各部分介绍 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实用工具功能和关联的操作。  
  
  ## <a name="utility-dashboard-sql-server-utility"></a>实用工具面板（SQL Server 实用工具）
 若要在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实用工具仪表板中查看数据，请在标有“Utility<UCP_Name>\\(ComputerName\UCP)”的实用工具资源管理器树中选择顶端节点。 该面板包括来自 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的所有托管实例和 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实用工具中所有数据层应用程序的摘要和详细信息数据。 若要刷新仪表板中的数据，请在实用工具资源管理器树中右键单击该顶端节点，然后选择“刷新”。  
  
 有关如何创建实用工具控制点的详细信息点，请参阅 [创建 SQL Server 实用工具控制点（SQL Server 实用工具）](../../relational-databases/manage/create-a-sql-server-utility-control-point-sql-server-utility.md)。 有关如何将 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实例添加到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实用工具的详细信息，请参阅 [注册 SQL Server 实例（SQL Server 实用工具）](../../relational-databases/manage/enroll-an-instance-of-sql-server-sql-server-utility.md)。  
 
  
### <a name="uielement-list"></a>UIElement 列表  
 托管实例运行状况  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的托管实例的运行状态显示在实用工具资源管理器内容窗格的左侧。  
  
 托管实例的运行状况参数如下所示：  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]实例的 CPU 使用率。  
  
-   数据库文件使用率。  
  
-   存储卷空间使用率。  
  
-   计算机的 CPU 使用率。  
  
-   每个参数的状态划分为三个类别：  
  
-   很好地利用 - 没有违反资源使用策略的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 托管实例的数目。  
  
-   使用不足 - 违反资源使用不足策略的托管资源的数目。  
  
-   使用过度 - 违反资源使用过度策略的托管资源的数目。  
  
-   没有可用数据 - 数据不可用于 SQL Server 的托管实例，这或者是因为 SQL Server 刚注册并且第一个数据收集操作尚未完成，或者是因为存在与收集数据并将数据上载到 UCP 的 SQL Server 托管实例有关的问题。  
  
 每个运行状况参数的详细状态在滑动指示器中列出。 滑动指示器右侧的部分显示有多少个托管实例处于各状态类别中。  
  
 若要创建 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的托管实例或数据层应用程序的筛选视图，请在实用工具面板中单击其滑动指示器旁的使用率类别链接。 例如，如果您在 **“实用工具资源管理器内容”** 窗格中单击 **“使用过度的实例 CPU”** ，则 SSMS 将基于当前策略设置创建具有使用过度的 CPU 的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 托管实例的筛选后列表视图。  
  
 请注意，在你单击某一使用率类别链接时，实用工具资源管理器导航窗格中的相应节点将追加“(已筛选)”- 也就是说，“托管实例”将标记为“托管实例(已筛选)”。 若要查看筛选设置，请在导航窗格中右键单击该节点，选择“筛选器”，然后单击“筛选设置”。 若要清除筛选设置，请在导航窗格中右键单击该节点，选择“筛选器”，然后单击“删除筛选器”。  
  
 有关查看 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的单独实例的运行状况的详细信息，或者有关查看或更改策略配置设置的详细信息，请参阅[托管实例详细信息（SQL Server 实用工具）](http://msdn.microsoft.com/library/6e51b7bb-a733-4852-8c33-7f4dbdf931c2)。  
  
 实用工具摘要  
 显示 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的托管实例的数目以及 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实用工具管理的数据层应用程序的数目。  
  
 数据层应用程序运行状况  
 数据层应用程序的运行状态显示在实用工具资源管理器内容窗格的右侧。  
  
 数据层应用程序运行状况参数如下所示：  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]实例的 CPU 使用率。  
  
-   数据库文件使用率。  
  
-   存储卷空间使用率。  
  
-   计算机的 CPU 使用率。  
  
 每个参数的状态划分为三个类别：  
  
-   很好地利用 - 没有违反资源使用策略的数据层应用程序的数目。  
  
-   使用过度 - 违反资源使用过度策略的数据层应用程序的数目。  
  
-   使用过度 - 违反资源使用过度策略的数据层应用程序的数目。  
  
-   没有可用数据 - 数据不可用于数据层应用程序，因为包含数据层应用程序的 SQL Server 托管实例未报告数据。  
  
 每个运行状况参数的详细状态在滑动指示器中列出。 滑动指示器右侧的部分显示有多少个数据层应用程序处于各状态类别中。 有关查看单独数据层应用程序运行状况的详细信息，或者有关查看或更改策略配置设置的详细信息，请参阅[已部署的数据层应用程序详细信息（SQL Server 实用工具）](http://msdn.microsoft.com/library/79c41dd9-abcb-434e-9326-00a341d5c867)。  
  
 实用工具存储使用率历史记录  
 实用工具历史记录显示在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实用工具面板底部的时间图中。 请注意，时间数据使用 datetime 数据类型显示 UCP 本地日期和时间。 有关详细信息，请参阅 [datetime (Transact-SQL)](http://go.microsoft.com/fwlink/?LinkId=164071) 主题。 在使用实用工具对象模型时，请注意 SSMS 使用 datetimeoffset 数据类型。 有关详细信息，请参阅 [datetimeoffset (Transact-SQL)](http://go.microsoft.com/fwlink/?LinkId=141713) 主题。  
  
 使用显示区域左侧的单选按钮可以更改图形的报告期间。  
  
 报告间隔选项包括：  
  
-   1 天，以 15 分钟间隔显示。  
  
-   1 周，以 1 天间隔显示。  
  
-   1 个月，以 1 周间隔显示。  
  
-   1 年，以 1 个月间隔显示。  
  
 在对报告间隔进行更改后，数据将自动刷新。  
  
 实用工具存储使用率  
 在面板的右下角中，存储使用率饼图显示在包含 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]的托管实例的计算机上驻留的卷中已用空间与可用空间的比率。 此显示数据每隔 15 分钟刷新一次。  
 
 ## <a name="deployed-data-tier-application-details-sql-server-utility"></a>已部署的数据层应用程序详细信息（SQL Server 实用工具）
  实用工具资源管理器的“已部署的数据层应用程序”视图中的信息为单独的数据层应用程序提供使用率数据、CPU 使用率历史数据、文件级别的存储使用率详细信息，并且提供查看和更新策略阈值的能力。 可以在数据层应用程序级别为 CPU 使用率以及数据库数据文件和日志文件控制策略阈值。 您还可以查看各数据层应用程序的属性详细信息。  
  
### <a name="uielement-list"></a>UIElement 列表  
 列表视图  
 顶部窗格中的列表视图显示与单独的数据层应用程序有关的数据。 运行状态图标按使用率类别为各数据层应用程序提供摘要状态：  
  
-   绿色的选中标记 - ![](../../relational-databases/manage/media/well-utilized.gif "Well_utilized") - 没有违反资源使用策略的数据层应用程序的数目。 资源得到很好地利用。  
  
-   绿色向下箭头 - ![](../../relational-databases/manage/media/utility-down-arrow.gif "Utility_down_arrow") - 资源使用不足。  
  
-   红色向上箭头 - ![](../../relational-databases/manage/media/utility-up-arrow.gif "Utility_up_arrow") - 资源使用过度。  
  
 可以通过将列表视图中的列向左或向右拖动，更改这些列在列表视图中的顺序。 可通过右键单击列标题并选择或取消选择列，添加或删除列表视图中的列。 右键单击菜单还提供了排序选项。 还可以通过单击列名称的顶部激活排序。  
  
 若要访问 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实用工具列表视图的筛选器选项，请右键单击实用工具资源管理器导航窗格中的“已部署的数据层应用程序”节点，然后选择“筛选器”。 实现筛选设置后，实用工具资源管理器中的“已部署的数据层应用程序”节点将标记为“已部署的数据层应用程序 (已筛选)”。**** 有关详细信息，请参阅[筛选设置（对象资源管理器和实用工具资源管理器）](http://msdn.microsoft.com/library/4aab04bc-e1ab-4d4b-ab74-b287fc805bc2)。  
  
 默认情况下，下面的列将显示与每个数据层应用程序有关的运行状态信息。  
  
-   名称 - 数据层应用程序名称。  
  
-   应用程序 CPU - 显示此数据层应用程序的处理器使用率的运行状态。 根据为数据层应用程序设置的 CPU 使用策略以及易失性资源评估策略的配置设置，确定此参数的运行状态。 有关详细信息，请参阅[减少 CPU 使用策略中的干扰（SQL Server 实用工具）](../../relational-databases/manage/reduce-noise-in-cpu-utilization-policies-sql-server-utility.md)。  
  
     若要查看此数据层应用程序的处理器使用率历史记录，或者查看或更改策略限制，请单击“CPU 使用率”选项卡。  
  
-   计算机 CPU - 显示计算机处理器使用率的运行状态。 根据为计算机设置的 CPU 使用策略以及易失性资源评估策略的配置设置，确定此参数的运行状态。 有关详细信息，请参阅[减少 CPU 使用策略中的干扰（SQL Server 实用工具）](../../relational-databases/manage/reduce-noise-in-cpu-utilization-policies-sql-server-utility.md)。  
  
     若要查看此数据层应用程序的处理器使用率历史记录，或者查看或更改策略限制，请单击“CPU 使用率”选项卡。  
  
-   文件空间 - 为每个数据层应用程序显示文件空间使用率的运行状态的摘要。  
  
    -   绿色的选中标记 - 所有文件组和日志文件组的运行状态是既没有使用过度，也没有使用不足。  
  
    -   绿色向下箭头 - 至少一个文件组或日志文件组的运行状态是使用不足，并且没有文件组或日志文件组被使用过度。  
  
    -   红色向上箭头 - 至少一个文件组或日志文件组的运行状态是使用过度。 注意，如果数据库处于“紧急”状态，则运行状态将显示日志文件空间使用过度。  
  
     若要查看或更改文件空间策略限制，请单击 **“存储使用率”** 选项卡。  
  
-   卷空间 - 为包含属于所选数据层应用程序的数据库的所有卷显示卷空间使用率的运行状态的摘要。 如果任何卷的运行状态为使用过度，则卷运行状态将在此列表视图中报告为使用过度。 如果任何卷的运行状态为使用不足，并且没有卷被使用过度，则卷空间运行状态将在此列表视图中报告为使用不足。 否则，卷空间运行状态将在列表视图中报告为很好地利用。 若要查看或更改策略限制，请单击 **“存储使用率”** 选项卡。  
  
-   策略类型 - 指示对于数据层应用程序，“全局”默认策略或“覆盖”自定义策略是否有效。  
  
-   实例名称 - 显示承载数据层应用程序的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实例的名称。  
  
 可以在列表视图的列标题区域中使用右键单击菜单显示的其他列：  
  
-   数据库名称  
  
-   部署日期  
  
-   可信：（True 或 False）  
  
-   排序规则  
  
-   兼容级别：（例如 Version100）  
  
-   启用加密：（True 或 False）  
  
-   恢复模式：（简单、完全或大容量日志记录）  
  
-   上次报告的时间：此列使用 datetime 数据类型显示 UCP 本地日期和时间。 有关详细信息，请参阅 [datetime (Transact-SQL)](http://go.microsoft.com/fwlink/?LinkId=164071) 主题。 在使用实用工具对象模型时，请注意 SSMS 使用 datetimeoffset 数据类型。 有关详细信息，请参阅 [datetimeoffset (Transact-SQL)](http://go.microsoft.com/fwlink/?LinkId=141713) 主题。  
  
 “CPU 使用率”选项卡  
 “CPU 使用率”选项卡为数据层应用程序和计算机 CPU 使用率显示历史数据的并排图形。  
  
 该图形按照显示区域右侧的单选按钮中指定的间隔显示处理器使用率历史记录。 若要更改显示间隔和刷新数据集，请从列表中选择一个单选按钮。  
  
 间隔选项如下所示：  
  
-   1 天，以 15 分钟间隔显示。  
  
-   1 周，以 1 天间隔显示。  
  
-   1 个月，以 1 周间隔显示。  
  
-   1 年，以 1 个月间隔显示。  
  
 “存储使用率”选项卡  
 “存储使用率”选项卡具有一个树视图，它显示属于列表视图中选定数据层应用程序的数据库文件和日志文件的存储使用率详细信息。 请注意，时间数据使用 datetime 数据类型显示 UCP 本地日期和时间。 有关详细信息，请参阅 [datetime (Transact-SQL)](http://go.microsoft.com/fwlink/?LinkId=164071) 主题。 在使用实用工具对象模型时，请注意 SSMS 使用 datetimeoffset 数据类型。 有关详细信息，请参阅 [datetimeoffset (Transact-SQL)](http://go.microsoft.com/fwlink/?LinkId=141713) 主题。  
  
 显示可按文件组或按卷分组。 若要使用文件组树视图，请在 **“文件分组依据:”** 选择中选择 **“文件组”** 单选按钮。  
  
 存储使用率历史数据图形中显示的数据会根据树视图中选择的节点发生变化：  
  
-   选择文件组节点以便显示由属于所选文件组的所有数据文件使用的文件空间图形。  
  
-   选择日志文件节点以便显示由属于所选数据库的所有日志文件使用的文件空间图形。  
  
-   选择数据库节点以便显示一个图形，该图形添加由属于所选数据库的所有数据文件和所有日志文件使用的文件空间。  
  
 若要查看单独文件的存储使用率状态，请单击树视图中文件名旁的加号。  
  
 运行状态图标为每个文件组提供一目了然的状态（与策略阈值进行比较）：  
  
-   绿色的选中标记 - 文件组中至少一个数据文件的文件空间使用率是既没有使用过度，也没有使用不足。  
  
-   绿色向下箭头 - 文件组中至少一个数据文件的文件空间使用率是使用不足，并且文件组中没有文件被使用过度。  
  
-   红色向上箭头 - 文件组中所有数据文件的文件空间使用率被使用过度。 注意，如果数据库处于“紧急”状态，则运行状态将显示日志文件空间使用过度。  
  
 若要按卷查看文件，请在 **“文件分组依据:”** 选择中选择 **“卷”** 单选按钮。 存储使用率历史记录图形显示存储卷上所有数据文件和所有日志文件使用的文件空间。 展开树可以查看单独数据库数据文件和日志文件的详细信息。  
  
 状态图标用来为每个卷提供状态：  
  
-   绿色的选中标记 - 资源被很好地利用。  
  
-   绿色向下箭头 - 资源使用不足。  
  
-   红色向上箭头 - 资源被使用过度。  
  
 “存储使用率”选项卡上每个文件名旁边的仪表表示相对于文件的有效容量的文件所使用空间量。 仪表旁边显示的百分比值是相对于文件的有效容量的文件所使用空间量的比率。 工具提示提供的数据用于计算与有效容量相比每个卷和每个文件的百分比。  
  
 如果该文件未配置为自动增长，则有效容量是分配给该文件的空间量。 如果该文件配置为自动增长，则有效容量是当前分配给该文件的空间量与目前卷上可用空间量之和。  
  
 可为数据文件和日志文件配置存储使用率策略。 若要查看或更改文件的存储使用率策略阈值，请单击“存储使用率”窗格底部的 **“文件策略”** 链接。 若要查看或更改存储卷的存储使用率策略阈值，请单击“存储使用率”窗格底部的 **“卷策略”** 链接。  
  
 若要覆盖默认策略阈值，请单击单选按钮 **“覆盖默认策略”**，指定上限和下限值，然后单击 **“确定”**。  
  
 有关更改违反策略容限的详细信息，请参阅[减少 CPU 使用策略中的干扰（SQL Server 实用工具）](../../relational-databases/manage/reduce-noise-in-cpu-utilization-policies-sql-server-utility.md)。  
  
 “属性详细信息”选项卡  
 为数据层应用程序列出的属性详细信息包括以下类别：  
  
-   数据库名称  
  
-   部署日期  
  
-   可信：（True 或 False）  
  
-   排序规则  
  
-   兼容级别：（例如 Version100）  
  
-   启用加密：（True 或 False）  
  
-   恢复模式：（简单、完全或大容量日志记录）  
  
-   上次报告的时间：此列使用 datetime 数据类型显示 UCP 本地日期和时间。 有关详细信息，请参阅 [datetime (Transact-SQL)](http://go.microsoft.com/fwlink/?LinkId=164071) 主题。 在使用实用工具对象模型时，请注意 SSMS 使用 datetimeoffset 数据类型。 有关详细信息，请参阅 [datetimeoffset (Transact-SQL)](http://go.microsoft.com/fwlink/?LinkId=141713) 主题。

## <a name="managed-instance-details-sql-server-utility"></a>托管实例详细信息（SQL Server 实用工具）
 实用工具资源管理器的“托管实例”视图中的信息为 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]的单独实例提供使用率数据、CPU 使用率历史记录、文件级别的存储使用率详细信息，并且提供查看和更新策略阈值的能力。 对于计算机，可以在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实例级别控制策略阈值；对于数据库文件和日志文件，可以在存储卷的级别控制策略阈值。 您还可以查看 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]的各个托管实例的属性详细信息。  
  
### <a name="uielement-list"></a>UIElement 列表  
 列表视图  
 顶部窗格中的列表视图可以显示行中按 ComputerName\InstanceName 列出的各 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实例的有关数据。  
  
 运行状态图标按使用率类别为 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的各实例提供摘要状态：  
  
-   绿色的选中标记 - ![](../../relational-databases/manage/media/well-utilized.gif "Well_utilized") - 没有违反资源使用策略的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 托管实例的数目。 资源得到很好地利用。  
  
-   绿色向下箭头 - ![](../../relational-databases/manage/media/utility-down-arrow.gif "Utility_down_arrow") - 资源使用不足。  
  
-   红色向上箭头 - ![](../../relational-databases/manage/media/utility-up-arrow.gif "Utility_up_arrow") - 资源使用过度。  
  
 可以通过将列表视图中的列向左或向右拖动，更改这些列在列表视图中的顺序。 可通过右键单击列标题并选择或取消选择列，添加或删除列表视图中的列。 右键单击菜单还提供了排序选项。 还可以通过单击列名称的顶部激活排序。  
  
 若要访问实用工具列表视图的筛选器选项，请右键单击实用工具资源管理器导航窗格中的“托管实例”节点，然后选择“筛选器”。 在实现了筛选器设置后，实用工具资源管理器中的“托管实例”节点将标有“托管实例(已筛选)”。 有关详细信息，请参阅[筛选设置（对象资源管理器和实用工具资源管理器）](http://msdn.microsoft.com/library/4aab04bc-e1ab-4d4b-ab74-b287fc805bc2)。  
  
 默认情况下，下面的列将显示与 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]的每个托管实例有关的运行状态信息。  
  
-   实例 CPU - 显示分配给此 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]实例的处理器使用率的运行状态。 根据为 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的实例设置的 CPU 使用策略以及易失性资源评估策略的配置设置，确定此参数的运行状态。 有关详细信息，请参阅[减少 CPU 使用策略中的干扰（SQL Server 实用工具）](../../relational-databases/manage/reduce-noise-in-cpu-utilization-policies-sql-server-utility.md)。  
  
     若要查看此 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]实例的处理器使用率历史记录，或者查看或更改策略限制，请单击 **“CPU 使用率”** 选项卡。  
  
-   计算机 CPU - 显示计算机处理器使用率的运行状态。 根据为计算机设置的 CPU 使用策略以及易失性资源评估策略的配置设置，确定此参数的运行状态。 有关详细信息，请参阅[减少 CPU 使用策略中的干扰（SQL Server 实用工具）](../../relational-databases/manage/reduce-noise-in-cpu-utilization-policies-sql-server-utility.md)。  
  
     若要查看此 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]实例的处理器使用率历史记录，或者查看或更改策略限制，请单击 **“CPU 使用率”** 选项卡。  
  
-   文件空间 - 为属于所选 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]实例的所有数据库显示文件空间使用率的运行状态的摘要。 如果任何数据库的运行状态为使用过度，则文件空间运行状态将在此列表视图中报告为使用过度。 如果任何数据库的运行状态为使用不足，并且没有数据库被使用过度，则文件空间运行状态将在此列表视图中报告为使用不足。 否则，文件空间运行状态将在列表视图中报告为很好地利用。 若要查看或更改策略限制，请单击 **“存储使用率”** 选项卡。  
  
-   卷空间 - 为包含属于所选 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]实例的数据库的所有卷显示卷空间使用率的运行状态的摘要。 如果任何卷的运行状态为使用过度，则卷运行状态将在此列表视图中报告为使用过度。 如果任何卷的运行状态为使用不足，并且没有卷被使用过度，则卷空间运行状态将在此列表视图中报告为使用不足。 否则，卷空间运行状态将在列表视图中报告为很好地利用。 若要查看或更改策略限制，请单击 **“存储使用率”** 选项卡。  
  
-   策略类型 - 指示对于 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]的托管实例，“全局”默认策略或“覆盖”自定义策略是否有效。  
  
 可以在列表视图的列标题区域中使用右键单击菜单显示的其他列：  
  
-   处理器名称：  
  
-   处理器速度 (MHz)：  
  
-   处理器计数：  
  
-   物理内存 (MB)：  
  
-   操作系统版本：  
  
-   SQL Server 版本：  
  
-   SQL Server 发行版：  
  
-   群集：（True 或 False）  
  
-   备份目录：  
  
-   排序规则：  
  
-   区分大小写：（True 或 False）  
  
-   语言:  
  
-   上次报告的时间：此列使用 datetime 数据类型显示 UCP 本地日期和时间。 有关详细信息，请参阅 [datetime (Transact-SQL)](http://go.microsoft.com/fwlink/?LinkId=164071) 主题。 在使用实用工具对象模型时，请注意 SSMS 使用 datetimeoffset 数据类型。 有关详细信息，请参阅 [datetimeoffset (Transact-SQL)](http://go.microsoft.com/fwlink/?LinkId=141713) 主题。  
  
 “CPU 使用率”选项卡  
 “CPU 使用率”选项卡为 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实例和计算机 CPU 使用率显示历史数据的并排图形。  
  
 该图形按照显示区域右侧的单选按钮中指定的间隔显示处理器使用率历史记录。 若要更改显示间隔和刷新数据集，请从列表中选择一个单选按钮。  
  
 间隔选项如下所示：  
  
-   1 天，以 15 分钟间隔显示。  
  
-   1 周，以 1 天间隔显示。  
  
-   1 个月，以 1 周间隔显示。  
  
-   1 年，以 1 个月间隔显示。  
  
 “存储使用率”选项卡  
 “存储使用率”选项卡具有显示存储使用率详细信息的树视图。 请注意，时间数据使用 datetime 数据类型显示 UCP 本地日期和时间。 有关详细信息，请参阅 [datetime (Transact-SQL)](http://go.microsoft.com/fwlink/?LinkId=164071) 主题。 在使用实用工具对象模型时，请注意 SSMS 使用 datetimeoffset 数据类型。 有关详细信息，请参阅 [datetimeoffset (Transact-SQL)](http://go.microsoft.com/fwlink/?LinkId=141713) 主题。  
  
 显示可按数据库或按卷分组。 若要使用数据库树视图，请在 **“文件分组依据:”** 选择中选择 **“数据库”** 单选按钮。 若要查看单独数据库文件的存储使用率状态，请单击树视图中数据库名称旁的加号。 列出的数据库文件包括属于列表视图中所选 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的托管实例的所有系统数据库和用户数据库。  
  
 树结构与存储层次结构相对应。 树视图中的根节点是数据库。 树视图的下一个级别包含一个文件组节点或属于数据库的节点，以及属于数据库的日志的日志文件节点。 下一个级别包含属于文件组的数据文件。  
  
 存储使用率历史数据图形中显示的数据会根据树视图中选择的节点发生变化：  
  
-   选择文件组节点以便显示由属于所选文件组的所有数据文件使用的文件空间图形。  
  
-   选择日志文件节点以便显示由属于所选数据库的所有日志文件使用的文件空间图形。  
  
-   选择数据库节点以便显示一个图形，该图形添加由属于所选数据库的所有数据文件和所有日志文件使用的文件空间。  
  
 运行状态图标为数据库文件、文件组和日志文件提供一目了然的状态：  
  
 对于数据库：  
  
-   绿色的选中标记 - 所有文件组和日志文件的运行状态是既没有使用过度，也没有使用不足。  
  
-   绿色向下箭头 - 至少一个文件组或日志文件的运行状态是使用不足，并且没有运行状态是使用过度。  
  
-   红色向上箭头 - 至少一个文件组或日志文件的运行状态是使用过度。  
  
 对于文件组和日志文件：  
  
-   绿色的选中标记 - 文件组中所有文件的文件空间使用率是既没有使用过度，也没有使用不足。  
  
-   绿色向下箭头 - 文件组中至少一个文件的文件空间使用率是使用不足，并且文件组中没有文件被使用过度。  
  
-   红色向上箭头 - 文件组中所有数据文件的文件空间使用率被使用过度。  
  
 若要按卷查看文件，请在 **“文件分组依据:”** 选择中选择 **“卷”** 单选按钮。 存储使用率历史记录图形显示存储卷上所有数据文件和所有日志文件使用的文件空间。 展开树可以查看单独数据库数据文件和日志文件的详细信息。  
  
 状态图标用来为每个卷提供状态：  
  
-   绿色的选中标记 - 资源被很好地利用。  
  
-   绿色向下箭头 - 资源使用不足。  
  
-   红色向上箭头 - 资源被使用过度。  
  
 “存储使用率”选项卡上每个文件名旁边的仪表表示相对于文件的有效容量的文件所使用空间量。 仪表旁边显示的百分比值是相对于文件的有效容量的文件所使用空间量的比率。 工具提示提供的数据用于计算与有效容量相比每个卷和每个文件的百分比。  
  
 如果该文件未配置为自动增长，则有效容量是分配给该文件的空间量。 如果该文件配置为自动增长，则有效容量是当前分配给该文件的空间量与目前卷上可用空间量之和。  
  
 可为数据文件和日志文件配置存储使用率策略。 若要查看或更改文件的存储使用率策略阈值，请单击“存储使用率”窗格底部的 **“文件策略”** 链接。 若要查看或更改存储卷的存储使用率策略阈值，请单击“存储使用率”窗格底部的 **“卷策略”** 链接。  
  
 若要覆盖默认策略阈值，请单击单选按钮 **“覆盖默认策略”**，指定上限和下限值，然后单击 **“确定”**。  
  
 有关更改违反策略容限的详细信息，请参阅[减少 CPU 使用策略中的干扰（SQL Server 实用工具）](../../relational-databases/manage/reduce-noise-in-cpu-utilization-policies-sql-server-utility.md)。  
  
 “属性详细信息”选项卡  
 为 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实例列出的属性详细信息包括以下类别：  
  
-   处理器名称：  
  
-   处理器速度 (MHz)：  
  
-   处理器计数：  
  
-   物理内存 (MB)：  
  
-   操作系统版本：  
  
-   SQL Server 版本：  
  
-   SQL Server 发行版：  
  
-   群集：（True 或 False）  
  
-   备份目录：  
  
-   排序规则：  
  
-   区分大小写：（True 或 False）  
  
-   语言:  

## <a name="utility-administration-sql-server-utility"></a>实用工具管理（SQL Server 实用工具）
使用“实用工具管理”选项卡可以管理 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实用工具的策略、安全性和数据仓库设置。 有关 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实用工具概念的详细信息，请参阅 [SQL Server 实用工具功能和任务](../../relational-databases/manage/sql-server-utility-features-and-tasks.md)。  
  
### <a name="uielement-list"></a>UIElement 列表
 **“策略”选项卡** - 使用“策略”选项卡可查看或指定全局监视策略。  
  
 设置全局数据层应用程序监视策略。 若要展开此选项的值列表，请单击策略名称旁的箭头，或者单击策略标题。  
 何时应用程序会用尽处理器容量？ 若要更改此策略，请使用策略说明右侧的控件，然后单击 **“应用”**。 您还可以使用显示底部的按钮还原默认值或放弃更改。  
  
-   处理器使用率的默认最大值是 70%。  
  
-   处理器使用率的默认最小值是 0%。  
  
 何时应用程序会用尽文件空间？ 若要更改数据文件或日志文件空间使用率的策略，请使用策略说明右侧的控件，然后单击“应用” 。 您还可以使用显示底部的按钮还原默认值或放弃更改。  
  
-   文件空间使用率的默认最大值是 70%。  
  
-   文件空间使用率的默认最小值是 0%。  
  
 设置全局 SQL Server 托管实例应用程序监视策略。 若要展开此选项的值列表，请单击策略名称旁的箭头，或者单击策略标题。  
 何时 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的托管实例会用尽处理器容量？ 若要更改此策略，请使用策略说明右侧的控件，然后单击 **“应用”**。 您还可以使用显示底部的按钮还原默认值或放弃更改。  
  
-   实例处理器使用率的默认最大值是 70%。  
  
-   实例处理器使用率的默认最小值是 0%。  
  
 何时 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 计算机的托管实例会用尽处理器容量？ 若要更改此策略，请使用策略说明右侧的控件，然后单击 **“应用”**。 您还可以使用显示底部的按钮还原默认值或放弃更改。  
  
-   计算机处理器使用率的默认最大值是 70%。  
  
-   计算机处理器使用率的默认最小值是 0%。  
  
 何时 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的托管实例会用尽文件空间？ 若要更改数据文件或日志文件空间使用率的策略，请使用策略说明右侧的控件，然后单击 **“应用”**。 您还可以使用显示底部的按钮还原默认值或放弃更改。  
  
-   文件空间使用率的默认最大值是 70%。  
  
-   文件空间使用率的默认最小值是 0%。  
  
 何时 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 计算机的托管实例会用尽存储卷空间？ 若要更改此策略，请使用策略说明右侧的控件，然后单击 **“应用”**。 您还可以使用显示底部的按钮还原默认值或放弃更改。  
  
-   计算机卷空间使用率的默认最大值是 70%。  
  
-   计算机卷空间使用率的默认最小值是 0%。  
  
 减少高度易失性资源中的策略违反干扰。 若要展开此功能的控件，请单击显示右侧的向下箭头。  
 有关详细信息，请参阅[减少 CPU 使用策略中的干扰（SQL Server 实用工具）](../../relational-databases/manage/reduce-noise-in-cpu-utilization-policies-sql-server-utility.md)  
  
 
**“安全性”选项卡** - 显示有权管理 UCP 或从 UCP 进行读取的登录名。  
  
 从将添加到实用工具读取者角色的 UCP 选择登录名。  
 实用工具读取者权限允许用户帐户：  
  
-   连接到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实用工具。  
  
-   在 SSMS 的实用工具资源管理器中查看所有视点。  
  
-   在 SSMS 的实用工具资源管理器中查看“实用工具管理”节点的设置。  
  
 实用工具管理员可以将 SQL Server 的实例注册到 SQL Server 实用工具中和从 SQL Server 实用工具中删除 SQL Server 的实例，以及修改托管实例上的策略和修改 UCP 上的管理设置。  
  
 要作为实用工具管理员，您必须对 SQL Server 的实例具有 sysadmin 权限。 若要添加或更改 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] UCP 的用户帐户，请使用 SSMS 中的对象资源管理器将该用户添加到 SQL Server 的 UCP 实例的服务器登录名中。 有关详细信息，请参阅 [sp_addlogin (Transact-SQL)](../../relational-databases/system-stored-procedures/sp-addlogin-transact-sql.md)。  
  
 
“数据仓库”选项卡 - 为实用工具管理数据仓库显示配置详细信息。  
  
 数据保持期  
 针对为 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]的托管实例收集的使用率信息，指定数据保持期。 默认保持期为 1 年。 最小值为 1 个月。 支持的最长的值是 2 年。  
  
 实用工具数据仓库配置信息  
 以下配置设置在此版本的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]中不可配置：  
  
-   UMDW 名称：Sysutility_mdw_\<GUID>_DATA。  
  
-   收集组上载频率：每隔 15 分钟。  
  
 UMDW 目录是可配置的：\<System drive>:\Program Files\Microsoft SQL Server\MSSQL10_50.<UCP_Name>\MSSQL\Data\\，其中，\<System drive> 通常为 C:\ 驱动器。 日志文件 UMDW_\<GUID>_LOG 位于同一目录中。  
  
> **注意：** 可以使用 detach/attach 或 ALTER DATABASE 更改该 UMDW (sysutility_mdw) 文件位置。 我们建议使用 ALTER DATABASE。 有关详细信息，请参阅 [ALTER DATABASE (Transact-SQL)](../../t-sql/statements/alter-database-transact-sql.md)。  
  
 返回到出厂默认值  
 若要将此选项卡上的设置重置为默认值，请单击“还原默认设置”按钮，然后单击“应用”。  
 
  
## <a name="reference"></a>参考  
 [创建 SQL Server 实用工具控制点（SQL Server 实用工具）](../../relational-databases/manage/create-a-sql-server-utility-control-point-sql-server-utility.md)  
  
 [连接到 SQL Server 实用工具](../../relational-databases/manage/connect-to-a-sql-server-utility.md)  
  
 [注册 SQL Server 实例（SQL Server 实用工具）](../../relational-databases/manage/enroll-an-instance-of-sql-server-sql-server-utility.md)  
  
 [配置运行状况策略（SQL Server 实用工具）](../../relational-databases/manage/configure-health-policies-sql-server-utility.md)  
  
 [在 SQL Server 实用工具中监视 SQL Server 的实例](../../relational-databases/manage/monitor-instances-of-sql-server-in-the-sql-server-utility.md)  
  
## <a name="see-also"></a>另请参阅  
 [SQL Server 实用工具的功能和任务](../../relational-databases/manage/sql-server-utility-features-and-tasks.md)   
 [SQL Server 实用工具故障排除](http://msdn.microsoft.com/library/f5f47c2a-38ea-40f8-9767-9bc138d14453)  
  
  

