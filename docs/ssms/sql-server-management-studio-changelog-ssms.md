---
title: SQL Server Management Studio - Changelog (SSMS) | Microsoft Docs
ms.custom: ''
ms.date: 09/04/2018
ms.prod: sql
ms.prod_service: sql-tools
ms.component: ssms
ms.reviewer: ''
ms.suite: sql
ms.technology: ssms
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: 3dc76cc1-3b4c-4719-8296-f69ec1b476f9
caps.latest.revision: 72
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: edfb4248c5f5102742ab13d7a2615bb3c192481b
ms.sourcegitcommit: 2666ca7660705271ec5b59cc5e35f6b35eca0a96
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/06/2018
ms.locfileid: "43889793"
---
# <a name="sql-server-management-studio---changelog-ssms"></a>SQL Server Management Studio - Changelog (SSMS)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
本文提供有关 SSMS 的当前和以前版本的更新、改进和 bug 修复的详细信息。 下载[下方的 SSMS 早期版本](#previous-ssms-releases)。


## <a name="ssms-179download-sql-server-management-studio-ssmsmd"></a>[SSMS 17.9](download-sql-server-management-studio-ssms.md)


生成号：14.0.17285.0<br>
发布日期：2018 年 9 月 4 日

### <a name="whats-new"></a>新增功能

**常规 SSMS**


显示计划：

- “图形显示计划”功能现在对特定计划激活后显示新行模式内存授予反馈特性：MemoryGrantInfo 查询计划 XML 元素中新增了 IsMemoryGrantFeedbackAdjusted 和 LastRequestedMemory。 若要详细了解行模式内存授予反馈，请参阅 [SQL 数据库中的自适应查询处理](https://docs.microsoft.com/sql/relational-databases/performance/adaptive-query-processing)。

Azure SQL： 

- 现已开始支持在创建 Azure DB 时使用 vCore SKU。 有关详细信息，请参阅[基于 vCore 的购买模型](https://docs.microsoft.com/azure/sql-database/sql-database-service-tiers#vcore-based-purchasing-model)。
 

### <a name="bug-fixes"></a>Bug 修复

**常规 SSMS**
    
复制监视器：

- 修复了以下问题：复制监视器 (SqlMonitor.exe) 无法启动（UserVoice 项： https://feedback.azure.com/forums/908035-sql-server/suggestions/34791079) 

导入平面文件向导： 

- 修复了“平面文件向导”对话框的帮助页链接 
- 修复了向导不允许更改现有目标表的问题：这样，用户无需退出向导，即可重试删除失败的表，然后重新在向导中输入信息（UserVoice 项： https://feedback.azure.com/forums/908035-sql-server/suggestions/32896186)。 

导入/导出数据层应用程序：

- 修复了 DacFx 中的以下问题：处理已定义分区但未编制索引的表时，无法导入 .bacpac，错误消息为“错误 SQL72014: .Net SqlClient 数据提供程序: Msg 9108，级别 16，状态 10，行 1。不支持递增这种类型的统计信息 ”。 

Intellisense：

- 修复了以下问题：结合使用 AAD 和 MFA 时，无法正常使用 IntelliSense 填写。 

对象资源管理器： 

- 修复了以下问题：“筛选器对话框”显示在随机监视器上，而不是显示在运行 SSMS 的监视器上（多监视器系统）。

Azure SQL： 

- 修复了以下问题：如果在“可用数据库”中枚举数据库，在连接到特定数据库时，在下拉列表中看不到“master”。 
- 修复了以下问题：无法尝试生成脚本（“数据”或“架构和数据”），进而无法通过结合使用 AAD 和 MFA 连接到 SQL Azure DB。 
- 修复了视图设计器（视图）中的以下问题：连接到 SQL Azure DB 时，无法在 UI 中选择“添加表”。 
- 修复了以下问题：在 MFA 令牌续订期间，SSMS 查询编辑器静默关闭，并重新打开连接。 这有助于避免对用户造成未知的负面影响（如关闭事务且永不再次重新打开）。 此变更向属性窗口添加令牌到期时间。 
- 修复了以下问题：SSMS 不对结合使用 AAD 和 MFA 登录的已导入 MSA 帐户强制提示输入密码。 

活动监视器： 

- 修复了以下问题：使用 SQL 身份验证时，在活动监视器中启动的“实时查询统计信息”挂起。 

Microsoft Azure 集成： 

- 修复了以下问题：SSMS 仅显示前 50 个订阅（“Always Encrypted”对话框、“从 URL 备份/还原”对话框等）。 
- 修复了以下问题：当用户尝试（在“从 URL 备份/还原”对话框中）登录不含任何存储帐户的 Microsoft Azure 帐户时，SSMS 抛出异常（“索引超出范围”）。 

对象脚本： 

- SSMS 现在可避免在编写脚本“删除和创建”时生成动态 T-SQL。
- 编写数据库对象的脚本时，SSMS 现在不生成脚本来设置数据库范围内配置（如果设置为默认值的话）。

帮助：

- 修复了以下长期未得到解决的问题：“如何使用帮助”未采用联机/脱机模式。
- 当用户单击“帮助 | 社区项目和示例”时，SSMS 现在会打开默认浏览器，它指向 Git 页，其中不显示由于使用旧浏览器而发出的错误/警告。

### <a name="known-issues"></a>已知问题

- 此版本暂无已知问题。



## <a name="previous-ssms-releases"></a>SSMS 的早期版本

通过单击以下部分中的标题链接，下载 SSMS 的早期版本。

## <a name="downloadssdtmediadownloadpng-ssms-1781httpsgomicrosoftcomfwlinklinkid875802"></a>![下载](../ssdt/media/download.png) [SSMS 17.8.1](https://go.microsoft.com/fwlink/?linkid=875802)
在 17.8 中发现了与配置 SQL 数据库相关的错误，因此 SSMS 17.8.1 取代了 17.8。

生成号：14.0.17277.0<br>
发布日期：2018 年 6 月 26 日

[中文（中国）](https://go.microsoft.com/fwlink/?linkid=875802&clcid=0x804) | [中文（台湾）](https://go.microsoft.com/fwlink/?linkid=875802&clcid=0x404) | [英语（美国）](https://go.microsoft.com/fwlink/?linkid=875802&clcid=0x409) | [法语](https://go.microsoft.com/fwlink/?linkid=875802&clcid=0x40c) | [德语](https://go.microsoft.com/fwlink/?linkid=875802&clcid=0x407) | [意大利语](https://go.microsoft.com/fwlink/?linkid=875802&clcid=0x410) | [日语](https://go.microsoft.com/fwlink/?linkid=875802&clcid=0x411) | [朝鲜语](https://go.microsoft.com/fwlink/?linkid=875802&clcid=0x412) | [葡萄牙语（巴西）](https://go.microsoft.com/fwlink/?linkid=875802&clcid=0x416) | [俄语](https://go.microsoft.com/fwlink/?linkid=875802&clcid=0x419) | [西班牙语](https://go.microsoft.com/fwlink/?linkid=875802&clcid=0x40a)


### <a name="whats-new"></a>新增功能

**常规 SSMS**

数据库属性：

- 此改进公开了文件组的 AUTOGROW_ALL_FILES 配置选项。 此新配置选项在“数据库属性”>“文件组”窗口下以每个可用文件组复选框的新列（自动增长所有文件）的形式添加（文件流和内存优化文件组除外）。 用户可以通过切换相应的 Autogrow_All_Files 复选框来为特定文件组启用/禁用 AUTOGROW_ALL_FILES。 相应地，在编写数据库脚本为数据库（SQL 2016 及更高版本）创建/生成脚本时，AUTOGROW_ALL_FILES 选项已正确编写脚本。
    
SQL 编辑器：

- 改进了当用户没有主访问权限时 Azure SQL 数据库中 Intellisense 的使用体验。

脚本：

- 常规性能改进，尤其针对高延迟连接。
    
Analysis Servics (AS)

- Analysis Services 客户端库和数据提供程序已更新到最新版本，该版本添加了对新 Azure 政府 AAD 颁发机构 (login.microsoftonline.us) 的支持。



### <a name="bug-fixes"></a>Bug 修复

**常规 SSMS**
    
维护计划：

- 修复了使用 SQL 身份验证编辑维护计划时出现的问题，即在使用 SQL 身份验证时，“通知操作员”任务失败。
    
脚本：

- 修复了 SMO 中的 PostProcess 操作导致资源耗尽和 SQL 登录失败的问题
    
SMO：

- 修复了添加具有默认约束的列并且表已有数据的情况下 Table.Alter() 失败的问题。 有关详细信息，请参阅 [sql server smo 在向包含数据的表中添加列时生成内联默认约束](https://feedback.azure.com/forums/908035-sql-server/suggestions/32895625)。
    
Always Encrypted：

- 修复了在分区表上启用 Always Encrypted 时导致锁超时错误的问题（在 DacFx 中）
    

**Analysis Services (AS)**

- 修复了在表格 Analysis Services 1400 级兼容性模型中修改 OAuth 数据源时出现的问题，该问题导致 OAuth 令牌中的更改未在数据源中更新。
- 修复了在 Analysis Services 表格 1400 级兼容性模型中使用某些无效数据源凭据或编辑不支持在 Power Query 中更改数据源迁移（例如，Oracle）的数据源时可能在 SSMS 中发生的故障。


### <a name="known-issues"></a>已知问题

- 在“属性”窗口中修改任何文件组属性后，单击“脚本”按钮，生成两个脚本 - 一个脚本带有 USE<database> 语句，另一个脚本带有 USE master 语句。  带有 USE master 的脚本错误生成，应该放弃。 运行包含 USE<database> 语句的脚本。
- 使用新的“常规用途”或“业务关键”Azure SQL 数据库版本时，部分对话框显示版本无效错误。
- 可能会观察到 XEvents 查看器中的一些延迟。 这是 [.Net Framework 中的已知问题](https://github.com/Microsoft/dotnet/blob/master/releases/net472/dotnet472-changes.md#sql)。 请考虑升级到 NetFx 4.7.2。




## <a name="downloadssdtmediadownloadpng-ssms-177httpsgomicrosoftcomfwlinklinkid873126"></a>![下载](../ssdt/media/download.png) [SSMS 17.7](https://go.microsoft.com/fwlink/?linkid=873126)

内部版本号：14.0.17254.0<br>
发布日期：2018 年 5 月 9 日

[中文（中国）](https://go.microsoft.com/fwlink/?linkid=873126&clcid=0x804) | [中文（台湾）](https://go.microsoft.com/fwlink/?linkid=873126&clcid=0x404) | [英语（美国）](https://go.microsoft.com/fwlink/?linkid=873126&clcid=0x409) | [法语](https://go.microsoft.com/fwlink/?linkid=873126&clcid=0x40c) | [德语](https://go.microsoft.com/fwlink/?linkid=873126&clcid=0x407) | [意大利语](https://go.microsoft.com/fwlink/?linkid=873126&clcid=0x410) | [日语](https://go.microsoft.com/fwlink/?linkid=873126&clcid=0x411) | [朝鲜语](https://go.microsoft.com/fwlink/?linkid=873126&clcid=0x412) | [葡萄牙语（巴西）](https://go.microsoft.com/fwlink/?linkid=873126&clcid=0x416) | [俄语](https://go.microsoft.com/fwlink/?linkid=873126&clcid=0x419) | [西班牙语](https://go.microsoft.com/fwlink/?linkid=873126&clcid=0x40a)


### <a name="whats-new"></a>新增功能

**常规 SSMS**

复制监视器：   
- 现在，在发布服务器数据库和/或分发服务器数据库属于可用性组的情况下，复制监视器支持注册侦听器。 现在可以监视发布服务器数据库和/或分发数据库属于 AlwaysOn 的复制环境。 
 
Azure SQL 数据仓库： 
- 为 Azure SQL 数据仓库的外部表添加了“已拒绝的行位置”支持。 

**Integration Services (IS)**

- 为部署到 Azure SQL 数据库的 SSIS 包添加了计划安排功能。 本地 SQL Server 和 SQL 数据库托管实例（预览版）将 SQL Server 代理作为一级作业计划程序，与之不同的是，SQL 数据库并没有内置计划程序。 这项新的 SSMS 功能可提供类似于 SQL Server 代理的熟悉用户界面，用于计划安排部署到 SQL 数据库的包。 如果要使用 SQL 数据库承载 SSIS 目录数据库、SSISDB，可使用此 SSMS 功能生成计划 SSIS 包所需的数据工厂管道、活动和触发器。 然后可在数据工厂中编辑和扩展这些对象。 有关详细信息，请参阅[通过 SSMS 计划安排 Azure SQL 数据库上的 SSIS 包执行](../integration-services/lift-shift/ssis-azure-schedule-packages-ssms.md)。 若要了解 Azure 数据工厂管道、活动和触发器的详细信息，请参阅 [Azure 数据工厂中的管道和活动](https://docs.microsoft.com/azure/data-factory/concepts-pipelines-activities)和 [Azure 数据工厂中的管道执行和触发器](https://docs.microsoft.com/azure/data-factory/concepts-pipeline-execution-triggers)。
- 支持在 SQL 代理中计划安排在 SQL 托管实例上执行的 SSIS 包。 现在可以创建 SQL 代理作业，在托管实例上执行 SSIS 包。 

### <a name="bug-fixes"></a>Bug 修复

**常规 SSMS** 

维护计划：   
- 修复了尝试更改现有维护计划时会引发异常的错误。 有关详细信息，请参阅[单击维护计划中的日程安排时 SSMS 17.6 崩溃](https://feedback.azure.com/forums/908035-sql-server/suggestions/33712924)。

Always On： 
- 修复了 AlwaysOn 延迟仪表板无法与 SQL Server 2012 一起使用的问题。
 
脚本： 
- 修复了针对 Azure SQL 数据仓库的存储过程编写脚本不适用于非管理员用户的问题。
- 修复了针对 Azure SQL 数据库编写数据库脚本时不会为 SCOPED CONFIGURATION 属性编写脚本的问题。
 
遥测： 
- 修复了选择退出发送遥测后尝试连接服务器时 SSMS 崩溃的问题。
 
Azure SQL 数据库： 
- 修复了用户无法设置或更改兼容性级别（下拉列表为空）的问题。 注意：若要将兼容性级别设置为 150，用户仍需使用“脚本”按钮并手动编辑脚本。 
 
SMO： 
- 公开了 SMO 中的“错误日志大小”设置。 有关详细信息，请参阅[设置 SQL Server 错误日志的最大大小](https://feedback.azure.com/forums/908035-sql-server/suggestions/33624115)。  
- 修复了 Linux 上的 SMO 中的换行符脚本。
- 改进了检索极少使用的属性时的杂项性能。  

Intellisense： 
- 性能改进：减少了列数据的 IntelliSense 查询量。 处理包含大量列的表时，此功能特别有用。 

SSMS 用户设置：
- 修复了不能正确调整选项页大小的问题。

杂项：  
- 改进了“统计详细信息”页上文本的显示方式。 

**Integration Services (IS)**

- 实现了对 Azure SQL 数据库托管实例的更好支持。
- 修复了用户无法为 SQL Server 2014 或早期版本创建目录的问题。
- 修复了两个有关报表问题：
   - 删除了 Azure 服务器的计算机名称。
   - 改进了对本地化对象名称的处理方式。


### <a name="known-issues"></a>已知问题

使用新的“常规用途”或“业务关键”Azure SQL 数据库版本时，部分对话框显示版本无效错误。

## <a name="downloadssdtmediadownloadpng-ssms-176httpsgomicrosoftcomfwlinklinkid870039"></a>![下载](../ssdt/media/download.png) [SSMS 17.6](https://go.microsoft.com/fwlink/?linkid=870039)

生成号：14.0.17230.0<br>
发布日期：2018 年 3 月 20 日

[中文（中国）](https://go.microsoft.com/fwlink/?linkid=870039&clcid=0x804) | [中文（台湾）](https://go.microsoft.com/fwlink/?linkid=870039&clcid=0x404) | [英语（美国）](https://go.microsoft.com/fwlink/?linkid=870039&clcid=0x409) | [法语](https://go.microsoft.com/fwlink/?linkid=870039&clcid=0x40c) | [德语](https://go.microsoft.com/fwlink/?linkid=870039&clcid=0x407) | [意大利语](https://go.microsoft.com/fwlink/?linkid=870039&clcid=0x410) | [日语](https://go.microsoft.com/fwlink/?linkid=870039&clcid=0x411) | [朝鲜语](https://go.microsoft.com/fwlink/?linkid=870039&clcid=0x412) | [葡萄牙语（巴西）](https://go.microsoft.com/fwlink/?linkid=870039&clcid=0x416) | [俄语](https://go.microsoft.com/fwlink/?linkid=870039&clcid=0x419) | [西班牙语](https://go.microsoft.com/fwlink/?linkid=870039&clcid=0x40a)

### <a name="whats-new"></a>新增功能

**常规 SSMS**

SQL 数据库托管实例：

- 添加了对 [Azure SQL 数据库托管实例](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance)的支持。 Azure SQL 数据库托管实例（预览版）是 Azure SQL 数据库的一种新风格，提供与本地 SQL Server 的接近 100% 的兼容性，是一个解决常见安全问题的本机[虚拟网络 (VNet)](https://docs.microsoft.com/azure/virtual-network/virtual-networks-overview) 实现和一个有利于本地 SQL Server 客户的[业务模型](https://azure.microsoft.com/pricing/details/sql-database/)。
- 支持常见管理方案，例如：
   - 创建和更改数据库。
   - 备份和还原数据库。
   - 导入、导出、提取和发布数据层应用程序。
   - 查看和更改服务器属性。
   - 完全支持对象资源管理器。
   - 编写数据库对象的脚本。
   - 支持 SQL 代理作业。
   - 支持链接服务器。
- 在[此处](https://azure.microsoft.com/blog/migrate-your-databases-to-a-fully-managed-service-with-azure-sql-database-managed-instance/)了解有关托管实例的更多信息。

对象资源管理器：
- 添加了设置，以便在从对象资源管理器拖放至查询窗口时，不强制使用括号括住名称。 （用户建议 [32911933](https://feedback.azure.com/forums/908035-sql-server/suggestions/32911933) 和 [32671051](https://feedback.azure.com/forums/908035-sql-server/suggestions/32671051)。）

数据分类：
- 一般改进和 bug 修复。

**Integration Services (IS)**

- 添加了支持，便于将包部署到 [SQL 数据库托管实例](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance)。

### <a name="bug-fixes"></a>Bug 修复

**常规 SSMS**

数据分类：

- 修复了数据分类中的问题，该问题导致显示的新添加的分类包含过时的信息类型和敏感度标签。
- 修复了面向设置为区分大小写的排序规则的服务器集时，数据分类不起作用的问题。
        
Always On：

- 修复了服务器设置为区分大小写的排序规则时，单击“收集延迟数据”可能导致错误的 AG 显示仪表板中的问题。
- 修复了群集服务关闭时，SSMS 错误地将 AG 报告为分布式的问题。
- 修复了使用“创建可用性组”对话框创建 AG 时需要 ReadOnlyRoutingUrl 的问题。
- 修复了主数据库出现故障，手动故障转移到辅助数据库时将引发 NullReferenceException 的问题。
- 修复了使用备份/还原创建可用性组以在次要副本上初始化数据库时，将在默认目录中创建数据库文件的问题。 修复包括：
   - 添加数据/日志目录验证程序。
   - 仅在副本位于不同于主要副本的 OS 上时才执行文件重定位操作。
- 修复了 SSMS 向导不生成 CLUSTER_TYPE 选项，导致辅助联接失败的问题。

安装程序：
- 修复了在非默认位置安装 SSMS 时，尝试通过安装“升级包”升级 SSMS 失败的问题。

SMO：
- 修复了在 SQL Server 2016 及更高版本中编写表的脚本可能需要多达 30 秒（现在减少到了小于 1 秒）的性能问题。

对象资源管理器：
- 修复了在尝试展开对象资源管理器中的管理节点时，SSMS 可能会引发“不能将对象从 DBNull 强制转换为其他类型”异常的问题。
- 修复了在用户定义的 PS 配置文件发出输出时，启动 PowerShell 未能检测到 SQLServer 模块的问题。
- 修复了右键单击对象资源管理器中的表或索引节点时，可能发生的间歇性挂起的问题。

数据库邮件：
- 修复了尝试显示/管理 16 个以上的配置文件时，数据库邮件配置向导引发异常的问题。


**Analysis Services (AS)**

- 修复了修改 SSMS 中 1400 兼容性级别模型上的数据源后，所做更改未保存到服务器的问题。

**Integration Services (IS)**

- 修复了连接到 SQL 数据库托管实例时，SSMS 未显示 SSIS 目录节点和报表的问题

### <a name="known-issues"></a>已知问题

> [!WARNING]
> 存在已知问题：当使用[维护计划](../relational-databases/maintenance-plans/maintenance-plans.md)时，SSMS 17.6 变得不稳定，甚至崩溃。 如果使用维护计划，请勿安装 SSMS 17.6。 如果已经安装 SSMS 17.6，且此问题正在产生不良影响，请降级到 17.5。 



## <a name="downloadssdtmediadownloadpng-ssms-175httpsgomicrosoftcomfwlinklinkid867670"></a>![下载](../ssdt/media/download.png) [SSMS 17.5](https://go.microsoft.com/fwlink/?linkid=867670)
正式发布版 | 内部版本号：14.0.17224.0

[中文（中国）](https://go.microsoft.com/fwlink/?linkid=867670&clcid=0x804) | [中文（台湾）](https://go.microsoft.com/fwlink/?linkid=867670&clcid=0x404) | [英语（美国）](https://go.microsoft.com/fwlink/?linkid=867670&clcid=0x409) | [法语](https://go.microsoft.com/fwlink/?linkid=867670&clcid=0x40c) | [德语](https://go.microsoft.com/fwlink/?linkid=867670&clcid=0x407) | [意大利语](https://go.microsoft.com/fwlink/?linkid=867670&clcid=0x410) | [日语](https://go.microsoft.com/fwlink/?linkid=867670&clcid=0x411) | [朝鲜语](https://go.microsoft.com/fwlink/?linkid=867670&clcid=0x412) | [葡萄牙语（巴西）](https://go.microsoft.com/fwlink/?linkid=867670&clcid=0x416) | [俄语](https://go.microsoft.com/fwlink/?linkid=867670&clcid=0x419) | [西班牙语](https://go.microsoft.com/fwlink/?linkid=867670&clcid=0x40a)

### <a name="whats-new"></a>新增功能

**常规 SSMS**

数据发现和分类：

- 添加了新的 SQL 数据发现和分类功能，可用于发现数据库中的敏感数据并对其进行分类、标记和报告。 
- 自动发现最敏感的数据（如商业、金融、医疗和 PII 等）并对其进行分类在组织的信息保护中可起到关键作用。
- 详细了解 [SQL 数据发现和分类](../relational-databases/security/sql-data-discovery-and-classification.md)。

查询编辑器：

- 为 Azure SQL DW 的带分隔符的文本外部文件格式添加了 SkipRows 选项的支持。 此功能允许用户在将带分隔符的文本文件加载到 SQL DW 时，跳过指定的行数。 还为 FIRST_ROW 关键字添加了相应的 IntelliSense/SMO 支持。 

Showplan：

- 为 SQL 数据仓库启用了“显示估计计划”按钮
- 添加了新显示计划属性 EstimateRowsWithoutRowGoal；还向 QueryTimeStats: UdfCpuTime 和 UdfElapsedTime 添加了新显示计划属性。 有关详细信息，请参阅 [SQL Server 2017 CU3 中添加的查询执行计划中的优化器行目标信息](http://support.microsoft.com/help/4051361)。



### <a name="bug-fixes"></a>Bug 修复

**常规 SSMS**

Showplan：

- 修复了实时查询统计信息运行时间，以显示引擎执行时间（而非 LQS 连接运行时间）。
- 修复了显示计划无法识别应用逻辑运算符（如 GbApply 和 InnerApply）的问题。
- 修复了与 ExchangeSpill 相关的问题。

查询编辑器：

- 修复了在执行由“SET SHOWPLAN_ALL ON”开头的简单查询时，与 SPID 相关的问题， 例如 SSMS 无法引发“输入字符串格式不正确。(mscorlib)”等错误。 


SMO：

- 修复了当服务器排序规则区分大小写时，SMO 无法提取 AvailabilityReplica 属性的问题（修复后，SSM 可显示错误消息，例如“无法绑定多部分标识符 a.delimited。”）
- 修复了 DatabaseScopedConfigurationCollection 类中无法正确处理排序规则的问题（修复后，右键单击在具有区分大小写排序规则的服务器中运行的数据库时，在区域设置为土耳其语的 ma 计算机上运行的 SSMS 可显示错误，如“旧版基数估计不是有效范围配置”）。
- 修复了 JobServer 类中 SMO 无法在 SQL 2005 服务器上提取 SQL 代理属性的问题（修复后，SSMS 可引发如“无法向局部变量分配默认值。 必须声明标量变量“\@ServiceStartMode”的错误，此外，SSMS 不会在对象资源管理器中显示 SQL 代理节点）。

模板： 

- “数据库邮件”：修复了几个拼写错误 [(https://feedback.azure.com/forums/908035/suggestions/33143512)](https://feedback.azure.com/forums/908035/suggestions/33143512)。  

对象资源管理器：
- 修复了索引的托管压缩失败的问题 (https://feedback.azure.com/forums/908035-sql-server/suggestions/32610058-ssms-17-4-error-when-enabling-page-compression-o)。

审核：
- 修复了“合并审核文件”功能的问题。
<br>

### <a name="known-issues"></a>已知问题

数据分类：
- 如果删除一个分类并为相同的列手动添加一个新分类，则旧信息类型和敏感标签将被分配给主视图中的该列。<br>
解决方法：在将分类添加回主视图之后且在保存之前，先分配新信息类型和敏感标签。


## <a name="downloadssdtmediadownloadpng-ssms-174httpsgomicrosoftcomfwlinklinkid864329"></a>![download](../ssdt/media/download.png) [SSMS 17.4](https://go.microsoft.com/fwlink/?linkid=864329)
正式发布版 | 内部版本号：14.0.17213.0

[中文（中国）](https://go.microsoft.com/fwlink/?linkid=864329&clcid=0x804) | [中文（台湾）](https://go.microsoft.com/fwlink/?linkid=864329&clcid=0x404) | [英语（美国）](https://go.microsoft.com/fwlink/?linkid=864329&clcid=0x409) | [法语](https://go.microsoft.com/fwlink/?linkid=864329&clcid=0x40c) | [德语](https://go.microsoft.com/fwlink/?linkid=864329&clcid=0x407) | [意大利语](https://go.microsoft.com/fwlink/?linkid=864329&clcid=0x410) | [日语](https://go.microsoft.com/fwlink/?linkid=864329&clcid=0x411) | [朝鲜语](https://go.microsoft.com/fwlink/?linkid=864329&clcid=0x412) | [葡萄牙语（巴西）](https://go.microsoft.com/fwlink/?linkid=864329&clcid=0x416) | [俄语](https://go.microsoft.com/fwlink/?linkid=864329&clcid=0x419) | [西班牙语](https://go.microsoft.com/fwlink/?linkid=864329&clcid=0x40a)


### <a name="whats-new"></a>新增功能

**常规 SSMS**

漏洞评估：
- 添加了一个新的 SQL 漏洞评估服务，以扫描数据库的潜在漏洞和最佳方案偏差，如配置错误、权限过多和敏感数据公开。 
- 评估结果包括旨在解决每个问题的可操作步骤，并提供自定义修正脚本（若适用）。 可以为每个环境自定义评估报表并进行调整以满足特定需求。 访问 [SQL 漏洞评估](https://docs.microsoft.com/sql/relational-databases/security/sql-vulnerability-assessment)了解详细信息。

SMO：
- 修复了 HasMemoryOptimizedObjects 在 Azure 上引发异常的问题。
- 添加了对新 CATALOG_COLLATION 功能的支持。

AlwaysOn 仪表板：
- 可用性组中的延迟分析有所改进。
- 添加了两个新报表：AlwaysOn\_Latency\_Primary 和 AlwaysOn\_Latency\_Secondary。

Showplan：
- 已更新指向正确文档的链接。
- 允许直接从生成的实际计划进行单个计划分析。
- 新图标集。
- 添加了对识别 GbApply、InnerApply 等“应用逻辑运算符”的支持。
        
XE 探查器：
- 更名为 XEvent 探查器。
- 默认情况下，停止/启动菜单命令会立即停止/启动会话。
- 已启用键盘快捷方式（例如，用于搜索的 CTRL-F）。
- 向 XEvent 探查器会话中的相应事件添加了 database\_name 和 client\_hostname 操作。 为了使更改生效，你可能需要删除服务器上现有 QuickSessionStandard 或 QuickSessionTSQL 会话实例 - [连接 3142981](https://connect.microsoft.com/SQLServer/feedback/details/3142981)

命令行：
- 添加了新的命令行选项 (“-G”)，可以用于自动将 SSMS 连接到使用 Active Directory 身份验证（“集成”或“密码”）的服务器/数据库。 有关详细信息，请参阅 [Ssms 实用工具](ssms-utility.md)。

导入平面文件向导：
- 添加了一种方式，以在创建表时选择默认名称 (“dbo”) 以外的架构名称。

查询存储：
- 在展开查询存储可用报表列表时，还原了“回归查询”报表。

**Integration Services (IS)**
- 在部署向导中添加了包验证函数，可帮助用户找出 SSIS 包内在 Azure SSIS IR 中不受支持的组件。

### <a name="bug-fixes"></a>Bug 修复

**常规 SSMS**

- 对象资源管理器：
    - 修复了表值函数节点未显示在数据库快照中的问题 - [连接 3140161](https://connect.microsoft.com/SQLServer/feedback/details/3140161)。
    - 在服务器具有 autoclose 数据库的情况下，提高了在展开“数据库”节点时的性能。
- 查询编辑器：
    - 修复了 IntelliSense 对于无权访问 master 数据库的用户不可用的问题。
    - 修复在远程计算机连接关闭时导致 SSMS 在某些情况下崩溃的问题 - [连接 3142557](https://connect.microsoft.com/SQLServer/feedback/details/3142557)。
- XEvent 查看器：
    - 重新启用了该功能，以便导出到 XEL。
    - 修复了在某些情况下用户无法加载整个 XEL 文件的问题。
- XEvent 探查器：
    - 修复了在用户没有“查看服务器状态”权限时，导致 SSMS 崩溃的问题。
    - 修复了在关闭 XE 探查器实时数据窗口时未停止基础会话的问题。
- 已注册的服务器：
    - 修复了“Move To…”命令停止工作的问题 - [连接 3142862](https://connect.microsoft.com/SQLServer/feedback/details/3142862) 和[连接 3144359](https://connect.microsoft.com/SQLServer/feedback/details/3144359/)。
- SMO：
    - 修复了 Transfer 对象上 TransferData 方法不工作的问题。
    - 修复了 Server 数据库引发暂停 SQL DW 数据库异常的问题。
    - 修复了在编写针对 SQL DW 的 SQL 数据库脚本时生成了不正确的 T-SQL 参数值的问题。
    - 修复了在编写延伸 DB 脚本时，错误发出“DATA\_COMPRESSION”选项的问题。
- 作业活动监视器：
    - 修复了在用户尝试按类别进行筛选时收到“索引已超出范围。 必须为非负数且小于集合大小。 
        参数名称：索引 (System.Windows.Forms)”错误的问题 - [连接 3138691](https://connect.microsoft.com/SQLServer/feedback/details/3138691)。
- 连接对话框：
    - 修复了对读/写域控制器不具备访问权限的域用户无法使用 SQL 身份验证登录到 SQL Server 的问题 - [连接 2373381](https://connect.microsoft.com/SQLServer/feedback/details/2373381)。
- 复制：
    - 修复了在查看 SQL Server 中的请求订阅属性时，显示一个类似于“无法将值 'null' 应用到属性 ServerInstance”的错误的问题。
- SSMS 安装：
    - 修复了 SSMS 安装错误导致计算机上所有已安装产品都要进行重新配置的问题。
- 用户设置：
   - 美国政府 sovereign 云用户可以利用此修复，通过通用身份验证和 Azure Active Directory 登录，使用 SSMS 不间断地访问其 Azure SQL 数据库和 ARM 资源。  使用以前版本 SSMS 的用户需要打开“工具”|“选项”|“Azure 服务”并在“资源管理”下，将“Active Directory 颁发机构”属性的配置更改为 https://login.microsoftonline.us。

**Analysis Services (AS)**

- 探查器：修复了尝试使用 Window 身份验证连接 Azure AS 时的问题。
- 修复了在取消有关 1400 模型的连接详细信息时可能会导致崩溃的问题。
- 刷新凭据时，在连接属性对话框中设置 Azure blob 密钥，它将被直观屏蔽。
- 修复了在搜索时，Azure Analysis Services 用户选择对话框显示应用程序 ID guid 而不是对象 ID 的问题。
- 修复了浏览数据库\MDX 查询设计器工具栏中导致图标不正确地映射到某些按钮的问题。
- 修复了阻止通过 msmdpump IIS http/https 地址连接到 SSAS 的问题。
- Azure Analysis Services 用户选取器对话框中的多个字符串现在均已转换为其他语言。
- MaxConnections 属性现对表格模型中的数据源可见。
- 现在，部署向导将为 Azure AS 角色成员生成正确的 JSON 定义。
- 修复了在 SQL 探查器中当选择针对 Azure AS 的 Windows 身份验证时仍会提示登录的问题。



## <a name="downloadssdtmediadownloadpng-ssms-173httpsgomicrosoftcomfwlinklinkid858904"></a>![下载](../ssdt/media/download.png) [SSMS 17.3](https://go.microsoft.com/fwlink/?linkid=858904)
正式发布版 | 内部版本号：14.0.17199.0

[中文（中国）](https://go.microsoft.com/fwlink/?linkid=858904&clcid=0x804) | [中文（台湾）](https://go.microsoft.com/fwlink/?linkid=858904&clcid=0x404) | [英语（美国）](https://go.microsoft.com/fwlink/?linkid=858904&clcid=0x409) | [法语](https://go.microsoft.com/fwlink/?linkid=858904&clcid=0x40c) | [德语](https://go.microsoft.com/fwlink/?linkid=858904&clcid=0x407) | [意大利语](https://go.microsoft.com/fwlink/?linkid=858904&clcid=0x410) | [日语](https://go.microsoft.com/fwlink/?linkid=858904&clcid=0x411) | [朝鲜语](https://go.microsoft.com/fwlink/?linkid=858904&clcid=0x412) | [葡萄牙语（巴西）](https://go.microsoft.com/fwlink/?linkid=858904&clcid=0x416) | [俄语](https://go.microsoft.com/fwlink/?linkid=858904&clcid=0x419) | [西班牙语](https://go.microsoft.com/fwlink/?linkid=858904&clcid=0x40a)


### <a name="enhancements"></a>增强功能

- 新添加的“导入平面文件”向导通过智能框架简化了 CSV 文件的导入体验，极大地减少了所需的用户干预或领域的专业知识。 有关详细信息，请参阅[将平面文件导入到 SQL 向导](../relational-databases/import-export/import-flat-file-wizard.md)。
- “XEvent 探查器”节点已添加到对象资源管理器。 有关详细信息，请参阅[使用 SSMS XEvent 探查器](../relational-databases/extended-events/use-the-ssms-xe-profiler.md)。
- 更新了性能仪表板历史等待报表中的等待过滤和分类。
- 添加了“预测”函数的语法检查。
- 添加了外部库管理查询的语法检查。
- 添加了对外部库管理的 SMO 支持。
- 添加了对“已注册服务器”窗口的“启动 PowerShell”支持（需要新的 SQL PowerShell 模块）。
- AlwaysOn：已为可用性组添加[只读路由支持](../database-engine/availability-groups/windows/configure-read-only-routing-for-an-availability-group-sql-server.md)。
- 添加了一个用于将跟踪详细信息发送到“Active Directory - 含 MFA 支持的通用身份验证”登录的输出窗口（默认为关闭状态；必须在“工具”>“选项”>“Azure 服务”>“Azure 云”>“ADAL 输出窗口跟踪级别”下的用户设置中开启）。 
- 查询存储： 
  - 即使 QDS 为关闭状态，只要 QDS 已记录任何数据，就可以访问查询存储 UI。
  - 查询存储 UI 现在会在所有现有报表中公开等待分类。 这会让客户解锁顶级等待查询等方案。
- 包含可选的脚本参数标头（默认为关闭状态；可在“工具”>“选项”>“SQL Server 对象资源管理器”>“脚本”>“包括脚本参数标头”下的用户设置中启用）- [连接项 3139199](https://connect.microsoft.com/SQLServer/feedback/details/3139199)。
- 已删除“RC”商标。

### <a name="bug-fixes"></a>Bug 修复

**常规 SSMS**

- XEvent： 
   - 修复了 SSMS 仅打开 .xel 文件中的部分事件的问题。
   - 改进了默认数据库不是“master”时的“查看实时数据”体验 - [连接项 1222582](https://connect.microsoft.com/SQLServer/feedback/details/1222582)。
- AlwaysOn：修复了“还原日志备份”可能出现故障的问题，其错误信息为“此备份集中的日志终止于 LSN x，该日志过早地应用到了数据库中”。
- 作业活动监视器：修复了不一致的图标 - [连接项 3133100](https://connect.microsoft.com/SQLServer/feedback/details/3133100)。
- 查询存储：修复了用户无法为查询存储报表选择“自定义”日期范围的问题。 链接到下面的连接项。
   - [连接项 3139842](https://connect.microsoft.com/SQLServer/feedback/details/3139842)
   - [连接项 3139399](http://connect.microsoft.com/SQLServer/feedback/details/3139399)
- 修复了保存的信息具有命名的数据库和用户选择 <default> 时，连接对话框未“清除”最近使用的数据库的问题。
- 对象脚本：
    - 修复了用户在服务器上具有暂停的 DW 数据库，但选择了其他非 DW 数据库并尝试进行脚本编辑，在该情况下“生成数据库脚本”无法正常工作并引发了错误的问题。
    - 修复了脚本化存储过程的标头与脚本设置不匹配，而导致生成误导性的脚本的问题 - [连接项 3139784](http://connect.microsoft.com/SQLServer/feedback/details/3139784)。
    - 面向 SQL Azure 对象时，重新启用了“脚本”按钮。
    - 修复了连接到 Azure SQL 数据库时，SSMS 不允许在某些对象（UDF、视图、SP、触发器）上为“更改”或“执行”编写脚本的问题 - [连接项 3136386](https://connect.microsoft.com/SQLServer/feedback/details/3136386)。
- 查询编辑器：
  - 改进了面向 Azure SQL 数据库时的智能功能。
  - 修复了查询由于身份验证令牌（通用身份验证）过期而失败的问题。
  - 改进了针对 Azure SQL 数据库工作时的智能功能（具体来说，连接到 Azure SQL 数据库时，会使用最新的 T-SQL 语法 (140)）。
  - 修复了在服务器上使用指向非数据仓库数据库的连接打开查询窗口，这一操作会导致该服务器指向数据仓库数据库的所有后续查询窗口引发各种有关不受支持的类型/选项的错误的问题。
- Always On：
   - 向 AlwaysOn 仪表板和 AG 属性页添加了种子设定模式列。
   - 修复了主系统为 Windows 时无法创建 Linux AG 的问题 - [连接项 3139856](https://connect.microsoft.com/SQLServer/feedback/details/3139856)。
- 修复了运行查询时 SSMS 中出现的多个“内存不足”的问题 - [连接项 2845190](https://connect.microsoft.com/SQLServer/feedback/details/2845190)、[连接项 3123864](https://connect.microsoft.com/SQLServer/feedback/details/3123864)。
- 探查器： 
   - 修复了面向 SQL 2005 时探查器不工作的问题。
   - 修复了探查器不遵循“信任服务器证书”连接选项的问题。
- 活动监视器：修复了指向在 Linux 上运行的 SQL Server 时活动监视器不工作的问题。
- 修复了 SMO 传输类的相关问题，即它不会传输外部数据源或外部文件格式对象，这些类型的对象现在应正确包含在传输中。
- 已注册的服务器：
   - 启用了 UA 服务器的多服务器查询（它会尝试在组中为每个 UA 服务器使用相同的令牌）。
- AD 通用身份验证：
   - 修复了不支持 Azure AD 身份验证的问题。
   - 修复了表格/视图设计器不工作的问题。
   - 修复了“选择前 1000 行”和“编辑前 200 行”不工作的问题。
- 数据库还原：修复了将文件移动到另一个位置时，还原操作会忽略路径中最后一个文件夹的问题。
- 压缩向导：
   - 修复了索引的管理压缩向导的相关问题；修复了压缩数据向导在 SQL 2016 和更低版本中中断的问题。
        https://connect.microsoft.com/SQLServer/feedback/details/3139342
   - 向 Azure 表和索引添加了压缩向导。
- Showplan： 
   - 修复了未识别 PDW 运算符的问题。
- 服务器属性：
   - 修复了无法修改服务器处理器关联的问题。


**Analysis Services (AS)**

- 修复了有关部署向导的大量问题，以支持表格 1400 兼容级别模型和 Power Query 数据源。
- 从命令行运行时，部署向导现可部署到 AS Azure 中。
- 在 AS Azure 中使用 Windows 身份验证时，用户现在可在对象资源管理器中看到用户帐户的正确名称。


### <a name="known-issues-in-this-173-release"></a>此 17.3 版本中的已知问题：

**常规 SSMS**

- 对于使用含 MFA 的 UA 的 Azure AD 身份验证，不支持以下 SSMS 功能：
   - 对于 Azure AD 身份验证，不支持数据库引擎优化顾问；存在以下已知问题：向用户显示的错误消息“无法加载文件或程序集 Microsoft.IdentityModel.Clients.ActiveDirectory,…”令人费解，而不是预期的“数据库引擎优化顾问不支持 Microsoft Azure SQL 数据库。 (DTAClient)”。
- 尝试在 DTA 中分析查询会导致发生错误：“对象必须实现 IConvertible。 (mscorlib)”。
- 回归的查询缺少对象资源管理器中报表的查询存储列表。
   - 解决方法：右键单击“查询存储”节点，然后选择“查看回归的查询”。

**Integration Services (IS)**

- 对于 Scale Out 中的包执行，[catalog].[event_messagea] 中的 [execution_path] 不正确。[execution_path] 以“\Package”开头，而不是以包可执行文件的对象名称开头。 在 SSMS 中查看包执行的概述报表时，执行概述中“执行路径”的链接不起作用。 解决方法是，在概述报表上单击“查看消息”，检查所有事件消息。


## <a name="downloadssdtmediadownloadpng-ssms-172httpsgomicrosoftcomfwlinklinkid854085"></a>![download](../ssdt/media/download.png) [SSMS 17.2](https://go.microsoft.com/fwlink/?linkid=854085)
公开发布 | 版本号：14.0.17177.0

[中文（中国）](https://go.microsoft.com/fwlink/?linkid=854085&clcid=0x804) | [中文（台湾）](https://go.microsoft.com/fwlink/?linkid=854085&clcid=0x404) | [英语（美国）](https://go.microsoft.com/fwlink/?linkid=854085&clcid=0x409) | [法语](https://go.microsoft.com/fwlink/?linkid=854085&clcid=0x40c) | [德语](https://go.microsoft.com/fwlink/?linkid=854085&clcid=0x407) | [意大利语](https://go.microsoft.com/fwlink/?linkid=854085&clcid=0x410) | [日语](https://go.microsoft.com/fwlink/?linkid=854085&clcid=0x411) | [朝鲜语](https://go.microsoft.com/fwlink/?linkid=854085&clcid=0x412) | [葡萄牙语（巴西）](https://go.microsoft.com/fwlink/?linkid=854085&clcid=0x416) | [俄语](https://go.microsoft.com/fwlink/?linkid=854085&clcid=0x419) | [西班牙语](https://go.microsoft.com/fwlink/?linkid=854085&clcid=0x40a)

### <a name="enhancements"></a>增强功能

- 多重身份验证 (MFA)
  - 用于含多重身份验证的通用身份验证的多用户 Azure AD 身份验证（具有 MFA 的 UA）
  - 为含 MFA 的通用身份验证添加了新的用户凭据输入字段，以支持多用户身份验证。
- 连接对话框现在支持以下 5 种身份验证方法：
  - Windows 身份验证
  - SQL Server 身份验证
  - Active Directory - 含 MFA 支持的通用身份验证
  - Active Directory - 密码
  - Active Directory - 集成

- DacFx 向导的数据库导出/导入使用含 MFA 的通用身份验证。
- 有关 API 支持，请参阅 [IUniversalAuthProvider 接口](https://msdn.microsoft.com/library/microsoft.sqlserver.dac.iuniversalauthprovider.aspx)。
- 具有 MFA 的 Azure AD 通用身份验证使用的 ADAL 托管库已升级到 3.13.9 版本。
- 此外，加入了新 CLI 接口，支持用于 SQL 数据库和 SQL 数据仓库的 Azure AD 管理设置。

 有关 Active Directory 身份验证方法的详细信息，请参阅[使用 SQL 数据库和 SQL 数据仓库进行通用身份验证（MFA 的 SSMS 支持）](https://docs.microsoft.com/azure/sql-database/sql-database-ssms-mfa-authentication)和[配置 SQL Server Management Studio 的 Azure SQL 数据库多重身份验证](https://docs.microsoft.com/azure/sql-database/sql-database-ssms-mfa-authentication-configure)。

- 输出窗口具有在对象资源管理器节点扩展期间运行的查询条目
- 为 Azure SQL 数据库启用了查看设计器
- SSMS 中的对象资源管理器脚本对象的默认脚本选项已更改：
  - 以前，新安装的默认值是将生成的脚本面向最新版本的 SQL Server（当前为 SQL Server 2017）。
  - 在 SSMS 17.2 中，添加了一个新选项：将脚本设置与源进行匹配。 当设置为 True 时，生成的脚本面向与要从其中脚本化对象的服务器相同的版本、引擎类型和引擎版本。
  - 默认情况下，“将脚本设置与源进行匹配”值设置为 True，因此新安装的 SSMS 将自动默认始终将对象脚本化到与原始服务器相同的目标。
  - 当“将脚本设置与源进行匹配”设置为 False 时，正常的脚本目标选项将被启用，并像以前那样运行。
    - 此外，所有脚本选项已移动到其各自的部分 - 版本选项。 它们不再位于“常规脚本选项”下。

- 在“从 URL 还原”中增加了对国家云的支持
- QueryStoreUI 报表现在支持来自 sys.query_store_runtime_stats 的其他指标（RowCount、DOP、CLR Time 等）。
- Azure SQL 数据库现在支持 IntelliSense
    - https://connect.microsoft.com/SQLServer/feedback/details/3100677/ssms-2016-would-be-nice-to-have-intellisense-on-azure-sql-databases
- 安全性：连接对话框将默认不信任服务器证书，并为 Azure SQL DB 连接请求加密
- 对 Linux 上的 SQL Server 支持的常规改进：
 - 重新使用数据库邮件节点
 - 解决了与路径相关的其他问题
 - 活动监视器更加稳定
 - “连接属性”对话框将显示正确的平台
- 现在可将性能仪表板服务器报表用作默认报表：
  - 可连接到 SQL Server 2008 和更新版本。
  - 缺失索引子报表使用计分来帮助确定最有用的索引。
  - 历史等待统计信息子报表现在将等待聚合为类别。 默认情况下，将筛选出空闲和睡眠等待。
  - 新的历史闩锁子报表。
- Showplan 节点搜索允许在计划属性中进行搜索。 轻松查找任何操作符属性，如表名。 在查看计划时使用此选项：
  - 右键单击计划，并在上下文菜单中单击“查找节点”选项
  - 使用 Ctrl+F


**Analysis Services (AS)**

- 用于在 SSMS 中的 AS Azure 模型中无电子邮件地址用户的新的 AAD 角色成员选择

**Integration Services (IS)**

- 向 SSIS 的执行报表添加了新列（“执行计数”）

### <a name="known-issues-in-this-release"></a>此版本中的已知问题：

- 使用“Active Directory - 含 MFA 支持的通用身份验证”身份验证的查询窗口在打开一小时后尝试执行查询时可能会遇到类似以下错误：

   `Msg 0, Level 11, State 0, Line 0
The connection is broken and recovery is not possible. The client driver attempted to recover the connection one or more times and all attempts failed. Increase the value of ConnectRetryCount to increase the number of recovery attempts.`

   重新运行查询应忽略错误并成功。

- 对于使用含 MFA 的通用身份验证的 Azure AD 身份验证，不支持以下 SSMS 功能：
  - “新建表/视图”设计器显示旧式登录提示，并且不适用于 Azure AD 身份验证。
  - “编辑前 200 行”功能不支持 Azure AD 身份验证。
  - “已注册的服务器”组件不支持 Azure AD 身份验证。
  - “数据库引擎优化顾问”不支持 Azure AD 身份验证。 存在以下已知问题：向用户显示的错误消息“无法加载文件或程序集 Microsoft.IdentityModel.Clients.ActiveDirectory”无用， 而不是显示“数据库引擎优化顾问不支持 Microsoft Azure SQL 数据库 (DTAClient)”。

**Analysis Services (AS)**

- SSAS 中的对象资源管理器将不会在 AS Azure 连接属性中显示 Windows 身份验证用户名。

### <a name="bug-fixes"></a>Bug 修复

- 修复了尝试打印查询结果（打印成文本）时的问题。  https://connect.microsoft.com/SQLServer/feedback/details/3055225/
- 修复了在 SQL Azure 数据库上脚本化删除这些对象时 SSMS 未正确删除表和其他对象的问题。
- 修复了以下问题：SSMS 偶尔拒绝启动，出现错误“找不到一个或多个组件。 请重新安装应用程序”
- 修复了 SSMS UI 中的 SPID 可能会过时和不同步的问题。 https://connect.microsoft.com/SQLServer/feedback/details/1898875
- 修复了 SSMS（无提示）安装中 /passive 参数被视为 /quiet 的问题。
- 修复了 SSMS 偶尔在启动时引发“未将对象引用设置为对象的实例”错误的问题。 http://connect.microsoft.com/SQLServer/feedback/details/3134698
- 修复了“数据压缩向导”上导致 SSMS 在图形表上按“计算”会崩溃的问题
- 解决了右键单击表的索引（通过缓慢的 Internet 连接）时遇到性能问题。 https://connect.microsoft.com/SQLServer/feedback/details/3120783
- 修复了 SSMS 无法枚举使用区分大小写排序规则的服务器上的备份文件的问题。 http://connect.microsoft.com/SQLServer/feedback/details/3134787 和 https://connect.microsoft.com/SQLServer/feedback/details/3137000
- 显示计划和显示计划比较各种修复
- 修复了以下问题：除非运行 SSMS 的计算机上安装了 SQL Server，否则连接对话框不允许用户指定用于连接的“网络协议”。 https://connect.microsoft.com/SQLServer/feedback/details/3134997
- 改进了对多监视器配置的支持，其中某些 SSMS 对话框显示在“随机”位置。 在“SQL Server 对象资源管理器 | 命令”用户设置下添加了新选项“任务对话框”，以便任务对话框或属性表关闭时记住其位置。 https://connect.microsoft.com/SQLServer/feedback/details/889169、 https://connect.microsoft.com/SQLServer/feedback/details/1158271、 https://connect.microsoft.com/SQLServer/feedback/details/3135260 
- 修复了 SSMS 无法更改加密的 Azure SQL DB 的 DB 属性的问题
- 改进了“执行后放弃结果”选项。 https://connect.microsoft.com/SQLServer/feedback/details/1196581
- 改进/修复了用户无法访问其不是管理员的 Azure 订阅的问题。
- 改进了“数据库恢复”向导以保持在 OE 中选择目标数据库（无论选择什么源数据库）。 https://connect.microsoft.com/SQLServer/feedback/details/3118581
- 修复了对象资源管理器未正确排序新添加的“本机编译的存储过程”的问题。 http://connect.microsoft.com/SQLServer/feedback/details/3133365
- 修复了“SELECT TOP n ROWS”不包含“TOP”子句的问题。 对于 Azure SQLDW。 https://connect.microsoft.com/SQLServer/feedback/details/3133551 和 https://connect.microsoft.com/SQLServer/feedback/details/3135874
- QueryStoreUI：修复了非自定义时间间隔对于所有报表都无法正确工作的问题。
- Always Encrypted：
    - 改进了新 CMK 对话框中 AKV 权限状态的消息传递
    - 向 CEK 下拉列表添加了工具提示，以便更容易区分具有长名称的 CEK
    - 修复了某些 CNG 密钥存储提供程序不会显示在 Always Encrypted 的“新列主密钥”对话框中的问题
- 修复了 SSMS 连接的“应用程序名称”不一致的问题。 http://connect.microsoft.com/SQLServer/feedback/details/3135115
- 修复了 SSMS 未为 SQL Azure（具有 DATA_COMPRESSIONS 选项的表和索引）生成正确脚本的问题。 https://connect.microsoft.com/SQLServer/feedback/details/3133148
- 修复了用户无法使用 Ctrl+Q 快捷方式进行快速启动的问题（请注意：在查询编辑器中切换“IntelliSense 已启用”选项的新键绑定现在是 Ctrl+B、Ctrl+I）。 https://connect.microsoft.com/SQLServer/feedback/details/3131968
- 修复了“还原数据库”中，SSMS 在尝试从具有定义了自定义域的帐户的订阅中选择存储帐户时引发异常的问题
- 修复了“数据库关系图”中 SSMS 引发“索引超出了数组界限”错误的问题；以及用户无法将“表视图”更改为除标准之外的任何内容的问题。 https://connect.microsoft.com/SQLServer/feedback/details/3133792 和 http://connect.microsoft.com/SQLServer/feedback/details/3135326
- 修复了“备份/还原到 URL”中 SSMS 没有枚举经典存储帐户的问题。
- 修复了在尝试向 DB 角色添加架构绑定安全对象时引发异常的问题。 https://connect.microsoft.com/SQLServer/feedback/details/3118143
- 修复了 SSMS 间歇性显示错误“数据为 Null。 不能对 Null 值调用此方法或属性。”的问题 当展开表节点 http://connect.microsoft.com/SQLServer/feedback/details/3136283 时
- DTA：修复了当使用特定边界值评估分区功能时，DTAEngine.exe 因堆损坏终止的问题。


**Analysis Services (AS)**

- 修复了如果 DB 具有与 ID 不同的名称，AS 还原数据库将失败并出现错误的问题
- 修复了导致 DAX 查询窗口忽略用于切换已启用 IntelliSense 功能的菜单选项的问题
- 修复了阻止通过 msmdpump IIS http/https 地址连接到 SSAS 的问题
- 允许使用包含分号的密码连接到 AS Azure
- 使用“跳过成员身份”选项脚本化 AS 还原数据库命令将包括与 SQL Server 2017 AS 服务器或 AS Azure 一起使用时的新对应 JSON 选项
- 修复了一个非常罕见的问题，该问题可能导致删除数据库对话框在加载时出错
- 修复了尝试在包含混合了 SQL 查询和 M 分区定义的 1400 兼容级别模型中查看分区时可能会出现的问题

**Integration Services (IS)**
- 修复了无法显示 SSISDB 目录的执行信息报表的问题
- 修复了 SSMS 中与大量项目/包性能不佳相关的问题

## <a name="downloadssdtmediadownloadpng-ssms-171httpsgomicrosoftcomfwlinklinkid849819"></a>![下载](../ssdt/media/download.png) [SSMS 17.1](https://go.microsoft.com/fwlink/?linkid=849819)
公开发布 | 内部版本号：14.0.17119.0

[中文（中国）](https://go.microsoft.com/fwlink/?linkid=849819&clcid=0x804) | [中文（台湾）](https://go.microsoft.com/fwlink/?linkid=849819&clcid=0x404) | [英语（美国）](https://go.microsoft.com/fwlink/?linkid=849819&clcid=0x409) | [法语](https://go.microsoft.com/fwlink/?linkid=849819&clcid=0x40c) | [德语](https://go.microsoft.com/fwlink/?linkid=849819&clcid=0x407) | [意大利语](https://go.microsoft.com/fwlink/?linkid=849819&clcid=0x410) | [日语](https://go.microsoft.com/fwlink/?linkid=849819&clcid=0x411) | [朝鲜语](https://go.microsoft.com/fwlink/?linkid=849819&clcid=0x412) | [葡萄牙语（巴西）](https://go.microsoft.com/fwlink/?linkid=849819&clcid=0x416) | [俄语](https://go.microsoft.com/fwlink/?linkid=849819&clcid=0x419) | [西班牙语](https://go.microsoft.com/fwlink/?linkid=849819&clcid=0x40a)

### <a name="enhancements"></a>增强功能

- 现可通过探查器：“帮助”>“关于”查看发行版本号（例如 17.1）
- Analysis Service 用户可以从数据源上的上下文菜单中针对 1200 TM 模型及更高版本刷新其数据源的凭据
- 内置 SSIS 报表现在可显示 CTP 2.1 中 SSIS 扩展执行的日志
- SSIS 扩展管理应用程序
  - 查看扩展主要角色的基本信息。
  - 轻松向扩展部署添加辅助角色。
  - 查看所有扩展辅助角色及其相关基本信息，还可将它们轻松启用或禁用。

### <a name="bug-fixes"></a>Bug 修复
- Always On：
  - 修复了可用性副本的属性对于 WSFC AG 始终显示为“自动故障转移”模式的问题。
  - 修复了更新可用性组时覆盖只读路由列表的问题
- Always Encrypted：修复了生成的日志文件缺少 DacFx 生成的信息的问题。
- 显示计划：修复了用户界面总是显示非自适应联接运算符的实际联接类型属性的问题。
- 安装程序：
  - 修复了 SSMS 17.0 中断 Visual Studio 2013 上的 SSDT 的问题 [Connect 项目 3133479]
  - 修复了安装结束时单击“重启”不会重启计算机的问题
- 脚本：通过禁用选项，暂时阻止了 SSMS 尝试编写删除脚本时误删 Azure 数据库对象的问题。  即将发布的 SSMS 版本中将提供正式修复。
- 对象资源管理器：修复了使用“AS COPY”将“数据库”节点连接到创建的 Azure 数据库时此节点无法展开的问题

## <a name="downloadssdtmediadownloadpng-ssms-170httpgomicrosoftcomfwlinklinkid847722"></a>![下载](../ssdt/media/download.png) [SSMS 17.0](http://go.microsoft.com/fwlink/?LinkID=847722)
公开发布 | 内部版本号：14.0.17099.0

[中文（中国）](https://go.microsoft.com/fwlink/?linkid=847722&clcid=0x804) | [中文（台湾）](https://go.microsoft.com/fwlink/?linkid=847722&clcid=0x404) | [英语（美国）](https://go.microsoft.com/fwlink/?linkid=847722&clcid=0x409) | [法语](https://go.microsoft.com/fwlink/?linkid=847722&clcid=0x40c) | [德语](https://go.microsoft.com/fwlink/?linkid=847722&clcid=0x407) | [意大利语](https://go.microsoft.com/fwlink/?linkid=847722&clcid=0x410) | [日语](https://go.microsoft.com/fwlink/?linkid=847722&clcid=0x411) | [朝鲜语](https://go.microsoft.com/fwlink/?linkid=847722&clcid=0x412) | [葡萄牙语（巴西）](https://go.microsoft.com/fwlink/?linkid=847722&clcid=0x416) | [俄语](https://go.microsoft.com/fwlink/?linkid=847722&clcid=0x419) | [西班牙语](https://go.microsoft.com/fwlink/?linkid=847722&clcid=0x40a)

### <a name="enhancements"></a>增强功能 

- 升级包和 Windows Software Update Services (WSUS) 
    - 未来的 17.X 版本将包括较小的累积更新包 
  - 更新包还将发布到 WSUS 目录  
- 图标更新
    - 已更新图标，其与 VS Shell 提供的图标保持一致并且支持高 DPI 分辨率
    - 新增了 SSMS 和探查器程序图标，用于区分 16.X 和 17.X 版本
- SQL PowerShell 模块
  - 已从 SSMS 中删除 SQL Server PowerShell 模块，现通过 PowerShell 库提供（现在需要 PowerShell 5.0 才能支持模块版本控制）
  - 对一些 SMO 对象的“演示”（格式设置）进行了其他改进（例如，数据库现在显示大小和可用空间，表显示行计数和空间使用情况）
  - 对通过 OE 中的“启动 PowerShell”菜单调用的 PowerShell 命令提示符添加了着色
  - 向 AG cmdlet（New-SqlAvailabilityGroup、Join-SqlAvailabilityGroup 和 Set-SqlAvailabilityGroup cmdlet）添加了 -ClusterType 和 -RequiredCopiesToCommit 参数
  - 向 Add-SqlAzureAuthenticationContext cmdlet 添加了 -ActiveDirectoryAuthority 和 -AzureKeyVaultResourceId 参数
  - 添加了 Revoke SqlAvailabilityGroupCreateAnyDatabase、Grant-SqlAvailabilityGroupCreateAnyDatabase 和 Set-SqlAvailabilityReplicaRoleToSecondary cmdlet
  - 向 Set-SqlAvailabilityReplica 和 New-SqlAvailabilityReplica cmdlet 添加了 -SeedingMode 参数
  - 向 Get-SqlDatabase 添加了 -ConnectionString 参数
- Linux 上的 SQL Server
    - 全面改进和修复了日志传送
  - 添加了对本机 Linux 路径附加、还原和备份数据库的支持
  - 添加了对审核日志目标文件夹的本机 Linux 路径的支持
- Analysis Services
  - DAX 查询窗口：
    - 编辑器中的括号匹配
    - DEFINE MEASURE 和 DEFINE VAR 语法支持
    - 多种 Intellisense 改进
  - 通用身份验证
    - 允许用户指定用户名而不指定密码，然后 Azure 登录对话框将处理连接
  - SSMS PQ 集成： 
    - 支持对结构化数据源编写脚本 
    - 在 PQ UI 中查看和编辑结构化数据源
- 新增了“添加唯一约束”模板
- Showplan
    - 在运行时间的属性窗口中显示线程最大值（而非总和）
    - 公开了新的内存授予操作符属性
    - 在实时查询统计信息中启用了“编辑查询”按钮
    - 支持交错执行
  - 为“分析实际执行计划”提供了新选项
  - 对显示计划比较进行了整体改进
  - 在“显示计划比较”功能中引入了功能，可用于查找两个查询计划的匹配节点间基数估计的显著区别，并对可能的根本原因执行基本分析
- 从已注册的服务器资源管理器中删除了配置管理器
- 支持从 Azure Blob 存储中读取审核日志
- 添加了“始终加密的参数化”，有关详细信息请参阅[本页](https://blogs.msdn.microsoft.com/sqlsecurity/2016/12/13/parameterization-for-always-encrypted-using-ssms-to-insert-into-update-and-filter-by-encrypted-columns/) 
- AAD 通用身份验证连接到 Azure SQL DB 支持自定义租户 ID 
- 为 Azure SQL 数据库生成脚本，现在为全文、规则和数据库编写脚本
- 解决了 SSMS 和探查器的初始屏幕的外观方案问题
- 从 SSMS 删除了实用工具控制点 UI
- SSMS 现在可以创建“PremiumRS”版 SQL Azure 数据库
- Always On 可用性组
  - 添加了对新群集类型 EXTERNAL 和 NONE 的支持
    - 添加了对 Linux SQL Server 的支持
    - 为初始数据同步添加了自动种子设定选项
    - 修复了一些不足，包括终结点 URL 处理、DB 刷新和用户界面布局
    - 删除了 Azure 副本相关的功能
  - 改进了几个可用性组关键字的 IntelliSense
- 活动监视器
  - 在 SSMS 输出窗口中添加了新的“活动监视器”窗格
  - 将连接错误/超时消息更改为输出窗口的日志信息，而不是弹出消息
  - 删除了“概述”部分中的空图表（第 5 个图表）
  - 针对活动监视器数据收集暂停的情况，在“概述”标题中添加了“(暂停)”
  - 到 SQL Server 的图形扩展 
    - 图形节点和边界表采用了新图标
    - 图形节点和边界表将显示在“图形表”文件夹下
    - 提供了用于创建图形节点和边界表的模板
- 演示模式
    - 新增了 3 个可通过快速启动 (Ctr-Q) 执行的任务
    - PresentOn - 打开演示模式
    - PresentEdit - 编辑演示模式的演示字号。  对查询编辑器使用“文本编辑器字体”。  对其他组件使用“环境字体”。
    - RestoreDefaultFonts - 还原默认设置。
    - *注意：暂无 PresentOff 命令。请使用 RestoreDefaultFonts 关闭演示模式*

### <a name="bug-fixes"></a>Bug 修复

- 修复了通过 Surface Book 触摸板滚动显示计划时 SSMS 崩溃的问题
- 修复了获取正在还原或脱机的数据库的属性时 SSMS 长时间挂起的问题 
- 修复了无法在 RC 内部版本中打开“帮助查看器”的问题
- 修复了 SSMS 中可能缺少“维护计划任务工具箱”项的问题。
- 修复了 SSMS 中的一个问题：数据库名称包含大括号时，用户无法收缩数据库。 [连接项](https://connect.microsoft.com/SQLServer/feedback/details/3122618)
- 修复了 SSMS 尝试编写删除 Azure 数据库的脚本时导致实际删除数据库本身的问题。 [连接项](http://connect.microsoft.com/SQLServer/feedback/details/3131458/)
- 解决了没有为用户定义的表类型编写默认值的问题。 [连接项](https://connect.microsoft.com/SQLServer/feedback/details/3119027)
- 对索引中的上下文菜单进行了另一轮性能改进。 [连接项](https://connect.microsoft.com/SQLServer/feedback/details/3120783)
- 解决了将鼠标悬停在执行计划缺少的索引之上时，闪烁次数过多的问题。 [连接项](https://connect.microsoft.com/SQLServer/feedback/details/3118510)
- 解决了编写脚本时 SSMS 导致 DB 脱机的问题 [连接项](https://connect.microsoft.com/SQLServer/feedback/details/3118550)
- 对本地化（非英语）版本的 SSMS 进行了其他 UI 修复。
- 解决了定位 SQL 2016 SP1 标准版时没有“Always Encrypted 密钥”节点的问题。
- 始终加密
    - 定位 SQL 2016 RTM 标准版或任意 SQL 2014（及更低版本）服务器时，“Always Encrypted”菜单未正确启用
    - 解决了使用 CREATE OR ALTER 语法时 IntelliSense 报告错误的问题
    - 解决了当 CMK/CEK 包含应转义的字符（即用括号括住）时无法加密的问题
    - 当 SSMS 中发生内存不足异常时，用户会看到一个错误消息，建议其改用本机（64 位）PowerShell。
    - 解决了在用户使用资源组管理器订阅（而不是经典 Azure 订阅）时，AE 向导无法运行的问题
    - 解决了在用户对任何订阅都没有权限，或对任何订阅都没有 Azure Key Vault 时，AE 向导显示不正确错误消息的问题。
    - 解决了在有多个 AAD 的情况下，AE 向导中的 Azure Key Vault 登录页不显示 Azure 订阅的问题
    - 解决了 AE 向导中的 Azure Key Vault 登录页不显示用户有权读取的 Azure 订阅的问题
  - 修复了资源文件可能未正确加载而导致错误消息不准确的问题
- 改进了 SSMS 安装页上的超链接对比度
- 解决了连接 SQL Server Express (2016 SP1) 时看不到 PolyBase 节点的问题
- 修复了 SSMS 无法将 Azure DB 的兼容级别更改为 v140 的问题
- 改进了展开 Azure 数据库列表时的对象资源管理器性能 [连接项](https://connect.microsoft.com/SQLServer/feedback/details/3100675)
- 解决了对非关系服务器类型 (AS\RS\IS) 错误显示“查看 SQL Server 日志”上下文菜单项的问题 
- 解决了使用 SQL 身份验证查看 Analysis Services 分区查询的语法时看到登录失败消息的问题
- 解决了在 SSMS 中无法重命名预览 1400 兼容性级别 AS 表格模型的问题
- 解决了在模型保存失败后还原本地更改的极少数情况下，尝试在 AS 服务器上执行无效操作后可能看到“无法对模型执行操作”错误消息的问题
- 更正了 Analysis Services 同步数据库弹出式对话框中的错别字
- 在多个监视器设置中，备份/还原容器对话框出现在屏幕外。 
- 如果目标对象的名称中有 ]，则无法创建 SecurityPolicy。
- SSMS 2016 的“打开最近的文件”菜单不显示最近保存的文件。 [连接项](https://connect.microsoft.com/SQLServer/feedback/details/3113288/ssms-2016-open-recent-menu-doesnt-show-recently-saved-files)
- 删除了 VS Shell 更新后用户设置的重置。
- 修复了用户无法在 SQL Server 2017 中更改数据库兼容级别的问题。
- 使用 AAD 通用身份验证的查询窗口在一小时后无法刷新查询。
- 从 SSMS 删除了实用工具控制点 UI。
- 初始令牌过期后，AD 通用身份验证连接无法查询数据。
- 无法从 Azure SQL DB 将规则脚本编写到 Azure SQL DB。
- 解决了 SQL PowerShell 无法连接旧 SQL 实例（2014 或更早版本）的问题。 [连接项](https://connect.microsoft.com/SQLServer/feedback/details/1138754/sql-server-sqlps-powershell-module-fails-connection-to-sql-2012-instance)
- 解决了无法导入已注册的服务器时导致 SSMS 崩溃的问题。
- 解决了在用户具有数据库特定权限的情况下导致 SSMS 崩溃的问题。 
- SSMS - 查看视图时表从设计图面消失。 [连接项](https://connect.microsoft.com/SQLServer/feedback/details/2946125/ssms-tables-disappears-from-design-surface-while-reviewing-views) 
- 表滚动条不允许用户滚动表内容，仅向上/向下键允许此操作。 在尝试使用滚动条滚动（而这是一个 Bug）时，有可能滚动表内容。 [连接项](
http://connect.microsoft.com/SQLServer/feedback/details/3106561/sql-server-manager-2016-bug-in-design-view) 
- 刷新根节点后，已注册的服务器不显示图标。
- Azure v12 服务器上的“创建数据库”脚本按钮执行脚本，然后显示消息“没有要编写脚本的操作”。
- “SSMS 连接到服务器”对话框不为每个新连接清除“附加属性”选项卡。
- 生成任务脚本不会为 Azure SQL DB 生成“创建数据库”脚本。
- 视图设计器中的滚动条显示为已禁用。
- 始终加密 AVK 密钥路径不包括版本 ID。
- 减少查询窗口中引擎版本查询的数量。 [连接项](http://connect.microsoft.com/SQLServer/feedback/details/3113387)
- 错误处理加密后，刷新模块出现“始终加密”错误。
- 更改 OLTP 和 OLAP 的默认连接超时，将其从 15 秒更改为 30 秒，以修复一类被忽略的连接故障。 
- 解决了启动自定义报表时 SSMS 崩溃的问题。 [连接项](http://connect.microsoft.com/SQLServer/feedback/details/3118856)
- 修复了 Azure SQL 数据库“生成脚本...”失败的问题。
- 解决了“编写脚本为”和“生成脚本向导”问题，避免在对象脚本编写（如存储过程）时添加额外的换行符。 [连接项](http://connect.microsoft.com/SQLServer/feedback/details/3115850)
- SQLAS PowerShell 提供程序：向 Dimension 和 MeasureGroup 文件夹添加 LastProcessed 属性。 [连接项](http://connect.microsoft.com/SQLServer/feedback/details/3111879)
- 实时查询统计信息：解决了在批处理中仅显示第一个查询的问题。 [连接项] (http://connect.microsoft.com/SQLServer/feedback/details/3114221)  
- Showplan：在属性窗口中显示线程的最大值而非总和。
- 查询存储：使用高执行变体在查询中添加新报表。
- 对象资源管理器性能问题：[连接项](http://connect.microsoft.com/SQLServer/feedback/details/3114074)
    - 表的上下文菜单暂时挂起
    - 右键单击表的索引（通过远程 (Internet) 连接）时，SSMS 运行缓慢。 
    - 避免发出在服务器上排序的表查询
- 从 SSMS 删除 Azure 部署向导（向 Azure VM 部署数据库）
- 解决了 SSMS 的执行计划中不显示丢失的索引的问题[连接项](http://connect.microsoft.com/SQLServer/feedback/details/3114194)
- 解决了 SSMS 中常见的崩溃关闭问题
- 解决了对象资源管理器中，在 Polybase|扩展组节点上调用上下文菜单时出错的问题[连接项](http://connect.microsoft.com/SQLServer/feedback/details/3115128)
- 解决了尝试显示数据库上的权限时 SSMS 可能崩溃的问题
- 查询存储：查询存储报表的结果网格的上下文菜单项中的常规功能增强
- 为现有表配置“始终加密”功能失败，在不相关的对象上出错。 [连接项](http://connect.microsoft.com/SQLServer/feedback/details/3103181)
- 为现有数据库配置“始终加密”功能时，多个架构无法正常运行。 [连接项] (http://connect.microsoft.com/SQLServer/feedback/details/3109591)
- 由于数据库包含引用系统视图的视图，“始终加密、已加密列”向导失败。 [连接项] (http://connect.microsoft.com/SQLServer/feedback/details/3111925)
- 使用“始终加密”功能进行加密时，错误处理加密后刷新模块出现错误。
- 解决了“新建服务器注册”对话框中的 UI 截断问题
- 解决了 DMF 条件 UI 无法正确更新带有其中包含引号的字符串常量值的表达式的问题
- 解决了在运行自定义报表时有可能导致 SSMS 崩溃的问题
- 将“在扩展中执行…”菜单项 添加到文件夹节点
- 修复了 Azure SQL DB 防火墙白名单 IP 地址功能的问题
- 修复了 SSMS 中的一个问题：编辑 AS 多维分区的源时，此问题会导致对象引用不会设置为异常
- 修复了 SSMS 中的一个问题：删除多维 AS 服务器中的客户程序集时，此问题会导致对象引用不会设置为异常
- 修复了重命名 AS 表格 1400 db 失败的问题
- 修复了为连接属性对话框中的 1400 兼容级别 AS 表格数据源编写脚本时出现的 问题
- 消除了 AS 1400 兼容级别模型中的表至少有一个分区的假设
- 现在按 Ctrl-R 可在 SSMS DAX 查询编辑器中切换结果窗格


## <a name="downloadssdtmediadownloadpng-ssms-1653httpgomicrosoftcomfwlinklinkid840946"></a>![下载](../ssdt/media/download.png) [SSMS 16.5.3](http://go.microsoft.com/fwlink/?LinkID=840946)
公开发布 | 内部版本号 ：13.0.16106.4

[中文（中国）](https://go.microsoft.com/fwlink/?linkid=840946&clcid=0x804) | [中文（台湾）](https://go.microsoft.com/fwlink/?linkid=840946&clcid=0x404) | [英语（美国）](https://go.microsoft.com/fwlink/?linkid=840946&clcid=0x409) | [法语](https://go.microsoft.com/fwlink/?linkid=840946&clcid=0x40c) | [德语](https://go.microsoft.com/fwlink/?linkid=840946&clcid=0x407) | [意大利语](https://go.microsoft.com/fwlink/?linkid=840946&clcid=0x410) | [日语](https://go.microsoft.com/fwlink/?linkid=840946&clcid=0x411) | [朝鲜语](https://go.microsoft.com/fwlink/?linkid=840946&clcid=0x412) | [葡萄牙语（巴西）](https://go.microsoft.com/fwlink/?linkid=840946&clcid=0x416) | [俄语](https://go.microsoft.com/fwlink/?linkid=840946&clcid=0x419) | [西班牙语](https://go.microsoft.com/fwlink/?linkid=840946&clcid=0x40a)

此版本已解决以下问题：

* 解决了 SSMS 16.5.2 中引入的问题，即当表具有多个稀疏列时，导致“表”节点扩展。

* 用户可以部署包含 OData 连接管理器的 SSIS 包，这些包连接到 SSIS 目录的 Microsoft Dynamics AX / CRM Online 资源。 有关详细信息，请参阅 [OData 连接管理器](../integration-services/connection-manager/odata-connection-manager.md)。

* 为现有表配置“始终加密”功能失败，在不相关的对象上出错。 [连接 ID 3103181](https://connect.microsoft.com/SQLServer/feedback/details/3103181/setting-up-always-encrypted-on-an-existing-table-fails-with-errors-on-unrelated-objects)

* 为现有数据库配置“始终加密”功能时，多个架构无法正常运行。 [连接 ID 3109591](https://connect.microsoft.com/SQLServer/feedback/details/3109591/sql-server-2016-always-encrypted-against-existing-database-with-multiple-schemas-doesnt-work)

* 由于数据库包含引用系统视图的视图，“始终加密、已加密列”向导失败。 [连接 ID 3111925](https://connect.microsoft.com/SQLServer/feedback/details/3111925/sql-server-2016-always-encrypted-encrypted-column-wizard-failed-task-failed-due-to-following-error-cannot-save-package-to-file-the-model-has-build-blocking-errors)

* 使用“始终加密”功能进行加密时，错误处理加密后刷新模块出现错误。

* “打开最近的文件”菜单不显示最近保存的文件。 [连接 ID 3113288](https://connect.microsoft.com/SQLServer/feedback/details/3113288/ssms-2016-open-recent-menu-doesnt-show-recently-saved-files)

* 右键单击表的索引（通过远程 (Internet) 连接）时，SSMS 运行缓慢。 [连接 ID 3114074](https://connect.microsoft.com/SQLServer/feedback/details/3114074/ssms-slow-when-right-clicking-an-index-for-a-table-over-a-remote-internet-connection)
 
* 解决了 SQL 设计器滚动条的问题。 [连接 ID 3114856](http://connect.microsoft.com/SQLServer/feedback/details/3114856/bug-in-scrollbar-on-sql-desginer-in-ssms-2016)

* 表的上下文菜单暂时挂起 
 
* SSMS 偶尔在活动监视器中引发异常和崩溃。 [连接 ID 697527](https://connect.microsoft.com/SQLServer/feedback/details/697527/)

* SSMS 2016 崩溃，显示错误“由于在 IP 71AF8579 (71AE0000) 的 .NET 运行时出现内部错误，进程终止，退出代码 80131506”


## <a name="ssms-1651"></a>SSMS 16.5.1
公开发布 | 版本号：13.0.16100.1

* 修复了在发生检查约束时 Invoke-Sqlcmd 会错误插入多个行的问题。 [Microsoft Connect 项目：811560](https://connect.microsoft.com/SQLServer/feedback/details/811560)

* 修复了创建可用性组时非 ENU 语言版本无法完全使用的问题。

* 修复了单击查询计划 XML 时不能打开相应 SSMS UI 的问题。


## <a name="downloadssdtmediadownloadpng-ssms-165httpgomicrosoftcomfwlinklinkid832812"></a>![下载](../ssdt/media/download.png) [SSMS 16.5](http://go.microsoft.com/fwlink/?LinkID=832812)
公开发布 | 版本号：13.0.16000.28


[中文（中国）](https://go.microsoft.com/fwlink/?linkid=832812&clcid=0x804) | [中文（台湾）](https://go.microsoft.com/fwlink/?linkid=832812&clcid=0x404) | [英语（美国）](https://go.microsoft.com/fwlink/?linkid=832812&clcid=0x409) | [法语](https://go.microsoft.com/fwlink/?linkid=832812&clcid=0x40c) | [德语](https://go.microsoft.com/fwlink/?linkid=832812&clcid=0x407) | [意大利语](https://go.microsoft.com/fwlink/?linkid=832812&clcid=0x410) | [日语](https://go.microsoft.com/fwlink/?linkid=832812&clcid=0x411) | [朝鲜语](https://go.microsoft.com/fwlink/?linkid=832812&clcid=0x412) | [葡萄牙语（巴西）](https://go.microsoft.com/fwlink/?linkid=832812&clcid=0x416) | [俄语](https://go.microsoft.com/fwlink/?linkid=832812&clcid=0x419) | [西班牙语](https://go.microsoft.com/fwlink/?linkid=832812&clcid=0x40a)

* 修复了当单击具有包含“;:”的表名称的数据库时可能发生故障的问题。
* 修复了在“AS 表格数据库属性”窗口中对“模型”页所做的更改将编写原始定义的脚本的问题。 
[Microsoft Connect 项：3080744](https://connect.microsoft.com/SQLServer/feedback/details/3080744) 
* 修复了将临时文件添加到“最近使用过的文件”列表的问题。  
[Microsoft Connect 项：2558789](https://connect.microsoft.com/SQLServer/feedback/details/2558789)
* 修复了在对象资源管理器树中对用户表节点禁用“管理压缩”菜单项的问题。  
[Microsoft Connect 项：3104616](https://connect.microsoft.com/SQLServer/feedback/details/3104616)

* 修复了用户不能设置对象资源管理器、已注册的服务器资源管理器、模板资源管理器以及对象资源管理器详细信息的字体大小的问题。 资源管理器的字体将会使用“环境”字体。  
[Microsoft Connect 项：691432](https://connect.microsoft.com/SQLServer/feedback/details/691432)

* 修复了在连接丢失时 SSMS 始终重新连接到默认数据库的问题。  
[Microsoft Connect 项：3102337](https://connect.microsoft.com/SQLServer/feedback/details/3102337)

* 修复了策略管理和查询编辑器窗口中许多高 DPI 的问题，包括执行计划图标。

* 修复了缺少为扩展的事件配置字体和颜色的选项问题。

* 修复了在关闭应用程序或 SSMS 尝试显示错误对话框时发生故障的问题。


## <a name="downloadssdtmediadownloadpng-ssms-1641-september-2016httpgomicrosoftcomfwlinklinkid828615"></a>![下载](../ssdt/media/download.png) [SSMS 16.4.1（2016 年 9 月）](http://go.microsoft.com/fwlink/?LinkID=828615)
公开发布 | 版本号：13.0.15900.1

[中文（中国）](https://go.microsoft.com/fwlink/?linkid=828615&clcid=0x804) | [中文（台湾）](https://go.microsoft.com/fwlink/?linkid=828615&clcid=0x404) | [英语（美国）](https://go.microsoft.com/fwlink/?linkid=828615&clcid=0x409) | [法语](https://go.microsoft.com/fwlink/?linkid=828615&clcid=0x40c) | [德语](https://go.microsoft.com/fwlink/?linkid=828615&clcid=0x407) | [意大利语](https://go.microsoft.com/fwlink/?linkid=828615&clcid=0x410) | [日语](https://go.microsoft.com/fwlink/?linkid=828615&clcid=0x411) | [朝鲜语](https://go.microsoft.com/fwlink/?linkid=828615&clcid=0x412) | [葡萄牙语（巴西）](https://go.microsoft.com/fwlink/?linkid=828615&clcid=0x416) | [俄语](https://go.microsoft.com/fwlink/?linkid=828615&clcid=0x419) | [西班牙语](https://go.microsoft.com/fwlink/?linkid=828615&clcid=0x40a)

*  解决了尝试更改/修改存储过程失败的问题：  
[Microsoft Connect 项目 #3103831](https://connect.microsoft.com/SQLServer/feedback/details/3103831)

* 新增了通过 PowerShell 来查看和写入数据的“Read-SqlTableData”、“Read-SqlViewData”和“Write-SqlTableData”cmdlet。  
[Trello Read-SqlTableData 卡](https://trello.com/c/FXVUNJ8x/131-read-sqltabledata)  
[Microsoft Connect 项目 #2685363](https://connect.microsoft.com/SQLServer/feedback/details/2685363)
    
* 新增了用于通过 PowerShell 来启用新登录管理方案的“Add-SqlLogin”cmdlet。  
[Microsoft Connect 项目 #2588952](https://connect.microsoft.com/SQLServer/feedback/details/2588952)
    
*  为连接到各种国内云的用户改进了支持和可用性。
    
    
*  解决了引发内存不足异常的问题。  
[Microsoft Connect 项目 #3062914](https://connect.microsoft.com/SQLServer/feedback/details/3062914)  
[Microsoft Connect 项目 #3074856](https://connect.microsoft.com/SQLServer/feedback/details/3074856)
    
*  解决了按架构筛选不是有效筛选选项的问题。  
[Microsoft Connect 项目 #3058105](https://connect.microsoft.com/SQLServer/feedback/details/3058105)  
[Microsoft Connect 项目 #3101136](https://connect.microsoft.com/SQLServer/feedback/details/3101136)
    
*  解决了拉伸数据库监视器窗口不可访问的问题。
    
*  解决了 F1 帮助始终打开联机内容的问题。 用户现可选择通过“帮助”菜单中“设置帮助首选项”来实现联机帮助还是脱机帮助。   
[Microsoft Connect 项目 #2826366](https://connect.microsoft.com/SQLServer/feedback/details/2826366)
    
*  解决了以下问题：删除 1200 级别 Analysis Services 表格模型不会删除用于脚本编写的密码，即使服务器版本有密码 [客户端模型对象在脚本编写前现已同步]。
    
*  解决了“选择前 N 行”选项生成了 TOP 运算符的已弃用语法的问题。  
[Microsoft Connect 项目 #3065435](https://connect.microsoft.com/SQLServer/feedback/details/3065435)
    
*  解决了整个 SSMS 的布局问题，包括登录属性页和高级查询执行选项。   
[Microsoft Connect 项目 #3058199](https://connect.microsoft.com/SQLServer/feedback/details/3058199)  
[Microsoft Connect 项目 #3079122](https://connect.microsoft.com/SQLServer/feedback/details/3058199)  
[Microsoft Connect 项目 #3071384](https://connect.microsoft.com/SQLServer/feedback/details/3071384)
    
*  解决了只要用户打开新查询窗口即自动创建解决方案的问题。   
[Microsoft Connect 项目 #2924667](https://connect.microsoft.com/SQLServer/feedback/details/2924667)    
[Microsoft Connect 项目 #2917742](https://connect.microsoft.com/SQLServer/feedback/details/2917742)   
[Microsoft Connect 项目 #2612635](https://connect.microsoft.com/SQLServer/feedback/details/2612635)
    
*  解决了临时表位于系统数据库时无法在对象资源管理器中展开的问题。  
[Microsoft Connect 项目 #2551649](https://connect.microsoft.com/SQLServer/feedback/details/2551649)
    
*  解决了 SSMS 执行批处理后运行 SELECT @@trancount 查询的问题。    
[Microsoft Connect 项目 #3042364](https://connect.microsoft.com/SQLServer/feedback/details/3042364)
    
*  解决了 Analysis Services 中从服务器属性页创建脚本产生隐藏连接对话框的问题。
    
*  解决了按 Ctrl+Q 不会选择“快速启动”工具栏的问题。
    
*  解决了使用“服务器属性”对话框更改数据库最大大小对超过 2 TB 数据库不起作用的问题。  
[Microsoft Connect 项目 #1231091](https://connect.microsoft.com/SQLServer/feedback/details/1231091)
    
*  解决了“还原数据库”向导不接受含前导空格的文件名的问题：   
[Microsoft Connect 项目 #2395147](https://connect.microsoft.com/SQLServer/feedback/details/2395147)



## <a name="downloadssdtmediadownloadpng-ssms-163-august-2016httpgomicrosoftcomfwlinklinkid824938"></a>![下载](../ssdt/media/download.png) [SSMS 16.3（2016 年 8 月）](http://go.microsoft.com/fwlink/?LinkID=824938)
公开发布 | 版本号：13.0.15700.28


[中文（中国）](https://go.microsoft.com/fwlink/?linkid=824938&clcid=0x804) | [中文（台湾）](https://go.microsoft.com/fwlink/?linkid=824938&clcid=0x404) | [英语（美国）](https://go.microsoft.com/fwlink/?linkid=824938&clcid=0x409) | [法语](https://go.microsoft.com/fwlink/?linkid=824938&clcid=0x40c) | [德语](https://go.microsoft.com/fwlink/?linkid=824938&clcid=0x407) | [意大利语](https://go.microsoft.com/fwlink/?linkid=824938&clcid=0x410) | [日语](https://go.microsoft.com/fwlink/?linkid=824938&clcid=0x411) | [朝鲜语](https://go.microsoft.com/fwlink/?linkid=824938&clcid=0x412) | [葡萄牙语（巴西）](https://go.microsoft.com/fwlink/?linkid=824938&clcid=0x416) | [俄语](https://go.microsoft.com/fwlink/?linkid=824938&clcid=0x419) | [西班牙语](https://go.microsoft.com/fwlink/?linkid=824938&clcid=0x40a)

* SSMS 月度版本目前以数字命名。

* [新身份验证选项 **“Active Directory 通用身份验证”**](https://azure.microsoft.com/documentation/articles/sql-database-ssms-mfa-authentication/)。 这是一种由 Azure Active Directory 驱动的基于令牌的身份验证机制，支持多重身份验证、密码身份验证和集成身份验证机制。

* 新扩展事件模板匹配 SQL Server Profiler 模板的功能[（Microsoft Connect 项目 #2543925）。](../tools/sql-server-profiler/sql-server-profiler-templates.md)

* Azure SQL 数据库的新的“创建数据库和数据库属性”对话框。

* 使用 PowerShell 帮助执行 SQL Server 登录管理的新“Get-SqlLogin”和“Remove-SqlLogin”cmdlet。  
*链接的客户 Bug 请求：*   
[Microsoft Connect 项目 #2588952.](https://connect.microsoft.com/SQLServer/feedback/details/2588952/)

* 新的 PowerShell cmdlet“New-SqlColumnMasterKeySettings”，可以增加对为任意提供程序和密钥路径创建列主密钥的支持。

* 新“创建数据库”对话框，可以简化在 SSMS 中创建 Azure SQL 数据库的流程>

* 支持在 SSMS 对象资源管理器的“数据库”节点中进行筛选。 导航至对象资源管理器中的“数据库”节点，然后单击对象资源管理器中的筛选器图标以筛选数据库列表。

* 支持“备份和还原”向导中的 Azure 资源管理器 (ARM) 类型存储帐户。

* [对高分辨率显示器的初始测试版支持](https://blogs.msdn.microsoft.com/sqlreleaseservices/ssms-highdpi-support/)。  
*链接的客户 Bug 请求：*   
[Microsoft Connect 项目 #1129301](https://connect.microsoft.com/SQLServer/feedback/details/1129301/management-studio-is-unusable-on-a-4k-display)[Microsoft Connect 项目 #1858763](https://connect.microsoft.com/SQLServer/feedback/details/1858763/)[Microsoft Connect 项目 #1852671](https://connect.microsoft.com/SQLServer/feedback/details/1852671/)[Microsoft Connect 项目 #1487643](https://connect.microsoft.com/SQLServer/feedback/details/1487643/)[Microsoft Connect 项目 #1355641](https://connect.microsoft.com/SQLServer/feedback/details/1355641/)[Microsoft Connect 项目 #2161595](https://connect.microsoft.com/SQLServer/feedback/details/2161595/)[Microsoft Connect 项目 #1854041](https://connect.microsoft.com/SQLServer/feedback/details/1854041/)[Microsoft Connect 项目 #1055617](https://connect.microsoft.com/SQLServer/feedback/details/1055617/)[Microsoft Connect 项目 #2448774](https://connect.microsoft.com/SQLServer/feedback/details/2448774/)[Microsoft Connect 项目 #1521405](https://connect.microsoft.com/SQLServer/feedback/details/1521405/)[Microsoft Connect 项目 #2117853](https://connect.microsoft.com/SQLServer/feedback/details/2117853/)[Microsoft Connect 项目 #2014256](https://connect.microsoft.com/SQLServer/feedback/details/2014256/)[Microsoft Connect 项目 #2162218](https://connect.microsoft.com/SQLServer/feedback/details/2162218/)[Microsoft Connect 项目 #2344551](https://connect.microsoft.com/SQLServer/feedback/details/2344551/)[Microsoft Connect 项目 #1664436](https://connect.microsoft.com/SQLServer/feedback/details/1664436/)[Microsoft Connect 项目 #2554043](https://connect.microsoft.com/SQLServer/feedback/details/2554043/)[Microsoft Connect 项目 #2983216](https://connect.microsoft.com/SQLServer/feedback/details/2983216/)[Microsoft Connect 项目 #2021706](https://connect.microsoft.com/SQLServer/feedback/details/2021706/)

* 数据库引擎优化顾问 (DTA) 改进，支持自动读取 SQL Server Query Store 中的工作负载。

* 数据库引擎优化顾问 (DTA) 改进，可以显示聚集列存储索引、非聚集列存储索引和行存储索引的索引建议。

* 支持使用 SQL Server Analysis Services PowerShell cmdlet 发送数据库控制台 (DBCC) 命令。

* 修复了 Bug，可以查看 SSMS 中已解密的“始终加密”大型对象 (LOB) 列的明文。  
*链接的客户 Bug 请求：*   
[Microsoft Connect 项目 #2413024](https://connect.microsoft.com/SQLServer/feedback/details/2413024/cannot-view-cleartext-of-alwaysencrypted-lob-columns-in-ssms)

* “始终加密”对话框中的 Bug 修复，可以修复在 Windows 视觉样式未启用（例如，启用高对比度显示器）时的故障。

* “找不到方法”错误阻止连接到 SQL Server 实例的 Bug 修复。

* 使用日期时间偏移创建分区函数时出现 SSMS 故障的 Bug 修复。

* 用于添加删除启动分布式重播管理工具 (DReplay.exe) 的 Microsoft .NET 3.5 要求的 Bug 修复。

* Analysis Services 部署向导中的 Bug 修复，支持完全限定的服务器名称。

* SSMS 中的 Bug 修复，可以使用 2016 兼容性模型显示 Analysis Services 表格模型中的分区。  
*链接的客户 Bug 请求：*   
[Microsoft Connect 项目 #2845053](https://connect.microsoft.com/SQLServer/feedback/details/2845053/ssms-cannot-display-partitions-in-tabular-models-in-2016-compatibility-level) 

* Analysis Services 表格模型以及 SQL Server 共享管理对象 (SMO) 中的性能改进和 Bug 修复。 


---
## <a name="downloadssdtmediadownloadpng-ssms-july-2016-hotfix-updatehttpgomicrosoftcomfwlinklinkid822301"></a>![下载](../ssdt/media/download.png) [SSMS 2016 年 7 月修补程序更新](http://go.microsoft.com/fwlink/?LinkID=822301)
公开发布 | 版本号：13.0.15600.2

[中文（中国）](https://go.microsoft.com/fwlink/?linkid=822301&clcid=0x804) | [中文（台湾）](https://go.microsoft.com/fwlink/?linkid=822301&clcid=0x404) | [英语（美国）](https://go.microsoft.com/fwlink/?linkid=822301&clcid=0x409) | [法语](https://go.microsoft.com/fwlink/?linkid=822301&clcid=0x40c) | [德语](https://go.microsoft.com/fwlink/?linkid=822301&clcid=0x407) | [意大利语](https://go.microsoft.com/fwlink/?linkid=822301&clcid=0x410) | [日语](https://go.microsoft.com/fwlink/?linkid=822301&clcid=0x411) | [朝鲜语](https://go.microsoft.com/fwlink/?linkid=822301&clcid=0x412) | [葡萄牙语（巴西）](https://go.microsoft.com/fwlink/?linkid=822301&clcid=0x416) | [俄语](https://go.microsoft.com/fwlink/?linkid=822301&clcid=0x419) | [西班牙语](https://go.microsoft.com/fwlink/?linkid=822301&clcid=0x40a)

* **SSMS 中的 Bug 修复，用于启用缺失的右键菜单项**。  
*链接的客户 Bug 请求：*  
[Microsoft Connect 项目 #2883440](https://connect.microsoft.com/SQLServer/feedback/details/2883440/lost-table-design-and-edit-top-n-rows-in-tables-context-menu)  
[Microsoft Connect 项目 #2909644](https://connect.microsoft.com/SQLServer/feedback/details/2909644/ssms-2016-is-missing-edit-options-against-sql-express-2014)  
[Microsoft Connect 项目 #2924345](https://connect.microsoft.com/SQLServer/feedback/details/2924345/some-ssms-object-explorer-right-click-menu-options-missing-in-july-update)

---
## <a name="ssms-july-2016-install-the-july-2016-hotfix"></a>SSMS 2016 年 7 月版（安装 2016 年 7 月版修补程序）
公开发布 | 版本号：13.0.15500.91

* 7 月 5 日编辑：改进了对“Analysis Services 进程”对话框和“Analysis Services 部署”向导中 SQL Server 2016（1200 兼容级别）表格数据库的支持。

* 7 月 5 日编辑：SSMS“查询执行选项”对话框中的新选项，用来设置“XACT_ABORT”。 此选项在此版本的 SSMS 中默认启用，指示 SQL Server 回退整个事务，且如果出现运行时错误，则中止批处理。

* 在 SSMS 中对 Azure SQL 数据仓库的支持。

* 对 SQL Server PowerShell 模块的重要更新。 这包括新的 [SQL PowerShell 模块和用于始终加密的新 CMDLET、SQL 代理和 SQL 错误日志](https://blogs.technet.microsoft.com/dataplatforminsider/2016/06/30/sql-powershell-july-2016-update)。

* “始终加密”向导中对 PowerShell 脚本生成的支持。

* 显著改善了到 Azure SQL 数据库的连接时间。

* 新的“备份到 URL”对话框，用于支持为 SQL Server 2016 数据库备份创建 Azure 存储凭据。 该对话框使得用户可在 Azure 存储帐户中更流畅地存储数据库备份。
 
* 新的“还原”对话框，用来简化从 Microsoft Azure 存储服务还原 SQL Server 2016 数据库备份。
 
* SSMS 查询设计器中的 Bug 修复，如果用户对表没有 SELECT 权限，允许将表添加到设计器中。

* 修复了 Bug，为“TRY_CAST()”和“TRY_CONVERT()”函数增加了 IntelliSense 支持。  
*链接的客户 Bug 请求：*  
[Microsoft Connect 项目 #2453461](https://connect.microsoft.com/SQLServer/feedback/details/2453461/sql-server-2012-issue-with-try-cast)。

* PowerShell 模块中用于启用加载“SQLAS” Analysis Services 扩展的 Bug 修复。  
*链接的客户 Bug 请求：*  
[Microsoft Connect 项目 #2544902](https://connect.microsoft.com/SQLServer/feedback/details/2544902/ssms-march-2016-refresh-sqlps-failed-to-load-the-sqlas-extension)。

* SSMS 编辑器窗口中允许拖放打开 Sql 文件的 Bug 修复。  
*链接的客户 Bug 请求：*  
[Microsoft Connect 项目 #2690658](https://connect.microsoft.com/SQLServer/feedback/details/2690658/cannot-drag-sql-files-into-management-studios)。

* 探查器中用于修复探查器故障（问题存在时）的 Bug 修复。  
*链接的客户 Bug 请求：*  
[Microsoft Connect 项目 #2616550](https://connect.microsoft.com/SQLServer/feedback/details/2616550/sql-server-2016-rc2-profiler-version-13-0-1300-275-wont-close-after-trace-is-started-even-after-trace-is-stopped)。  
[Microsoft Connect 项目 #2319968](https://connect.microsoft.com/SQLServer/Feedback/Details/2319968)。

* SSMS 中用于防止在尝试编辑 SSMS 表设计器中的联接链接时出现故障的 Bug 修复。  
*链接的客户 Bug 请求：*  
[Microsoft Connect 项目 #2721052](https://connect.microsoft.com/SQLServer/feedback/details/2721052/ssms-view-design-mode-right-click-on-join-crashes-ssms)。

* SSMS 中用于为 db_owner 角色成员启用数据库脚本生成的 Bug 修复。  
*链接的客户 Bug 请求：*  
[Microsoft Connect 项目 #2869241](https://connect.microsoft.com/SQLServer/feedback/details/2869241/error-with-script-database-as-create-to-in-ssms-2008r2-and-ssms-2016-june)。

* SSMS 编辑器中，如果服务器脱机，用于删除关闭查询选项卡的延迟的 Bug 修复。  
*链接的客户 Bug 请求：*  
[Microsoft Connect 项目 #2656058](https://connect.microsoft.com/SQLServer/feedback/details/2656058/ssms-2014-2016-query-tab-takes-significantly-longer-to-close-if-the-instance-it-was-connected-to-is-now-offline)。

* 用于启用 SQL Server Express 数据库中的备份选项的 Bug 修复。 
*链接的客户 Bug 请求：*  
[Microsoft Connect 项目 #2801910](https://connect.microsoft.com/SQLServer/feedback/details/2801910/ssms-2016-backup-option-not-appearing-in-tasks)。  
[Microsoft Connect 项目 #2874434](https://connect.microsoft.com/SQLServer/feedback/details/2874434/backup-missing-from-tasks-context-menu-in-ssms-2016-when-you-are-connected-to-an-express-instance)。

* Analysis Services 中用于对多维 Analysis Services 模型正确显示数据馈送提供程序的 Bug 修复。

----
## <a name="downloadssdtmediadownloadpng-ssms-june-2016httpgomicrosoftcomfwlinklinkid799832"></a>![下载](../ssdt/media/download.png) [SSMS 2016 年 6 月版本](http://go.microsoft.com/fwlink/?LinkID=799832)
公开发布 | 版本号：13.0.15000.23

[中文（中国）](https://go.microsoft.com/fwlink/?linkid=799832&clcid=0x804) | [中文（台湾）](https://go.microsoft.com/fwlink/?linkid=799832&clcid=0x404) | [英语（美国）](https://go.microsoft.com/fwlink/?linkid=799832&clcid=0x409) | [法语](https://go.microsoft.com/fwlink/?linkid=799832&clcid=0x40c) | [德语](https://go.microsoft.com/fwlink/?linkid=799832&clcid=0x407) | [意大利语](https://go.microsoft.com/fwlink/?linkid=799832&clcid=0x410) | [日语](https://go.microsoft.com/fwlink/?linkid=799832&clcid=0x411) | [朝鲜语](https://go.microsoft.com/fwlink/?linkid=799832&clcid=0x412) | [葡萄牙语（巴西）](https://go.microsoft.com/fwlink/?linkid=799832&clcid=0x416) | [俄语](https://go.microsoft.com/fwlink/?linkid=799832&clcid=0x419) | [西班牙语](https://go.microsoft.com/fwlink/?linkid=799832&clcid=0x40a)

* SSMS 与 2016 年 6 月版本一起开始公开发布。

* SSMS 中新的“快速查找”对话框，可以更好地集成到当前文档中并支持通过正则表达式进行搜索。 
*链接的客户 Bug 请求：*  
<https://connect.microsoft.com/SQLServer/feedback/details/2735513/quick-find-replace-in-ssms-2016-rc3/>

* SSMS 安装程序改进，支持跟踪安装进程并通过脚本处理无人参与的安装的退出代码。

* SSMS 上下文相关 F1 帮助中的 Bug 修复，可以正确显示帮助文档和文章。

* 查询数据存储“回归查询”视图中导致 SSMS 在滚动时出现故障的 Bug 修复。

* Excel Analysis Services OLEDB 连接器中的 Bug 修复，支持从 Excel 2016 到 SQL Server Analysis Services 的连接。

* “SSMS 连接”对话框中的 Bug 修复，可以显示与多监视器系统的 SSMS 主窗口相同的监视器上的“连接”对话框。  
*链接的客户 Bug 请求：*  
<https://connect.microsoft.com/SQLServer/feedback/details/724909/connection-dialog-appears-off-screen/>
<https://connect.microsoft.com/SQLServer/feedback/details/755689/sql-server-management-studio-connect-to-server-popup-dialog/>  
<https://connect.microsoft.com/SQLServer/feedback/details/389165/sql-server-management-studio-gets-confused-dealing-with-multiple-displays/>

* “始终加密”体验的 Bug 修复。 修复了“始终加密”菜单项未正确针对延伸数据库启用的 Bug。 还修复了“始终加密”向导中未正确使用 SafeNet (Luna SA) HSM 提供程序的 Bug。


## <a name="additional-downloads"></a>其他下载  
有关所有 SQL Server Management Studio 下载的列表，请搜索 [Microsoft 下载中心](https://www.microsoft.com/en-us/download/search.aspx?q=sql%20server%20management%20studio&p=0&r=10&t=&s=Relevancy~Descending)。  
  
有关最新版本的 SQL Server Management Studio 的信息，请参阅 [下载 SQL Server Management Studio &#40;SSMS&#41;](../ssms/download-sql-server-management-studio-ssms.md)。  
