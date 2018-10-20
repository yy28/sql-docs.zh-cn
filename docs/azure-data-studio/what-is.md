---
title: 什么是 Azure Data Studio？ | Microsoft Docs
description: Azure Data Studio 是一个免费的轻型工具，用于管理 SQL Server、 Azure SQL 数据库和 Azure SQL 数据仓库; 在 Windows、 macOS 和 Linux 上运行它们正在运行的任何位置。
ms.custom: tools|sos
ms.date: 09/24/2018
ms.prod: sql
ms.technology: azure-data-studio
ms.reviewer: alayu; sstein
ms.topic: overview
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 296274548b725a620d577916d2c76d31c923c4c0
ms.sourcegitcommit: 35e4c71bfbf2c330a9688f95de784ce9ca5d7547
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/16/2018
ms.locfileid: "49356528"
---
# <a name="what-is-includename-sosincludesname-sosmd"></a>什么是[!INCLUDE[name-sos](../includes/name-sos.md)]？

Azure Data Studio 是一个跨平台数据库工具的数据专业人员使用 Microsoft 系列的本地和云平台 Windows、 MacOS 和 Linux 上的数据。

此前已发布预览版名称 SQL Operations Studio 下，Azure Data Studio 提供了与 Intellisense、 代码段、 源代码管理集成和集成的终端的现代编辑器体验。 它设计，与数据平台用户的需求，提供内置的查询结果集和可自定义仪表板的图表。

**[下载并安装 [!INCLUDE[name-sos](../includes/name-sos-short.md)]](download.md)**


## <a name="transact-sql-t-sql-code-editor-with-intellisense"></a>具有 IntelliSense 的 TRANSACT-SQL (T-SQL) 代码编辑器

[!INCLUDE[name-sos](../includes/name-sos-short.md)] 提供了现代、 键盘焦点位于 T-SQL 的编码体验，与内置功能，例如多个选项卡窗口、 丰富的 T-SQL 编辑器、 IntelliSense、 关键字完成、 代码段、 代码导航和源代码管理简化日常任务(Git) 的集成。 运行按需的 T-SQL 查询、 查看以及将结果保存为文本、 JSON 或 Excel。 编辑数据，组织您最喜欢的数据库的连接，并浏览类似对象浏览体验中的数据库对象。 若要了解如何使用 T-SQL 编辑器，请参阅[使用 T-SQL 编辑器来创建数据库对象](tutorial-sql-editor.md)。

## <a name="smart-t-sql-code-snippets"></a>智能 T-SQL 代码片段

T-SQL 代码片段生成正确的 T-SQL 语法来创建数据库、 表、 视图、 存储的过程、 用户、 登录名、 角色、 等，并更新现有数据库对象。 使用智能代码片段来快速创建开发或测试目的，数据库的副本和要生成并执行创建和插入脚本。

[!INCLUDE[name-sos](../includes/name-sos-short.md)] 此外提供了功能，以创建自定义 T-SQL 代码片段。 若要了解详细信息，请参阅[创建和使用代码片段](code-snippets.md)。


## <a name="customizable-server-and-database-dashboards"></a>可自定义服务器和数据库仪表板

创建丰富的可自定义仪表板来监视并快速解决您的数据库中的性能瓶颈。 若要了解有关见解小组件和数据库 （和服务器） 的仪表板，请参阅[管理服务器和数据库与见解小组件](insight-widgets.md)。

## <a name="connection-management-server-groups"></a>（服务器组） 的连接管理

服务器组提供一种方法来组织的服务器和数据库使用的连接信息。 有关详细信息，请参阅[服务器组](server-groups.md)。

## <a name="integrated-terminal"></a>集成的终端

使用你最喜爱的命令行工具 (例如 Bash、 PowerShell、 sqlcmd、 bcp 和 ssh 配合使用) 在集成终端窗口中右[!INCLUDE[name-sos](../includes/name-sos-short.md)]用户界面。 若要了解有关集成终端的信息，请参阅 [集成终端] (集成 terminal.md)。

## <a name="extensibility-and-extension-authoring"></a>可扩展性和扩展创建

增强[!INCLUDE[name-sos](../includes/name-sos-short.md)]通过扩展功能的基本安装体验。 [!INCLUDE[name-sos](../includes/name-sos-short.md)] 数据管理活动，以及对扩展创建的支持，提供了扩展点。

若要了解有关中的可扩展性[!INCLUDE[name-sos](../includes/name-sos-short.md)]，请参阅[扩展性](extensibility.md)。
若要了解有关创作扩展，请参阅[扩展插件创作](extension-authoring.md)。




## <a name="next-steps"></a>后续步骤
- [下载并安装 [!INCLUDE[name-sos](../includes/name-sos-short.md)]](download.md)
- [连接和查询 SQL Server](quickstart-sql-server.md)
- [连接和查询 Azure SQL 数据库](quickstart-sql-database.md)
