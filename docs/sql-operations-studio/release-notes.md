---
title: Microsoft SQL Operations Studio (preview) 发行说明 |Microsoft 文档
description: Microsoft SQL Operations Studio (preview) 发行说明
ms.custom: tools|sos
ms.date: 03/28/2018
ms.prod: sql-non-specified
ms.reviewer: alayu; erickang; sstein
ms.suite: sql
ms.prod_service: sql-tools
ms.component: sos
ms.tgt_pltfrm: ''
ms.topic: article
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: ba86403e791af25de4f7bcd8b1cbd7b5f188897b
ms.sourcegitcommit: d6881107b51e1afe09c2d8b88b98d075589377de
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/28/2018
---
# <a name="sql-operations-studio-preview-release-notes"></a>SQL Operations Studio (preview) 发行说明

**[下载年 3 月公共预览版](download.md)**

## <a name="march-2018-march-public-preview"></a>年 3 月 2018 （年 3 月公共预览版）

发布日期： 2018 年 3 月 28，  
version: 0.27.3

*年 3 月公共预览版*继续解决的首要 GitHub 问题并集中于改进我们的扩展性故事。 具体而言启用扩展管理器，改进了仪表板管理，并提供 SQL 代理和 insights 扩展。 此版本包括以下增强功能：

- 增强仪表板扩展性模型以支持选项卡式的见解和配置窗格。
   - 扩展管理器使简单获取扩展。
   - 从 sp_whoisactive 的仪表板扩展[whoisactive.com](http://www.whoisactive.com)。
   - 有关详细信息，请参阅[扩展的功能的 SQL Operations Studio](extensions.md)。
- 添加其他[连接和对象资源管理器的扩展性 Api](https://github.com/Microsoft/sqlopsstudio/wiki/Extensibility-API)管理。
- 继续修复影响的重要客户[GitHub 问题](https://github.com/Microsoft/sqlopsstudio/issues)。

有关详细信息，请参阅[更改日志](https://github.com/Microsoft/sqlopsstudio/blob/master/CHANGELOG.md)。


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
