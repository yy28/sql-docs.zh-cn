---
title: 常见问题解答
titleSuffix: Azure Data Studio
description: 有关 Azure Data Studio 常见问题常见问题 (FAQ)。
ms.prod: sql
ms.technology: azure-data-studio
ms.topic: conceptual
author: markingmyname
ms.author: maghan
manager: craigg
ms.reviewer: alayu; sstein
ms.custom: seodec18
ms.date: 09/24/2018
ms.openlocfilehash: 0b73dabb77ae04b915efa50dd8e0a8453b3ab3be
ms.sourcegitcommit: bb5484b08f2aed3319a7c9f6b32d26cff5591dae
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/06/2019
ms.locfileid: "65105084"
---
# <a name="includeazure-data-studioincludesname-sosmd-faq"></a>[!INCLUDE[Azure Data Studio](../includes/name-sos.md)] 常见问题

## <a name="what-is-azure-data-studio"></a>什么是 Azure Data Studio？

Azure Data Studio 是新的开放源跨平台桌面环境，用于数据专业人员使用 Azure 数据系列的本地和云平台 Windows、 MacOS 和 Linux 上的数据。 此前已发布预览版名称 SQL Operations Studio 下，Azure Data Studio 产品/服务的现代编辑器体验的既快速 IntelliSense、 代码段、 源代码管理集成和集成的终端。 它在设计时考虑了数据平台用户，内置了查询结果集和可自定义的仪表板。

研究表明，用户会更多的时间用在查询编辑比使用 SQL Server Management Studio 的任何其他任务上花费的数量级。 为此，Azure Data Studio 旨在深入地专注于最多用于可作为可选扩展到产品的其他体验的功能。 这允许以自定义其环境的工作流的他们最常使用的每个用户。


## <a name="how-much-does-azure-data-studio-cost"></a>Azure Data Studio 费用是多少？

Azure Data Studio 是免费的专用或商用。

## <a name="who-should-use-azure-data-studio"></a>谁应该使用 Azure Data Studio

任何人都可以使用 Azure Data Studio。 但是，它旨在简化执行数据库开发人员、 数据库管理员、 系统管理员和独立软件供应商的任务。

## <a name="what-can-i-do-with-azure-data-studio"></a>使用 Azure Data Studio 可以做什么？

