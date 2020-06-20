---
title: 托管实例详细信息（SQL Server 实用工具） |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
ms.assetid: 6e51b7bb-a733-4852-8c33-7f4dbdf931c2
author: mashamsft
ms.author: mathoma
ms.openlocfilehash: edd9853a68fd86481e32cfa9dee69b0be8b577a7
ms.sourcegitcommit: 9ee72c507ab447ac69014a7eea4e43523a0a3ec4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/17/2020
ms.locfileid: "84930909"
---
# <a name="managed-instance-details-sql-server-utility"></a>托管实例详细信息（SQL Server 实用工具）
  实用工具资源管理器的“托管实例”视图中的信息为 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]的单独实例提供使用率数据、CPU 使用率历史记录、文件级别的存储使用率详细信息，并且提供查看和更新策略阈值的能力。 对于计算机，可以在 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 实例级别控制策略阈值；对于数据库文件和日志文件，可以在存储卷的级别控制策略阈值。 您还可以查看 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]的各个托管实例的属性详细信息。  
  
## <a name="ui-element-list"></a>UI 元素列表  
 “列表”视图  
 顶部窗格中的列表视图可以显示行中按 ComputerName\InstanceName 列出的各 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 实例的有关数据。  
  
 运行状态图标按使用率类别为 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 的各实例提供摘要状态：  
  
-   绿色的选中标记 - ![](../../2014/database-engine/media/well-utilized.gif "Well_utilized") - 没有违反资源使用策略的 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 托管实例的数目。 资源得到很好地利用。  
  
-   绿色向下箭头 - ![](../../2014/database-engine/media/utility-down-arrow.gif "Utility_down_arrow") - 资源使用不足。  
  
-   红色向上箭头 - ![](../../2014/database-engine/media/utility-up-arrow.gif "Utility_up_arrow") - 资源使用过度。  
  
 可以通过将列表视图中的列向左或向右拖动，更改这些列在列表视图中的顺序。 可通过右键单击列标题并选择或取消选择列，添加或删除列表视图中的列。 右键单击菜单还提供了排序选项。 还可以通过单击列名称的顶部激活排序。  
  
 若要访问实用工具列表视图的筛选器选项，请右键单击实用工具资源管理器导航窗格中的“托管实例”**** 节点，然后选择“筛选器”****。 在实现了筛选器设置后，实用工具资源管理器中的“托管实例”**** 节点将标有“托管实例(已筛选)”****。 有关详细信息，请参阅[筛选设置（对象资源管理器和实用工具资源管理器）](../ssms/object/filter-settings-object-explorer-and-utility-explorer.md)。  
  
 默认情况下，下面的列将显示与 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]的每个托管实例有关的运行状态信息。  
  
-   实例 CPU - 显示分配给此 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]实例的处理器使用率的运行状态。 根据为 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 的实例设置的 CPU 使用策略以及易失性资源评估策略的配置设置，确定此参数的运行状态。 有关详细信息，请参阅[减少 CPU 使用策略中的干扰（SQL Server 实用工具）](../relational-databases/manage/reduce-noise-in-cpu-utilization-policies-sql-server-utility.md)。  
  
     若要查看此 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]实例的处理器使用率历史记录，或者查看或更改策略限制，请单击 **“CPU 使用率”** 选项卡。  
  
-   计算机 CPU - 显示计算机处理器使用率的运行状态。 根据为计算机设置的 CPU 使用策略以及易失性资源评估策略的配置设置，确定此参数的运行状态。 有关详细信息，请参阅[减少 CPU 使用策略中的干扰（SQL Server 实用工具）](../relational-databases/manage/reduce-noise-in-cpu-utilization-policies-sql-server-utility.md)。  
  
     若要查看此 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]实例的处理器使用率历史记录，或者查看或更改策略限制，请单击 **“CPU 使用率”** 选项卡。  
  
-   文件空间 - 为属于所选 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]实例的所有数据库显示文件空间使用率的运行状态的摘要。 如果任何数据库的运行状态为使用过度，则文件空间运行状态将在此列表视图中报告为使用过度。 如果任何数据库的运行状态为使用不足，并且没有数据库被使用过度，则文件空间运行状态将在此列表视图中报告为使用不足。 否则，文件空间运行状态将在列表视图中报告为很好地利用。 若要查看或更改策略限制，请单击 **“存储使用率”** 选项卡。  
  
