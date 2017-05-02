---
title: SQL Server Management Studio - Changelog (SSMS) | Microsoft Docs
ms.custom: 
ms.date: 01/30/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- tools-ssms
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 3dc76cc1-3b4c-4719-8296-f69ec1b476f9
caps.latest.revision: 72
author: stevestein
ms.author: sstein
manager: jhubbard
translationtype: Human Translation
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: f2144751277bb10897e0ed39ee24dbad8a32b4ce
ms.lasthandoff: 04/11/2017

---
# <a name="sql-server-management-studio---changelog-ssms"></a>SQL Server Management Studio - Changelog (SSMS)

## <a name="ssms-1653-release"></a>SSMS 16.5.3 版本
公开发布 | 内部版本号 ：13.0.16106.4

此版本已解决以下问题：

* 解决了 SSMS 16.5.2 中引入的问题，即当表具有多个稀疏列时，导致“表”节点扩展。

* 用户可以部署包含 OData 连接管理器的 SSIS 包，这些包连接到 SSIS 目录的 Microsoft Dynamics AX / CRM Online 资源。 有关详细信息，请参阅 [OData 连接管理器](https://msdn.microsoft.com/library/dn584133.aspx)。

* 为现有表配置“始终加密”功能失败，在不相关的对象上出错。 [连接 ID 3103181](https://connect.microsoft.com/SQLServer/feedback/details/3103181/setting-up-always-encrypted-on-an-existing-table-fails-with-errors-on-unrelated-objects)

* 为现有数据库配置“始终加密”功能时，多个架构无法正常运行。 [连接 ID 3109591](https://connect.microsoft.com/SQLServer/feedback/details/3109591/sql-server-2016-always-encrypted-against-existing-database-with-multiple-schemas-doesnt-work)

* 由于数据库包含引用系统视图的视图，“始终加密、已加密列”向导失败。 [连接 ID 3111925](https://connect.microsoft.com/SQLServer/feedback/details/3111925/sql-server-2016-always-encrypted-encrypted-column-wizard-failed-task-failed-due-to-following-error-cannot-save-package-to-file-the-model-has-build-blocking-errors)

* 使用“始终加密”功能进行加密时，错误处理加密后刷新模块出现错误。

* “打开最近的文件”菜单不显示最近保存的文件。** [连接 ID 3113288](https://connect.microsoft.com/SQLServer/feedback/details/3113288/ssms-2016-open-recent-menu-doesnt-show-recently-saved-files)

* 右键单击表的索引（通过远程 (Internet) 连接）时，SSMS 运行缓慢。 [连接 ID 3114074](https://connect.microsoft.com/SQLServer/feedback/details/3114074/ssms-slow-when-right-clicking-an-index-for-a-table-over-a-remote-internet-connection)
 
* 解决了 SQL 设计器滚动条的问题。 [连接 ID 3114856](http://connect.microsoft.com/SQLServer/feedback/details/3114856/bug-in-scrollbar-on-sql-desginer-in-ssms-2016)

* 表的上下文菜单暂时挂起 
 
* SSMS 偶尔在活动监视器中引发异常和崩溃。 [连接 ID 697527](https://connect.microsoft.com/SQLServer/feedback/details/697527/)

* SSMS 2016 崩溃，显示错误“由于在 IP 71AF8579 (71AE0000) 的 .NET 运行时出现内部错误，进程终止，退出代码 80131506”


## <a name="ssms-1651-release"></a>SSMS 16.5.1 版本
公开发布 | 版本号：13.0.16100.1

* 修复了在发生检查约束时 Invoke-Sqlcmd 会错误插入多个行的问题。 [Microsoft Connect 项目：811560](https://connect.microsoft.com/SQLServer/feedback/details/811560)

* 修复了创建可用性组时非 ENU 语言版本无法完全使用的问题。

* 修复了单击查询计划 XML 时不能打开相应 SSMS UI 的问题。


## <a name="ssms-165-release"></a>SSMS 16.5 版本
公开发布 | 版本号：13.0.16000.28

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


## <a name="ssms-1641-september-2016-release"></a>SSMS 16.4.1（2016 年 9 月）版本
公开发布 | 版本号：13.0.15900.1

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



## <a name="ssms-163-august-2016-release"></a>SSMS 16.3（2016 年 8 月）版本
公开发布 | 版本号：13.0.15700.28

* SSMS 月度版本目前以数字命名。

* [新身份验证选项**“Active Directory 通用身份验证”**](https://azure.microsoft.com/documentation/articles/sql-database-ssms-mfa-authentication/)。 这是一种由 Azure Active Directory 驱动的基于令牌的身份验证机制，支持多重身份验证、密码身份验证和集成身份验证机制。

* 新扩展事件模板匹配 SQL Server Profiler 模板的功能 [（Microsoft Connect 项目 #2543925）](https://connect.microsoft.com/SQLServer/feedback/details/2543925/sql-server-extended-events-profiler-tool)。 详细了解附带的 [SQL Server Profiler 模板](https://msdn.microsoft.com/library/ms190176.aspx)。

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
## <a name="ssms-july-2016-hotfix-update-release"></a>SSMS 2016 年 7 月修补程序更新版本 
公开发布 | 版本号：13.0.15600.2

* **SSMS 中的 Bug 修复，用于启用缺失的右键菜单项**。  
*链接的客户 Bug 请求：*  
[Microsoft Connect 项目 #2883440](https://connect.microsoft.com/SQLServer/feedback/details/2883440/lost-table-design-and-edit-top-n-rows-in-tables-context-menu)  
[Microsoft Connect 项目 #2909644](https://connect.microsoft.com/SQLServer/feedback/details/2909644/ssms-2016-is-missing-edit-options-against-sql-express-2014)  
[Microsoft Connect 项目 #2924345](https://connect.microsoft.com/SQLServer/feedback/details/2924345/some-ssms-object-explorer-right-click-menu-options-missing-in-july-update)

---
## <a name="ssms-july-2016-release"></a>SSMS 2016 年 7 月版本 
公开发布 | 版本号：13.0.15500.91

* *7 月 5 日编辑：* **改进了对“Analysis Services 进程”对话框和“Analysis Services 部署”向导中 SQL Server 2016（1200 兼容级别）表格数据库的支持。**

* *7 月 5 日编辑：* **SSMS“查询执行选项”对话框中的新选项，用来设置“XACT_ABORT”。此选项在此版本的 SSMS 中默认启用，将指示 SQL Server 回滚整个事务，且如果出现运行时错误，则中止批处理。**

* **SSMS 中对 Azure SQL 数据仓库的支持。**

* **对 SQL Server PowerShell 模块的重要更新。这包括新的 [SQL PowerShell 模块和用于始终加密的新 CMDLET、SQL 代理和 SQL 错误日志](https://blogs.technet.microsoft.com/dataplatforminsider/2016/06/30/sql-powershell-july-2016-update)**。

* **支持在“始终加密”向导中生成 PowerShell 脚本**。

* **大幅缩短了到 Azure SQL 数据库的连接时间。**

* **通过新的“备份到 URL”对话框，可为 SQL Server 2016 数据库备份创建 Azure 存储凭据。这使得用户可在 Azure 存储帐户中更流畅地存储数据库备份。**
 
* **通过新的“还原”对话框，可更轻松地从 Microsoft Azure 存储服务还原 SQL Server 2016 数据库备份。**
 
* **如果用户没有表的 SELECT 权限，则可通过 SSMS 查询设计器中的 Bug 修复将表添加到设计器中。**

* **通过 Bug 修复，可为“TRY_CAST()”和“TRY_CONVERT()”函数增加 IntelliSense 支持。**  
*链接的客户 Bug 请求：*  
[Microsoft Connect 项目 #2453461](https://connect.microsoft.com/SQLServer/feedback/details/2453461/sql-server-2012-issue-with-try-cast)。

* **通过 PowerShell 模块中的 Bug 修复，可实现“SQLAS”Analysis Services 扩展的加载。**  
*链接的客户 Bug 请求：*  
[Microsoft Connect 项目 #2544902](https://connect.microsoft.com/SQLServer/feedback/details/2544902/ssms-march-2016-refresh-sqlps-failed-to-load-the-sqlas-extension)。

* **通过 SSMS 编辑器窗口中的 Bug 修复，可拖放打开 Sql 文件。**  
*链接的客户 Bug 请求：*  
[Microsoft Connect 项目 #2690658](https://connect.microsoft.com/SQLServer/feedback/details/2690658/cannot-drag-sql-files-into-management-studios)。

* **通过探查器中的 Bug 修复，可在问题存在时修复探查器故障。**  
*链接的客户 Bug 请求：*  
[Microsoft Connect 项目 #2616550](https://connect.microsoft.com/SQLServer/feedback/details/2616550/sql-server-2016-rc2-profiler-version-13-0-1300-275-wont-close-after-trace-is-started-even-after-trace-is-stopped)。  
[Microsoft Connect 项目 #2319968](https://connect.microsoft.com/SQLServer/Feedback/Details/2319968)。

* **通过 SSMS 中的 Bug 修复，可在尝试编辑 SSMS 表设计器中的联接链接时防止发生故障。**  
*链接的客户 Bug 请求：*  
[Microsoft Connect 项目 #2721052](https://connect.microsoft.com/SQLServer/feedback/details/2721052/ssms-view-design-mode-right-click-on-join-crashes-ssms)。

* **通过 SSMS 中的 Bug 修复，可为 db_owner 角色成员生成数据库脚本。**  
*链接的客户 Bug 请求：*  
[Microsoft Connect 项目 #2869241](https://connect.microsoft.com/SQLServer/feedback/details/2869241/error-with-script-database-as-create-to-in-ssms-2008r2-and-ssms-2016-june)。

* **通过 SSMS 编辑器中的 Bug 修复，可在服务器脱机时消除查询选项卡关闭操作中的延迟。**  
*链接的客户 Bug 请求：*  
[Microsoft Connect 项目 #2656058](https://connect.microsoft.com/SQLServer/feedback/details/2656058/ssms-2014-2016-query-tab-takes-significantly-longer-to-close-if-the-instance-it-was-connected-to-is-now-offline)。

* **通过 Bug 修复，可启用 SQL Server Express 数据库中的“备份”选项。**  
*链接的客户 Bug 请求：*  
[Microsoft Connect 项目 #2801910](https://connect.microsoft.com/SQLServer/feedback/details/2801910/ssms-2016-backup-option-not-appearing-in-tasks)。  
[Microsoft Connect 项目 #2874434](https://connect.microsoft.com/SQLServer/feedback/details/2874434/backup-missing-from-tasks-context-menu-in-ssms-2016-when-you-are-connected-to-an-express-instance)。

* **通过 Analysis Services 中的 Bug 修复，可正确显示多维 Analysis Services 模型的数据馈送提供程序。**

----
## <a name="ssms-june-2016-generally-available-release"></a>SSMS 2016 年 6 月公开发布版本
公开发布 | 版本号：13.0.15000.23

* **SSMS 与 2016 年 6 月版本一起开始公开发布。**

* **通过 SSMS 中新的“快速查找”对话框，可更好地集成到当前文档中，并支持通过正则表达式进行搜索。**  
*链接的客户 Bug 请求：*  
<https://connect.microsoft.com/SQLServer/feedback/details/2735513/quick-find-replace-in-ssms-2016-rc3/>

* **通过 SSMS 安装程序的改进，可跟踪安装进程并通过脚本处理无人参与的安装的退出代码。**

* **通过 SSMS 上下文相关 F1 帮助中的 Bug 修复，可正确显示帮助文档和文章。**

* **查询数据存储“回归查询”视图中导致 SSMS 在滚动时出现故障的 Bug 修复。** 

* **通过 Excel Analysis Services OLEDB 连接器中的 Bug 修复，可支持从 Excel 2016 到 SQL Server Analysis Services 的连接。**

* **通过“SSMS 连接”对话框中的 Bug 修复，可显示与多监视器系统的 SSMS 主窗口相同的监视器上的“连接”对话框。**  
*链接的客户 Bug 请求：*  
<https://connect.microsoft.com/SQLServer/feedback/details/724909/connection-dialog-appears-off-screen/>
<https://connect.microsoft.com/SQLServer/feedback/details/755689/sql-server-management-studio-connect-to-server-popup-dialog/>  
<https://connect.microsoft.com/SQLServer/feedback/details/389165/sql-server-management-studio-gets-confused-dealing-with-multiple-displays/>

* **Always Encrypted 体验中的 Bug 修复。修复了“始终加密”菜单项未正确针对延伸数据库启用的 Bug。还修复了 Always Encrypted 向导中未正确使用 SafeNet (Luna SA) HSM 提供程序的 Bug。**

---
## <a name="ssms-april-2016-preview"></a>SSMS 2016 年 4 月预览版 
版本号：13.0.14000.36
  
* **通过 SSMS 安装程序改进，可添加能人工读取的错误消息。**  
  
* **“延伸数据库”向导改进，增加对谓词的支持**。  
  
* **“始终加密”Powershell commandlet 改进，可以添加密钥加密 API**。  
  
* **通过 Bug 修复，可在 SSMS 工具栏中关闭 IntelliSense（如果其已在“工具”、“选项”对话框中禁用）。**  
*链接的客户 Bug 请求：*  
<https://connect.microsoft.com/SQLServer/feedback/details/2555163/sql-2016-rc2-turning-off-intellisense-from-options-does-not-turn-it-off-on-toolbar/>  
    
* **显示计划比较用户界面中的改进和 Bug 修复，可以减少长查询计划使用的空间**。  
  
* **SSMS 中的 Bug 修复，可以修复导致 SSMS 在退出时出现故障的问题**。   
  
* **“始终加密”向导中的 Bug 修复，可以在加密期间保留用户权限并支持在该向导完成后进行数据库分离操作**。  
  
* **通过“Always Encrypted 新列主密钥”对话框中的 Bug 修复，可提供有关尝试使用不受支持的加密算法 (CNG) 提供程序生成密钥的反馈。**  
  
---  
## <a name="ssms-march-2016-preview-refresh"></a>SSMS 2016 年 3 月预览版刷新
版本号：13.0.13000.55
  
* **SSMS 目前使用 Visual Studio 2015 独立 Shell。**  
*链接的客户 Bug 请求：*  
<https://connect.microsoft.com/SQLServer/feedback/details/2390544/update-ssms-to-use-visual-studio-2015-dependencies/>  
  
* **通过新的快速启动工具栏，可帮助你快速查找菜单项和选项。（VS 2015 独立 shell）**  
  
* **通过 SSMS 主题选项改进，增加对 SSMS 浅色主题的支持。（VS 2015 独立 shell）**  
  
* **通过 SSMS 工具菜单选项中的 Bug 修复，如果按下“重置为默认值”按钮，可正确重置查询快捷方式。**  
  
* **通过 SSMS 新项目模板中的 Bug 修复，可显示易读模板名称。**  
  
* **修复了查看 SSMS 中 SQL 代理作业历史记录时出现的错误。**  
*链接的客户 Bug 请求：*  
<https://connect.microsoft.com/SQLServer/feedback/details/2458860/error-viewing-job-history-microsoft-datawarehouse-sqm/>  
    
* **通过 Bug 修复，可支持离线安装 SSMS。支持无需连接 Internet 即可进行安装。（VS 2015 独立 shell）**  
*链接的客户 Bug 请求：*  
<https://connect.microsoft.com/SQLServer/feedback/details/2497178/cannot-install-ssms-when-server-has-no-internet-access/>  
    
* **通过 Bug 修复，在导入 SQL Server PowerShell (SQLPS) 模块时可以保留用户当前目录。**  
*链接的客户 Bug 请求：*  
<https://connect.microsoft.com/SQLServer/feedback/details/2434605/loading-sqlps-module-changes-current-directory-to-ps-sqlserver/>  
    
* **通过 SQL Server PowerShell (SQLPS) 模块中的 Bug 修复，可使用批准的 PowerShell 动词。**  
*链接的客户 Bug 请求：*  
<https://connect.microsoft.com/SQLServer/feedback/details/2432891/sqlps-module-uses-unapproved-powershell-verbs/>  
    
* **通过 SQL Server Powershell (SQLPS) 模块中的 Bug 修复，可更快地加载模块。**  
*链接的客户 Bug 请求：*  
<https://connect.microsoft.com/SQLServer/feedback/details/2429153/sqlps-module-is-slow-to-load/>  
    
* **通过 SQL 代理作业步骤中的 Bug 修复，可支持修改作业步骤。**  
*链接的客户 Bug 请求：*  
<https://connect.microsoft.com/SQLServer/feedback/details/2453996/issues-with-agent-in-ssms-2016-rc0-13-0-12000-65/>  
    
* **通过 SSMS 对象资源管理器中的 Bug 修复，可按字母顺序列出表格。**  
*链接的客户 Bug 请求：*  
<https://connect.microsoft.com/SQLServer/feedback/details/2424718/sql-server-2016-ssms-table-list-confusing/>  
    
* **通过“可用数据库”下拉列表中的 Bug 修复，可在 SQL Server 连接发生更改时显示数据库名称的准确列表。**  
*链接的客户 Bug 请求：*  
<https://connect.microsoft.com/SQLServer/feedback/details/2513420/available-databases-drop-down-box-does-not-update-when-connection-changes-in-ssms/>  
    
* **通过 SSMS 键盘快捷方式中的 Bug 修复，如果按下“CTRL+U”按键，则可以将焦点移动至“可用数据库”下拉列表**  
*链接的客户 Bug 请求：*  
<https://connect.microsoft.com/SQLServer/feedback/details/2534820/ssms-ctrl-u-doesnt-work/>  
  
---  
## <a name="ssms-march-2016-preview"></a>SSMS 2016 年 3 月预览版 
版本号：13.0.12500.29 
  
* **通过 SSMS Web 安装程序改进，可支持使用键盘键导航。**  
  
* **通过 AlwaysEncrypted 向导改进，可支持使用别名数据类型进行加密。**  
  
* **通过 AlwaysOn“新建可用性组”向导中的 Bug 修复，可显示自动故障转移目标准确的最大数目。**  
*链接的客户 Bug 请求：* <https://connect.microsoft.com/SQLServer/feedback/details/2333670/ssms-is-showing-the-wrong-number-of-maximum-automatic-failover-targets/>  
    
* **通过 SSMS Web 安装程序中的 Bug 修复，可修复影响安装的错误。**  
*链接的客户 Bug 请求：*  
<https://connect.microsoft.com/SQLServer/feedback/details/2181548/sql-server-2016-ctp-3-2-management-studio-setup/>  
    
* **通过 SSMS 预览版本中的 Bug 修复，可支持在 SQL Server 2012 及更低版本中保存维护计划。**  
      
* **通过“备份”向导中的 Bug 修复，可支持自定义的多个备份名称用于带区备份，并且在选定存储凭据后，如果输入新名称则可显示相应的备份文件名称。**  
  
---  
## <a name="ssms-february-2016-preview"></a>SSMS 2016 年 2 月预览版 
版本号：13.0.12000.65
  
* **通过活动监视器改进，在 SSMS 中启用高对比度设置后，可显示文本选项。**  
  
* **通过“Always Encrypted 向导”对话框改进，可在加密过程中要更改列的排序规则时显示警告。**  
  
* **通过策略管理改进，可添加对创建有关列加密密钥、列加密密钥值和列主密钥条件的支持。**  
  
* **通过 Bug 修复，可提高“Always Encrypted 主密钥清除”对话框和“Always Encrypted”错误消息可用性。**  
  
* **通过 Bug 修复，可在仅存在一个密钥时禁用“Always Encrypted”列主密钥轮换。**  
  
* **修复了 Bug：使用 SSMS 1 月版本或与 SQL Server RC0 媒介绑定的 SSMS 版本启动“始终加密”对话框后，出现“类型初始值设定项”错误。**  
  
---  
## <a name="ssms-january-2016-preview"></a>SSMS 2016 年 1 月预览版 
版本号：13.0.11000.78 
  
* **通过 SSMS 中的 Bug 修复，可允许删除扩展事件 (XEvent) 会话。**  
  
* **通过 Bug 修复，可打开 SQL Server 2014 可用性组的属性对话框。**  
 *链接的客户 Bug 请求：*  
 <https://connect.microsoft.com/SQLServer/feedback/details/1609719/>  
     
* **通过 Bug 修复，可启用将 Azure 副本添加到可用性组的功能。**  
 *链接的客户 Bug 请求：*  
 <https://connect.microsoft.com/SQLServer/feedback/details/2029135/>  
     
* **通过 Bug 修复，可打开 SQL Server 2014 数据库的属性对话框。**  
 *链接的客户 Bug 请求：*  
 <https://connect.microsoft.com/SQLServer/feedback/details/2080209/>  
     
* **通过 Bug 修复，可删除在连接到 Azure SQL 数据库时每个表出现的重复列。**  
 *链接的客户 Bug 请求：*  
 <https://connect.microsoft.com/SQLServer/feedback/details/2103116/>  
---  
## <a name="ssms-december-2015-preview"></a>SSMS 2015 年 12 月预览版 
版本号：13.0.900.73
  
* **通过对显示计划比较的改进，可支持将当前查询执行计划与文件中保存的计划进行比较。**  
  
* **通过改进 IntelliSense，可支持 SSMS 中的内联列存储索引。**  
  
* **通过扩展事件会话向导中的 Bug 修复，可支持在连接到 Azure V12 服务器时选择模板。**  
  
* **通过“安全性”文件夹下的“创建审核”和“新建登录名”对话框中的全新制表位，可支持更方便的键盘导航。**  
  
* **通过 Bug 修复，可支持“查询执行后切换到结果选项卡”功能（当 SSMS 设置为以网格格式显示结果时）。**   
 *链接的客户 Bug 请求：*  
  <https://connect.microsoft.com/SQLServer/feedback/details/1390296/switch-to-results-tab-after-query-execution-grid-mode-in-ssms-2016>  
  
* **通过 Bug 修复，可显示未被截断的列标题（当 SSMS 设置为以网格格式显示结果时）。**  
 *链接的客户 Bug 请求：*  
  <https://connect.microsoft.com/SQLServer/feedback/details/2004111/bugbash-column-headers-in-grid-mode-truncated-with-courier-new-8>  
      
* **通过 Bug 修复，可允许正确安装 SSMS Web 安装程序。**  
 *链接的客户 Bug 请求：*  
<https://connect.microsoft.com/SQLServer/feedback/details/2003865/ssms-october-preview-incoherent-error-message>  
<https://connect.microsoft.com/SQLServer/feedback/details/2079557/unable-to-instal-sql-server-update-13-0-800-111-over-13-0-700-242-error-code-2711>  
  
---  
## <a name="ssms-november-2015-preview"></a>SSMS 2015 年 11 月预览版
版本号：13.0.800.111
  
* **SSMS 中的高 DPI 显示器支持进行位图缩放。**  
  
* **“AlwaysEncrypted”对话框和向导的用户界面有所改进，简化了创建数据库加密密钥的流程。**  
  
* **活动监视器中的“进程”列表的右键单击上下文菜单新增了一个选项，用于查看实时查询统计信息。**  
  
* **通过 Bug 修复，可正确卸载客户端计算机上的 SSMS 预览版。**  
  *链接的客户 Bug 请求：*  
  <https://connect.microsoft.com/SQLServer/feedback/details/1868474/ssms-2016-preview-can-be-installed-but-not-uninstalled>  
  
* **修复了 Bug，允许在 SQL 作业代理中执行编辑作业的步骤，即使缺少文件也能实现此操作**。  
  *链接的客户 Bug 请求：*  
  <https://connect.microsoft.com/SQLServer/feedback/details/1769778/management-studio-2016-sql-job-agent>  
    <https://connect.microsoft.com/SQLServer/feedback/details/1502100/ssms-preview-error>  
      
* **通过“查看目标数据”菜单选项中的 Bug 修复，可对在 Azure 虚拟机中运行的数据库进行扩展事件会话。**  
  *链接的客户 Bug 请求*：  
  <https://connect.microsoft.com/SQLServer/feedback/details/1769778/management-studio-2016-sql-job-agent>  
***  

## <a name="ssms-october-2015-preview"></a>SSMS 2015 年 10 月预览版 
版本号：13.0.700.242  
* **通过新的现代化轻型 Web 安装程序，可简化 SSMS 下载和安装过程。**  
  
* **通过新的 Always Encrypted 列加密向导，可启用选定列的客户端加密和解密。**  
  
* **新的“列主密钥 (CMK)轮换”对话框，用于始终加密数据库，可简化轮换加密密钥以保护数据安全的过程。**  
  
* **通过新的延伸数据库监视器，可允许你对 Azure 云的数据迁移状态进行疑难解答和监视。**  
  
* **通过对延伸数据库向导的改进，可支持选择不在默认的 Microsoft Azure 订阅中的 Microsoft Azure 服务器。**  
  *链接的客户 Bug 请求：*  
  <https://connect.microsoft.com/SQLServer/feedback/details/1687063/cannot-choose-from-multiple-microsoft-azure-subscriptions>  
* **通过 Bug 修复，可在 SSMS 中正确显示实时执行计划。**  
  *链接的客户 Bug 请求：*  
<https://connect.microsoft.com/SQLServer/feedback/details/1774446/viewing-live-execution-plan-from-activity-monitor-crashes-ssms>    
* **通过 Bug 修复，可在数据快照的 SSMS 脚本中删除无效选项**  
  *链接的客户 Bug 请求：*  
<https://connect.microsoft.com/SQLServer/feedback/details/1515168/ssms-scripting-of-database-snapshots-includes-invalid-options>  
* **通过查询数据存储 UI 中的 Bug 修复，可在“热门资源使用查询”窗格中显示详细信息。**  
  *链接的客户 Bug 请求：*  
<https://connect.microsoft.com/SQLServer/feedback/details/1737185/sql-server-2016-overall-resource-consumption-query-store-pane-issue>  
***  

## <a name="ssms-september-2015-preview"></a>SSMS 2015 年 9 月预览版 
版本号：13.0.600.65  
* **通过新的“防火墙规则”对话框，可简化连接到 Azure SQL 数据库的过程。**      
    
* **通过更新的“新建索引”对话框，可实现即使存在群集列存储索引时也能创建非群集行存储索引。此功能适用于 SQL 2016 和更高版本。**      
  *链接的客户 Bug 请求：*    
  <https://connect.microsoft.com/SQLServer/feedback/details/1552617/creation-of-nc-index-when-clustered-columnstore-index>  
      
* **通过 Bug 修复，可在 Windows 7 上运行的 SSMS 预览版中查看和编辑 SQL 代理作业步骤。**      
  *链接的客户 Bug 请求：*    
  <https://connect.microsoft.com/SQLServer/feedback/details/1548140/cannot-view-or-edit-any-sql-agent-job-step>、    
  <https://connect.microsoft.com/SQLServer/feedback/details/1626895/unable-to-load-dll-dts>、    
  <https://connect.microsoft.com/SQLServer/feedback/details/1576662/error-creating-new-job-step>     
      
* **通过 Bug 修复，可在适用于 SQL Server 2014 和更高版本的 SSMS 中显示触发器节点。**      
  *链接的客户 Bug 请求：*    
  <https://connect.microsoft.com/SQLServer/feedback/details/1617533/trigger-node-missing>   
      
* **通过数据和服务器标准报告用户界面中的 Bug 修复，可从标题中排除版本信息。**      
  *链接的客户 Bug 请求：*    
  <https://connect.microsoft.com/SQLServer/feedback/details/1387471/report-headings-wrongly-named>  
      
* **通过 Bug 修复，可防止实时查询统计信息节点在其不完整时显示为完整。**      
  *链接的客户 Bug 请求：*    
  <https://connect.microsoft.com/SQLServer/feedback/details/1589096/live-query-statistics-node-shows-as-completed>  
  
***      
## <a name="ssms-august-2015-preview"></a>SSMS 2015 年 8 月预览版 
版本号：13.0.500.53
  
* **通过对象资源管理器更新，可在存在大量数据库时减少加载延迟。**  
  
* **对在 Windows 10 计算机上安装 SSMS 的改进。**  
  
* **对 SQL Server 配置管理器和 SSMS 用户报告用户界面的 Bug 修复和更新**    
***  
  
## <a name="ssms-july-2015-preview"></a>SSMS 2015 年 7 月预览版
版本号：13.0.400.91
  
* **Azure SQL Database (V12) 的数据库关系图。**  
  
* **通过改进 IntelliSense，可支持新的临时表语法。**  
  
* **更新 DacFx 库，用于支持最新的 Azure SQL 数据库功能，包括行级安全和 Azure Active Directory 身份验证。**  
  
* **Bug 修复（已更新“检查更新”UI、“兼容性级别”列表中的 UI 修复等）。**  
***  
  
## <a name="ssms-june-2015-preview"></a>SSMS 2015 年 6 月预览版 
版本号：13.0.300.44
  
* **新的 SSMS 轻型 Web 安装程序。**  
  
* **自动检查更新。**  
  
* **SSMS 现在支持对 Azure SQL Database (V12) 进行全文搜索。**  
  
* **已解决的热门客户请求：**  
  * 为对象资源管理器中的表和视图启用了“编辑前 200 行”。  
  * 为 Azure SQL Database (V12) 启用了表设计器。  
  * 为 Azure SQL Database (V12) 启用了数据库和表属性对话框。  
    
 * **用于跳过保存 T-SQL 文件的提示的新选项。**  
   
 * **对新的 Azure SQL Database 服务层（基本、标准、高级）的导入/导出向导支持。**  
   
 * **大量 Bug 修复（脚本方案、为 SQL 数据库启用更改跟踪等）。**   
     
  
  
  
  
  
  
    

