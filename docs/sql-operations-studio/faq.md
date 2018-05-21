---
title: SQL 操作 Studio （预览版） 常见问题 |Microsoft 文档
description: 常见问题 (FAQ) SQL 操作 studio （预览版）。
ms.custom: tools|sos
ms.date: 11/15/2017
ms.prod: sql
ms.reviewer: alayu; sstein
ms.suite: sql
ms.prod_service: sql-tools
ms.component: sos
ms.tgt_pltfrm: ''
ms.topic: conceptual
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 2410938dbe57dc5bcb8032cb85daf6fb12bf1a1f
ms.sourcegitcommit: 6fd8a193728abc0a00075f3e4766a7e2e2859139
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/17/2018
---
# <a name="includename-sosincludesname-sosmd-faq"></a>[!INCLUDE[name-sos](../includes/name-sos.md)] 常见问题

## <a name="what-is-includename-sosincludesname-sos-shortmd"></a>什么是[!INCLUDE[name-sos](../includes/name-sos-short.md)]？

[!INCLUDE[name-sos](../includes/name-sos-short.md)] 是一个免费的轻型数据库开发和操作工具，在桌面上运行，并可用于 Windows、 macOS 和 Linux。 [!INCLUDE[name-sos](../includes/name-sos-short.md)] 具有内置支持，或在任何云的 Azure SQL 数据库、 Azure SQL 数据仓库和在本地运行的 SQL Server。 [!INCLUDE[name-sos](../includes/name-sos-short.md)] 跨你最喜欢的操作系统上所选的数据库提供一致的体验。

## <a name="where-can-i-get-includename-sosincludesname-sos-shortmd"></a>在何处获取[!INCLUDE[name-sos](../includes/name-sos-short.md)]？

