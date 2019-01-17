---
title: 发行说明和更改日志
titleSuffix: Azure Data Studio
description: Azure Data Studio 发行说明
ms.custom: seodec18
ms.date: 01/17/2019
ms.prod: sql
ms.technology: azure-data-studio
ms.reviewer: alayu; sstein
ms.topic: conceptual
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 163f5740626b0f4cb927272d46acddc79495e4c1
ms.sourcegitcommit: 9c99f992abd5f1c174b3d1e978774dffb99ff218
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/17/2019
ms.locfileid: "54361677"
---
# <a name="azure-data-studio-latest-release-notes-and-changelog"></a>Azure Data Studio 最新发行说明和更改日志

**[下载并安装最新版本 ！](download.md)**


## <a name="january-hotfix-2019-january-hotfix-release"></a>年 1 月修补程序 2019 （年 1 月修补程序版本）

发布日期：2019 年 1 月 16日日  
版本：1.3.9

版本 1.3.9 修复 1.3.8 中发现的一些问题。 有关详细信息，请参阅[年 1 月修补程序版本](https://github.com/Microsoft/azuredatastudio/milestone/24?closed=1)。

有关详细信息，请参阅[更改日志](https://github.com/Microsoft/azuredatastudio/blob/master/CHANGELOG.md)，并[版本](https://github.com/Microsoft/azuredatastudio/releases)。

## <a name="january-2019-january-release"></a>2019 年 1 月 （1 月份发行版）

发布日期：2019 年 1 月 9 日，  
版本：1.3.8

- 添加 Windows 的新用户安装程序。 与现有系统安装程序中，不同的是新用户的安装程序不需要管理员权限。 这样还可以更轻松的升级体验的非管理员。
- Azure Active Directory 身份验证支持。
- 宣布推出 Idera SQL DM 性能 Insights （预览版）。
- 在 SQL Server 导入扩展中的数据层应用程序向导支持。
- 更新到[SQL Server 2019 预览版扩展](https://docs.microsoft.com/sql/azure-data-studio/sql-server-2019-extension?view=sql-server-ver15)
- SQL Server Profiler 的改进。
- 针对大量查询 （预览版） 流式处理的结果。
- 社区扩展： sp_executesql to sql 和新的数据库。
- 解决[bug 和问题](https://github.com/Microsoft/azuredatastudio/milestone/19?closed=1)。

## <a name="november-2018-november-release"></a>2018 年 11 月 （年 11 月发行版）

发布日期：2018 年 11 月 6 日  
版本：1.2.4

- 更新到[SQL Server 2019 预览版扩展](https://docs.microsoft.com/sql/azure-data-studio/sql-server-2019-extension?view=sql-server-ver15)
- 引入粘贴计划扩展
- 引入了增强色查询扩展，包括 SSMS 编辑器主题
- 修复了在 SQL Server 代理、 Profiler 和导入扩展插件
- 修复.Net Core 在 macOS 上套接字 KeepAlive 问题导致已删除的非活动连接
- 升级到.Net Core 的 SQL 工具服务 2.2 预览版 3 （适用于最终 AAD 支持）

### <a name="bug-fixes"></a>Bug 修复

- 修复[发出 # 2933年](https://github.com/Microsoft/azuredatastudio/issues/2933):连接到 Azure SQL DB 中断
- 修复[发出 # 2914年](https://github.com/Microsoft/azuredatastudio/issues/2914):"参数无效"异常扩展 OE 数据库节点
- 修复[发出 # 2935年](https://github.com/Microsoft/azuredatastudio/pull/2935):在查询结果中正确显示多行消息
- 修复[发出 # 2906年](https://github.com/Microsoft/azuredatastudio/pull/2906):表名称包含特殊字符时，解决编辑数据的文档名称
- 修复[发出 # 2929年](https://github.com/Microsoft/azuredatastudio/issues/2929):生成扩展中的更改日志说以检查更改 VSCode 发行说明
- 修复[发出 # 2719年](https://github.com/Microsoft/azuredatastudio/issues/2719):高对比度主题双精度型值/三元组图标
- 修复[发出 #3047](https://github.com/Microsoft/azuredatastudio/pull/3047):添加用于连接到 SQL Server 命令行接口
- 修复[发出 #3031](https://github.com/Microsoft/azuredatastudio/pull/3031):添加查询计划的主题支持
- ...

## <a name="october-2018-october-release"></a>2018 年 10 月 （年 10 月发行版）

发布日期：2018 年 10 月 29日日  
版本：1.1.4

- 介绍 Azure 资源浏览器来浏览 Azure SQL 数据库
- 提高对象资源管理器和查询编辑器连接稳定性
- SQL 代理扩展的改进
- 更新到[SQL Server 2019 预览版扩展](https://docs.microsoft.com/sql/azure-data-studio/sql-server-2019-extension?view=sql-server-ver15)

### <a name="bug-fixes"></a>Bug 修复
- 修复[发出 # 2717年](https://github.com/Microsoft/azuredatastudio/issues/2717):XML 列结果单击格式设置
- 修复[发出 # 2993年](https://github.com/Microsoft/azuredatastudio/issues/2993):宽度的结果 windows 不完整
- 修复[发出 # 2999年](https://github.com/Microsoft/azuredatastudio/issues/2999):无法加载文件 System.Diagnostics.Tracing Mac 上的，连接到数据库时
- 修复[发出 # 2851年](https://github.com/Microsoft/azuredatastudio/issues/2851):TimeSeries 图表不会正确呈现
- 修复[发出 # 2996年](https://github.com/Microsoft/azuredatastudio/issues/2996):由于突然会话发生了更改的临时表丢失
- ...

有关详细信息，请参阅[更改日志](https://github.com/Microsoft/azuredatastudio/blob/master/CHANGELOG.md)，并[版本](https://github.com/Microsoft/azuredatastudio/releases)。

## <a name="september-2018-september-ga-release"></a>2018 年 9 月 （9 月 GA 版）

发布日期：2018 年 9 月 24日日  
版本：1.0

常规可用性版本的 Azure Data Studio (以前称为 SQL Operations Studio)。

- 宣布推出 SQL Server 2019 预览版扩展。
  - 支持的 SQL Server 2019 预览功能，包括[大数据群集](../big-data-cluster/big-data-cluster-overview.md)支持。
    - 连接到 HDFS/Spark 网关与 SQL Server 2019 预览版一起提供。
    - 浏览 HDFS 上, 传文件、 保存文件，并启动有用操作，例如在 Notebook 中分析 CSV 文件。
    - 提交 Spark 作业从仪表板，或右键单击对象资源管理器中的 HDFS/Spark 连接。
  - Azure 数据 Studio 笔记本
    - 创建或打开笔记本使用集成的笔记本查看器。 在此版本中将笔记本查看器支持连接到本地的内核和 SQL Server 2019 大数据群集。
    - 使用笔记本中的 PROSE 代码 Accelerator 库来了解适用于快速数据准备的文件格式和数据类型。
  - Azure 资源浏览器
    - Azure 资源浏览器视图，可以浏览数据相关的 Azure 帐户的终结点并在对象资源管理器中创建连接到它们连接。 在此版本中支持 Azure SQL 数据库和服务器。
  - SQL Server PolyBase 创建外部表向导
    - 使用简单易用的向导创建外部表和及其支持的元数据结构。 在此版本中，支持远程 SQL Server 和 Oracle 服务器。
- 查询结果网格性能和大量的结果集的用户体验改进功能。
- Visual Studio Code 源代码从 1.23 刷新到 1.26.1 网格布局和改进的设置编辑器 （预览版）。
- 屏幕阅读器、 键盘导航和高对比度的辅助功能改进。
- 添加`Connection name`选项来提供服务器视图允许中的可选显示名称。

### <a name="bug-fixes"></a>Bug 修复

- 修复[发出 # 2647年](https://github.com/Microsoft/azuredatastudio/issues/143):图表向后花费了一大步。
- 修复[发出 # 2648年](https://github.com/Microsoft/azuredatastudio/issues/143):返回 JSON 超链接的整个列的选择。
- ...

有关详细信息，请参阅[更改日志](https://github.com/Microsoft/azuredatastudio/blob/master/CHANGELOG.md)，并[版本](https://github.com/Microsoft/azuredatastudio/releases)。


## <a name="august-2018-august-public-preview"></a>2018 年 8 月 （年 8 月公共预览版）

发布日期：2018 年 8 月 30日日  
版本：0.32.8

*0.32.8 包含几个回归 0.32.7 中找到的修补程序 ([# 1971年](https://github.com/Microsoft/azuredatastudio/issues/1971)， [# 2372年](https://github.com/Microsoft/azuredatastudio/issues/2372)*)

*年 8 月公共预览版*侧重于 bug 修复、 产品稳定化和填充现有方案中的缺口。  

- 宣布推出 SQL Server 导入扩展
- SQL Server Profiler 会话管理
- SQL Server Profiler 会话模板支持
- SQL Server 代理的改进
- 新的社区扩展：第一个响应程序工具包
- 生命周期质量改进：连接字符串

### <a name="bug-fixes"></a>Bug 修复

- 分析 SQL 查询编辑器窗口中的，方法是使用`Parse Syntax`命令。
- 修复[发出 #143](https://github.com/Microsoft/azuredatastudio/issues/143):双击不选择变量名称。
- 修复[问题 #387](https://github.com/Microsoft/azuredatastudio/issues/387):SQL 选项卡 DB 图标为红色。
- 修复[发出 #825](https://github.com/Microsoft/azuredatastudio/issues/825):请求：自动连接到后脚本作为当前服务器... 
- 修复[发出 # 1278年](https://github.com/Microsoft/azuredatastudio/issues/1278): sqlops.desktop [桌面项目]-冗余值名称和注释。
- 修复[发出 # 1285年](https://github.com/Microsoft/azuredatastudio/issues/1285):正在更新会导致应用程序图标，以在 Windows 下无法删除/替换。
- 修复[发出 # 1317年](https://github.com/Microsoft/azuredatastudio/issues/1317):修复小数分隔符。
- 修复[发出 # 1474年](https://github.com/Microsoft/azuredatastudio/issues/1474):取消更改连接断开当前连接的连接。
- 修复[发出 # 1497年](https://github.com/Microsoft/azuredatastudio/issues/1497):作为选项都被截断在底部的图表进行查看。
- 修复[发出 # 1524年](https://github.com/Microsoft/azuredatastudio/issues/1524):Shell/仪表板：主要 viewlet 均图标可拖动，可能会崩溃应用程序。
- 修复[发出 # 1578年](https://github.com/Microsoft/azuredatastudio/issues/1578):不能通过单击名称的展开/折叠远程文件浏览器文件夹。
- 修复[发出 # 1620年](https://github.com/Microsoft/azuredatastudio/issues/1620):功能建议：获取现有连接的连接字符串。
- 修复[发出 # 1624年](https://github.com/Microsoft/azuredatastudio/issues/1624):SelectBox 不会更改颜色时禁用。
- 修复[发出 # 1728年](https://github.com/Microsoft/azuredatastudio/issues/1728):将另存为 JSON/EXCEL/CSV 不工作。
- 修复[发出 # 1744年](https://github.com/Microsoft/azuredatastudio/issues/1744):选项卡之间切换时，结果窗格中将失去其滚动位置。
- 修复[发出 # 1748年](https://github.com/Microsoft/azuredatastudio/issues/1748):保存 Excel 文件，第二个 （和后续） 时间时的错误消息。
- 修复[发出 # 1782年](https://github.com/Microsoft/azuredatastudio/issues/1782):编辑数据： 单元格不会恢复为原始值上点击 Esc 键。
- 修复[发出 # 1836年](https://github.com/Microsoft/azuredatastudio/issues/1836)： 不与 SQL Operations Studio 相关联的.sql 文件。
- 修复[发出 # 人工 1850年](https://github.com/Microsoft/azuredatastudio/issues/1850):键入 N ' 自动填充为 N '。
- 修复[发出 # 1985年](https://github.com/Microsoft/azuredatastudio/issues/1985):从查询结果网格复制处于关闭状态的 1 个列。
- 修复[发出 # 1998年](htpts://github.com/Microsoft/azuredatastudio/pull/1998):添加到有关对话框中的 VS Code 版本。
- 修复[发出 # 2042年](https://github.com/Microsoft/azuredatastudio/pull/2042):代理：启用按钮以从 sql 文件导入查询。
- 修复[发出 # 2091年](https://github.com/Microsoft/azuredatastudio/issues/2091):不能使用快捷方式 Ctrl + C 复制从结果窗格。
- 修复[发出 # 2099年](https://github.com/Microsoft/azuredatastudio/pull/2099):添加更多 saveAsCsv 选项。
- 修复[发出 # 2107年](https://github.com/Microsoft/azuredatastudio/issues/2107):更新仪表板和 Profiler 文档的文档图标。
- 修复[发出 # 2129年](https://github.com/Microsoft/azuredatastudio/pull/2129):切换选项卡时保存编辑数据滚动位置。
- 修复[发出 # 2152年](https://github.com/Microsoft/azuredatastudio/issues/2152):结果网格行指示器从零开始。

### <a name="known-issues"></a>已知问题

- [问题 # 2371年](https://github.com/Microsoft/azuredatastudio/issues/2371)另存为 Excel 仅保存的数据的第一行
- [问题 # 2150年](https://github.com/Microsoft/azuredatastudio/issues/2150):无法连接到容器中的 SQL 的 Ubuntu 16.04 上


## <a name="july-2018-july-public-preview"></a>2018 年 7 月 （7 月公共预览版）

发布日期：2018 年 7 月 19日日  
版本：0.31.4

*年 7 月公共预览版*重点初始版本的 SQL Server 代理配置方案、 SQL Server Profiler 会话和视图模板增强功能，并持续的 bug 修复，为客户报告的 GitHub 问题。 此版本包含以下突出显示部分：  

- [SQL Operations Studio 扩展的 SQL Server 代理](sql-server-agent-extension.md)改进
 - 在左窗格中的警报、 运算符和代理和图标的添加的视图
 - 添加了的对话框用于新的作业、 新建作业步骤、 新建警报和 New 运算符
 - 添加了删除作业、 删除警报和 Delete 运算符 （右键单击）
 - 添加了之前运行可视化效果
 - 对于每个列名称添加筛选器
- [SQL Operations Studio 扩展 SQL Server Profiler](sql-server-profiler-extension.md)改进
 - 添加了快速启动并启动/停止 Profiler 的热键
 - 添加了 5 个默认模板，若要查看扩展事件
 - 添加了的服务器/数据库的连接名称
 - 添加了的对 Azure SQL 数据库实例
 - 添加了的建议 Profiler 仍在运行时关闭选项卡时退出 Profiler
- 版本的合并脚本扩展
- 添加扩展创建者的向导和对话框可扩展性点
- 修复 GitHub 问题：
 - 修复[发出 728](https://github.com/Microsoft/azuredatastudio/issues/728):添加连接到在 macOS 上没有响应
 - 修复[发出 1612年](https://github.com/Microsoft/azuredatastudio/issues/1612):结果网格文本显示全乱了由国际字符
 - 修复[发出 1693年](https://github.com/Microsoft/azuredatastudio/issues/1693):备份对话框：文件浏览器 UI 已中断
 - 修复[发出 1713年](https://github.com/Microsoft/azuredatastudio/issues/1713):受影响行数
 - 修复[发出 1718年](https://github.com/Microsoft/azuredatastudio/issues/1718):无法连接到任何数据源
 - 修复[发出 1719年](https://github.com/Microsoft/azuredatastudio/issues/1719):TypeError 连接到服务器时
 - 修复[发出 1724年](https://github.com/Microsoft/azuredatastudio/issues/1724):扩展对话框已停止工作
 - 修复[发出 1749年](https://github.com/Microsoft/azuredatastudio/issues/1749):BUG:获取解释列中的 HTML 数据
 - 修复[发出 1789年](https://github.com/Microsoft/azuredatastudio/issues/1789):可扩展性： 如果添加连接提供程序卸载将永远不会从列表中删除
 - 修复[发出 1791年](https://github.com/Microsoft/azuredatastudio/issues/1791):Sqlops 扩展： queryeditor.connect() 连接到目标数据库，但用户界面不显示编辑器连接
 - 修复[发出 1799年](https://github.com/Microsoft/azuredatastudio/issues/1799):前 10 个数据库大小图表不区分大小写的实例起作用
 - 修复[发出 1814年](https://github.com/Microsoft/azuredatastudio/issues/1814): sqlops.d.ts 拼写错误导致隐式 any 的类型定义
 - 修复[发出 1817年](https://github.com/Microsoft/azuredatastudio/issues/1817):错误 de Ortografia
 - 修复[发出 1830年](https://github.com/Microsoft/azuredatastudio/issues/1830):在 ButtonComponent 设置 iconPath component() 调用后不会更改图标
 - 修复[发出 1843年](https://github.com/Microsoft/azuredatastudio/issues/1843):更好地表组织


## <a name="june-2018-june-public-preview"></a>2018 年 6 月 （年 6 月公共预览版）

发布日期：2018 年 6 月 20日日  
版本：0.30.6

*年 6 月公共预览版*包含以下突出显示部分：  

- **SQL Operations Studio 为 SQL Server Profiler*预览版*** 扩展初始版本。
- 新**SQL 数据仓库**扩展包含丰富的可自定义仪表板小组件集成到数据仓库的见解。 管理和优化数据仓库以确保它非常适合一致的性能方面的关键方案带来突破。
- **编辑数据"筛选和排序"** 支持。
- **SQL Operations Studio 的 SQL Server 代理*预览版*** 扩展增强功能的作业和作业历史记录视图。
- 改进了**向导和对话框的 UI 生成器框架**扩展性 Api。
- 更新 VS 代码平台源代码集成[2018 年 3 月 (1.22)](https://code.visualstudio.com/updates/v1_22)并[2018 年 4 月 (1.23)](https://code.visualstudio.com/updates/v1_23)释放。
- 修复 GitHub 问题：
  - 功能请求 ([发出 1204年](https://github.com/Microsoft/azuredatastudio/issues/1204)):请到数据，使结果网格自动调整列宽和/或记住手动更改，如果重新运行相同的查询。
  - 修复[发出 1398年](https://github.com/Microsoft/azuredatastudio/issues/1398):应显示添加消息和链接的帐户为空时添加帐户客户按钮。
  - 修复[发出 1399年](https://github.com/Microsoft/azuredatastudio/issues/1399):视图处于折叠状态时，将断开链接的帐户选项卡。
  - 修复[发出 1374年](https://github.com/Microsoft/azuredatastudio/issues/1374):从磁盘打开的.sql 文件时，SQL 工具服务崩溃。
  - 修复[发出 1372年](https://github.com/Microsoft/azuredatastudio/issues/1372):缺少 SQL 关键字"BETWEEN"。
  - 修复[发出 1395年](https://github.com/Microsoft/azuredatastudio/issues/1395):匹配关键字崩溃 SQL 工具服务。
  - 修复[发出 1496年](https://github.com/Microsoft/azuredatastudio/issues/1496):"新 Profiler"对象资源管理器的上下文菜单选项不执行任何操作。
  - 修复[发出 1495年](https://github.com/Microsoft/azuredatastudio/issues/1495):查询编辑器"Explain"查询计划已断开。


## <a name="may-2018-may-public-preview"></a>2018 年 5 月 （可能公共预览版）

发布日期：2018 年 5 月 7 日  
版本：0.29.3

*可能公共预览版*侧重于稳定性和 bug 修复。 此内部版本包含以下突出显示部分：  

- 宣布推出 Redgate SQL 搜索扩展在扩展管理器中提供。
- 社区本地化 10 种语言提供：德语、 西班牙语、 法语、 意大利语、 日语、 朝鲜语、 葡萄牙语、 俄语、 简体中文和繁体中文。
- 减少的遥测集合、 改进的选择退出体验和产品内隐私声明的链接。
- 扩展管理器已改进了的 Marketplace 体验来轻松地发现社区扩展。
- 扩展的 SQL 代理作业和作业历史记录视图的改进。
- Whoisactive 和服务器报表扩展插件的更新。
- 提高管理仪表板属性滚动。
- 修复 GitHub 问题：
   - 修复[发出 703](https://github.com/Microsoft/azuredatastudio/issues/703):输入类似于 HTML 的文本中编辑数据会导致值刷新后无法正确显示
   - 修复[发出 821](https://github.com/Microsoft/azuredatastudio/issues/821): azuredatastudio.deb 包依赖项
   - 修复[发出 1260年](https://github.com/Microsoft/azuredatastudio/issues/1260):关键字 distinct 不会突出显示
   - 修复[发出 1332年](https://github.com/Microsoft/azuredatastudio/issues/1332):编辑数据恢复行不起作用
   - 修复[发出 1215年](https://github.com/Microsoft/azuredatastudio/issues/1215):SQL 代理扩展和状态栏
   - 修复[发出 1316年](https://github.com/Microsoft/azuredatastudio/issues/1316):SQL 代理不再重设大小后更改窗口大小




## <a name="april-2018-april-public-preview"></a>2018 年 4 月 （年 4 月公共预览版）

发布日期：2018 年 4 月 25日日  
版本：0.28.6

*年 4 月公共预览版*包含 bug 修复和改进。 

- SQL 代理预览版扩展的改进。
- 改进了大型和受保护的文件是否支持保存受保护的管理员和 > 在 SQL Operations Studio 256 亿个文件。
- 集成的终端中拆分，以在一次处理多个打开终端。
- 减少的安装磁盘上的文件计数英尺打印速度更快的安装和启动时间。
- 继续修复 GitHub 问题：
   - 修复[发出 37](https://github.com/Microsoft/azuredatastudio/issues/37):如果图表查看器将引发错误，将出现意外的行为。
   - 修复[发出 462](https://github.com/Microsoft/azuredatastudio/issues/462):功能请求：默认情况下展开服务器组的选项。
   - 修复[发出 606](https://github.com/Microsoft/azuredatastudio/issues/606): intellisense 的更新命令的糟糕的建议。
   - 修复[发出 967](https://github.com/Microsoft/azuredatastudio/issues/967):预期的查询计划时在结果网格中选择 XML 显示计划。
   - 修复[发出 1023年](https://github.com/Microsoft/azuredatastudio/issues/1023):从 flyfishingdba 添加 ms_foreachdb 调用的方括号。
   - 修复[发出 1048年](https://github.com/Microsoft/azuredatastudio/issues/1048):预登录 SSL/TLS 握手时出错。
   - 修复[发出 1050年](https://github.com/Microsoft/azuredatastudio/issues/1050):清除 insights 视图，然后再显示错误。
   - 修复[发出 1057年](https://github.com/Microsoft/azuredatastudio/issues/1057):还原和资源管理器小组件中的新查询操作中断。
   - 修复[发出 1068年](https://github.com/Microsoft/azuredatastudio/issues/1068):仪表板输出 windows 弹出并为 Azure SQL 数据库的错误消息。
   - 修复[发出 1069年](https://github.com/Microsoft/azuredatastudio/issues/1069):连接对话框显示了所需的服务器错误时的初始显示。
   - 修复[发出 1070年](https://github.com/Microsoft/azuredatastudio/issues/1070):服务器组现在需要双击以展开。
   - 修复[发出 1072年](https://github.com/Microsoft/azuredatastudio/issues/1072):选择控件背景为半透明。
   - 修复[发出 1115年](https://github.com/Microsoft/azuredatastudio/issues/1115):在 SQL Operations Studio 修复所有高对比度的辅助功能问题。
   - 修复[发出 1101年](https://github.com/Microsoft/azuredatastudio/issues/1101):扩展无法升级"下载手动"链接将转到错误的位置。
   - 修复[发出 1103年](https://github.com/Microsoft/azuredatastudio/issues/1103):无效的主页选项卡上的 V 滚动。
   - 修复[发出 1104年](https://github.com/Microsoft/azuredatastudio/issues/1104):SQL 扩展选项卡停止工作。


对于年 4 月公共预览版的重要突出显示是 Visual Studio 代码 1.21 平台源代码刷新。 这会在多个更新的核心编辑器和 workbench 中从上一 1.19 同步点。 一些示例包括：

- [新的通知 UI](https://code.visualstudio.com/updates/v1_21#_new-notifications-ui) -轻松地管理和查看 SQL Operations Studio 通知。
- [集成终端拆分](https://code.visualstudio.com/updates/v1_21#_split-terminals)-同时使用多个打开终端。
- [保存大型和受保护文件](https://code.visualstudio.com/updates/v1_20#_save-files-that-need-admin-privileges)-将管理受保护的保存和 > 在 SQL Operations Studio 256 亿个文件。
- [改进了大型文件支持](https://code.visualstudio.com/updates/v1_21#_text-buffer-improvements)-文本缓冲区优化大型文件。
- [改进的设置搜索](https://code.visualstudio.com/updates/v1_20#_settings-search)-轻松地找到正确设置了自然语言搜索。
- [全局片段](https://code.visualstudio.com/updates/v1_20#_global-snippets)-创建可以跨所有文件类型使用的代码段。
- [资源管理器多重选择](https://code.visualstudio.com/updates/v1_20#_multi-select-in-the-explorer)-多个文件一次执行的操作。
- [错误和警告在资源管理器](https://code.visualstudio.com/updates/v1_20#_error-indicators-in-the-explorer)-快速导航到您的代码库中的错误。
- [拖动和删除、 复制和粘贴在 windows 上](https://code.visualstudio.com/updates/v1_21#_better-drag-and-drop-support)-在打开的 SQL Operations Studio 窗口之间移动文件。
- [Git 子模块支持](https://code.visualstudio.com/updates/v1_20#_git-submodules)-对嵌套的 Git 存储库执行 Git 操作。
- [终端屏幕阅读器支持](https://code.visualstudio.com/updates/v1_20#_screen-reader-support)-集成终端现在具有"屏幕读取器优化"模式。
- [居中的编辑器布局](https://code.visualstudio.com/updates/v1_21#_centered-editor-layout)-最大化代码查看屏幕空间。
- [水平搜索结果 （预览版）](https://code.visualstudio.com/updates/v1_21#_horizontal-search) -你可以在水平的面板中现在查看搜索结果。

有关其他详细信息，签出[Visual Studio 代码年 2 月发行说明](https://code.visualstudio.com/updates/v1_21)，并[Visual Studio 代码年 1 月发行说明](https://code.visualstudio.com/updates/v1_20)。

有关详细信息，请参阅[更改日志](https://github.com/Microsoft/azuredatastudio/blob/master/CHANGELOG.md)。

## <a name="march-2018-march-public-preview"></a>2018 年 3 月 （年 3 月公共预览版）

发布日期：2018 年 3 月 28日日  
版本：0.27.3

*年 3 月公共预览版*不断处理最主要的 GitHub 问题并集中于改进我们的可扩展性故事。 具体而言，启用扩展管理器中，改进的仪表板管理，并提供 SQL 代理和 insights 扩展。 此版本包括以下增强功能：

- 增强仪表板可扩展性模型，以支持选项卡式的见解和配置窗格。
   - 扩展管理器启用扩展的简单的采购。
   - 仪表板扩展从 sp_whoisactive [whoisactive.com](http://www.whoisactive.com)。
   - 有关详细信息，请参阅[扩展功能的 SQL Operations Studio](extensions.md)。
- 可添加更多[连接和对象资源管理器的扩展性 Api](https://github.com/Microsoft/azuredatastudio/wiki/Extensibility-API)管理。
- 继续修复影响的重要客户[GitHub 问题](https://github.com/Microsoft/azuredatastudio/issues)。


## <a name="february-2018-february-public-preview"></a>2018 年 2 月 （年 2 月公共预览版）

发布日期：2018 年 2 月 15日日  
版本：0.26.7

*年 2 月公共预览版*包括一些功能建议和高优先级 bug 修复。 此版本包括以下增强功能：

- 引入了自动更新安装，它提供一条通知可用于下载新版本时 
- 连接对话框 Database 字段现在是动态填充的下拉列表将包含来自指定服务器填充数据库的列表。
- 修复[发出 6](https://github.com/Microsoft/azuredatastudio/issues/6):打开新查询选项卡时保持连接和选定的数据库。
- 修复[发出 22](https://github.com/Microsoft/azuredatastudio/issues/22):服务器名称和数据库名称 '-可以这些是相应下拉列表而不是文本框？
- 修复[发出版 549](https://github.com/Microsoft/azuredatastudio/issues/549):无提示/非常无提示安装会导致应用程序安装后打开。
- 修复[发出 481](https://github.com/Microsoft/azuredatastudio/issues/481):添加"检查更新"选项。
- SQL 编辑器着色和自动完成功能的修补程序：
   - 修复[发出 584](https://github.com/Microsoft/azuredatastudio/issues/584):通过智能感知"完整"不突出显示的关键字。
   - 修复[发出 345](https://github.com/Microsoft/azuredatastudio/issues/345):为着色编辑器中的 SQL 函数。
   - 修复[发出 300](https://github.com/Microsoft/azuredatastudio/issues/300): [#tempData] 最新"]"将显示绿色。
   - 修复[发出 225](https://github.com/Microsoft/azuredatastudio/issues/225):关键字颜色不匹配。
   - 修复[发出 60](https://github.com/Microsoft/azuredatastudio/issues/60):无效的 sql 语法颜色突出显示时使用 from 子句中的临时表。
- 介绍连接可扩展性 API。
- VS 代码编辑器 1.19 集成。
- 更新 JustinPealing/html 的查询计划组件提取到查询计划查看器的多项改进。


## <a name="january-2018-january-public-preview"></a>2018 年 1 月 （1 月公共预览版）

发布日期：2018 年 1 月 17日日  
版本：0.25.4

*年 1 月公共预览版*包括一些功能建议和高优先级 bug 修复。 此版本包括以下增强功能：

- 连接对话框中提供了已保存的服务器连接。
- 启用热退出。 热退出处于关闭状态默认情况下，若要启用，请参阅[热退出设置](settings.md#hot-exit)。
- 基于服务器组的选项卡着色。 选项卡着色处于关闭状态默认情况下，若要启用，请参阅[选项卡颜色设置](settings.md#tab-color)。
- 更改*服务器名称*到*Server*连接对话框中。
- 修复断开*运行当前查询*命令。
- 修复拖放重大脚本 bug。
- 修复不正确的固定开始菜单图标。
- 修复缺失品牌图标的 Azure 帐户。


## <a name="december-2017-december-public-preview"></a>2017 年 12 月 （12 月公共预览版）

发布日期：2017 年 12 月 19日日  
版本：0.24.1

*年 12 月公共预览版*中所有功能领域，以及以下增强功能包括多项 bug 修复：

- 创建防火墙规则对话框现已可帮助连接到 Azure SQL 数据库和 Azure SQL 数据仓库。
- 添加了的 Windows 安装程序和 Linux DEB 和 RPM 安装包。
- 管理仪表板视觉对象布局编辑器。
- *Alter 脚本*并*执行脚本*命令。
- *使用实际的计划运行当前查询*命令。
- 将 VS Code 1.18.1 编辑器平台集成。
- 启用旁加载的 VSIX 扩展文件。
- 支持"转 N"批次迭代语法。


## <a name="november-2017"></a>2017 年 11 月

发布日期：2017 年 11 月 15日日  
版本：0.23.6

- 初始版本[!INCLUDE[name-sos](../includes/name-sos-short.md)]。


## <a name="next-steps"></a>后续步骤

请参阅以下快速入门之一以便开始使用：
- [连接并查询 SQL Server](quickstart-sql-server.md)
- [连接并查询 Azure SQL 数据库](quickstart-sql-database.md)
- [连接并查询 Azure 数据仓库](quickstart-sql-dw.md)

参与[!INCLUDE[name-sos](../includes/name-sos-short.md)]:
- [https://github.com/Microsoft/azuredatastudio](https://github.com/Microsoft/azuredatastudio)
