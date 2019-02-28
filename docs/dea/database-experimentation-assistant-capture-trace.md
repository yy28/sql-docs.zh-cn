---
title: 捕获的跟踪将在数据库实验助手面向 SQL Server 升级
description: 捕获的跟踪将在数据库实验助手
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
ms.reviewer: douglasl
manager: craigg
ms.openlocfilehash: a616686649ae6c373d3537d397fe56d709f08712
ms.sourcegitcommit: 1ab115a906117966c07d89cc2becb1bf690e8c78
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/27/2018
ms.locfileid: "56987803"
---
# <a name="capture-a-trace-in-database-experimentation-assistant"></a>捕获的跟踪将在数据库实验助手

可以在数据库实验助手 (DEA) 使用跟踪捕获，若要创建具有捕获的服务器事件日志的跟踪文件。 捕获的服务器事件是在特定时间段内特定服务器发生的事件。 跟踪捕获必须运行一次每台服务器。

在开始跟踪捕获之前，请确保备份所有目标数据库。

在 SQL Server 中查询缓存可能会影响计算结果。 我们建议来提高评估结果的一致性在服务应用程序中的重新启动 SQL Server 服务 (MSSQLSERVER)。

## <a name="create-a-trace-capture"></a>创建跟踪捕获

1. 在 DEA，选择左侧菜单中的菜单图标。 在展开的菜单中，选择**捕获跟踪**照相机图标的旁边。

    ![在菜单中选择捕获的跟踪](./media/database-experimentation-assistant-capture-trace/dea-capture-trace-capture.png)

1. 下**新建捕获**，输入或选择以下信息：

    - **SQL Server 实例名称**:输入运行你想要捕获的服务器跟踪的 SQL Server 的计算机的名称。
    - **数据库名称**:输入在其上开始数据库跟踪数据库的名称。 如果不指定数据库，在服务器上的所有数据库上捕获跟踪。
    - **跟踪文件名**:输入捕获的跟踪文件的名称。
    - **最大文件大小 (MB)**:选择文件滚动更新大小。 根据需要在你选择的文件大小创建新文件。 建议滚动更新大小为 200 MB。
    - **持续时间 （以分钟为单位）**:选择你想跟踪捕获运行的时间 （以分钟为单位） 的长度。
    - **用于存储输出跟踪文件路径**:选择跟踪文件的目标路径。 

    > [!NOTE]
    > 跟踪文件的文件路径必须是运行 SQL Server 的计算机上。 如果 SQL Server 服务未设置为特定帐户，可能需要该服务写入到跟踪文件写入指定的文件夹的权限。
    >
    >

    ![新的捕获页面](./media/database-experimentation-assistant-capture-trace/dea-capture-trace-inputs.png)

## <a name="start-the-trace-capture"></a>启动跟踪捕获

输入或选择所需的信息后，选择**启动**开始捕获跟踪。 如果您输入的信息是有效的开始跟踪捕获流程。 否则，包含无效的条目的文本框将用红色突出显示。 

请确保已选择或输入的值是否正确，然后选择**启动**。

跟踪捕获完成后运行，在中指定的文件位置中找到新的跟踪文件**用于存储输出跟踪文件路径**。 选择底部的左侧菜单中，若要捕获的进度的钟形图标。

![捕获跟踪进度](./media/database-experimentation-assistant-capture-trace/dea-capture-trace-progress.png)

### <a name="trace-file"></a>跟踪文件

跟踪捕获写出指定的位置中的.trc 文件。 跟踪文件包括 SQL Server 数据库的活动的跟踪结果。 TRC 文件旨在提供有关错误的检测和报告的 SQL Server 的详细信息。

## <a name="frequently-asked-questions-about-trace-capture"></a>有关跟踪捕获的常见问题

以下是一些常见问题中 DEA 跟踪捕获有关。

### <a name="what-events-are-captured-when-i-run-a-trace-capture-on-a-production-database"></a>当我在生产数据库上运行的跟踪捕获时，会捕获哪些事件？

下表提供了事件和相应的列数据，我们收集的跟踪的列表：
  
|事件名称|文本数据 (1)|二进制数据 (2)|数据库 ID 为 (3)|主机名 (8)|应用程序名称 (10)|登录名 (11)|SPID (12)|开始时间 (14)|结束时间 (15)|数据库名称 (35)|事件序列 (51)|IsSystem (60)|  
|---|---|---|---|---|---|---|---|---|---|---|---|---|  
|**RPC:Completed (10)**||*|*|*|*|*|*|*|*|*|*|*|  
|**RPC： 正在启动 (11)**||*|*|*|*|*|*|*||*|*|*|  
|**RPC Output Parameter (100)**|*||*|*|*|*|*|*||*|*|*|  
|**SQL:BatchCompleted (12)**|*||*|*|*|*|*|*|*|*|*|*|  
|**Sql: batchstarting (13)**|*||*|*|*|*|*|*||*|*|*|  
|**审核登录名 (14)**|*|*|*|*|*|*|*|*||*|*|*|  
|**审核注销 (15)**|*||*|*|*|*|*|*|*|*|*|*|  
|**ExistingConnection (17)**|*|*|*|*|*|*|*|*||*|*|*|  
|**CursorOpen (53)**|*||*|*|*|*|*|*||*|*|*|  
|**CursorPrepare (70)**|*||*|*|*|*|*|*||*|*|*|  
|**准备 SQL (71)**|||*|*|*|*|*|*||*|*|*|  
|**Exec Prepared SQL (72)**|||*|*|*|*|*|*||*|*|*|  
|**CursorExecute (74)**|*||*|*|*|*|*|*||*|*|*|  
|**CursorUnprepare (77)**|*||*|*|*|*|*|*||*|*|*|  
|**CursorClose (78)**|*||*|*|*|*|*|*||*|*|*|  