下载[!INCLUDE[name-sos](../includes/name-sos-short.md)]于 Windows、 macOS 和从 Linux [http://aka.ms/sqlopsstudio](download.md)

## <a name="how-much-does-includename-sosincludesname-sos-shortmd-cost"></a>多少[!INCLUDE[name-sos](../includes/name-sos-short.md)]成本？

[!INCLUDE[name-sos](../includes/name-sos-short.md)] 对于是免费的私有或商业使用。

## <a name="who-should-use-includename-sosincludesname-sos-shortmd"></a>哪些人应该使用[!INCLUDE[name-sos](../includes/name-sos-short.md)]？

任何人都可以使用[!INCLUDE[name-sos](../includes/name-sos-short.md)]。 但是，它旨在简化执行数据库开发人员、 数据库管理员、 系统管理员和独立软件供应商的任务。


## <a name="what-can-i-do-with-includename-sosincludesname-sos-shortmd"></a>可以使用干什么[!INCLUDE[name-sos](../includes/name-sos-short.md)]？ 

[!INCLUDE[name-sos](../includes/name-sos-short.md)] 构建在 Visual Studio Code 之上，并提供一种轻型聚焦于键盘现代代码流体验使用 SQL 时。 

[!INCLUDE[name-sos](../includes/name-sos-short.md)] 使依赖于每天简单且轻松地使用多个选项卡窗口、 丰富的 SQL 编辑器、 IntelliSense、 关键字完成、 代码段和的代码导航和源代码管理集成 （Git 和 TFS） 等的内置功能的核心体验。 你可以执行按需查询、 查看和将结果另存为文本、 JSON 或 Excel，编辑数据、 组织和管理你最喜欢的数据库的连接，并浏览浏览体验熟悉对象中的数据库对象。

使用你最喜欢的命令行工具 (例如，Bash，PowerShell、 sqlcmd、 bcp、 psql，和 ssh) 中集成的终端窗口中右[!INCLUDE[name-sos](../includes/name-sos-short.md)]用户界面。 轻松地生成并执行创建和数据库对象创建的进行开发或测试你的数据库副本的插入脚本。 提高工作效率与智能代码段和丰富图形体验，创建新的数据库和数据库对象 （如表、 视图、 存储的过程、 用户、 登录名、 角色等） 或更新现有数据库对象。 使用丰富可自定义仪表板来监视和快速解决性能瓶颈上本地数据库中，在 Azure 中或任何云。

[!INCLUDE[name-sos](../includes/name-sos-short.md)] 提供一致的体验来备份和还原数据库。 SQL Server Alwayson 可用性组的计划支持，你可以轻松地配置、 监视和诊断承载个可用性组您执行关键任务的 SQL Server 数据库和快速故障转移到辅助数据库发生灾难期间。
[!INCLUDE[name-sos](../includes/name-sos-short.md)] 旨在让您选择在所选的操作系统上的数据库的 DevOps 生命周期中提高工作效率。 因此，你可以始终在控件中，并可以降低风险、 更快、 解决问题和连续提供超过客户预期的价值。


## <a name="is-includename-sosincludesname-sos-shortmd-open-source"></a>是[!INCLUDE[name-sos](../includes/name-sos-short.md)]打开源？ 

源代码[!INCLUDE[name-sos](../includes/name-sos-short.md)]并且其数据访问接口在 GitHub 上提供。 前端的源代码[!INCLUDE[name-sos](../includes/name-sos-short.md)]（它基于 Visual Studio Code） 位于下源代码提供权限以修改并使用该软件，但不是能重新分发它，或在云服务中托管它的 EULA。 数据提供程序的源代码是依据 MIT 许可在可用[ https://github.com/Microsoft/sqltoolsservice ](https://github.com/Microsoft/sqltoolsservice)。

## <a name="do-you-plan-to-open-source-ssms"></a>你是否打算开源 SSMS？

否。 但是下, 一代 multi-OS CLI 和 GUI 工具是开放源代码。 例如，VS Code、 mssql 脚本编写器和 msql CLI mssql 扩展是在 GitHub 上的所有开放源代码。 源代码[!INCLUDE[name-sos](../includes/name-sos-short.md)]GitHub 上提供。


## <a name="now-that-there-is-includename-sosincludesname-sos-shortmd-does-microsoft-plan-to-deprecate-ssms-and-ssdt"></a>现在，没有[!INCLUDE[name-sos](../includes/name-sos-short.md)]，没有 Microsoft 计划否决 SSMS 和 SSDT？

否。 除了 multi-OS 和多 DB CLI 和 GUI 工具的下一代外，还将继续旗舰 Windows 工具 （SSMS、 SSDT、 PowerShell） 中的投资。
目标是能够为客户提供对其方案在他们选择的平台上使用他们希望的工具的选择。


## <a name="includename-sosincludesname-sos-shortmd-is-missing-a-feature-that-is-in-ssmsssdt-will-you-add-it"></a>[!INCLUDE[name-sos](../includes/name-sos-short.md)] 缺少 SSMS/SSDT 中的功能。 你将添加它？
它依赖于方案和客户/业务需要。 若要帮助确定的优先级，文件的建议上[GitHub](https://github.com/microsoft/sqlopsstudio/issues)。


## <a name="i-understand-includename-sosincludesname-sos-shortmd-and-the-mssql-extension-for-vs-code-are-powered-by-a-new-tools-service-that-uses-smo-apis-under-the-covers-is-smo-available-on-linux-and-macos"></a>我了解[!INCLUDE[name-sos](../includes/name-sos-short.md)]和由一个新的电源都已 VS Code 的 mssql 扩展*工具服务*，实际上使用 SMO Api。 在 Linux 和 macOS 上提供了 SMO。

SMO Api 尚不可用在 Linux 或 macOS 上可使用的方式。 我们移植到我们所需的.NET 核心 SMO Api 的子集通过[!INCLUDE[name-sos](../includes/name-sos-short.md)]，并且我们打算展开路线图的一部分。
在 GitHub 上的 SQL 工具服务是： [ https://github.com/Microsoft/sqltoolsservice ](https://github.com/Microsoft/sqltoolsservice)。


## <a name="do-you-plan-to-port-the-dacfx-apis-andor-sqlpackageexe-andor-ssdt-to-linux-and-macos"></a>你是否打算端口的 DACFx Api 和/或 sqlpackage.exe 和/或 SSDT 到 Linux 和 macOS？

它位于长期的路线图上。 若要帮助确定的优先级，文件的建议上[GitHub](https://github.com/microsoft/sqlopsstudio/issues)。


## <a name="will-sql-powershell-cmdlets-be-available-on-linux-and-macos"></a>将 SQL PowerShell cmdlet 可在 Linux 和 macOS 上？

SQL PowerShell 目前已在 PowerShell 库上，你可以使用它在 Windows 上运行任何位置，包括在 Linux 上的 SQL 的 SQL Server 使用。 产品 SQL PowerShell cmdlet 在 Linux 和 macOS 上的是在规划之中。 若要帮助确定的优先级，文件的建议上[GitHub](https://github.com/microsoft/sqlopsstudio/issues)。

