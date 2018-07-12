---
title: 概述 SQL Server 服务安装 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: 6a9fd19b-2367-4908-b638-363b1e929e1e
caps.latest.revision: 29
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 7906a576bab6ad6dd35da0f863a20ad02e56d342
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/02/2018
ms.locfileid: "37230149"
---
# <a name="overview-of-sql-server-servicing-installation"></a>SQL Server 服务安装概述
  您可以利用 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 服务更新将更新应用到任何已安装的 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 组件。 如果现有 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 组件的版本级别高于更新版本的级别，则安装程序会将其从更新中排除。 更新应用服务的详细信息，请参阅[安装 SQL Server 2014 服务更新](../../database-engine/install-windows/install-sql-server-servicing-updates.md)。  
  
 安装 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 更新时需要注意以下注意事项：  
  
-   必须同时更新属于一个 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实例的所有功能。 例如，更新 [!INCLUDE[ssDE](../../includes/ssde-md.md)]时，如果 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 组件和 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 组件作为同一个 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]实例的一部分安装，则也必须对其进行更新。 共享功能，如管理工具[!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]，并[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]，必须始终更新到最新状态。 如果未在功能树中选定某个组件或实例，则不会更新该组件或实例。  
  
-   默认情况下[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]更新日志文件保存到 %Program Files %\\[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]\120\Setup Bootstrap\LOG\\。  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 安装程序现在可以将更新与原始介质集成，以便同时运行原始介质和更新。 有关详细信息，请参阅[What's New in SQL Server 安装](../../../2014/sql-server/install/what-s-new-in-sql-server-installation.md)。  
  
-   建议您先备份您的数据，然后再应用 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 服务更新。  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 更新可通过 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 获得。 我们建议您定期扫描更新，以便将 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实例保持为最新并确保其安全。 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] SP1 将作为完整 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 安装提供。 对于此版本，没有在标准修补程序可执行文件包中提供 Service Pack 以应用到 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] RTM 实例，而是提供安装包（包含 2 个文件）。 执行时，将安装预安装 SP1 的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 新实例。  
  
## <a name="requirements-and-known-issues"></a>要求和已知问题  
 推荐的磁盘空间要求约为软件包的 2.5 倍，以便安装、下载和解压缩该软件包。 安装完 Service Pack 后，可以删除下载的软件包。 所有临时文件将会自动删除。  
  
 **查看已知问题：** 有关当前版本的已知问题的详细信息，请参阅此处相应的发行说明主题： [SQL Server 发行说明](http://msdn.microsoft.com/en-us/f617a0af-92dd-47aa-82c3-f51b1346bcd8)。  
  
## <a name="installation-overview"></a>安装概述  
 本节讨论如何安装 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 累积更新和 Service Pack，包括如何执行以下操作：  
  
-   准备安装 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 更新  
  
-   安装 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 更新  
  
-   重新启动服务和应用程序  
  
### <a name="prepare-for-a-includesscurrentincludessscurrent-mdmd-update-installation"></a>准备安装 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 更新  
 强烈建议在安装 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 更新之前执行以下操作：  
  
-   **备份你[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]系统数据库**-在安装之前[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]更新，备份会`master`， `msdb`，并`model`数据库。 安装 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 更新会更改这些数据库，使它们与 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 的早期版本不兼容。 如果决定重新安装 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] （不包含这些更新），则需要使用这些数据库的备份。  
  
     出于谨慎起见，还应备份用户数据库。  
  
    > [!IMPORTANT]  
    >  将更新应用于参与复制拓扑的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实例时，必须在应用更新之前，将复制的数据库与系统数据库一起备份。  
  