-   卷空间 - 为包含属于所选 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]实例的数据库的所有卷显示卷空间使用率的运行状态的摘要。 如果任何卷的运行状态为使用过度，则卷运行状态将在此列表视图中报告为使用过度。 如果任何卷的运行状态为使用不足，并且没有卷被使用过度，则卷空间运行状态将在此列表视图中报告为使用不足。 否则，卷空间运行状态将在列表视图中报告为很好地利用。 若要查看或更改策略限制，请单击 **“存储使用率”** 选项卡。  
  
-   策略类型 - 指示对于 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]的托管实例，“全局”默认策略或“覆盖”自定义策略是否有效。  
  
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
  
-   Language：  
  
-   上次报告的时间：此列使用 datetime 数据类型显示 UCP 本地日期和时间。 有关详细信息，请参阅 SQL Server 联机丛书中的 [datetime (Transact-SQL)](https://go.microsoft.com/fwlink/?LinkId=164071) 主题。 在使用实用工具对象模型时，请注意 SSMS 使用 datetimeoffset 数据类型。 有关详细信息，请参阅 SQL Server 联机丛书中的 [datetimeoffset (Transact-SQL)](https://go.microsoft.com/fwlink/?LinkId=141713) 主题。  
  
 “CPU 使用率”选项卡  
 “CPU 使用率”选项卡为 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 实例和计算机 CPU 使用率显示历史数据的并排图形。  
  
 该图形按照显示区域右侧的单选按钮中指定的间隔显示处理器使用率历史记录。 若要更改显示间隔和刷新数据集，请从列表中选择一个单选按钮。  
  
 间隔选项如下所示：  
  
-   1 天，以 15 分钟间隔显示。  
  
-   1 周，以 1 天间隔显示。  
  
-   1 个月，以 1 周间隔显示。  
  
-   1 年，以 1 个月间隔显示。  
  
 “存储使用率”选项卡  
 “存储使用率”选项卡具有显示存储使用率详细信息的树视图。 请注意，时间数据使用 datetime 数据类型显示 UCP 本地日期和时间。 有关详细信息，请参阅 SQL Server 联机丛书中的 [datetime (Transact-SQL)](https://go.microsoft.com/fwlink/?LinkId=164071) 主题。 在使用实用工具对象模型时，请注意 SSMS 使用 datetimeoffset 数据类型。 有关详细信息，请参阅 SQL Server 联机丛书中的 [datetimeoffset (Transact-SQL)](https://go.microsoft.com/fwlink/?LinkId=141713) 主题。  
  
 显示可按数据库或按卷分组。 若要使用数据库树视图，请在 **“文件分组依据:”** 选择中选择 **“数据库”** 单选按钮。 若要查看单独数据库文件的存储使用率状态，请单击树视图中数据库名称旁的加号。 列出的数据库文件包括属于列表视图中所选 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 的托管实例的所有系统数据库和用户数据库。  
  
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
  
 有关更改违反策略容限的详细信息，请参阅[减少 CPU 使用策略中的干扰（SQL Server 实用工具）](../relational-databases/manage/reduce-noise-in-cpu-utilization-policies-sql-server-utility.md)。  
  
 “属性详细信息”选项卡  
 为 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 实例列出的属性详细信息包括以下类别：  
  
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
  
-   Language：  
  
## <a name="see-also"></a>另请参阅  
 [已部署的数据层应用程序详细信息 &#40;SQL Server 实用工具&#41;](../../2014/database-engine/deployed-data-tier-application-details-sql-server-utility.md)   
 [实用工具仪表板 &#40;SQL Server 实用工具&#41;](../../2014/database-engine/utility-dashboard-sql-server-utility.md)   
 [监视 SQL Server 实用工具中 SQL Server 的实例](../relational-databases/manage/monitor-instances-of-sql-server-in-the-sql-server-utility.md)   
 [SQL Server 实用工具功能和任务](../relational-databases/manage/sql-server-utility-features-and-tasks.md)   
 [SQL Server 实用工具故障排除](../../2014/database-engine/troubleshoot-the-sql-server-utility.md)  
  
  