Azure Data Studio 基于 Visual Studio Code，并提供了一种轻型，键盘焦点位于新式代码工作流体验，使用 SQL Server、 Azure SQL 数据库，Azure SQL 数据仓库时。 Azure Data Studio 使依赖于每日简单而轻松的内置功能，如多个选项卡窗口、 丰富的 SQL 编辑器、 IntelliSense、 关键字完成、 代码片段和代码导航和源代码管理集成 (Git 核心体验和 TFS）。 可以执行按需查询、 查看 （& a） 将结果保存为文本、 JSON 或 Excel，编辑数据、 组织和管理您最喜欢的数据库的连接，并浏览类似对象浏览体验中的数据库对象。

使用你最喜爱的命令行工具 (例如 Bash、 PowerShell、 sqlcmd、 bcp、 psql，和 ssh) 直接在 Azure Data Studio 用户界面在集成终端窗口中。 轻松地生成并执行创建和数据库对象创建的开发或测试用途的数据库副本的插入脚本。 提高工作效率与智能代码段和丰富图形体验，创建新的数据库和数据库对象 （如表、 视图、 存储的过程、 用户、 登录名、 角色等） 或更新现有数据库对象。 使用丰富可自定义仪表板来监视并快速解决在您本地数据库中，在 Azure 或任何云的性能瓶颈。

Azure Data Studio 提供了一致的体验来备份和还原数据库。 SQL Server Always-On 可用性组的支持计划，可以轻松地配置、 监视和诊断 Ag 您关键任务 SQL Server 数据库和快速故障转移到辅助数据库在发生灾难期间。 Azure Data Studio 旨在让你选择在所选的操作系统上的数据库的开发运营生命周期中提高工作效率。 因此，您可以始终控制，并可以降低风险和更快地解决问题并持续提供超过客户期望的值。

## <a name="is-azure-data-studio-open-source"></a>是 Azure 数据 Studio 开放源代码？

Azure Data Studio 和其数据访问接口的源代码是 GitHub 上提供。 前端的 Azure Data Studio （这基于 Visual Studio Code） 的源代码，请参阅源代码提供权限以修改并使用该软件，但不是能重新分发它，或在云服务中托管它的 EULA。 数据提供程序的源代码可在 MIT 许可证下[ https://github.com/Microsoft/sqltoolsservice ](https://github.com/Microsoft/sqltoolsservice)。

## <a name="do-we-plan-to-open-source-ssms"></a>我们是否打算开放源代码 SSMS？

否。 但是下, 一代多操作系统 CLI 和 GUI 工具是开放源代码。 例如，适用于 VS Code、 mssql 脚本编写者和 msql CLI 的 mssql 扩展是 GitHub 上的所有开放源代码。 Azure Data Studio 的源代码是 GitHub 上提供。  

## <a name="now-that-there-is-azure-data-studio-does-microsoft-plan-to-deprecate-ssms-and-ssdt"></a>现在，没有 Azure Data Studio，的确 Microsoft 计划不推荐使用的 SSMS 和 SSDT？ 

否。 除了新一代的多操作系统和多 DB CLI 和 GUI 工具外，还将继续旗舰 Windows 工具 （SSMS、 SSDT、 PowerShell） 中的投资。 目标是能够为客户提供其方案为他们选择的平台上使用所需的工具的选择。 Azure Data Studio 更紧密地致力于解决查询编辑体验和数据开发，哪些调查显示是 SQL Server Management Studio 中通过一个数量级的最常用的功能。 其他高价值管理功能，例如备份、 还原、 代理作业管理和服务器配置文件，还提供作为 Azure Data Studio 中的扩展。 Azure Data Studio 也是跨平台，允许用户选择的其平台上工作。 但是，SQL Server Management Studio 仍提供了广泛的管理功能，并保持平台管理任务的旗舰工具。 

## <a name="when-should-i-use-azure-data-studio-vs-sql-server-management-studio"></a>当我应该使用 Azure Data Studio 与 SQL Server Management Studio？

*如果使用 Azure Data Studio 您：*

- 花大部分时间编辑或执行查询。
- 需要快速图表和可视化处理的结果集的能力。
- 可以执行大多数管理任务通过使用 sqlcmd 或 Powershell 集成终端。
- 对向导体验的最小需求。
- 不需要执行深度管理或平台相关的配置。
- 需要在 macOS 或 Linux 上运行。

*如果使用 SQL Server Management Studio 您：*

- 数据库管理任务上花费的大部分时间。
- 执行复杂的管理或平台配置。
- 执行安全管理，包括用户管理、 漏洞评估和安全功能的配置。
- 需要进行性能优化顾问和仪表板的使用。
- 使用数据库关系图和表设计器。
- 正在导入/导出的 Dacpac。
- 需要已注册的服务器访问。
- 请使用 sqlcmd 模式下，实时查询统计信息或客户端统计信息。

## <a name="feature-comparison"></a>功能比较

### <a name="shell-features"></a>Shell 功能

|功能|Azure Data Studio|SSMS|
|:---|:---|:---|
|Azure 登录|是|是|
|面板|是| |
|Extensions|是| |
|集成的终端|是||
|“对象资源管理器”|是|是|
|对象脚本|是|是|
|项目系统|是||
|从表中选择|是|是|
|源代码管理|是||
|任务窗格|是||
|主题设置|是||
|深色模式|是||
|Azure 资源浏览器|预览||
|生成脚本向导||是
|Import\Export DACPAC||是|
|对象属性||是|
|表设计器||是|

### <a name="query-editor"></a>查询编辑器

|功能|Azure Data Studio|SSMS|
|:---|:---|:---|
|图表查看器|是||
|将结果导出到 CSV、 JSON、 XLSX|是||
|IntelliSense|是|是|
|代码段|是|是|
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

|功能|Azure Data Studio|SSMS|
|:---|:---|:---|
|Windows|是|是|
|macOS|是||
|Linux|是||

### <a name="data-engineering"></a>数据工程

|功能|Azure Data Studio|SSMS|
|:---|:---|:---|
|外部数据向导|预览||
|HDFS 的集成|预览||
|笔记本|预览||

### <a name="database-administration"></a>数据库管理

|功能|Azure Data Studio|SSMS|
|:---|:---|:---|
|备份/还原|是|是|
|平面文件导入|预览|是|
|SQL 代理|预览|是|
|SQL Profiler|预览|是|
|AlwaysOn||是|
|始终加密||是|
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
|Replication||是|
|安全管理||是|
|Service Broker||是|
|SQL Mail||是|
|Template Explorer||是|
|漏洞评估||是|
|XEvent 管理||是|


## <a name="azure-data-studio-is-missing-a-feature-that-is-in-ssmsssdt-will-you-add-it"></a>Azure Data Studio 缺少 SSMS/SSDT 中的功能。 您将添加它吗？

这取决于方案和客户/业务需求。 若要帮助确定优先级，文件的一项建议上[GitHub](https://github.com/microsoft/azuredatastudio/issues)。

## <a name="i-understand-azure-data-studio-and-the-mssql-extension-for-vs-code-are-powered-by-a-new-tools-service-that-uses-smo-apis-under-the-covers-is-smo-available-on-linux-and-macos"></a>我了解由在后台使用 SMO Api 的新工具服务提供支持 Azure Data Studio 和适用于 VS Code 的 mssql 扩展。 SMO 是可在 Linux 和 macOS 上？

SMO Api 尚不可用在 Linux 或 macOS 中使用的方式。 我们移植到.NET Core，我们所需的 Azure Data Studio，并且我们打算作为路线图的一部分展开 SMO Api 的子集。 SQL 工具服务是在 GitHub 上： [ https://github.com/Microsoft/sqltoolsservice ](https://github.com/Microsoft/sqltoolsservice)。

## <a name="do-you-plan-to-port-the-dacfx-apis-andor-sqlpackageexe-andor-ssdt-to-linux-and-macos"></a>你是否打算端口的 DACFx Api 和/或 sqlpackage.exe 和/或 SSDT 到 Linux 和 macOS？

它是在较长期的计划之中。 若要帮助确定优先级，文件的一项建议上[GitHub](https://github.com/microsoft/azuredatastudio/issues)。

## <a name="will-sql-powershell-cmdlets-be-available-on-linux-and-macos"></a>将 SQL PowerShell cmdlet 可在 Linux 和 macOS 上？

SQL PowerShell 现已提供在 PowerShell 库上，您可以使用它在 Windows 上使用运行任何位置，包括 Linux 上的 SQL 的 SQL Server。 提供 SQL PowerShell 已在规划 Linux 和 macOS 上的 cmdlet。 若要帮助确定优先级，文件的一项建议上[GitHub](https://github.com/microsoft/azuredatastudio/issues)。

## <a name="who-usually-uses-azure-data-studio"></a>谁通常可使用 Azure Data Studio？

开发人员和 Dba 通常是 Azure Data Studio 的用户。

## <a name="does-azure-data-studio-integrate-with-azure-sql-data-warehouse"></a>与 Azure SQL 数据仓库可以集成 Azure Data Studio 吗？

是。 针对 Azure SQL 数据仓库的 azure Data Studio 支持当前处于预览状态，以及 Azure SQL 数据库托管实例和 SQL Server 2019 大数据。

## <a name="why-is-azure-data-studio-important-for-the-new-version-of-sql-server"></a>为何重要的新版本的 SQL Server 的 Azure Data Studio？

SQL Server 扩展了其功能到大数据领域，因为它需要新的工具来支持那些用例。 为此，Azure Data Studio 将立即发布的适用于 SQL Server 大数据，包括第一个支持新的预览版体验过的笔记本体验中的 SQL Server 工具集和一个新的 Create External Table 向导，用于从远程 SQL 使访问数据Server 和 Oracle 实例更加快捷和方便。