-   **备份 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 数据库、配置文件和存储库** - 更新 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 实例之前，应备份以下内容：  
  
    -   [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 数据库。 默认情况下，这些安装在 C:\Program Files\\[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]\MSAS12。\<InstanceID > \OLAP\Data\\。 对于 WOW 安装，默认路径为 C:\ProgramFiles (x86) \ [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]\MSAS12。\<InstanceID > \OLAP\Data\\。  
  
    -   [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] msmdsrv.ini 配置文件中的配置设置。 默认情况下，该文件位于 C:\Program Files\\[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]\MSAS12。\<InstanceID > \OLAP\Config\ 目录。  
  
    -   （可选）包含 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 存储库的数据库。 仅当已将 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 配置为与决策支持对象 (DSO) 库一起使用后，才需要执行此步骤。  
  
    > [!NOTE]  
    >  如果备份 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 数据库、配置文件和存储库失败，则无法将更新后的 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 实例恢复到早期版本。  
  
-   **验证系统数据库有足够的可用空间**— 如果没有选择自动增长选项`master`和`msdb`系统数据库，每个数据库必须至少具有 500 KB 的可用空间。 若要验证数据库是否有足够的空间，请对 `sp_spaceused` 和 `master` 数据库运行 `msdb` 系统存储过程。 如果其中任一数据库的未分配空间少于 500 KB，则应增加该数据库的大小。  
  
-   **停止服务和应用程序** — 为避免系统可能重启，请在安装 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 更新前，停止与要升级的 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 实例连接的所有应用程序和服务。 其中包括 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]和 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]。 有关详细信息，请参阅 [启动、停止、暂停、继续、重新启动数据库引擎、SQL Server 代理或 SQL Server Browser 服务](../../database-engine/configure-windows/start-stop-pause-resume-restart-sql-server-services.md)。  
  
    > [!NOTE]  
    >  不能停止故障转移群集环境中的服务。 有关详细信息，请参阅本主题后面的故障转移群集安装一节。  
  
-   为了使更新安装后无需重新启动计算机，安装程序将显示锁定文件的进程列表。 如果更新安装程序必须在安装过程中结束某个服务，它将在安装完成后重新启动该服务。  
  
-   如果安装程序确定在安装过程中文件已被锁定，则在安装完成后可能需要重新启动计算机。 如有必要，安装程序将提示您重新启动计算机。  
  
### <a name="install-includesscurrentincludessscurrent-mdmd-updates"></a>安装 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 更新  
 本节介绍安装过程。  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 必须安装其中的计算机具有管理权限的帐户下安装更新。 对于本地安装，必须以管理员身份运行安装程序。 如果从远程共享安装 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ，则必须使用对远程共享具有读取和执行权限的域帐户。  
  
#### <a name="starting-a-includesscurrentincludessscurrent-mdmd-update"></a>启动 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 更新  
 若要安装 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 更新，请运行自解压缩包文件。  
  
 累积更新包 (CU): \<SQLServer2014 >-KBxxxxxx-*PPP*.exe  
  
 Service pack 包 (PCU): \<SQLServer2014 >\<SPx >-KBxxxxxx-PPP LLL.exe  
  
-   x 表示 Service Pack 编号  
  
-   PPP 表示特定的平台。  
  
-   LLL 表示 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 语言的字符缩写形式，例如：英语的 LLL 为 ENU。  
  
 若要将更新应用于故障转移群集中的 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 组件，请参阅故障转移群集安装的相关章节。 有关如何在无人参与模式下运行更新安装的详细信息，请参阅[从命令提示符安装 SQL Server 2014](../../database-engine/install-windows/install-sql-server-from-the-command-prompt.md)。  
  
####  <a name="Slipstream"></a> 中的产品更新[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]安装  
 产品更新是 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 安装程序中的一项功能。 该安装程序可以将最新的产品更新与主产品安装相集成，以便可以同时安装主产品及其适用的更新。 产品更新可以搜索 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Update、Windows Server Update Services (WSUS)、本地文件夹或网络共享以获取适用的更新。  在找到最新版本的适用更新后，安装程序将下载这些更新并将其与当前的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 安装过程集成在一起。 产品更新可请求累积更新、Service Pack 或者 Service Pack 连同累积更新。 产品更新功能是已在 [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] PCU1 中提供的 Slipstream 功能的扩展。  
  
## <a name="updating-a-prepared-image-of-includessnoversionincludesssnoversion-mdmd"></a>更新已准备的映像 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]  
 可以在未完成已准备实例配置的情况下，将更新应用到未配置的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的已准备实例。 下面介绍将更新应用到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的已准备实例的不同方法：  
  
