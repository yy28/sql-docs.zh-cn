---
title: 重播跟踪的 SQL Server 升级与数据库实验助手
description: 重播跟踪与数据库实验助手
ms.custom: ''
ms.date: 10/22/2018
ms.prod: sql
ms.prod_service: dea
ms.suite: sql
ms.technology: dea
ms.tgt_pltfrm: ''
ms.topic: conceptual
author: HJToland3
ms.author: ajaykar
ms.reviewer: mathoma
manager: jroth
ms.openlocfilehash: 7db0e6a83997a3be7b204f780f3c0a7ad856b0d8
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/15/2019
ms.locfileid: "66794452"
---
# <a name="replay-a-trace-in-database-experimentation-assistant"></a>重播的跟踪将在数据库实验助手

在数据库实验助手 (DEA) 可以重播针对升级后的测试环境的捕获的跟踪文件。 例如，请考虑在 SQL Server 2008 R2 运行的生产工作负荷。 必须两次重播跟踪文件工作负荷： 具有相同版本的生产和再次升级目标 SQL Server 版本，如 SQL Server 2016 的环境上运行的 SQL Server 的环境上一次。

> [!NOTE]
> 若要运行此操作，您必须手动设置虚拟机或物理计算机以运行分布式重播跟踪。 有关详细信息，请参阅[Distributed Replay 控制器和客户端安装程序](https://blogs.msdn.microsoft.com/datamigration/distributed-replay-controller-and-client-setup/)。
>
>

## <a name="create-a-trace-replay"></a>创建跟踪重播

在 DEA，选择菜单图标。 在展开的菜单中，选择**重播跟踪**play 图标的旁边。

![在菜单中选择重播跟踪](./media/database-experimentation-assistant-replay-trace/dea-replay-trace-open.png)

> [!NOTE]
> Distributed Replay 控制器计算机需要远程连接到您使用的用户帐户的权限。
>

### <a name="grant-access-to-the-distributed-replay-controller"></a>授予对分布式重播控制器访问权限

1. 在命令提示符下输入**dcomcnfg**以打开**组件服务**接口。
1. 展开**组件服务** > **计算机** > **我的计算机** > **DCOM 配置** >  **DReplayController**。
1. 右键单击**DReplayController**，然后选择**属性**。
1. 上**安全**选项卡上，选择**编辑**若要添加的用户帐户。
1. 选择 **确定**。

### <a name="verify-setup"></a>验证设置

1.  **SQL Server 安装路径**:输入安装了 SQL Server 的路径。 例如，c:\\Program Files (x86)\\Microsoft SQL Server\\120。
1.  **控制器计算机的名称**:输入已设置为控制器的计算机的名称。 此计算机正在运行名为 SQL Server 分布式重播控制器的 Windows 服务。 Distributed Replay 控制器协调的分布式重播客户端的操作。 在每个 Distributed Replay 环境中只能有一个控制器实例。
1.  **客户端计算机名称**:输入由逗号分隔每个客户端计算机的名称。 示例： client1，客户端 2。 您可以最多五个客户端控制器。 客户端是一个或多个计算机中，物理或虚拟的该项运行名为 SQL Server Distributed Replay 客户端的 Windows 服务。 多个 Distributed Replay 客户端一起来模拟 SQL Server 实例的工作负荷。 在每个 Distributed Replay 环境中可以有一个或多个客户端。
1.  选择“**下一步**”。

### <a name="select-a-trace"></a>选择一个跟踪

1.  **跟踪文件的路径**:输入的输入的跟踪 (.trc) 文件的路径。
1.  **路径来存储 replay 预处理输出**:  
    \- 如果还没有 IRF 文件，输入你想要存储 IRF 文件的位置的路径和其他预处理输出。  
    \- 如果已有 IRF 文件，输入 IRF 文件的路径。
1. 选择“**下一步**”。

### <a name="replay-a-trace"></a>重播跟踪

1.  **跟踪文件名**:输入跟踪文件名称。
1.  **最大文件大小 (MB)** :输入跟踪文件滚动更新大小值。 默认值为 200 MB。 可以输入自定义值。
1.  **用于存储重播跟踪输出路径**:输入输出.trc 文件的路径。
1.  **SQL Server 实例名称**:输入要重播跟踪的 SQL Server 实例的名称。
1.  选择“开始”  。

如果您输入的信息是有效的启动分布式重播过程。 否则，不正确的信息文本 boses 是以红色突出显示。 请确保你输入的值是否正确，然后选择**启动**。

等待重播完成运行，以查看您指定的位置。 选择底部的左侧菜单中，若要监视重播进度的钟形图标。

![重播跟踪进度](./media/database-experimentation-assistant-replay-trace/dea-replay-trace-progress.png)

## <a name="frequently-asked-questions-about-trace-replay"></a>有关跟踪重播常见问题

### <a name="what-security-permissions-do-i-need-to-start-a-replay-capture-on-my-target-server"></a>在我的目标服务器上启动重播捕获时，需要什么安全权限？

- DEA 应用程序中运行的跟踪操作的 Windows 用户必须运行 SQL Server 的目标计算机上具有 sysadmin 权限。 这些用户权限所需启动跟踪。
- 运行 SQL Server 的目标计算机运行的服务帐户必须具有写入访问权限指定的跟踪文件路径。
- 分布式重播客户端服务所运行的服务帐户必须具有连接到运行 SQL Server 的目标计算机并执行查询的用户权限。

### <a name="can-i-start-more-than-one-replay-in-the-same-session"></a>可以在同一会话中启动多个重播？

是的可以启动多个重播，并跟踪到同一会话中完成。

### <a name="can-i-start-more-than-one-replay-in-parallel"></a>可以并行启动多个重播？

是的但不是具有相同设置在所选的计算机**控制器和客户端**。 控制器和客户端将正忙。 设置一组单独的计算机下**控制器和客户端**若要启动并行重播。

### <a name="how-long-does-a-replay-typically-take-to-finish"></a>重播通常需要多长完成？

重播通常使用的同一个用作源跟踪的时间量以及进行预处理源跟踪所需的时间量。 但是，如果向控制器注册的客户端计算机不足以管理重播从生成的负载，可能需要长时间才能完成重播。 可以向控制器注册最多 16 个客户端计算机。

### <a name="how-large-do-target-trace-files-get"></a>目标跟踪文件会有多大？

大小的源跟踪文件可能是介于 5 到 15 之间的目标跟踪倍。 文件大小取决于运行多少查询。 例如，查询计划 blob 可能较大。 如果这些查询的统计信息经常更改，会捕获更多的事件。

### <a name="why-do-i-need-to-restore-databases"></a>为什么需要还原数据库？

SQL Server 是一个有状态的关系数据库管理系统。 若要正常运行 A / B 测试，数据库的状态必须保留在所有时间。 否则，您可能不会出现在生产环境中的重播期间看到查询中的错误。 若要避免这些错误，我们建议您看前面源捕获备份。 同样，运行 SQL Server 的目标计算机上的备份时需要防止重播期间出错。

### <a name="what-does-pass--on-the-replay-page-mean"></a>什么"pass %"上的重播页平均值？

**传递 %** 仅占查询传递的方式。 您可以诊断是否预期的错误数。 可能会发生错误，或可能会发生错误，因为数据库已丢失其完整性。 如果为值**pass %** 不是你的期望，可以停止跟踪并查看在 SQL Profiler，若要查看哪些查询不成功的跟踪文件。

### <a name="how-can-i-look-at-the-trace-events-that-were-collected-during-replay"></a>如何可以查看在重播期间所收集的跟踪事件？

打开目标跟踪文件，并在 SQL Profiler 中查看它。 或者，如果你想要进行重播捕获的修改，所有 SQL Server 脚本都则可以在 c:\\Program Files (x86)\\Microsoft Corporation\\数据库实验助手\\脚本\\StartReplayCapture.sql。

### <a name="what-trace-events-does-dea-collect-during-replay"></a>DEA 重播期间 does 收集哪些跟踪事件？

DEA 捕获跟踪事件包含与性能相关的信息。 捕获配置是 StartReplayCaptureTrace.sql 脚本中。 这些事件是典型中列出的 SQL Server 跟踪事件[sp_trace_setevent (TRANSACT-SQL) 的参考文档](https://docs.microsoft.com/sql/relational-databases/system-stored-procedures/sp-trace-setevent-transact-sql)。

## <a name="troubleshoot-trace-replay"></a>跟踪重播进行故障排除

### <a name="i-cant-connect-to-the-computer-thats-running-sql-server"></a>我无法连接到运行 SQL Server 的计算机

- 确认运行 SQL Server 的计算机的名称有效。 若要确认，请尝试使用 SQL Server Management Studio (SSMS) 连接到服务器。
- 确认防火墙配置不会阻止连接到运行 SQL Server 的计算机。
- 确认用户具有所需的用户权限。
- 确认 Distributed Replay 客户端的服务帐户有权访问运行 SQL Server 的计算机。

可以在日志中获取更多详细信息，%temp%中\\DEA。 如果问题仍然存在，请与产品团队联系。

### <a name="i-cant-connect-to-the-distributed-replay-controller"></a>我无法连接到 Distributed Replay 控制器

- 验证 Distributed Replay 控制器服务在控制器计算机上运行。 若要验证，请使用分布式重播管理工具 (运行命令`dreplay.exe status -f 1`)。
- 如果远程启动重播：
  - 确认运行 DEA 的计算机可以成功地 ping 控制器。 确认防火墙设置允许说明每个连接上**配置重播环境**页。 有关详细信息，请参阅文章[SQL Server Distributed Replay](https://docs.microsoft.com/sql/tools/distributed-replay/sql-server-distributed-replay?view=sql-server-2017)。
  - 请确保在分布式重播控制器用户允许 DCOM 远程启动和远程激活。
  - 请确保为 Distributed Replay 控制器用户允许 DCOM 远程访问的用户权限。

### <a name="the-trace-file-path-exists-on-my-machine-why-cant-distributed-replay-controller-find-it"></a>我的计算机上存在该跟踪文件路径。 为什么 Distributed Replay 控制器找不到它？

分布式的重播可以访问仅本地磁盘资源。 在开始重播之前，必须将源跟踪文件复制到分布式重播控制器计算机。 此外，你必须提供路径上 DEA**新的重播**页。 

UNC 路径不是与分布式重播兼容。 分布式的重播路径必须是第一个的源跟踪文件，其中包括扩展的本地、 绝对路径。

### <a name="why-cant-i-browse-for-files-on-the-new-replay-page"></a>为什么不能浏览新的重播页上的文件？

由于我们不能浏览远程计算机的文件夹，请浏览文件并不很有用。 复制和粘贴的绝对路径会更有效。

### <a name="i-started-replay-with-a-trace-but-distributed-replay-didnt-replay-any-events"></a>我开始重播跟踪时，但分布式重播不重播的任何事件

因为跟踪文件不具有可重播事件，或者它不具有有关如何重播事件的信息，则可能会出现此问题。 确认提供的跟踪文件路径是否为源跟踪文件。 通过使用 StartCaptureTrace.sql 脚本中提供的配置创建源跟踪文件。

### <a name="i-see-unexpected-error-occurred-when-i-try-to-preprocess-my-trace-files-by-using-the-sql-server-2017-distributed-replay-controller"></a>我看到"出现意外的错误 ！" 当我尝试使用 SQL Server 2017 Distributed Replay 控制器预处理我的跟踪文件

在 SQL Server 2017 的 RTM 版本中已知此问题。 有关详细信息，请参阅[DReplay 功能用于重播捕获的跟踪在 SQL Server 2017 时出现意外的错误](https://support.microsoft.com/help/4045678/fix-unexpected-error-when-you-use-the-dreplay-feature-to-replay-a)。  
  
SQL Server 2017，在最新累积更新 1 中解决该问题。 下载最新版[SQL Server 2017 的累积更新 1](https://support.microsoft.com/help/4038634/cumulative-update-1-for-sql-server-2017)。

## <a name="next-steps"></a>后续步骤

- 若要创建分析报表，可帮助您深入了解建议的更改，请参阅[创建报表](database-experimentation-assistant-create-report.md)。

- DEA 和演示的 19 分钟介绍，请观看以下视频：

  > [!VIDEO https://channel9.msdn.com/Shows/Data-Exposed/Introducing-the-Database-Experimentation-Assistant/player]
