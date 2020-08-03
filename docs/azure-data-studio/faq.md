---
title: Azure Data Studio 常见问题解答
description: 获取有关 Azure Data Studio 的常见问题的解答，例如“它有什么作用？”、“它的受众是谁？”、“费用是多少？”。
ms.prod: azure-data-studio
ms.technology: ''
ms.topic: conceptual
author: markingmyname
ms.author: maghan
ms.reviewer: alayu, maghan, sstein
ms.custom: seodec18
ms.date: 09/24/2018
ms.openlocfilehash: 123618a84b07aa2215a2666f9d427f669247c5d7
ms.sourcegitcommit: 620a868e623134ad6ced6728ce9d03d7d0038fe0
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/29/2020
ms.locfileid: "87411093"
---
# <a name="azure-data-studio-faq"></a>Azure Data Studio 常见问题解答

## <a name="what-is-azure-data-studio"></a>什么是 Azure Data Studio？

Azure Data Studio 是一种新的开源跨平台桌面环境，适合在 Windows、macOS 和 Linux 上使用 Azure Data 系列本地及云数据平台的数据专业人员。 Azure Data Studio 提供现代编辑器体验，其中包括速度超快的 IntelliSense、代码片段、源代码管理集成和集成终端，之前发布的 SQL Operations Studio 是它的预览版。 它在设计时考虑了数据平台用户，带有内置查询结果集图表和可自定义的仪表板。

研究表明，在使用 SQL Server Management Studio 时，相比其他任务，用户在处理查询编辑上花费的时间要多得多。 出于这个原因，Azure Data Studio 侧重于关注最常用的功能，并通过产品的可选扩展项提供更丰富的体验。 这使得每个用户都可以根据自己最常用的工作流对环境进行自定义。

## <a name="how-much-does-azure-data-studio-cost"></a>Azure Data Studio 的费用是多少？

Azure Data Studio 面向私人或商业用途免费提供。

## <a name="who-should-use-azure-data-studio"></a>哪些人适合使用 Azure Data Studio

任何人都可以使用 Azure Data Studio。 但它的目的主要是简化数据库开发人员、数据库管理员、系统管理员和独立软件供应商所执行的任务。

## <a name="what-can-i-do-with-azure-data-studio"></a>Azure Data Studio 有什么用途？

Azure Data Studio 在 Visual Studio Code 的基础上构建，为使用 SQL Server、Azure SQL 数据库、Azure SQL DW 的用户提供轻量级、以键盘为主要输入方式的现代代码工作流体验。 Azure Data Studio 提供的内置功能能够使用户每天赖以工作的核心操作变得简单易实现，这些功能包括多个选项卡窗口、丰富的 SQL 编辑器、IntelliSense、关键字完成、代码片段和代码导航、源代码管理集成（Git 和 TFS）等。 可以执行按需查询，查看结果并将其另存为文本、JSON 或 Excel，编辑数据，组织和管理常用的数据库连接，以及通过熟悉的方式来浏览数据库对象。

在 Azure Data Studio 用户界面中的“集成终端”窗口中使用常用的命令行工具（例如，Bash、PowerShell、sqlcmd、bcp、psql 和 ssh）。 轻松为自己的数据库对象生成并执行 CREATE 和 INSERT 脚本，以便创建数据库副本，供开发或测试用。 通过智能代码段和丰富的图形体验，创建新的数据库和数据库对象（例如，表、视图、存储过程、用户、登录名、角色等）或更新现有数据库对象，从而大幅提高工作效率。 丰富的可自定义仪表板可用于监视并快速排查本地、Azure 或任何云中的数据库中出现的性能瓶颈问题。

Azure Data Studio 提供一致的备份和还原数据库的体验。 通过 SQL Server Always-On 可用性组的计划支持，可以轻松地为任务关键型 SQL Server 数据库配置、监视 AG 并对其进行故障排除，并在灾难期间快速故障转移到辅助数据库。 Azure Data Studio 旨在提高你在所需操作系统中所需数据库（在其 DevOps 生命周期中）上的工作效率。 其结果是，一切都在你的掌控之中，你可以降低风险、更快速地解决问题，并持续提供超出客户期望的价值。

## <a name="is-azure-data-studio-open-source"></a>Azure Data Studio 是开源环境吗？