-   更新先前准备的实例 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]  
  
     可在配置之前应用已准备实例的更新。 该更新包检测实例是否处于已准备状态并将修补程序应用到已准备的实例，但不完成配置。  
  
-   通过 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Update 更新已准备实例：  
  
     可以通过 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Update 将更新应用到 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 的已准备实例。 该 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Update 包将检测实例是否处于已准备状态并将修补程序应用到已准备的实例，但不完成配置。  
  
 如果要更新 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]的已准备映像，则需要指定 InstanceID 参数。 有关详细信息和语法示例，请参阅 [Installing Updates from the Command Prompt](../../database-engine/install-windows/installing-updates-from-the-command-prompt.md)。  
  
## <a name="updating-a-completed-image-of-includessnoversionincludesssnoversion-mdmd"></a>更新 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的已完成映像  
 更新 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的已完成和已配置实例的过程与更新任何其他 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]已安装实例的过程相同。  
  
## <a name="rebuilding-a-includesscurrentincludessscurrent-mdmd-failover-cluster-node"></a>重新生成 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 故障转移群集节点  
 应用更新之后，如果必须重新生成故障转移群集中的某个节点，请执行以下步骤：  
  
1.  在故障转移群集中重新生成该节点。 有关重新生成节点的详细信息，请参阅 [Recover from Failover Cluster Instance Failure](../failover-clusters/windows/recover-from-failover-cluster-instance-failure.md)。  
  
2.  运行原始的 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 安装程序，将 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 安装在故障转移群集节点上。  
  
3.  在添加的节点上运行 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 更新安装程序。  
  
## <a name="restart-services-and-applications"></a>重新启动服务和应用程序  
 安装程序完成后，系统可能会提示您重新启动计算机。 系统重新启动后，或者安装程序完成但未要求重新启动，请使用“控制面板”中的 **“服务”** 节点重新启动在应用 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 更新之前停止的服务。 其中包括像分布式事务处理协调器和 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Search 这样的服务，或实例特定的同等服务。  
  
 重新启动在运行 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 更新安装程序之前关闭的应用程序。 成功安装后，可能还需要立即对升级后的 `master`、`msdb` 和 `model` 数据库再进行一次备份。  
  
## <a name="uninstalling-updates-from-includesscurrentincludessscurrent-mdmd"></a>卸载更新 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]  
 可以使用“控制面板”中的 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] “程序和功能” **卸载** 累积更新或 Service Pack。 要查看已安装的更新列表，请通过依次单击 **“开始”** 按钮、 **“控制面板”**、 **“程序”**，然后在 **“程序和功能”** 下单击 **“查看已安装的更新”**，打开“已安装的更新”。 每个累积更新是分别列出的。 但是，如果安装的 Service Pack 版本高于累积更新，累积更新条目将会隐藏起来，并且仅在卸载了 Service Pack 后才会显示出来。  
  
 若要卸载任何 Service Pack 和更新，必须按先新后旧顺序，先卸载应用于 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实例的最新更新或 Service Pack。 在下面的每个示例中，卸载完其他 Service Pack 或更新之后，最后剩下的都是 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 累积更新 1：  
  
-   对于安装有累积更新 1 和 SP1 的 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 实例，先卸载 SP1。  
  
-   对于安装有累积更新 1、SP1 和累积更新 2 的 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 实例，先卸载累积更新 2，然后卸载 SP1。  
  
## <a name="see-also"></a>请参阅  
 [从命令提示符安装 SQL Server 2014](../../database-engine/install-windows/install-sql-server-from-the-command-prompt.md)   
 [安装 SQL Server 2014 服务更新](../../database-engine/install-windows/install-sql-server-servicing-updates.md)   
 [验证 SQL Server 安装](../../database-engine/install-windows/validate-a-sql-server-installation.md)   
 [查看和读取 SQL Server 安装程序日志文件](../../database-engine/install-windows/view-and-read-sql-server-setup-log-files.md)  
  
  
