---
title: 部署数据层应用程序详细信息 （SQL Server 实用工具） |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
f1_keywords:
- SQL12.SWB.UE.dac.details.F1
helpviewer_keywords:
- utility, management
- Utility
- SQL Server Utility [SQL Server]
- data-tier application [SQL Server], utility details
- Multi-server management [SQL Server]
ms.assetid: 79c41dd9-abcb-434e-9326-00a341d5c867
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: eb7b23b6ff9bf81d9c156f52dd93797203c1161f
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/02/2018
ms.locfileid: "48073289"
---
# <a name="deployed-data-tier-application-details-sql-server-utility"></a>已部署的数据层应用程序详细信息（SQL Server 实用工具）
  实用工具资源管理器的“已部署的数据层应用程序”视图中的信息为单独的数据层应用程序提供使用率数据、CPU 使用率历史数据、文件级别的存储使用率详细信息，并且提供查看和更新策略阈值的能力。 可以在数据层应用程序级别为 CPU 使用率以及数据库数据文件和日志文件控制策略阈值。 您还可以查看各数据层应用程序的属性详细信息。  
  
## <a name="uielement-list"></a>UIElement 列表  
 列表视图  
 顶部窗格中的列表视图显示与单独的数据层应用程序有关的数据。 运行状态图标按使用率类别为各数据层应用程序提供摘要状态：  
  
-   绿色的选中标记 - ![](../../2014/database-engine/media/well-utilized.gif "Well_utilized") - 没有违反资源使用策略的数据层应用程序的数目。 资源得到很好地利用。  
  
-   绿色向下箭头 - ![](../../2014/database-engine/media/utility-down-arrow.gif "Utility_down_arrow") - 资源未充分利用。  
  
-   红色向上箭头 - ![](../../2014/database-engine/media/utility-up-arrow.gif "Utility_up_arrow") - 资源过度利用。  
  
 可以通过将列表视图中的列向左或向右拖动，更改这些列在列表视图中的顺序。 可通过右键单击列标题并选择或取消选择列，添加或删除列表视图中的列。 右键单击菜单还提供了排序选项。 还可以通过单击列名称的顶部激活排序。  
  
 若要访问 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 实用工具列表视图的筛选器选项，请右键单击实用工具资源管理器导航窗格中的“已部署的数据层应用程序”节点，然后选择“筛选器”。 实现筛选设置后，实用工具资源管理器中的“已部署的数据层应用程序”节点将标记为“已部署的数据层应用程序 (已筛选)”。 有关详细信息，请参阅[筛选设置（对象资源管理器和实用工具资源管理器）](../ssms/object/filter-settings-object-explorer-and-utility-explorer.md)。  
  
 默认情况下，下面的列将显示与每个数据层应用程序有关的运行状态信息。  
  
-   名称 - 数据层应用程序名称。  
  
-   应用程序 CPU - 显示此数据层应用程序的处理器使用率的运行状态。 根据为数据层应用程序设置的 CPU 使用策略以及易失性资源评估策略的配置设置，确定此参数的运行状态。 有关详细信息，请参阅[减少 CPU 使用策略中的干扰（SQL Server 实用工具）](../relational-databases/manage/reduce-noise-in-cpu-utilization-policies-sql-server-utility.md)。  
  
     若要查看此数据层应用程序的处理器使用率历史记录，或者查看或更改策略限制，请单击“CPU 使用率”选项卡。  
  
-   计算机 CPU - 显示计算机处理器使用率的运行状态。 根据为计算机设置的 CPU 使用策略以及易失性资源评估策略的配置设置，确定此参数的运行状态。 有关详细信息，请参阅[减少 CPU 使用策略中的干扰（SQL Server 实用工具）](../relational-databases/manage/reduce-noise-in-cpu-utilization-policies-sql-server-utility.md)。  
  
     若要查看此数据层应用程序的处理器使用率历史记录，或者查看或更改策略限制，请单击“CPU 使用率”选项卡。  
  
-   文件空间 - 为每个数据层应用程序显示文件空间使用率的运行状态的摘要。  
  
    -   绿色的选中标记 - 所有文件组和日志文件组的运行状态是既没有使用过度，也没有使用不足。  
  
    -   绿色向下箭头 - 至少一个文件组或日志文件组的运行状态是使用不足，并且没有文件组或日志文件组被使用过度。  
  
    -   红色向上箭头 - 至少一个文件组或日志文件组的运行状态是使用过度。 注意，如果数据库处于“紧急”状态，则运行状态将显示日志文件空间使用过度。  
  
     若要查看或更改文件空间策略限制，请单击 **“存储使用率”** 选项卡。  
  