GitHub 上提供了 Azure Data Studio 及其数据提供程序的源代码。 可通过一个提供软件修改和使用权限的源代码 EULA 来获取前端 Azure Data Studio（它在 Visual Studio Code 的基础上构建）的源代码，但不能在云服务中重新分发或托管该源代码。 可通过 MIT 许可证获取数据提供程序的源代码，其网址为 [https://github.com/Microsoft/sqltoolsservice](https://github.com/Microsoft/sqltoolsservice)。

## <a name="do-we-plan-to-open-source-ssms"></a>我们是否计划要使用开源 SSMS？

不是。 但新一代多操作系统 CLI 和 GUI 工具是开源工具。 例如，GitHub 上的 VS Code、mssql-scripter 和 msql-CLI 的 mssql 扩展都是开源的。 GitHub 上提供 Azure Data Studio 的源代码。  

## <a name="now-that-there-is-azure-data-studio-does-microsoft-plan-to-deprecate-ssms-and-ssdt"></a>既然要使用 Azure Data Studio，Microsoft 是否计划弃用 SSMS 和 SSDT？ 

不是。 除了要投资新一代多操作系统和多数据库 CLI 以及 GUI 工具，我们将继续投资重要的 Windows 工具（SSMS、SSDT、PowerShell）。 我们的目标是为客户提供工具使用上的选择，使其能够根据方案需要在所需平台上使用所需工具。 Azure Data Studio 更专注于查询编辑和数据开发体验，据研究表明，这项功能在 SQL Server Management Studio 中的使用频率比其他功能高出一个数量级。 Azure Data Studio 中还以扩展项的方式提供了其他高价值的管理功能，如备份、恢复、代理作业管理和服务器分析等。 Azure Data Studio 同时还是跨平台的环境，这使用户能够在所需平台上工作。 不过，SQL Server Management Studio 所提供的管理功能相较而言仍是最全面广泛的，因此仍是处理平台管理任务的一个非常重要的工具。 

## <a name="when-should-i-use-azure-data-studio-vs-sql-server-management-studio"></a>分别应在什么情况下使用 Azure Data Studio 和 SQL Server Management Studio？

*如为以下情况，请使用 Azure Data Studio：*

- 花费大量时间编辑或执行查询。
- 需要能够快速绘图和直观显示结果集。
- 可通过集成终端使用 sqlcmd 或 PowerShell 执行大多数管理任务。
- 对向导的使用需求较少。
- 不需要实施深层次的管理或平台配置。
- 需要在 macOS 或 Linux 上运行。

*如为以下情况，请使用 SQL Server Management Studio：*

- 在数据库管理任务上花费大量时间。
- 需要实施复杂的管理或平台配置。
- 要实施安全管理，包括用户管理、漏洞评估和安全功能配置。
- 需要使用性能优化顾问和仪表板。
- 使用数据库关系图和表设计器。
- 要导入/导出 DACPAC。
- 需要访问经过注册的服务器。
- 需要利用 sqlcmd 模式、实时查询统计信息或客户端统计信息。

## <a name="feature-comparison"></a>功能对比

### <a name="shell-features"></a>Shell 功能

|Feature|Azure Data Studio|SSMS|
|:---|:---|:---|
|Azure 登录|“是”|“是”|
|仪表板|是| |
|扩展|是| |
|集成终端|是||
|“对象资源管理器”|“是”|“是”|
|对象脚本|“是”|“是”|
|项目系统|是||
|从表中选择|“是”|“是”|
|源代码管理|是||
|任务窗格|是||
|主题|是||
|深色模式|是||
|Azure 资源浏览器|预览||
|生成脚本向导||是
|导入\导出 DACPAC||是|
|对象属性||是|
|表设计器||是|

### <a name="query-editor"></a>查询编辑器

|Feature|Azure Data Studio|SSMS|
|:---|:---|:---|
|图表查看器|是||
|将结果导出为 CSV、JSON、XLSX|是||
|IntelliSense|“是”|“是”|
|代码片段|“是”|“是”|
|显示计划|预览|是|
|客户端统计信息||是|
|实时查询统计信息||是|
|查询选项||是|
|将结果保存到文件||是|
|以文本格式显示结果||是|
|空间查看器||是|
|SQLCMD||是|
|T-SQL 调试程序||是|

### <a name="operating-system-support"></a>操作系统支持

|Feature|Azure Data Studio|SSMS|
|:---|:---|:---|
|Windows|“是”|“是”|
|macOS|是||
|Linux|是||

### <a name="data-engineering"></a>数据工程

|Feature|Azure Data Studio|SSMS|
|:---|:---|:---|
|外部数据向导|预览||
|HDFS 集成|预览||
|笔记本|预览||

### <a name="database-administration"></a>数据库管理

|Feature|Azure Data Studio|SSMS|
|:---|:---|:---|
|备份/还原|“是”|“是”|
|平面文件导入|预览|是|
|SQL 代理|预览|是|
|SQL Profiler|预览|是|
|AlwaysOn||是|
|Always Encrypted||是|
|复制数据向导||是|
|数据优化顾问||是|
|数据库关系图||是|
|错误日志查看器||是|
|维护计划||是|
|多服务器查询||是|
|基于策略的管理||是|
|PolyBase||是|
|查询存储||是|
|已注册的服务器||是|
|复制||是|
|安全管理||是|
|Service Broker||是|
|SQL Mail||是|
|模板资源管理器||是|
|漏洞评估||是|
|XEvent 管理||是|


## <a name="azure-data-studio-is-missing-a-feature-that-is-in-ssmsssdt-will-you-add-it"></a>Azure Data Studio 缺少 SSMS/SSDT 中提供的一项功能。 是否添加该功能？

这取决于方案和客户/业务需求。 为帮助确定优先级，请在 [GitHub](https://github.com/microsoft/azuredatastudio/issues) 上提交建议。

## <a name="i-understand-azure-data-studio-and-the-mssql-extension-for-vs-code-are-powered-by-a-new-tools-service-that-uses-smo-apis-under-the-covers-is-smo-available-on-linux-and-macos"></a>我了解 Azure Data Studio 和 VS Code 的 mssql 扩展由一个使用 SMO API 的新工具服务在后台提供支持。 SMO 是否可在 Linux 和 macOS 上使用？

目前用户还无法在 Linux 或 macOS 上使用 SMO API。 我们已将 SMO API 的一个子集移植到 .NET Core 中，Azure Data Studio 需要该子集，我们计划扩展该集合，并将该计划加入路线图。 SQL 工具服务位于 GitHub 上：[https://github.com/Microsoft/sqltoolsservice](https://github.com/Microsoft/sqltoolsservice)。

## <a name="do-you-plan-to-port-the-dacfx-apis-andor-sqlpackageexe-andor-ssdt-to-linux-and-macos"></a>是否计划将 DACFx API 和/或 sqlpackage.exe 和/或 SSDT 移植到 Linux 和 macOS 中？

长期路线图中包含此计划。 为帮助确定优先级，请在 [GitHub](https://github.com/microsoft/azuredatastudio/issues) 上提交建议。

## <a name="will-sql-powershell-cmdlets-be-available-on-linux-and-macos"></a>SQL PowerShell cmdlet 是否可在 Linux 和 macOS 上使用？

现在 PowerShell 库可使用 SQL PowerShell，可以在 Windows 上使用它来处理在任何位置运行的 SQL Server，包括 Linux 上的 SQL。 路线图中包含了这一计划：在 Linux 和 macOS 上提供 SQL PowerShell cmdlet。 为帮助确定优先级，请在 [GitHub](https://github.com/microsoft/azuredatastudio/issues) 上提交建议。

## <a name="who-usually-uses-azure-data-studio"></a>有哪些人员会经常使用 Azure Data Studio？

开发人员和 DBA 通常是 Azure Data Studio 的用户。

## <a name="does-azure-data-studio-integrate-with-azure-sql-data-warehouse"></a>Azure Data Studio 是否与 Azure SQL 数据仓库进行了集成？

是的。 Azure Data Studio 对 Azure SQL 数据仓库的支持目前为预览版，同时提供 Azure SQL 数据库管理实例和 SQL Server 2019 大数据。

## <a name="why-is-azure-data-studio-important-for-the-new-version-of-sql-server"></a>为何 Azure Data Studio 对于新版本的 SQL Server 而言很重要？

随着 SQL Server 将其功能扩展到大数据空间，它需要新的工具来支持这些用例。 出于此原因，Azure Data Studio 现在提供 SQL Server 大数据支持的全新预览体验，包括 SQL Server 工具集提供的前所未有的笔记本体验，以及新的“创建外部表”向导，可使从远程 SQL Server 和 Oracle 实例访问数据变得简单快捷。
