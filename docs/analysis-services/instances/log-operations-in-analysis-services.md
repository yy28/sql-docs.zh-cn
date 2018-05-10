---
title: Analysis Services 中记录操作 |Microsoft 文档
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.component: ''
ms.topic: article
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 4a4968a3c66100fd40871fa5e8231f19711361e2
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
---
# <a name="log-operations-in-analysis-services"></a>Analysis Services 中的日志操作
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
  Analysis Services 实例将会把服务器通知、错误和警告记录到 msmdsrv.log 文件中 – 你安装的每个实例都有该文件。 管理员参考此日志，了解例程和异常事件等信息。 在最新版本中，已增强日志记录，能容纳更多信息。 日志记录现在包括产品版本和版本信息以及处理器、内存、连接性和阻止事件。 你可在 [日志记录改进](http://support.microsoft.com/kb/2965035)中查看整个更改列表。  
  
 除了内置日志记录功能，许多管理员和开发人员还使用 Analysis Services 社区提供的工具来收集有关服务器操作（例如 **ASTrace**）的数据。 查看 [Microsoft SQL Server 社区示例：Analysis Services](https://sqlsrvanalysissrvcs.codeplex.com/) ，获得下载链接。  
  
 本主题包含以下各节：  
  
-   [日志的位置和类型](#bkmk_location)  
  
-   [日志文件配置设置的一般信息](#bkmk_general)  
  
-   [MSMDSRV 服务日志文件](#bkmk_msmdsrv)  
  
-   [查询日志](#bkmk_querylog)  
  
-   [Mini dump (.mdmp) 文件](#bkmk_mdmp)  
  
-   [提示和最佳实践](#bkmk_tips)  
  
> [!NOTE]  
>  如果你要查找日志记录的信息，你可能也对跟踪显示处理和查询执行路径的操作感兴趣。 临时跟踪目标和持续跟踪目标（例如审核多维数据集访问）以及如何最大程度利用 Flight Recorder、SQL Server Profiler 和 xEvents 的建议可通过此页中的链接找到： [监视 Analysis Services 实例](../../analysis-services/instances/monitor-an-analysis-services-instance.md)。  
  
##  <a name="bkmk_location"></a> 日志的位置和类型  
 Analysis Services 提供有以下所述日志。  
  
|文件名或位置|类型|用于|在默认情况下启用|  
|---------------------------|----------|--------------|-------------------|  
|Msmdsrv.log|错误日志|例程监控和基本故障排除|是|  
|关系数据库中的 OlapQueryLog 表|查询日志|为使用情况优化向导收集输入|否|  
|SQLDmp\<guid >.mdmp 文件|崩溃和异常|深度故障排除|否|  
  
 我们强烈建议使用以下链接查看此主题中未涉及的其他信息资源： [来自 Microsoft 支持的初始数据集合提示](http://blogs.msdn.com/b/as_emea/archive/2012/01/02/initial-data-collection-for-troubleshooting-analysis-services-issues.aspx)。  
  
##  <a name="bkmk_general"></a> 日志文件配置设置的一般信息  
 你可在 msmdsrv.ini 服务器配置文件中找到每个日志的部分，此文件位于 \Program Files\Microsoft SQL Server\MSAS13.MSSQLSERVER\OLAP\Config 文件夹。 有关编辑文件的说明，请参阅 [Analysis Services 中的服务器属性](../../analysis-services/server-properties/server-properties-in-analysis-services.md) 。  
  
 如有可能，我们建议你在 Management Studio 的服务器属性页设置日志记录属性。 但是在某些情况下，你必须直接编辑 msmdsrv.ini 文件以配置管理工具中不可见的设置。  
  
 ![显示日志设置配置文件部分](../../analysis-services/instances/media/ssas-logfilesettings.png "显示日志设置配置文件部分")  
  
##  <a name="bkmk_msmdsrv"></a> MSMDSRV 服务日志文件  
 Analysis Services 会将服务器操作记录到 msmdsrv.log 文件中，每个实例一个文件，位于 \program files\Microsoft SQL Server\\<instance\>\Olap\Log。  
  
 此日志文件会在每次重启服务时被清空。 在以前版本中，管理员有时会重启服务，其唯一目的是在其变得过大不能使用前清空日志文件。 现在已没有必要。 SQL Server 2012 SP2 和更高版本中引入的配置设置使你可控制日志文件及其历史记录的大小：  
  
-   **MaxFileSizeMB** 指定最大日志文件大小 (MB)。 默认值为 256。 有效替换值必须是正整数。 达到 **MaxFileSizeMB** 时，Analysis Services 将当前文件重命名为 msmdsrv{current timestamp}.log 文件，然后启动新的 msmdsrv.log 文件。  
  
-   **MaxNumberFiles** 指定较旧日志文件的持续时间。 默认值为 0（禁用）。 你可将其更改为正整数以保持日志文件的版本。 达到 **MaxNumberFiles** 时，Analysis Services 删除名称具有最旧时间戳的文件。  
  
 要使用这些设置，请进行以下操作：  
  
1.  在记事本中打开 msmdsrv.ini。  
  
2.  复制以下两行：  
  
    ```  
    <MaxFileSizeMB>256</MaxFileSizeMB>  
    <MaxNumberOfLogFiles>5</MaxNumberOfLogFiles>  
    ```  
  
3.  将两行粘贴到 msmdsrv.ini 的日志部分，在 msmdsrv.log 的文件名下方。 必须手动添加两个设置。 其在 msmdsrv.ini 文件中没有占位符。  
  
     更改的配置文件应该如下所示：  
  
    ```  
    <Log>  
    <File>msmdsrv.log</File>  
    <MaxFileSizeMB>256</MaxFileSizeMB>  
    <MaxNumberOfLogFiles>5</MaxNumberOfLogFiles>  
    <FileBufferSize>0</FileBufferSize>  
  
    ```  
  
4.  如果这些值与你要的值不同，请对其进行编辑。  
  
5.  保存该文件。  
  
6.  重新启动服务。  
  
##  <a name="bkmk_querylog"></a> 查询日志  
 查询日志有一点用词不当，因为它不记录你的用户的 MDX 或 DAX 查询活动。 它收集由 Analysis Services 生成的查询的数据，这些数据后续用作基于使用情况的优化向导中的数据输入。 查询日志中收集的数据不用于直接分析。 具体而言，数据集用比特数组表示，查询中包含指示数据集部分的 0 或 1。 再次说明，此数据用于向导。  
  
 对于查询监控和故障排除，许多开发人员和管理员使用社区工具 **ASTrace**来监控查询。 你还可使用 SQL Server Profiler、xEvents 或 Analysis Services 跟踪。 有关跟踪相关的链接，请参阅 [监视 Analysis Services 实例](../../analysis-services/instances/monitor-an-analysis-services-instance.md) 。  
  
 你应何时使用查询日志？ 我们建议启用查询日志，作为包括基于使用情况的优化向导的查询性能微调练习的一部分。 在你启用此功能、创建用于支持它的数据结构并设置 Analysis Services 使用的属性以查找和填充日志后，查询日志才存在。  
  
 要启用查询日志，请遵循以下步骤：  
  
1.  创建 SQL Server 关系数据库以存储查询日志。  
  
2.  授予 Analysis Services 帐户有关数据库的足够权限。 帐户需要创建表、写入表和从表读取的权限。  
  
3.  在 SQL Server Management Studio，右键单击**Analysis Services** | **属性** | **常规**，将其设置**CreateQueryLogTable**为 true。  
  
4.  或者，如果你要以不同速率取样查询，或者使用表的不同名称，则更改 **QueryLogSampling** 或 **QueryLogTableName** 。  
  
 将不会创建查询日志表，直到你已运行足够的 MDX 查询以满足取样需要。 例如，如果你保持默认值为 10，则必须运行至少 10 个查询才能创建表。  
  
 查询日志设置属于服务器范围。 你指定的设置将被此服务器上运行的所有数据库使用。  
  
 ![查询在 Management Studio 中的日志设置](../../analysis-services/instances/media/ssas-querylogsettings.png "在 Management Studio 中的查询日志设置")  
  
 指定配置设置后，多次运行 MDX 查询。 如果取样设置为 10，则运行 11 次查询。验证表是否创建。 在 Management Studio 中，连接到关系数据库引擎，打开数据库文件夹，打开 **“表”** 文件夹，并验证 **OlapQueryLog** 是否存在。 如果不能立即查看表，则刷新文件夹，提取其内容的任何更改。  
  
 允许查询日志为基于使用情况的优化向导积累足够数据。 如果查询量是周期性的，则捕获足够流量以包括具有代表性的一组数据。 有关如何运行向导的说明，请参见 [基于使用情况的优化向导](https://msdn.microsoft.com/library/ms189706.aspx) 。  
  
 有关查询日志配置的详细信息，请参见 [配置 Analysis Services 查询日志](http://technet.microsoft.com/library/Cc917676) 。 虽然文件很旧，但最新版本中的查询日志配置并未改变，其包含的信息仍适用。  
  
##  <a name="bkmk_mdmp"></a> Mini dump (.mdmp) 文件  
 转储文件捕获数据用于分析异常事件。 Analysis Services 自动生成迷你转储 (.mdmp) 以应对服务器崩溃、异常和一些配置错误。 已启用此功能，但不能自动发送崩溃报告。  
  
 崩溃报告通过 Msmdsrv.ini 文件中的“异常”部分配置。 这些设置可控制内存转储文件生成。 以下片段显示默认值：  
  
```  
<Exception>  
<CreateAndSendCrashReports>1</CreateAndSendCrashReports>  
<CrashReportsFolder/>  
<SQLDumperFlagsOn>0x0</SQLDumperFlagsOn>  
<SQLDumperFlagsOff>0x0</SQLDumperFlagsOff>  
<MiniDumpFlagsOn>0x0</MiniDumpFlagsOn>  
<MiniDumpFlagsOff>0x0</MiniDumpFlagsOff>  
<MinidumpErrorList>0xC1000000, 0xC1000001, 0xC102003F, 0xC1360054, 0xC1360055</MinidumpErrorList>  
<ExceptionHandlingMode>0</ExceptionHandlingMode>  
<CriticalErrorHandling>1</CriticalErrorHandling>  
<MaxExceptions>500</MaxExceptions>  
<MaxDuplicateDumps>1</MaxDuplicateDumps>  
</Exception>  
```  
  
 **配置崩溃报告**  
  
 除非 Microsoft 支持另有指示，否则大多数管理员使用默认设置。 这篇较旧的知识库文章仍用于提供有关如何配置转储文件的说明： [如何配置 Analysis Services 以生成内存转储文件](http://support.microsoft.com/kb/919711)。  
  
 最可能修改的配置设置是用于确定是否生成内存转储文件的 **CreateAndSendCrashReports** 设置。  
  
|“值”|说明|  
|-----------|-----------------|  
|0|关闭内存转储文件。 忽略在“例外”部分下的所有其他设置。|  
|1|（默认）启用，但不发送内存转储文件。|  
|2|启用并自动发送错误报告到 Microsoft。|  
  
 **CrashReportsFolder** 是转储文件的位置。 默认情况下，可在 \Olap\Log 文件夹找到 .mdmp 文件和相关日志记录。  
  
 **SQLDumperFlagsOn** 用于生成完全转储。 默认情况下，未启用完全转储。 你可将此属性设置为 **0x34**。  
  
 以下链接提供了更多背景信息：  
  
-   [深入了解使用 Minidumps 的 SQL Server](http://blogs.msdn.com/b/sqlcat/archive/2009/09/11/looking-deeper-into-sql-server-using-minidumps.aspx)  
  
-   [如何创建用户模式转储文件](http://support.microsoft.com/kb/931673)  
  
-   [如何使用 Sqldumper.exe 实用工具在 SQL Server 中生成转储文件](http://support.microsoft.com/kb/917825)  
  
##  <a name="bkmk_tips"></a> 提示和最佳实践  
 此部分是此文章中提到的提示回顾。  
  
-   配置 msmdsrv.log 文件以控制 msmdsrv 日志文件的大小和数量。 默认情况下不启用这些设置，请确保将其添加为安装后步骤。 请参阅本主题中的 [MSMDSRV 服务日志文件](#bkmk_msmdsrv) 。  
  
-   查看来自 Microsoft 客户支持的这篇博文，了解其使用什么资源来获取有关服务器操作的信息： [初始数据集合](http://blogs.msdn.com/b/as_emea/archive/2012/01/02/initial-data-collection-for-troubleshooting-analysis-services-issues.aspx)  
  
-   使用 ASTrace2012（而非查询日志）查找谁正在查询多维数据集。 查询日志通常用于提供输入到基于使用情况的优化向导，其捕获的数据不易读取或解释。 ASTrace2012 是一种广泛使用的用于捕获查询操作的社区工具。 请参阅 [Microsoft SQL Server 社区示例：Analysis Services](https://sqlsrvanalysissrvcs.codeplex.com/)。  
  
## <a name="see-also"></a>另请参阅  
 [Analysis Services 实例管理](../../analysis-services/instances/analysis-services-instance-management.md)   
 [监视 Analysis Services with SQL Server 事件探查器简介](../../analysis-services/instances/introduction-to-monitoring-analysis-services-with-sql-server-profiler.md)   
 [Analysis Services 中的服务器属性](../../analysis-services/server-properties/server-properties-in-analysis-services.md)  
  
  