-   卷空间 - 为包含属于所选数据层应用程序的数据库的所有卷显示卷空间使用率的运行状态的摘要。 如果任何卷的运行状态为使用过度，则卷运行状态将在此列表视图中报告为使用过度。 如果任何卷的运行状态为使用不足，并且没有卷被使用过度，则卷空间运行状态将在此列表视图中报告为使用不足。 否则，卷空间运行状态将在列表视图中报告为很好地利用。 若要查看或更改策略限制，请单击 **“存储使用率”** 选项卡。  
  
-   策略类型 - 指示对于数据层应用程序，“全局”默认策略或“覆盖”自定义策略是否有效。  
  
-   实例名称 - 显示承载数据层应用程序的 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 实例的名称。  
  
 可以在列表视图的列标题区域中使用右键单击菜单显示的其他列：  
  
-   数据库名称  
  
-   部署日期  
  
-   可信：（True 或 False）  
  
-   排序规则  
  
-   兼容级别：（例如 Version100）  
  
-   启用加密：（True 或 False）  
  
-   恢复模式：（简单、完全或大容量日志记录）  
  
-   上次报告的时间：此列使用 datetime 数据类型显示 UCP 本地日期和时间。 有关详细信息，请参阅 SQL Server 联机丛书中的 [datetime (Transact-SQL)](http://go.microsoft.com/fwlink/?LinkId=164071) 主题。 在使用实用工具对象模型时，请注意 SSMS 使用 datetimeoffset 数据类型。 有关详细信息，请参阅 SQL Server 联机丛书中的 [datetimeoffset (Transact-SQL)](http://go.microsoft.com/fwlink/?LinkId=141713) 主题。  
  
 “CPU 使用率”选项卡  
 “CPU 使用率”选项卡为数据层应用程序和计算机 CPU 使用率显示历史数据的并排图形。  
  
 该图形按照显示区域右侧的单选按钮中指定的间隔显示处理器使用率历史记录。 若要更改显示间隔和刷新数据集，请从列表中选择一个单选按钮。  
  
 间隔选项如下所示：  
  
-   1 天，以 15 分钟间隔显示。  
  
-   1 周，以 1 天间隔显示。  
  
-   1 个月，以 1 周间隔显示。  
  
-   1 年，以 1 个月间隔显示。  
  
 “存储使用率”选项卡  
 “存储使用率”选项卡具有一个树视图，它显示属于列表视图中选定数据层应用程序的数据库文件和日志文件的存储使用率详细信息。 请注意，时间数据使用 datetime 数据类型显示 UCP 本地日期和时间。 有关详细信息，请参阅 SQL Server 联机丛书中的 [datetime (Transact-SQL)](http://go.microsoft.com/fwlink/?LinkId=164071) 主题。 在使用实用工具对象模型时，请注意 SSMS 使用 datetimeoffset 数据类型。 有关详细信息，请参阅 SQL Server 联机丛书中的 [datetimeoffset (Transact-SQL)](http://go.microsoft.com/fwlink/?LinkId=141713) 主题。  
  
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
  
 有关更改违反策略容限的详细信息，请参阅[减少 CPU 使用策略中的干扰（SQL Server 实用工具）](../relational-databases/manage/reduce-noise-in-cpu-utilization-policies-sql-server-utility.md)。  
  
 “属性详细信息”选项卡  
 为数据层应用程序列出的属性详细信息包括以下类别：  
  
-   数据库名称  
  
-   部署日期  
  
-   可信：（True 或 False）  
  
-   排序规则  
  
-   兼容级别：（例如 Version100）  
  
-   启用加密：（True 或 False）  
  
-   恢复模式：（简单、完全或大容量日志记录）  
  
-   上次报告的时间：此列使用 datetime 数据类型显示 UCP 本地日期和时间。 有关详细信息，请参阅 SQL Server 联机丛书中的 [datetime (Transact-SQL)](http://go.microsoft.com/fwlink/?LinkId=164071) 主题。 在使用实用工具对象模型时，请注意 SSMS 使用 datetimeoffset 数据类型。 有关详细信息，请参阅 SQL Server 联机丛书中的 [datetimeoffset (Transact-SQL)](http://go.microsoft.com/fwlink/?LinkId=141713) 主题。  
  
## <a name="see-also"></a>请参阅  
 [托管实例详细信息（SQL Server 实用工具）](../../2014/database-engine/managed-instance-details-sql-server-utility.md)   
 [实用工具仪表板&#40;SQL Server 实用工具&#41;](../../2014/database-engine/utility-dashboard-sql-server-utility.md)   
 [在 SQL Server 实用工具中监视 SQL Server 的实例](../relational-databases/manage/monitor-instances-of-sql-server-in-the-sql-server-utility.md)   
 [SQL Server 实用工具功能和任务](../relational-databases/manage/sql-server-utility-features-and-tasks.md)  
  
  