### <a name="is-there-a-performance-effect-on-my-production-server-when-trace-capture-is-running"></a>当运行时跟踪捕获有对我的生产服务器的性能影响吗？
    
是的最小性能影响跟踪收集的过程。 在我们的测试，我们发现有关 3%内存不足的压力。
    
### <a name="what-kind-of-permissions-are-required-for-capturing-traces-on-a-production-workload"></a>以捕获跟踪对生产工作负荷需要哪种权限？
    
- DEA 应用程序中运行的跟踪操作的 Windows 用户必须运行 SQL Server 的计算机上具有 sysadmin 权限。
- 使用运行 SQL Server 的计算机上的服务帐户必须具有写入访问权限指定的跟踪文件路径。

### <a name="can-i-capture-traces-for-the-entire-server-or-only-on-a-single-database"></a>可以捕获整个服务器或仅在单个数据库上跟踪吗？
    
DEA 可用于捕获跟踪的服务器中的所有数据库也可用于单一数据库。
    
### <a name="i-have-a-linked-server-configured-in-my-production-environment-do-those-queries-show-up-in-the-traces"></a>我已配置为在我的生产环境中的链接的服务器。 这些查询显示在跟踪中？
    
如果运行的整个服务器的跟踪捕获，跟踪将捕获所有查询，包括链接的服务器查询。 若要运行整个服务器的跟踪捕获，请将**数据库名称**框下**新捕获**为空。
    
### <a name="whats-the-minimum-recommended-time-for-production-workload-traces"></a>什么是生产工作负荷跟踪的最小建议的时间？
    
我们建议你选择最能代表整个工作负荷的时间。 这样一来，你的工作负荷中的所有查询运行分析。
    
### <a name="how-important-is-to-take-a-database-backup-right-before-i-start-a-trace-capture"></a>如何重要的是执行数据库备份正确，然后再开始跟踪捕获？
    
在开始跟踪捕获之前，请确保备份所有目标数据库。 重播目标 1 和目标 2 中捕获的跟踪。 如果数据库状态不相同，该试验的结果是不一致的。

### <a name="can-i-collect-xevents-instead-of-traces-and-can-i-replay-xevents"></a>我可以收集 XEvents 而不是跟踪，并可以重播 XEvents？
    
是。 DEA 支持 XEvents。 下载 DEA 的最新版本并尝试一下。

## <a name="troubleshoot-trace-captures"></a>对跟踪捕获进行故障排除

如果在运行跟踪捕获时看到错误，请查看以下先决条件：

- 确认运行 SQL Server 的计算机的名称有效。 若要确认，请尝试连接到使用 SQL Server Management Studio (SSMS) 运行 SQL Server 的计算机。
- 确认你的防火墙配置不会阻止连接到运行 SQL Server 的计算机。
- 确认用户已在博客文章中列出的权限[重播常见问题解答](https://blogs.msdn.microsoft.com/datamigration/2017/03/24/dea-2-0-replay-faq/)。
- 确认跟踪名称不遵循标准的滚动更新约定 (捕获\_1)。 相反，请尝试类似捕获跟踪名称\_1A 或 Capture1。

以下是一些可能会看到可能出现的错误和解决问题的解决方案：

|可能的错误|解决方案|  
|---|---|  
|无法启动跟踪在目标 SQL Server 上的检查是否具有所需的权限以及 SQL Server 帐户具有写入访问权限指定的跟踪文件路径 Sql 错误代码 (53)|运行 DEA 工具的用户必须具有对运行 SQL Server 的计算机的访问。 用户必须分配 sysadmin 角色。|  
|无法启动跟踪在目标 SQL Server 上的检查是否具有所需的权限以及 SQL Server 帐户具有写入访问权限指定的跟踪文件路径 Sql 错误代码 (19062)|可能不存在指定的跟踪路径或文件夹没有写入权限的帐户下的 SQL Server 服务正在运行 （例如，网络服务）。 路径必须存在，并且它必须具有要启动跟踪所需的权限。|  
|DEA 跟踪当前正在运行的目标服务器上。|已在目标服务器上运行活动的跟踪。 当服务器范围内跟踪已在运行时，不能启动新的跟踪。|  
|无法打开用于捕获跟踪请求的数据库。 不正确的数据库名称可能会导致此错误。|指定的数据库不存在，或不是当前用户可以访问。 使用正确的数据库名称。|  

如果看到标记为任何其他错误*Sql 错误代码*，请参阅[系统错误消息](https://docs.microsoft.com/previous-versions/sql/sql-server-2008-r2/cc645603(v=sql.105))详细的说明和解决方法。
    
## <a name="next-steps"></a>后续步骤

- 若要了解如何在 SQL Server 中配置的分布式重播的工具，重播捕获的跟踪之前，请参阅[配置重播](database-experimentation-assistant-configure-replay.md)。

- DEA 和演示的 19 分钟介绍，请观看以下视频：

  > [!VIDEO https://channel9.msdn.com/Shows/Data-Exposed/Introducing-the-Database-Experimentation-Assistant/player]
