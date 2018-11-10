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
ms.openlocfilehash: e30906efb126b0c7fba225ff2aeb3308f0bf050c
ms.sourcegitcommit: 9f2edcdf958e6afce9a09fb2e572ae36dfe9edb0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/25/2018
ms.locfileid: "50099779"
---
# <a name="what-is-includename-sosincludesname-sosmd"></a>什么是[!INCLUDE[name-sos](../includes/name-sos.md)]？

Azure Data Studio是一种跨平台数据库工具，适用于在Windows，MacOS和Linux上使用Microsoft系列内部部署和云数据平台的数据专业人员。

此前在预览名称SQL Operations Studio下发布的Azure Data Studio提供了现代化编辑器体验，包括Intellisense，代码片段，源代码控制集成和集成终端。 它在设计时考虑了数据平台用户，内置了查询结果集和可自定义的仪表板。

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

使用你最喜爱的命令行工具 (例如 Bash、 PowerShell、 sqlcmd、 bcp 和 ssh 配合使用) 在集成终端窗口中右[!INCLUDE[name-sos](../includes/name-sos-short.md)]用户界面。 若要了解有关集成终端的信息，请参阅[集成的终端](integrated-terminal.md)。

## <a name="extensibility-and-extension-authoring"></a>可扩展性和扩展创建

增强[!INCLUDE[name-sos](../includes/name-sos-short.md)]通过扩展功能的基本安装体验。 [!INCLUDE[name-sos](../includes/name-sos-short.md)] 数据管理活动，以及对扩展创建的支持，提供了扩展点。

若要了解有关中的可扩展性[!INCLUDE[name-sos](../includes/name-sos-short.md)]，请参阅[扩展性](extensibility.md)。
若要了解有关创作扩展，请参阅[扩展插件创作](extension-authoring.md)。




## <a name="next-steps"></a>后续步骤
- [下载并安装 [!INCLUDE[name-sos](../includes/name-sos-short.md)]](download.md)
- [连接和查询 SQL Server](quickstart-sql-server.md)
- [连接和查询 Azure SQL 数据库](quickstart-sql-database.md)
