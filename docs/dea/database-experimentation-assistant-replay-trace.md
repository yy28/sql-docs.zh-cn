---
title: 重播跟踪以进行 SQL Server 升级
description: 使用数据库实验助手 SQL Server 升级重播跟踪
ms.custom: seo-lt-2019
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
ms.openlocfilehash: b1607aefdc8495f374b2586b0b896f20e87f62d1
ms.sourcegitcommit: d00ba0b4696ef7dee31cd0b293a3f54a1beaf458
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/13/2019
ms.locfileid: "74056698"
---
# <a name="replay-a-trace-in-database-experimentation-assistant"></a>在数据库实验助手中重播跟踪

在数据库实验助手（DEA）中，可以针对已升级的测试环境重播捕获的跟踪文件。 例如，请考虑在 SQL Server 2008 R2 上运行的生产工作负荷。 工作负荷的跟踪文件必须重播两次：一次是在具有相同版本的 SQL Server 的环境上运行，在生产环境中运行，并再次在具有升级目标 SQL Server 版本的环境上，如 SQL Server 2016。

> [!NOTE]
> 若要运行此操作，你必须手动设置虚拟机或物理计算机以运行 Distributed Replay 跟踪。 有关详细信息，请参阅[Distributed Replay 控制器和客户端设置](https://blogs.msdn.microsoft.com/datamigration/distributed-replay-controller-and-client-setup/)。
>
>

## <a name="create-a-trace-replay"></a>创建跟踪重播

在 DEA 中，选择菜单图标。 在展开的菜单中，选择 "播放" 图标旁边的 "**重播跟踪**"。

![在菜单中选择重播跟踪](./media/database-experimentation-assistant-replay-trace/dea-replay-trace-open.png)

> [!NOTE]
> Distributed Replay 控制器计算机要求使用远程用户帐户的权限。
>

### <a name="grant-access-to-the-distributed-replay-controller"></a>授予对 Distributed Replay 控制器的访问权限

1. 在命令提示符处，输入 " **dcomcnfg.exe** " 以打开 "**组件服务**" 界面。
1. 展开 "**组件服务**" > **计算机**" > **我的电脑** > **DCOM 配置** > **DReplayController**"。
1. 右键单击**DReplayController**，然后选择 "**属性**"。
1. 在 "**安全**" 选项卡上，选择 "**编辑**" 以添加用户帐户。
1. 选择“确定”。

### <a name="verify-setup"></a>验证设置

1.  **SQL Server 安装路径**：输入安装 SQL Server 的路径。 例如，C：\\Program Files （x86）\\Microsoft SQL Server\\120。
1.  **控制器计算机名称**：输入已设置为控制器的计算机的名称。 此计算机正在运行名为 SQL Server Distributed Replay 控制器的 Windows 服务。 Distributed Replay 控制器协调 Distributed Replay 客户端的操作。 在每个 Distributed Replay 环境中只能有一个控制器实例。
1.  **客户端计算机名称**：输入每台客户端计算机的名称，用逗号分隔。 例如： client1、client2。 最多可以有5个客户端控制器。 客户端是一个或多个物理或虚拟计算机，运行名为 SQL Server Distributed Replay 客户端的 Windows 服务。 多个 Distributed Replay 客户端一起来模拟 SQL Server 实例的工作负荷。 在每个 Distributed Replay 环境中可以有一个或多个客户端。
1.  选择“**下一步**”。

### <a name="select-a-trace"></a>选择跟踪

1.  **跟踪文件的路径**：输入输入跟踪（. trace.dat.trc）文件的路径。
1.  **用于存储重播预处理输出的路径**：  
    \- 如果你还没有 IRF 文件，请输入要存储 IRF 文件和其他预处理输出的位置的路径。  
    \- 如果已有 IRF 文件，请输入 IRF 文件的路径。
1. 选择“**下一步**”。

### <a name="replay-a-trace"></a>重播跟踪

1.  **跟踪文件名**：输入跟踪文件名。
1.  **最大文件大小（MB）** ：输入跟踪文件滚动更新大小值。 默认值为 200 MB。 您可以输入自定义值。
1.  **用于存储重播跟踪输出的路径**：输入 trace.dat.trc 文件的路径。
1.  **SQL Server 实例名称**：输入要重播跟踪的 SQL Server 实例的名称。
1.  选择“开始”。

如果输入的信息有效，Distributed Replay 过程将启动。 否则，具有错误信息的文本 boses 将突出显示为红色。 请确保输入的值正确，然后选择 "**启动**"。

等待重播运行完毕，以查看指定的位置。 选择左侧菜单底部的钟形图标来监视重播进度。

![重播跟踪进度](./media/database-experimentation-assistant-replay-trace/dea-replay-trace-progress.png)

## <a name="frequently-asked-questions-about-trace-replay"></a>有关跟踪重播的常见问题

### <a name="what-security-permissions-do-i-need-to-start-a-replay-capture-on-my-target-server"></a>在目标服务器上启动重播捕获需要哪些安全权限？

- 在 DEA 应用程序中运行跟踪操作的 Windows 用户在运行 SQL Server 的目标计算机上必须具有 sysadmin 权限。 需要这些用户权限才能启动跟踪。
- 运行 SQL Server 运行的目标计算机的服务帐户必须具有对指定跟踪文件路径的写访问权限。
- 运行 Distributed Replay 客户端服务的服务帐户必须具有连接到运行 SQL Server 的目标计算机和执行查询的用户权限。

### <a name="can-i-start-more-than-one-replay-in-the-same-session"></a>能否在同一会话中启动多个重播？

是的，您可以启动多个重播并在同一会话中跟踪它们以完成。

### <a name="can-i-start-more-than-one-replay-in-parallel"></a>能否并行启动多个重播？

是，但不是在**控制器和客户端**中选择的一组不同的计算机。 控制器和客户端将处于繁忙状态。 在**控制器和客户端**下设置一组单独的计算机，以开始并行重播。

### <a name="how-long-does-a-replay-typically-take-to-finish"></a>重播通常需要多长时间才能完成？

重播通常使用与源跟踪相同的时间，加上预处理源跟踪所需的时间量。 但是，如果向控制器注册的客户端计算机没有足够的时间来管理从重播中生成的负载，则重播可能需要更长的时间才能完成。 最多可以向控制器注册16台客户端计算机。

### <a name="how-large-do-target-trace-files-get"></a>目标跟踪文件有多大？

目标跟踪文件可能介于源跟踪大小的5到15倍之间。 文件大小基于运行的查询数。 例如，查询计划 blob 可能会很大。 如果这些查询的统计信息经常更改，则会捕获更多事件。

### <a name="why-do-i-need-to-restore-databases"></a>为什么需要还原数据库？

SQL Server 是有状态的关系数据库管理系统。 若要正确运行 A/B 测试，数据库的状态必须始终保持不变。 否则，在重播期间可能会出现不在生产中显示的错误。 若要防止出现这些错误，建议您在源捕获之前进行备份。 同样，必须在运行 SQL Server 的目标计算机上还原备份，以防止重播期间发生错误。

### <a name="what-does-pass--on-the-replay-page-mean"></a>重播页上的 "通过%" 是什么意思？

**Pass%** 表示只传递了百分比的查询。 您可以诊断是否应出现错误数。 这些错误可能是预期的，也可能是由于数据库丢失了其完整性导致的错误。 如果 "**传递%** " 的值不是预期的值，则可以停止跟踪，并在 SQL 事件探查器中查看跟踪文件，以查看哪些查询未成功。

### <a name="how-can-i-look-at-the-trace-events-that-were-collected-during-replay"></a>如何查看在重播期间收集的跟踪事件？

打开目标跟踪文件，并在 SQL 事件探查器中查看它。 或者，如果你想要对重播捕获进行修改，则所有 SQL Server 脚本都将在 C：\\Program Files （x86）\\Microsoft Corporation\\数据库实验助手\\\\StartReplayCapture 中使用。

### <a name="what-trace-events-does-dea-collect-during-replay"></a>在重播期间 DEA 收集哪些跟踪事件？

DEA 捕获包含与性能相关的信息的跟踪事件。 捕获配置位于 StartReplayCaptureTrace 脚本中。 这些事件是 SQL Server [sp_trace_setevent （transact-sql）参考文档](https://docs.microsoft.com/sql/relational-databases/system-stored-procedures/sp-trace-setevent-transact-sql)中列出的跟踪事件的典型事件。

## <a name="troubleshoot-trace-replay"></a>跟踪重播疑难解答

### <a name="i-cant-connect-to-the-computer-thats-running-sql-server"></a>我无法连接到运行 SQL Server 的计算机

- 确认运行 SQL Server 的计算机的名称有效。 若要确认，请尝试使用 SQL Server Management Studio （SSMS）连接到服务器。
- 确认防火墙配置不会阻止与运行 SQL Server 的计算机的连接。
- 确认用户具有所需的用户权限。
- 确认 Distributed Replay 客户端的服务帐户有权访问运行 SQL Server 的计算机。

可以在% temp%\\DEA 中的日志中获取更多详细信息。 如果问题仍然存在，请与产品团队联系。

### <a name="i-cant-connect-to-the-distributed-replay-controller"></a>无法连接到 Distributed Replay 控制器

- 验证 Distributed Replay 控制器服务是否正在控制器计算机上运行。 若要验证，请使用 Distributed Replay 管理工具（运行命令 `dreplay.exe status -f 1`）。
- 如果远程启动重播：
  - 确认运行 DEA 的计算机可以成功地 ping 控制器。 根据**配置重播环境**页面上的说明，确认防火墙设置允许连接。 有关详细信息，请参阅文章[SQL Server Distributed Replay](https://docs.microsoft.com/sql/tools/distributed-replay/sql-server-distributed-replay?view=sql-server-2017)。
  - 请确保 Distributed Replay 控制器的用户可以使用 DCOM 远程启动和远程激活。
  - 请确保 Distributed Replay 控制器的用户可以使用 DCOM 远程访问用户权限。

### <a name="the-trace-file-path-exists-on-my-machine-why-cant-distributed-replay-controller-find-it"></a>计算机上存在跟踪文件路径。 为什么 Distributed Replay 控制器找不到它？

Distributed Replay 只能访问本地磁盘资源。 必须先将源跟踪文件复制到 Distributed Replay 控制器计算机，然后才能开始重播。 此外，还必须提供 DEA**新重播**页上的路径。 

UNC 路径与 Distributed Replay 不兼容。 Distributed Replay 路径必须是第一个源跟踪文件（包括扩展名）的本地路径和绝对路径。

### <a name="why-cant-i-browse-for-files-on-the-new-replay-page"></a>为什么无法在新重播页面上浏览文件？

由于无法浏览远程计算机的文件夹，因此浏览文件并不有用。 复制和粘贴绝对路径更为有效。

### <a name="i-started-replay-with-a-trace-but-distributed-replay-didnt-replay-any-events"></a>我开始重播跟踪，但 Distributed Replay 未重播任何事件

出现此问题的原因可能是跟踪文件没有可重播事件，或者没有有关如何重播事件的信息。 确认提供的跟踪文件路径是否为源跟踪文件。 源跟踪文件是使用 StartCaptureTrace 脚本中提供的配置创建的。

### <a name="i-see-unexpected-error-occurred-when-i-try-to-preprocess-my-trace-files-by-using-the-sql-server-2017-distributed-replay-controller"></a>出现 "出现意外错误！" 尝试使用 SQL Server 2017 Distributed Replay 控制器预处理跟踪文件时

此问题在 SQL Server 2017 的 RTM 版本中已知。 有关详细信息，请参阅[使用 DReplay 功能重播捕获的跟踪 SQL Server 2017 中的意外错误](https://support.microsoft.com/help/4045678/fix-unexpected-error-when-you-use-the-dreplay-feature-to-replay-a)。  
  
此问题已在 2017 SQL Server 的最新累积更新1中解决。 下载[SQL Server 2017 的累积更新 1](https://support.microsoft.com/help/4038634/cumulative-update-1-for-sql-server-2017)的最新版本。

## <a name="next-steps"></a>后续步骤

- 若要创建分析报表来帮助获取有关建议更改的信息，请参阅[创建报表](database-experimentation-assistant-create-report.md)。

- 有关 DEA 和演示的19分钟简介，请观看以下视频：

  > [!VIDEO https://channel9.msdn.com/Shows/Data-Exposed/Introducing-the-Database-Experimentation-Assistant/player]
