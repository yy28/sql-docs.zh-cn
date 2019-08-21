---
title: 在数据库实验助手中捕获跟踪 SQL Server 升级
description: 在数据库实验助手中捕获跟踪
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
ms.openlocfilehash: 3887daff7807d57244449d4f35d220bb47b8f10d
ms.sourcegitcommit: 5e838bdf705136f34d4d8b622740b0e643cb8d96
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/20/2019
ms.locfileid: "69653819"
---
# <a name="capture-a-trace-in-database-experimentation-assistant"></a>在数据库实验助手中捕获跟踪

您可以使用数据库实验助手 (DEA) 中的跟踪捕获来创建具有捕获的服务器事件日志的跟踪文件。 捕获的服务器事件是在特定时间段内发生在特定服务器上的事件。 每个服务器必须运行一次跟踪捕获。

在开始跟踪捕获之前, 请确保备份所有目标数据库。

SQL Server 中的查询缓存可能会影响评估结果。 建议在服务应用程序中重新启动 SQL Server 服务 (MSSQLSERVER), 以提高评估结果的一致性。

## <a name="create-a-trace-capture"></a>创建跟踪捕获

1. 在 DEA 中, 选择左侧菜单中的菜单图标。 在展开的菜单中, 选择相机图标旁边的 "**捕获跟踪**"。

    ![选择菜单中的 "捕获跟踪"](./media/database-experimentation-assistant-capture-trace/dea-capture-trace-capture.png)

1. 在 "**新建捕获**" 下, 输入或选择以下信息:

    - **SQL Server 实例名称**:输入要在其上捕获服务器跟踪 SQL Server 的计算机的名称。
    - **数据库名称**:为要在其上启动数据库跟踪的数据库输入名称。 如果未指定数据库, 则会在服务器上的所有数据库中捕获跟踪。
    - **跟踪文件名**:输入捕获的跟踪文件的名称。
    - **最大文件大小 (MB)** :选择文件的滚动更新大小。 根据所选文件大小的需要, 将创建一个新的文件。 建议的滚动更新大小为 200 MB。
    - **持续时间 (分钟)** :选择希望跟踪捕获运行的时间长度 (以分钟为单位)。
    - **用于存储输出跟踪文件的路径**:选择跟踪文件的目标路径。 

    > [!NOTE]
    > 跟踪文件的文件路径必须位于运行 SQL Server 的计算机上。 如果没有为特定帐户设置 SQL Server 服务, 则该服务可能需要对要写入的跟踪文件的指定文件夹具有写入权限。
    >
    >

    ![新建捕获页面](./media/database-experimentation-assistant-capture-trace/dea-capture-trace-inputs.png)

## <a name="start-the-trace-capture"></a>启动跟踪捕获

输入或选择所需的信息后, 选择 "**开始**" 以开始捕获跟踪。 如果输入的信息有效, 则跟踪捕获过程将开始。 否则, 具有无效条目的文本框将突出显示为红色。 

请确保已选择或输入的值是正确的, 然后选择 "**启动**"。

跟踪捕获运行完毕后, 请在 "**用于存储输出跟踪文件的路径**" 中指定的文件位置找到新的跟踪文件。 选择左侧菜单底部的钟形图标来监视捕获进度。

![捕获跟踪进度](./media/database-experimentation-assistant-capture-trace/dea-capture-trace-progress.png)

### <a name="trace-file"></a>跟踪文件

跟踪捕获写出指定位置中的 trace.dat.trc 文件。 跟踪文件包含 SQL Server 数据库的活动的跟踪结果。 TRACE.DAT.TRC 文件旨在提供有关 SQL Server 检测和报告的错误的详细信息。

## <a name="frequently-asked-questions-about-trace-capture"></a>有关跟踪捕获的常见问题

下面是 DEA 中有关跟踪捕获的一些常见问题解答。

### <a name="what-events-are-captured-when-i-run-a-trace-capture-on-a-production-database"></a>在生产数据库上运行跟踪捕获时捕获哪些事件？

下表提供了事件列表以及我们为跟踪收集的相应列数据:
  
|事件名称|文本数据 (1)|二进制数据 (2)|数据库 ID (3)|主机名 (8)|应用程序名称 (10)|登录名 (11)|SPID (12)|开始时间 (14)|结束时间 (15)|数据库名称 (35)|事件序列 (51)|IsSystem (60)|  
|---|---|---|---|---|---|---|---|---|---|---|---|---|  
|**RPC: 已完成 (10)**||*|*|*|*|*|*|*|*|*|*|*|  
|**RPC: 正在启动 (11)**||*|*|*|*|*|*|*||*|*|*|  
|**RPC 输出参数 (100)**|*||*|*|*|*|*|*||*|*|*|  
|**SQL: BatchCompleted (12)**|*||*|*|*|*|*|*|*|*|*|*|  
|**SQL: BatchStarting (13)**|*||*|*|*|*|*|*||*|*|*|  
|**审核登录 (14)**|*|*|*|*|*|*|*|*||*|*|*|  
|**审核注销 (15)**|*||*|*|*|*|*|*|*|*|*|*|  
|**Existingconnection 事件类 (17)**|*|*|*|*|*|*|*|*||*|*|*|  
|**Cursoropen 事件类 (53)**|*||*|*|*|*|*|*||*|*|*|  
|**Cursorprepare 事件类 (70)**|*||*|*|*|*|*|*||*|*|*|  
|**准备 SQL (71)**|||*|*|*|*|*|*||*|*|*|  
|**Exec 准备的 SQL (72)**|||*|*|*|*|*|*||*|*|*|  
|**Cursorexecute 事件类 (74)**|*||*|*|*|*|*|*||*|*|*|  
|**Cursorunprepare 事件类 (77)**|*||*|*|*|*|*|*||*|*|*|  
|**Cursorclose 事件类 (78)**|*||*|*|*|*|*|*||*|*|*|  

