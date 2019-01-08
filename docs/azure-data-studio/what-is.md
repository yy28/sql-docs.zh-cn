---
title: 概述
titleSuffix: Azure Data Studio
description: Azure Data Studio 是免费的轻型工具，用于管理 SQL Server、 Azure SQL 数据库和 Azure SQL 数据仓库运行在 Windows、 macOS 和 Linux。
ms.custom: seodec18
ms.date: 09/24/2018
ms.prod: sql
ms.technology: azure-data-studio
ms.reviewer: alayu; sstein
ms.topic: overview
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: ca279b9bbc945cbd9aad5be0bce3165820598fe1
ms.sourcegitcommit: 189a28785075cd7018c98e9625c69225a7ae0777
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2018
ms.locfileid: "53030771"
---
# <a name="what-is-azure-data-studio"></a>什么是 Azure Data Studio？

Azure Data Studio是一种跨平台数据库工具，适用于在Windows，MacOS和Linux上使用Microsoft系列内部部署和云数据平台的数据专业人员。

此前在预览名称SQL Operations Studio下发布的Azure Data Studio提供了现代化编辑器体验，包括Intellisense，代码片段，源代码控制集成和集成终端。 它在设计时考虑了数据平台用户，内置了查询结果集和可自定义的仪表板。

**[下载并安装 [!INCLUDE[name-sos](../includes/name-sos-short.md)]](download.md)**


## <a name="transact-sql-t-sql-code-editor-with-intellisense"></a>具有 IntelliSense 的 TRANSACT-SQL (T-SQL) 代码编辑器

[!INCLUDE[name-sos](../includes/name-sos-short.md)] 提供了现代的、以键盘为中心的 T-SQL 编码体验，使用内置的功能使你的日常任务更加容易。这些功能包括：多选项卡窗口、丰富的 T-SQL 编辑器、IntelliSense、关键字补全、代码片段、代码导航和源代码管理集成 (Git)。 运行按需 T-SQL 查询，以文本、JSON 或 Excel 格式查看和保存结果。 编辑数据、组织最喜欢的数据库连接，以及以熟悉的对象浏览体验浏览数据库对象。 若要了解如何使用 T-SQL 编辑器，请参阅[使用 T-SQL 编辑器来创建数据库对象](tutorial-sql-editor.md)。

## <a name="smart-t-sql-code-snippets"></a>智能 T-SQL 代码片段

T-SQL 代码片段生成正确的 T-SQL 语法来创建数据库、 表、 视图、 存储的过程、 用户、 登录名、 角色、 等，并更新现有数据库对象。 使用智能代码片段来快速创建开发或测试目的，数据库的副本和要生成并执行创建和插入脚本。

[!INCLUDE[name-sos](../includes/name-sos-short.md)] 此外提供了功能，以创建自定义 T-SQL 代码片段。 若要了解详细信息，请参阅[创建和使用代码片段](code-snippets.md)。


## <a name="customizable-server-and-database-dashboards"></a>可自定义服务器和数据库仪表板

创建丰富的可定制仪表板，以监视并快速解决数据库中的性能瓶颈。 若要了解见解小组件和数据库（以及服务器）仪表板，请参阅[使用见解小组件管理服务器和数据库](insight-widgets.md)。

## <a name="connection-management-server-groups"></a>连接管理（服务器组）

可以通过服务器组来组织所用服务器和数据库的连接信息。 有关详细信息，请参阅[服务器组](server-groups.md)。

## <a name="integrated-terminal"></a>集成的终端

使用你最喜爱的命令行工具 (例如 Bash、 PowerShell、 sqlcmd、 bcp 和 ssh 配合使用) 在集成终端窗口中右[!INCLUDE[name-sos](../includes/name-sos-short.md)]用户界面。 若要了解有关集成终端的信息，请参阅[集成的终端](integrated-terminal.md)。

## <a name="extensibility-and-extension-authoring"></a>可扩展性和扩展创建

增强[!INCLUDE[name-sos](../includes/name-sos-short.md)]通过扩展功能的基本安装体验。 [!INCLUDE[name-sos](../includes/name-sos-short.md)] 数据管理活动，以及对扩展创建的支持，提供了扩展点。

若要了解有关中的可扩展性[!INCLUDE[name-sos](../includes/name-sos-short.md)]，请参阅[扩展性](extensibility.md)。
若要了解有关创作扩展，请参阅[扩展插件创作](extension-authoring.md)。




## <a name="next-steps"></a>后续步骤
- [下载并安装 [!INCLUDE[name-sos](../includes/name-sos-short.md)]](download.md)
- [连接和查询 SQL Server](quickstart-sql-server.md)
- [连接和查询 Azure SQL 数据库](quickstart-sql-database.md)
