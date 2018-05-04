---
title: Microsoft SQL 操作 Studio （预览版） 发行说明 |Microsoft 文档
description: Microsoft SQL 操作 Studio （预览版） 发行说明
ms.custom: tools|sos
ms.date: 04/25/2018
ms.prod: sql
ms.reviewer: alayu; erickang; sstein
ms.suite: sql
ms.prod_service: sql-tools
ms.component: sos
ms.tgt_pltfrm: ''
ms.topic: conceptual
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 3e13f0604ebbfc616a70768d7382b0e044055ec6
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
---
# <a name="sql-operations-studio-preview-release-notes"></a>SQL 操作 Studio （预览版） 发行说明

**[下载年 4 月公共预览版](download.md)**


## <a name="april-2018-april-public-preview"></a>年 4 月 2018 （年 4 月公共预览版）

发布日期： 2018 年 4 月 25，  
版本： 0.28.6

*年 4 月公共预览版*包含 bug 修复和改进。 

- 对 SQL 代理预览版扩展的改进。
- 改进了大型和受保护的文件是否支持保存受保护的管理员和 > 256 M SQL 操作 Studio 中的文件。
- 集成终端的拆分，若要同时使用多个打开终端。
- 减少的安装磁盘上的文件计数资源占用打印更快的安装和启动时间。
- 继续修复 GitHub 问题：
   - 修复[发出 37](https://github.com/Microsoft/sqlopsstudio/issues/37)： 当图表查看器引发错误时，会发生意外的行为。
   - 修复[发出 462](https://github.com/Microsoft/sqlopsstudio/issues/462)： 功能请求： 服务器组，默认情况下扩展的选项。
   - 修复[发出 606](https://github.com/Microsoft/sqlopsstudio/issues/606): intellisense 的更新命令的错误建议。
   - 修复[发出 967](https://github.com/Microsoft/sqlopsstudio/issues/967)： 预期查询计划时在结果网格中选择 XML 显示计划。
   - 修复[发出 1023年](https://github.com/Microsoft/sqlopsstudio/issues/1023)： 从 flyfishingdba 添加 ms_foreachdb 调用的方括号。
   - 修复[发出 1048年](https://github.com/Microsoft/sqlopsstudio/issues/1048)： 预登录 SSL/TLS 握手错误。
   - 修复[发出 1050年](https://github.com/Microsoft/sqlopsstudio/issues/1050)： 显示错误之前查看清除见解。
   - 修复[发出 1057年](https://github.com/Microsoft/sqlopsstudio/issues/1057)： 还原和新的查询操作，在资源管理器小组件已断开。
   - 修复[发出 1068年](https://github.com/Microsoft/sqlopsstudio/issues/1068)： 仪表板输出 windows 弹出使用 Azure SQL 数据库的错误消息。
   - 修复[发出 1069年](https://github.com/Microsoft/sqlopsstudio/issues/1069)： 连接对话框显示最初显示时所需的服务器错误。
   - 修复[发出 1070年](https://github.com/Microsoft/sqlopsstudio/issues/1070)： 服务器组现在需要一次双击以展开。
   - 修复[发出 1072年](https://github.com/Microsoft/sqlopsstudio/issues/1072)： 选择控件背景为不完全透明。
   - 修复[发出 1115年](https://github.com/Microsoft/sqlopsstudio/issues/1115): SQL 操作 Studio 请在修复所有高对比度可访问性问题。
   - 修复[发出 1101年](https://github.com/Microsoft/sqlopsstudio/issues/1101)： 升级"下载手动"链接到的扩展失败将转到错误的位置。
   - 修复[发出 1103年](https://github.com/Microsoft/sqlopsstudio/issues/1103): V 滚动主页选项卡上未工作。
   - 修复[发出 1104年](https://github.com/Microsoft/sqlopsstudio/issues/1104): SQL 扩展选项卡停止工作。


对于年 4 月公共预览版重要突出显示部分是 Visual Studio 代码 1.21 平台源代码刷新。 这将显示在多个更新的核心编辑器和 workbench，从上一个 1.19 同步点。 一些示例包括：

- [新的通知 UI](https://code.visualstudio.com/updates/v1_21#_new-notifications-ui) -轻松地管理和查看 SQL 操作 Studio 通知。
- [集成终端拆分](https://code.visualstudio.com/updates/v1_21#_split-terminals)-同时使用多个打开终端。
- [保存大型和受保护文件](https://code.visualstudio.com/updates/v1_20#_save-files-that-need-admin-privileges)-保存受保护的管理员和 > 256 M SQL 操作 Studio 中的文件。
- [改进了大型文件的支持](https://code.visualstudio.com/updates/v1_21#_text-buffer-improvements)的大型文件的文本缓冲区优化。
- [改善的设置搜索](https://code.visualstudio.com/updates/v1_20#_settings-search)-轻松地查找使用自然语言搜索的正确设置。
- [全局段](https://code.visualstudio.com/updates/v1_20#_global-snippets)-创建代码段可以跨所有文件类型使用。
- [资源管理器多选择](https://code.visualstudio.com/updates/v1_20#_multi-select-in-the-explorer)-同时在多个文件上执行操作。
- [错误 （&) 在资源管理器警告](https://code.visualstudio.com/updates/v1_20#_error-indicators-in-the-explorer)-快速导航到代码库中的错误。
- [拖动和删除、 复制和粘贴跨 windows](https://code.visualstudio.com/updates/v1_21#_better-drag-and-drop-support) -在打开的 SQL 操作 Studio 窗口移动文件。
- [Git 子模块支持](https://code.visualstudio.com/updates/v1_20#_git-submodules)-嵌套的 Git 存储库上的执行 Git 操作。
- [终端屏幕读取器支持](https://code.visualstudio.com/updates/v1_20#_screen-reader-support)-集成终端现在具有"屏幕读取器优化"模式。
- [居中的编辑器布局](https://code.visualstudio.com/updates/v1_21#_centered-editor-layout)-最大化代码查看屏幕的实际空间。
- [水平搜索结果 （预览版）](https://code.visualstudio.com/updates/v1_21#_horizontal-search) -您可以立即查看搜索结果中水平的面板。

有关其他详细信息，请查看[Visual Studio 代码年 2 月发行说明](https://code.visualstudio.com/updates/v1_21)，和[Visual Studio 代码年 1 月发行说明](https://code.visualstudio.com/updates/v1_20)。

有关详细信息，请参阅[更改日志](https://github.com/Microsoft/sqlopsstudio/blob/master/CHANGELOG.md)。

## <a name="march-2018-march-public-preview"></a>年 3 月 2018 （年 3 月公共预览版）

发布日期： 2018 年 3 月 28，  
版本： 0.27.3

*年 3 月公共预览版*继续解决的首要 GitHub 问题并集中于改进我们的扩展性故事。 具体而言启用扩展管理器，改进了仪表板管理，并提供 SQL 代理和 insights 扩展。 此版本包括以下增强功能：

- 增强仪表板扩展性模型以支持选项卡式的见解和配置窗格。
   - 扩展管理器使简单获取扩展。
   - 从 sp_whoisactive 的仪表板扩展[whoisactive.com](http://www.whoisactive.com)。
   - 有关详细信息，请参阅[扩展的功能的 SQL 操作 Studio](extensions.md)。
- 添加其他[连接和对象资源管理器的扩展性 Api](https://github.com/Microsoft/sqlopsstudio/wiki/Extensibility-API)管理。
- 继续修复影响的重要客户[GitHub 问题](https://github.com/Microsoft/sqlopsstudio/issues)。


## <a name="february-2018-february-public-preview"></a>年 2 月 2018 （年 2 月公共预览版）

发布日期： 2018 年 2 月 15，  
版本： 0.26.7

*年 2 月公共预览版*包括一些功能建议和高优先级 bug 修复。 此版本包括以下增强功能：

- 引入了自动更新安装，该属性提供通知可用于下载新的发行版时 
- 连接对话框 Database 字段现在为动态填充的下拉列表将包含从指定服务器填充数据库的列表。
- 修复[发出 6](https://github.com/Microsoft/sqlopsstudio/issues/6)： 打开新查询选项卡时保持连接和所选的数据库。
- 修复[发出 22](https://github.com/Microsoft/sqlopsstudio/issues/22): 服务器名称和数据库名称 '-可以这些是下拉列表而不是文本框？
- 修复[发出 549](https://github.com/Microsoft/sqlopsstudio/issues/549)： 无提示/十分无提示安装会导致应用程序安装后打开。
- 修复[发出 481](https://github.com/Microsoft/sqlopsstudio/issues/481)： 添加"检查更新"选项。
- SQL 编辑器着色和自动完成修补程序：
   - 修复[发出 584](https://github.com/Microsoft/sqlopsstudio/issues/584): intellisense 完全未突出显示的关键字。
   - 修复[发出 345](https://github.com/Microsoft/sqlopsstudio/issues/345)： 对编辑器内的着色 SQL 函数。
   - 修复[发出 300](https://github.com/Microsoft/sqlopsstudio/issues/300): [#tempData] 最新"]"将显示绿色。
   - 修复[发出 225](https://github.com/Microsoft/sqlopsstudio/issues/225)： 关键字颜色不匹配。
   - 修复[发出 60](https://github.com/Microsoft/sqlopsstudio/issues/60)： 无效的 sql 语法颜色突出显示使用 from 子句中的临时表时。
- 介绍连接扩展性 API。
- VS 代码编辑器 1.19 集成。
- 更新 JustinPealing/html-查询计划组件提取到查询计划查看器的多项改进。


## <a name="january-2018-january-public-preview"></a>年 1 月 2018 （年 1 月公共预览版）

发布日期： 2018 年 1 月 17，  
版本： 0.25.4

*年 1 月公共预览版*包括一些功能建议和高优先级 bug 修复。 此版本包括以下增强功能：

- 已保存的服务器连接是在连接对话框中可用。
- 启用热退出。 热退出处于关闭状态默认情况下，若要启用，请参阅[热退出设置](settings.md#hot-exit)。
- 基于服务器组的选项卡着色。 选项卡着色处于关闭状态默认情况下，若要启用，请参阅[选项卡颜色设置](settings.md#tab-color)。
- 更改*服务器名称*到*服务器*在连接对话框。
- 中断的修复*运行当前查询*命令。
- 修复拖放重大脚本 bug。
- 修复不正确的固定开始菜单图标。
- 修复缺少品牌图标的 Azure 帐户。


## <a name="december-2017-december-public-preview"></a>自 2017 年 12 月 （年 12 月公共预览版）

发布日期： 2017 年 12 月 19 日  
版本： 0.24.1

*年 12 月公共预览版*中所有功能区域，以及以下增强功能包括多项 bug 修复：

- 创建防火墙规则对话框现已可帮助连接到 Azure SQL 数据库和 Azure SQL 数据仓库。
- 添加的 Windows 安装程序和 Linux DEB 和 RPM 安装包。
- 管理仪表板可视布局编辑器。
- *Alter 脚本*和*执行脚本*命令。
- *使用实际的计划运行当前查询*命令。
- 将集成 VS Code 1.18.1 编辑器平台。
- 启用旁加载的 VSIX 扩展文件。
- 支持"转到 N"批处理迭代语法。


## <a name="november-2017"></a>自 2017 年 11 月

发布日期： 2017 年 11 月 15 日  
版本： 0.23.6

- 初始版本的[!INCLUDE[name-sos](../includes/name-sos-short.md)]。


## <a name="next-steps"></a>后续步骤

请参阅以下快速入门中，若要开始之一：
- [连接和查询 SQL Server](quickstart-sql-server.md)
- [连接和查询 Azure SQL 数据库](quickstart-sql-database.md)
- [连接和查询 Azure 数据仓库](quickstart-sql-dw.md)

贡献[!INCLUDE[name-sos](../includes/name-sos-short.md)]:
- [https://github.com/Microsoft/sqlopsstudio](https://github.com/Microsoft/sqlopsstudio)