### <a name="is-there-a-performance-effect-on-my-production-server-when-trace-capture-is-running"></a>在运行跟踪捕获时, 生产服务器上是否会产生性能影响？
    
是的, 跟踪收集过程中性能的影响最小。 在我们的测试中, 我们发现了 3% 的内存压力。
    
### <a name="what-kind-of-permissions-are-required-for-capturing-traces-on-a-production-workload"></a>捕获生产工作负荷的跟踪需要哪种权限？
    
- 在 DEA 应用程序中运行跟踪操作的 Windows 用户必须对运行 SQL Server 的计算机具有 sysadmin 权限。
- 在运行 SQL Server 的计算机上使用的服务帐户必须具有对指定跟踪文件路径的写访问权限。

### <a name="can-i-capture-traces-for-the-entire-server-or-only-on-a-single-database"></a>能否捕获整个服务器的跟踪, 还是只捕获单个数据库的跟踪？
    
您可以使用 DEA 来捕获服务器中的所有数据库或单个数据库的跟踪。
    
### <a name="i-have-a-linked-server-configured-in-my-production-environment-do-those-queries-show-up-in-the-traces"></a>我的生产环境中配置了链接服务器。 这些查询是否显示在跟踪中？
    
如果要为整个服务器运行跟踪捕获, 则跟踪将捕获所有查询, 包括链接服务器查询。 若要为整个服务器运行跟踪捕获, 请将 "**数据库名称**" 框留空。
    
### <a name="whats-the-minimum-recommended-time-for-production-workload-traces"></a>生产工作负荷跟踪的建议最小时间是多少？
    
建议选择最能准确表示工作负荷的时间。 这样, 分析就会在工作负荷中的所有查询上运行。
    
### <a name="how-important-is-to-take-a-database-backup-right-before-i-start-a-trace-capture"></a>在开始跟踪捕获之前, 数据库备份有多重要？
    
在开始跟踪捕获之前, 请确保备份所有目标数据库。 将重播目标1和目标2中捕获的跟踪。 如果数据库状态不相同, 则试验的结果不对称。

### <a name="can-i-collect-xevents-instead-of-traces-and-can-i-replay-xevents"></a>能否收集 XEvents 而不是跟踪, 能否重播 XEvents？
    
是。 DEA 支持 XEvents。 下载最新版本的 DEA 并试用。

## <a name="troubleshoot-trace-captures"></a>跟踪捕获疑难解答

如果在运行跟踪捕获时出现错误, 请查看以下先决条件:

- 确认运行 SQL Server 的计算机的名称有效。 若要确认, 请尝试使用 SQL Server Management Studio (SSMS) 连接到运行 SQL Server 的计算机。
- 确认防火墙配置不会阻止与运行 SQL Server 的计算机的连接。
- 确认用户具有博客张贴[重播常见问题解答](https://blogs.msdn.microsoft.com/datamigration/2017/03/24/dea-2-0-replay-faq/)中列出的权限。
- 确认跟踪名称不遵循标准翻转约定 (捕获\_1)。 改为尝试跟踪名称 (如\_Capture 1a 或 Capture1)。

下面是你可能会看到的一些可能的错误以及解决这些错误的解决方案:

|可能的错误|解决方案|  
|---|---|  
|无法在目标 SQL Server 上启动跟踪, 请检查您是否具有所需的权限, 以及 SQL Server 帐户是否有权访问指定的跟踪文件路径 Sql 错误代码 (53)|运行 DEA 工具的用户必须有权访问运行 SQL Server 的计算机。 必须为用户分配 sysadmin 角色。|  
|无法在目标 SQL Server 上启动跟踪, 请检查您是否具有所需的权限, 以及 SQL Server 帐户是否有权访问指定的跟踪文件路径 Sql 错误代码 (19062)|指定的跟踪路径可能不存在, 或者该文件夹不具有运行 SQL Server 服务所使用的帐户 (例如, NETWORK SERVICE) 的写入权限。 路径必须存在, 并且必须具有启动跟踪所需的权限。|  
|当前正在目标服务器上运行的 DEA 跟踪。|目标服务器上已运行活动跟踪。 当服务器范围内的跟踪已在运行时, 无法启动新跟踪。|  
|无法打开请求的数据库来捕获跟踪。 此错误可能是由数据库名称不正确引起的。|指定的数据库不存在, 或当前用户无法访问该数据库。 使用正确的数据库名称。|  

如果看到标记为 " *Sql 错误代码*" 的任何其他错误, 请参阅[数据库引擎错误](https://docs.microsoft.com/sql/relational-databases/errors-events/database-engine-events-and-errors)以了解详细说明。

## <a name="next-steps"></a>后续步骤

- 若要了解如何在重播捕获的跟踪之前配置 SQL Server 中的 Distributed Replay 工具, 请参阅[配置重播](database-experimentation-assistant-configure-replay.md)。

- 有关 DEA 和演示的19分钟简介, 请观看以下视频:

  > [!VIDEO https://channel9.msdn.com/Shows/Data-Exposed/Introducing-the-Database-Experimentation-Assistant/player]
