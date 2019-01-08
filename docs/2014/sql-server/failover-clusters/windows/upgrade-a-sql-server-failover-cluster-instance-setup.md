---
title: 升级 SQL Server 故障转移群集实例（安装程序）| Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
helpviewer_keywords:
- upgrading clusters
- clusters [SQL Server], upgrading
- failover clustering [SQL Server], creating clusters
- clusters [SQL Server], creating
- failover clustering [SQL Server], upgrading
ms.assetid: ea8b7d66-e5a1-402f-9928-8f7310e84f5c
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: d018fb391c7633877f985b4e5e0798bfd803a5fc
ms.sourcegitcommit: 334cae1925fa5ac6c140e0b2c38c844c477e3ffb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/13/2018
ms.locfileid: "53363709"
---
# <a name="upgrade-a-sql-server-failover-cluster-instance-setup"></a>升级 SQL Server 故障转移群集实例（安装程序）
  可以使用 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 安装向导或者命令提示符将 [!INCLUDE[ssSQL14](../../../includes/sssql14-md.md)] 故障转移群集升级为 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 故障转移群集。  
  
 在故障转移群集升级过程中，停机时间限制为故障转移时间和运行升级脚本所需的时间。 如果您遵循故障转移群集滚动升级过程，停机时间将最短。 根据您是否在故障转移群集节点上具备了所有必备组件，安装这些必备组件时可能会产生额外的停机时间。 有关如何在升级过程中尽量减少停机时间的详细信息，请参阅[最佳实践升级故障转移群集前](#BestPractices)此页上的部分。  
  
 有关如何升级的详细信息，请参阅[Supported Version and Edition Upgrades](../../../database-engine/install-windows/supported-version-and-edition-upgrades.md)并[升级到 SQL Server 2014](../../../database-engine/install-windows/upgrade-sql-server.md)。  
  
 有关命令提示符下使用情况的示例语法的详细信息，请参阅[从命令提示符安装 SQL Server 2014](../../../database-engine/install-windows/install-sql-server-from-the-command-prompt.md)。  
  
## <a name="prerequisites"></a>先决条件  
 开始之前，请仔细阅读以下重要信息：  
  
-   [安装故障转移群集前的准备工作](../install/before-installing-failover-clustering.md)  
  
-   [使用升级顾问准备升级](../../install/use-upgrade-advisor-to-prepare-for-upgrades.md)。  
  
-   [升级数据库引擎](../../../database-engine/install-windows/upgrade-database-engine.md)  
  
-   安装程序在群集化的操作系统上安装 .NET Framework 4.0。 若要最大程度地缩短任何可能的停机时间，请考虑在运行安装程序之前安装 .NET Framework 4.0。  
  
-   为了确保 Visual Studio 组件可以正确安装， [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 要求您安装更新。 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 安装程序会检查此更新是否存在，然后要求您先下载并安装此更新，接下来才能继续 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 安装。 若要避免在 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 安装期间中断，可在运行 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 安装程序之前先按下面所述下载并安装此更新（或安装 Windows Update 上提供的 .NET 3.5 SP1 的所有更新）：  
  
     如果您在安装[!INCLUDE[ssSQL14](../../../includes/sssql14-md.md)]在使用 Windows Server 2008 SP2 操作系统的计算机，您可以从所需的更新[此处](https://go.microsoft.com/fwlink/?LinkId=198093)  
  
     如果您在使用 [!INCLUDE[ssSQL14](../../../includes/sssql14-md.md)] SP1 或 [!INCLUDE[win7](../../../includes/win7-md.md)] SP1 操作系统的计算机上安装 [!INCLUDE[winserver2008r2](../../../includes/winserver2008r2-md.md)]，则已包含此更新。  
  
-   [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 安装程序不再安装 .NET Framework 3.5 SP1，但是在 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 上安装 [!INCLUDE[firstref_longhorn](../../../includes/firstref-longhorn-md.md)] 时可能需要该软件。 有关详细信息，请参阅 [!INCLUDE[ssSQL14](../../../includes/sssql14-md.md)][发行说明](https://go.microsoft.com/fwlink/?LinkId=296445)。  
  
-   对于本地安装，必须以管理员身份运行 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 安装程序。 如果从远程共享安装 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] ，则必须使用对远程共享具有读取权限的域帐户。  
  
-   若要升级的实例[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]到[!INCLUDE[ssSQL14](../../../includes/sssql14-md.md)]故障转移群集，要升级的实例必须是故障转移群集。  
  
     若要将 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 的独立实例移至 [!INCLUDE[ssSQL14](../../../includes/sssql14-md.md)] 故障转移群集，请安装新的 [!INCLUDE[ssSQL14](../../../includes/sssql14-md.md)] 故障转移群集，然后使用复制数据库向导迁移独立实例中的用户数据库。 有关详细信息，请参阅 [Use the Copy Database Wizard](../../../relational-databases/databases/use-the-copy-database-wizard.md)。  
  
## <a name="rolling-upgrades"></a>滚动升级  
 若要将 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 故障转移群集升级到 [!INCLUDE[ssSQL14](../../../includes/sssql14-md.md)]，必须从被动节点开始逐个在每个故障转移群集节点上运行具有升级操作的安装程序。 升级每个节点时，节点被放在故障转移群集的可能所有者之外。 如果发生意外故障转移，已升级的节点将不参与故障转移，直到 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 安装程序将群集资源组的所有权转移给已升级的节点。  
  
 默认情况下，安装程序自动确定发生故障后何时由已升级的节点接替工作。 这取决于故障转移群集实例中节点的总数和已经升级的节点数。 如果有一半或更多节点已经升级，则当您在下一个节点上执行升级时，如果发生故障，安装程序会让已升级的节点接替工作。 在故障转移到已升级的节点后，群集组将移至已升级的节点。 所有已升级的节点都放在可能的所有者列表中，所有尚未升级的节点都将从可能的所有者列表中删除。 升级剩余的每个节点时，节点被添加到故障转移群集的可能所有者那里。  
  
 此过程使停机时间限制为整个故障转移群集升级过程中的一次故障转移时间和数据库升级脚本执行时间。  
  
 若要控制升级过程中群集节点的故障转移行为，请从命令提示符运行升级操作，并使用 /FAILOVERCLUSTERROLLOWNERSHIP 参数。 有关详细信息，请参阅 [从命令提示符安装 SQL Server 2014](../../../database-engine/install-windows/install-sql-server-from-the-command-prompt.md)。  
  
 **请注意**单节点故障转移群集，是否[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]安装程序会使[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]资源组脱机。  
  
## <a name="considerations-when-upgrading-from-includessversion2005includesssversion2005-mdmd"></a>从 [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] 升级时的注意事项  
 如果为群集安全策略指定了域组，则不能在 [!INCLUDE[nextref_longhorn](../../../includes/nextref-longhorn-md.md)] 上指定服务 SID。 如果要使用服务 SID，则需要执行并行升级。  
  
 选择[!INCLUDE[ssDE](../../../includes/ssde-md.md)]进行升级时，无论是否在 [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] 中安装了全文搜索，安装程序中都将包括全文搜索。  
  
 如果在 [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] 中启用了全文搜索，则安装程序将重新生成全文搜索目录，而与有哪些可用的选项无关。  
  
## <a name="upgrading-to-a-includesssql14includessssql14-mdmd-multi-subnet-failover-cluster"></a>升级到 [!INCLUDE[ssSQL14](../../../includes/sssql14-md.md)] 多子网故障转移群集  
 有两个可能的升级方案：  
  
1.  [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 故障转移群集当前在单个子网配置：你必须首先将现有群集升级到 [!INCLUDE[ssSQL14](../../../includes/sssql14-md.md)]，方法是启动安装程序，然后按照升级过程进行操作。 完成现有故障转移群集的升级后，使用 AddNode 功能添加位于不同子网的节点。 确认在群集网络配置页将 IP 地址资源依赖关系更改为 OR。 您现在有了一个 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 多子网故障转移群集。  
  
2.  [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 故障转移群集当前使用拉伸 V-LAN 技术在多个子网上配置：你必须首先将现有群集升级到 [!INCLUDE[ssSQL14](../../../includes/sssql14-md.md)]。 由于拉伸 V-LAN 技术配置单个子网，因此必须将网络配置更改为多个子网，使用 Windows 故障转移群集管理工具更改 IP 地址资源依赖关系，将 IP 依赖关系更改为 OR。  
  
###  <a name="BestPractices"></a> 升级前的最佳做法[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]故障转移群集  
 若要避免出现由于重新启动而产生的意外停机时间，在群集节点上运行升级之前，请在所有故障转移群集节点上预安装 .NET Framework 4.0 的不重新引导包。 建议使用以下步骤预安装必备组件：  
  
-   安装 .NET Framework 4.0 的不重新引导包，从被动节点开始仅升级共享组件。 这将安装 [!INCLUDE[dnprdnshort](../../../includes/dnprdnshort-md.md)] 4.0、Windows Installer 4.5 和 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 支持文件。  
  
-   重新启动一次或多次（根据需要）。  
  
-   将故障转移到已升级的节点。  
  
-   在剩余的最后一个节点上升级共享组件。  
  
 在所有共享组件都已升级且必备组件都已安装后，开始故障转移群集升级过程。 必须在每个故障转移群集节点上运行升级，首先从被动节点开始并向着拥有群集资源组的节点进行。  
  
-   不能向现有故障转移群集中添加功能。  
  
-   仅允许在某些方案中更改故障转移群集的版本。 有关详细信息，请参阅 [支持的版本升级](../../../database-engine/install-windows/supported-version-and-edition-upgrades.md)。  
  
##  <a name="UpgradeSteps"></a> 升级 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 故障转移群集  
  
#### <a name="to-upgrade-a-includessnoversionincludesssnoversion-mdmd-failover-cluster"></a>升级 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 故障转移群集  
  
1.  插入 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 安装介质，然后双击根文件夹中的 Setup.exe。 若要从网络共享进行安装，请移动到共享中的根文件夹，然后双击 Setup.exe。 如果之前未安装必备组件，可能会要求您安装它们。  
  
2.  > [!IMPORTANT]  
    >  步骤 3 和 4 的详细信息，请参阅[最佳实践升级故障转移群集前](#BestPractices)部分。  
  
3.  必备组件安装完成后，安装向导会启动 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 安装中心。 若要升级的现有实例[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]，单击**从升级[!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)]， [!INCLUDE[ssKatmai](../../../includes/sskatmai-md.md)]， [!INCLUDE[ssKilimanjaro](../../../includes/sskilimanjaro-md.md)]，或[!INCLUDE[ssSQL11](../../../includes/sssql11-md.md)]。**  
  
4.  如果需要使用安装程序支持文件， [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 安装程序将安装它们。 如果安装程序指示您重新启动计算机，请在继续操作之前重新启动。  
  
5.  系统配置检查器将在您的计算机上运行发现操作。 若要继续， [!INCLUDE[clickOK](../../../includes/clickok-md.md)]。  
  
6.  在“产品密钥”页上输入与旧产品版本匹配的新版本的 PID 密钥。 例如，若要升级 Enterprise 故障转移群集，必须提供 [!INCLUDE[ssEnterprise](../../../includes/ssenterprise-md.md)]的 PID 密钥。 单击 **“下一步”** 继续。 请注意，对于同一 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 实例中的所有故障转移群集节点，用于故障转移群集升级的 PID 密钥必须一致。 有关详细信息，请参阅[各版本和 SQL Server 2014 的组件](../../editions-and-components-of-sql-server-2016.md)并[Supported Version and Edition Upgrades](../../../database-engine/install-windows/supported-version-and-edition-upgrades.md)。  
  
7.  在“许可条款”页上阅读许可协议，然后选中相应的复选框以接受许可条款和条件。 为了帮助改进 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]，您还可以启用功能使用情况选项并将报告发送给 [!INCLUDE[msCoName](../../../includes/msconame-md.md)]。 单击 **“下一步”** 继续。 若要结束安装程序，请单击 **“取消”**。  
  
8.  在“选择实例”页上指定要升级到 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 的 [!INCLUDE[ssSQL14](../../../includes/sssql14-md.md)]实例。 单击 **“下一步”** 继续。  
  
9. 在“功能选择”页上会预先选择要升级的功能。 选择功能名称后，右侧窗格中会显示每个组件组的说明。 请注意，您不能更改要升级的功能，并且不能在升级操作过程中添加功能。 若要将功能添加到已升级的实例[!INCLUDE[ssSQL14](../../../includes/sssql14-md.md)]升级操作完成后，请参阅[到 SQL Server 2014 实例添加功能&#40;安装&#41;](../../../database-engine/install-windows/add-features-to-an-instance-of-sql-server-setup.md)。  
  
     在右侧窗格中显示所选功能的必备组件。 SQL Server 安装程序将在本过程后面所述的安装步骤中安装尚未安装的必备组件。  
  
10. 在“实例配置”页上，那些字段自动从旧实例进行填充。 您可以选择指定新的 InstanceID 值。  
  
     **实例 ID** - 默认情况下，实例名称用作实例 ID。 这用于标识 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]实例的安装目录和注册表项。 默认实例和命名实例的默认方式都是如此。 对于默认实例，实例名称和实例 ID 为 MSSQLSERVER。 若要使用非默认的实例 ID，请选中 **“实例 ID”** 复选框，并提供一个值。 如果覆盖默认值，则必须为所有故障转移群集节点上要升级的实例指定相同的实例 ID。 已升级的实例的实例 ID 必须在所有节点上匹配。  
  
     **检测到的实例和功能**-该网格将显示的实例[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]上运行安装程序的计算机。 单击 **“下一步”** 继续。  
  
11. “磁盘空间要求”页计算指定的功能所需的磁盘空间，并将磁盘空间要求与正在运行安装程序的计算机上的可用磁盘空间进行比较。  
  
12. 在“全文搜索升级”页上为所升级的数据库指定升级选项。 有关详细信息，请参阅 [全文搜索升级选项](../../install/full-text-search-upgrade-options.md)。  
  
13. 在 **“错误报告”** 页上，指定要发送到 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] 以帮助改进 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]的信息。 默认情况下，将启用用于错误报告的选项。  
  
14. 在升级操作开始之前，系统配置检查器将运行多组规则来针对您指定的 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 功能验证您的计算机配置。  
  
15. “群集升级报告”页显示故障转移群集实例中的节点列表和每个节点上的 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 组件的实例版本信息。 它显示数据库脚本状态和复制脚本状态。 此外，还会显示有关单击 **“下一步”** 时会发生的情况的信息性消息。 具体取决于已升级，而总的节点的故障转移群集节点数量，安装程序将显示当您单击时，会发生情况的故障转移行为**下一步**。 如果您尚未安装必备组件，还会就潜在的不必要停机时间向您发出警告。  
  
16. “准备升级”页显示您在安装过程中指定的安装选项的树视图。 若要继续，请单击 **“升级”**。 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 安装程序将首先安装所选功能的必备组件，然后安装所选功能。  
  
17. 在升级过程中，“进度”页会提供相应的状态，因此您可以在安装程序进行的过程中监视当前节点上的升级进度。  
  
18. 完成当前节点的升级后，“群集升级报告”页将显示所有故障转移群集节点的升级状态信息、每个故障转移群集节点上的功能及其版本信息。 确认显示的版本信息正确，然后继续对剩余节点进行升级。 如果发生了向已升级的节点进行的故障转移，则也会显示在状态页上。 您还可以登入 Windows 群集管理员工具以进行确认。  
  
19. 升级完成后，“完成”页会提供指向安装摘要日志文件以及其他重要说明的链接。 若要完成 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 安装过程，请单击 **“关闭”**。  
  
20. 如果安装程序指示您重新启动计算机，请立即重新启动。 安装完成后，请务必阅读来自安装向导的消息。 有关安装程序日志文件的详细信息，请参阅 [查看和阅读 SQL Server 安装程序日志文件](../../../database-engine/install-windows/view-and-read-sql-server-setup-log-files.md)。  
  
21. 若要完成升级过程，请在 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 故障转移群集的所有其他节点上重复步骤 1 到步骤 21。  
  
## <a name="to-upgrade-a-includessnoversionincludesssnoversion-mdmd-multi-subnet-failover-cluster"></a>升级 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 多子网故障转移群集  
  
#### <a name="to-upgrade-to-a-includessnoversionincludesssnoversion-mdmd-multi-subnet-failover-cluster-existing-includessnoversionincludesssnoversion-mdmd-cluster-is-a-non-multi-subnet-cluster"></a>升级到 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 多子网故障转移群集（现有 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 群集是非多子网群集）。  
  
1.  执行步骤 1 至 24 中所述[SQL Server 故障转移群集升级](#UpgradeSteps)将群集升级到上一节[!INCLUDE[ssSQL14](../../../includes/sssql14-md.md)]。  
  
2.  使用 AddNode 安装程序操作添加不同子网上的节点，并确认在 **“群集网络配置”** 页将 IP 地址资源依赖关系更改为 OR。 有关详细信息，请参阅[在 SQL Server 故障转移群集中添加或删除节点（安装程序）](../install/add-or-remove-nodes-in-a-sql-server-failover-cluster-setup.md)。  
  
#### <a name="to-upgrade-a-multi-subnet-cluster-currently-using-stretch-v-lan"></a>当前使用拉伸 V-LAN 升级多子网群集。  
  
1.  执行步骤 1 至 24 中所述[SQL Server 故障转移群集升级](#UpgradeSteps)将群集升级到上一节[!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)]。  
  
2.  更改网络设置以将远程节点移到不同的子网。  
  
3.  使用 Windows 故障转移群集管理工具添加新子网的新 IP 地址，将 IP 地址资源依赖关系设置为 OR。  
  
## <a name="next-steps"></a>后续步骤  
 升级到 [!INCLUDE[ssSQL14](../../../includes/sssql14-md.md)]后，请完成下列任务：  
  
-   注册服务器  
  
     升级会删除早期的 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 实例的注册表设置。 升级之后，必须重新注册服务器。  
  
-   更新统计信息  
  
     建议您在升级之后对所有数据库更新统计信息，以便优化查询性能。 使用 **sp_updatestats** 存储过程可以更新 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 数据库中用户定义的表中的统计信息。  
  
-   [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]配置新安装的   
  
     为了减少系统的可攻击外围应用， [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 有选择地安装和启用了一些关键服务和功能。 有关外围应用配置器工具的详细信息，请参阅此版本的自述文件。  
  
## <a name="see-also"></a>请参阅  
 [从命令提示符安装 SQL Server 2014](../../../database-engine/install-windows/install-sql-server-from-the-command-prompt.md)   
 [查看和读取 SQL Server 安装程序日志文件](../../../database-engine/install-windows/view-and-read-sql-server-setup-log-files.md)  
  
  
