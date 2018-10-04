---
title: 重播选项（Distributed Replay 管理工具）| Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
ms.assetid: d7bce6a5-d414-488d-a3cd-50c1c62019c4
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: cb93c31fd8071e002ec3dd63a6add6ab7bd80e52
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/02/2018
ms.locfileid: "48177087"
---
# <a name="replay-option-distributed-replay-administration-tool"></a>重播选项（分布式重播管理工具）
  [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Distributed Replay 管理工具， `DReplay.exe`，是一个命令行工具，可用来与分布式的重播控制器进行通信。 本主题介绍 **replay** 命令行选项和相应的语法。  
  
 **replay** 选项启动事件重播阶段，在该阶段中，控制器将重播数据调度到指定客户端，启动分布式重播并同步客户端。 每个参与重播的客户端可以选择记录重播活动并在本地保存结果跟踪文件。  
  
 ![主题连接图标](../../database-engine/media/topic-link.gif "Topic link icon") 有关与此管理工具语法结合使用的语法约定的详细信息，请参阅 [Transact-SQL 语法约定 (Transact-SQL)](/sql/t-sql/language-elements/transact-sql-syntax-conventions-transact-sql)。  
  
## <a name="syntax"></a>语法  
  
```  
  
      dreplay replay [-mcontroller] -dcontroller_working_dir [-o]  
    [-starget_server] -wclients [-cconfig_file]  
    [-fstatus_interval]  
```  
  
#### <a name="parameters"></a>Parameters  
 **-m** *控制器*  
 指定控制器的计算机名称。 可以用“`localhost`”或“`.`”指代本地计算机。  
  
 如果未指定 **-m** 参数，则使用本地计算机。  
  
 **-d** *controller_working_dir*  
 指定控制器上用于存储中间文件的目录。 **-d** 参数是必需的。  
  
 需要满足以下要求：  
  
-   目录必须位于控制器上。  
  
-   必须指定以驱动器号开头（例如 `c:\WorkingDir`）的完整路径。  
  
-   路径不能以反斜杠“`\`”结尾。  
  
-   不支持 UNC 路径。  
  
 **-o**  
 捕获客户端的重播活动，并将其保存到一个结果跟踪文件中，该文件的路径由客户端配置文件 `<ResultDirectory>` 的 `DReplayClient.xml`元素指定。  
  
 当未指定 **–o** 参数时，不会生成结果跟踪文件。 在重播结束时，控制台输出将返回摘要信息，但不提供其他重播统计信息。  
  
 **-s** *target_server*  
 指定应针对其重播分布式工作负荷的 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 的目标实例。 必须以 **server_name[\instance name]** 格式指定此参数。  
  
 不能使用“`localhost`”或“`.`”作为目标服务器。  
  
 如果重播配置文件 **的** 部分指定了 `<Server>` 元素，则不需要 `<ReplayOptions>` -s `DReplay.exe.replay.config`参数。  
  
 如果使用 **-s** 参数，则将忽略重播配置文件 `<Server>` 部分中的 `<ReplayOptions>` 元素。  
  
 **-w** *clients*  
 此必需的参数是一个逗号分隔列表 （不含空格），用来指定应参与分布式重播的客户端的计算机名称。 不允许使用 IP 地址。 注意，客户端必须已向控制器注册。  
  
> [!NOTE]  
>  当客户端服务启动时，每个客户端都向客户端配置文件中指定的控制器注册。  
  
 **-c** *config_file*  
 重播配置文件的完整路径；当该文件存储在其他位置时，用于指定该位置。  
  
 若要使用重播配置文件 **的默认值，则不需要** -c `DReplay.exe.replay.config`参数。  
  
 **-f** *status_interval*  
 指定显示状态的频率（以秒为单位）。  
  
 如果未指定 **-f** ，则默认间隔为 30 秒。  
  
## <a name="examples"></a>示例  
 在本例中，分布式重播从修改的重播配置文件 `DReplay.exe.replay.config`派生其大部分行为。  
  
-   **-m** 参数指定名为 `controller1` 的计算机充当控制器。 当控制器服务在另一台计算机上运行时，必须指定计算机名称。  
  
-   **-d** 参数指定中间文件在控制器上的位置 `c:\WorkingDir`。  
  
-   **-o** 参数指定每个指定的客户端捕获重播活动并将其保存到结果跟踪文件中。 注意：可使用配置文件中的 `<ResultTrace>` 元素指定是否记录行计数和结果集。  
  
-   **-w** 参数指定计算机 `client1` 到 `client4` 作为客户端参与分布式重播。  
  
-   **-c** 参数用来指向修改过的配置文件 `DReplay.exe.replay.config`。  
  
-   因为重播配置文件 **的** 元素中指定了 `<Server>` 元素，所以不需要 `<ReplayOptions>` -s `DReplay.exe.replay.config`参数。  
  
 当管理工具从不是控制器的计算机运行时，使用下面的语法启动事件重播阶段：  
  
```  
dreplay replay -m controller1 -d c:\WorkingDir -o -w client1,client2,client3,client4 -c c:\DReplay.exe.replay.config  
```  
  
 若要指定同步顺序模式，应将 `<SequencingMode>` 文件的 `DReplay.exe.replay.config` 元素设置为与 `synchronization`值相等。 重播配置文件的 `<ResultTrace>` 部分经过修改以指定记录行计数。 以下 XML 示例显示了这些更改：  
  
```  
<?xml version='1.0'?>  
<Options>  
    <ReplayOptions>  
        <Server>server_name\replay_target_instance</Server>  
        <SequencingMode>synchronization</SequencingMode>  
        <ConnectTimeScale></ConnectTimeScale>  
        <ThinkTimeScale></ThinkTimeScale>  
        <HealthmonInterval>60</HealthmonInterval>  
        <QueryTimeout>3600</QueryTimeout>  
        <ThreadsPerClient></ThreadsPerClient>  
    </ReplayOptions>  
    <OutputOptions>  
        <ResultTrace>  
            <RecordRowCount>Yes</RecordRowCount>  
            <RecordResultSet>No</RecordResultSet>  
        </ResultTrace>  
    </OutputOptions>  
</Options>  
```  
  
 若要指定压力顺序模式，应将 `<SequencingMode>` 文件的 `DReplay.exe.replay.config` 元素设置为与 `stress`值相等。 `<ConnectTimeScale>` 和 `<ThinkTimeScale>` 元素设置为值 `50` （以指定 50%）。 有关连接时间和思考时间的详细信息，请参阅 [Configure Distributed Replay](configure-distributed-replay.md)。 以下 XML 示例显示了这些更改：  
  
```  
<?xml version='1.0'?>  
<Options>  
    <ReplayOptions>  
        <Server>server_name\replay_target_instance_name</Server>  
        <SequencingMode>stress</SequencingMode>  
        <ConnectTimeScale>50</ConnectTimeScale>  
        <ThinkTimeScale>50</ThinkTimeScale>  
        <HealthmonInterval>60</HealthmonInterval>  
        <QueryTimeout>3600</QueryTimeout>  
        <ThreadsPerClient></ThreadsPerClient>  
    </ReplayOptions>  
    <OutputOptions>  
        <ResultTrace>  
            <RecordRowCount>Yes</RecordRowCount>  
            <RecordResultSet>No</RecordResultSet>  
        </ResultTrace>  
    </OutputOptions>  
</Options>  
```  
  
## <a name="permissions"></a>Permissions  
 您必须作为交互用户、本地用户或域用户帐户运行管理工具。 若要使用本地用户帐户，管理工具和控制器必须在同一台计算机上运行。  
  
 有关详细信息，请参阅 [Distributed Replay Security](distributed-replay-security.md)。  
  
## <a name="see-also"></a>请参阅  
 [重播跟踪数据](replay-trace-data.md)   
 [查看重播结果](review-the-replay-results.md)   
 [SQL Server 分布式的重播](sql-server-distributed-replay.md)   
 [配置 Distributed Replay](configure-distributed-replay.md)   
 [SQL Server 分布式重播论坛](http://social.technet.microsoft.com/Forums/sl/sqldru/)   
 [使用 Distributed Replay 对 SQL Server 进行负载测试 – 第 2 部分](http://blogs.msdn.com/b/mspfe/archive/2012/11/14/using-distributed-replay-to-load-test-your-sql-server-part-2.aspx)   
 [使用 Distributed Replay 对 SQL Server 进行负载测试 – 第 1 部分](http://blogs.msdn.com/b/mspfe/archive/2012/11/08/using-distributed-replay-to-load-test-your-sql-server-part-1.aspx)  
  
  
