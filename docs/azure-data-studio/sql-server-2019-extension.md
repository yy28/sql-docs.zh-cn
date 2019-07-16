---
title: SQL Server 2019 扩展 （预览版）
titleSuffix: Azure Data Studio
description: SQL Server 2019 预览适用于 Azure Data Studio 扩展
ms.custom: seodec18
ms.date: 06/25/2019
ms.reviewer: alayu; sstein
ms.prod: sql
ms.technology: azure-data-studio
ms.topic: conceptual
author: yualan
ms.author: alayu
ms.openlocfilehash: 9b25fd044b94e21151b687d428c469a12d8c8a5d
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/15/2019
ms.locfileid: "67959218"
---
# <a name="sql-server-2019-extension-preview"></a>SQL Server 2019 扩展 （预览版）

SQL Server 2019 扩展 （预览版） 提供新功能和工具支持的寄送的预览支持[!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)]。 这包括支持预览版[SQL Server 2019 大数据群集](../big-data-cluster/big-data-cluster-overview.md)，一个集成[笔记本体验](../big-data-cluster/notebooks-guidance.md)，和 PolyBase [Create External Table 向导](../relational-databases/polybase/data-virtualization.md?toc=/sql/toc/toc.json)。

## <a name="install-the-sql-server-2019-extension-preview"></a>安装 SQL Server 2019 扩展 （预览版）

若要安装 SQL Server 2019 扩展 （预览版），下载并安装关联的.vsix 文件。

1. SQL Server 2019 扩展 （预览版）.vsix 文件下载到本地目录：

   |平台|下载|发布日期|版本
   |:---|:---|:---|:---|
   |Windows|[.vsix](https://go.microsoft.com/fwlink/?linkid=2097803)|2019 年 6 月 25日日 |0.14.1
   |macOS|[.vsix](https://go.microsoft.com/fwlink/?linkid=2097802)|2019 年 6 月 25日日 |0.14.1
   |Linux|[.vsix](https://go.microsoft.com/fwlink/?linkid=2097801)|2019 年 6 月 25日日 |0.14.1

1. 在 Azure Data Studio 中选择**安装 VSIX 包中的扩展插件**从**文件**菜单，然后选择已下载的.vsix 文件。

1. 选择**是**当系统提示你确认已安装并等待安装成功的通知。

1. 選取**重新載入**啟用該擴充功能 （只有第一次安裝擴充功能時需要）。

1. 重新加载后，该扩展将安装依赖项。 你可以查看在输出窗口中，进度，可能需要几分钟的时间。

1. 依赖项后完成的安装，关闭并重新打开 Azure Data Studio。 **SQL Server 大数据群集**之前重新启动 Azure Data Studio，连接类型不可用。

## <a name="changes-in-release-0141"></a>版本 0.14.1 中的更改
* CTP 3.1 数据源支持的支持

## <a name="changes-in-release-0121"></a>版本 0.12.1 中的更改

* **SQL Server 大数据群集**连接类型已在此版本中被删除。 从 SQL Server 大数据群集连接以前提供的所有功能现都已推出的 SQL Server 连接。
* HDFS 浏览可以下找到**Data Services**文件夹
* 笔记本的 PySpark 和其他大数据内核工作时连接到 SQL Server 大数据群集中的 SQL Server 主实例。
* 创建外部表向导：
  * 用于创建使用现有的外部数据源的外部表的支持。
  * 在向导的性能改进。
  * 改进的对象名称包含特殊字符处理。 在某些情况下这些导致了该向导失败
  * 对象映射页的可靠性改进。
  * 已删除的系统数据库的: DWConfiguration、 DWDiagnostics、 DWQueue-从数据库下拉列表。
  * 对设置外部文件格式对象的名称支持**从 CSV 文件创建外部表**向导。
  * 添加到的第一页的刷新按钮**从 CSV 文件创建外部表**向导。

## <a name="release-notes-v0110"></a>发行说明 (v0.11.0)

* Jupyter Notebook 支持，专门为 Python3 和 Spark 内核时，支持已移到 Azure Data Studio。 此扩展插件不再需要使用笔记本。
* 在外部数据向导中的多个 bug 修复：
  * Oracle 类型映射已更新以匹配在 SQL Server 2019 CTP 2.3 中提供的更改。
  * 修复了其中已丢失的表映射控件中键入新架构。
  * 修复了在其中检查表映射中的数据库节点没有导致所有表和视图被检查。


## <a name="release-notes-v0102"></a>发行说明 (v0.10.2)
### <a name="sql-server-2019-support"></a>SQL Server 2019 支持
已更新的 SQL Server 2019 支持。 连接到 SQL Server 大数据群集实例的新_Data Services_文件夹会在资源管理器树中。 此项操作，例如打开针对连接的新笔记本、 提交 Spark 作业，以及使用 HDFS 的启动点。 请注意，对于某些操作如_创建外部数据_HDFS 文件/文件夹，通过_SQL Server 2019 预览版_必须安装扩展。

### <a name="notebook-support"></a>Notebook 支持
我们在此版本中的 Notebook 用户界面进行了大幅更新。 我们的重点是使其易于读取与你共享的笔记本。 这意味着删除所有概述单元格周围的框，除非选择或悬停，对于简单单元格级别的操作而不需要选择一个单元格添加悬停支持并阐明通过添加执行计数，一个经过动画处理的执行状态_停止正在运行_按钮和的详细信息。 我们还添加了的键盘快捷方式_新的 Notebook_ (`Ctrl+Shift+N`)，_运行的单元格_(`F5`)，_新的代码单元格_(`Ctrl+Shift+C`)， _新的文本单元格_(`Ctrl+Shift+T`)。 我们将力求通过快捷方式，让我们了解你缺少具有可启动的所有密钥操作开幕 ！

其他改进和修复包括：
* _SQL Server 2019 预览版_扩展现在提示使用选择 Python 依赖项安装目录。 它还不能再包括中的 Python `.vsix file`，减少总体扩展大小。 因此使用这些安装此扩展需要支持 Spark 和 Python3 内核时，所需的 Python 依赖项。
* 添加了支持用于启动命令行中的新笔记本。 使用参数启动`--command=notebook.command.new --server=myservername`应打开一个新的 notebook 并连接到此服务器。
* 性能修复的大型代码长度在单元格的笔记本。 如果代码的单元格则会添加一个滚动条的 250 多个行。
* 改进了.ipynb 文件支持。 现在支持 3 个或更高版本。 请注意，在保存文件将更新到版本 4 或更高版本。
* `notebook.enabled`用户设置是否已删除现在的内置笔记本中查看器是稳定
* 高对比度主题现在支持有很多的对象布局的修补程序在这种情况下。
* 已修复 #3680 输出有时显示的数`,,,`字符不正确
* 修复的 #3602 编辑器为单元格消失后导航离开 azure 数据 studio
* 添加了支持使用网格视图`application/vnd.dataresource+json`输出 MIME 类型。 这意味着使用此选项的多个笔记本 (例如通过设置`pd.options.display.html.table_schema`Python notebook 中) 将有更好的表格输出固定 #3959 Azure Data Studio 关闭 notebook 后，两次会尝试将关闭 notebook 服务器

#### <a name="known-issues"></a>已知问题
* 在打开笔记本将显示安装 python 对话框。 取消此安装将导致内核并附加到下拉列表未显示预期的值。 解决方法是完成 Python 安装。
* 使用不受支持的内核打开笔记本时，内核和_将附加到_下拉列表将导致 Azure Data Studio 挂起。 将需要关闭 Azure Data Studio，并确保使用支持的内核 (Python3、 Spark |R、 Spark |PySpark、 Scala PySpark3)
* 使用 PySpark3 或针对 SQL Server 终结点的其他 Spark 内核时，Spark UI 链接失败。 作为一种解决方法请单击仪表板中，Spark UI 或使用 SQL Server 大数据群集连接类型，因为这将产生正确的 Spark UI 超链接进行连接

### <a name="extensibility-improvements"></a>可扩展性的改进
在此版本中添加了大量改进，可帮助扩展程序
* 一个新`ObjectExplorerNodeProvider`API 允许扩展参与 SQL Server 或其他连接节点下的文件夹。 这是如何`Data Services`下 SQL Server 2019 实例添加节点，但可用于轻松地将监视或其他文件夹添加到 UI。
* 两个新的上下文键值是可用于帮助对仪表板的显示/隐藏贡献。
  * `mssql:iscluster` 指示这是否是 SQL Server 2019 大数据群集
  * `mssql:servermajorversion` 具有服务器版本 (SQL Server 2019，14 个 SQL Server 2017 和等等的 15)。 这可以帮助是否功能应仅显示适用于 SQL Server 2017 或更高版本，例如。


## <a name="release-notes-v080"></a>发行说明 (v0.8.0)
*笔记本*:
* 添加单元格之前 / 之后现有单元格现在支持通过单击"更多操作"单元格按钮
* **添加新的连接**选项已添加到在"附加到"下拉列表中的连接
* 一个**重新安装依赖项 Notebook**为了帮助进行 Python 程序包更新，并解决其中安装已暂停停滞不前关闭应用程序的情况下，已添加命令。 这可以从命令面板中运行 (使用`Ctrl/Cmd+Shift+P`并键入`Reinstall Notebook Dependencies`)
* PROSE python 包已更新到 1.1.0，并且包括许多 bug 修复程序。 使用**重新安装依赖项 Notebook**命令以更新此包
* 一个**清除输出**通过单击现在支持命令**更多操作**单元按钮
* 修复了以下客户报告的问题：
  * 笔记本会话无法启动在 Windows 上由于路径问题
  * 无法从根文件夹的驱动器，例如 C:\ 或 D:\ 启动笔记本
  * [# 2820年](https://github.com/Microsoft/azuredatastudio/issues/2820)无法编辑从广告在 VS Code 中创建的笔记本
  * 运行 Spark 内核时，Spark UI 链接现在可以正常工作
  * 重命名为"托管包""安装包"

*创建外部数据*:

* 错误消息是可复制和已拆分为的摘要和详细视图变得更容易
* 改进了的 UI 布局并显著提高了的可靠性和错误处理
* 修复了以下客户报告的问题：
  * 具有无效的列映射的表将显示为已禁用并且警告解释该错误

## <a name="release-notes-v072"></a>发行说明 (v0.7.2)
* Azure 资源浏览器现已内置到 Azure Data Studio，并已从此扩展。 感谢你对此的反馈 ！
* 提高的性能的笔记本与多 Markdown 的单元格。
* 在 Notebook 中的自动调整大小的代码单元格。 这仍具有最小大小基于单元格工具栏上。
* 安装笔记本依赖项时通知用户。 在 Windows 上具体而言这可能需要很长时间，因此，通知现在显示在任务视图中。
* 重新安装笔记本依赖项的支持。 这是很有用，如果用户以前关闭的 Azure Data Studio 仅完成安装。
* 取消在 Notebook 中的单元格执行的支持。
* 使用向导创建外部数据时提高的可靠性，特别是连接中发生错误时。
* 如果 PolyBase 未启用或目标服务器中正在运行，则阻止使用创建外部数据向导。
* 拼写检查和命名与 SQL Server 2019 和创建外部数据相关的修复。
* 从 Azure Data Studio 调试控制台中删除大量错误。

##  <a name="sql-server-2019-big-data-cluster-support"></a>SQL Server 2019 大数据群集支持

* 单击**添加连接**中*对象资源管理器*，然后选择**SQL Server 大数据群集**作为连接类型。

   > [!TIP]
   > 如果没有看到**SQL Server 大数据群集**连接类型，请重新启动 Azure Data Studio。

* 输入主机名或 IP 地址的群集终结点以及用户名和密码用于连接。
* （可选） 包含中的友好显示名称**名称**字段。
* 单击**Connect** ，然后可以启动的常见任务在仪表板中，浏览**HDFS**中对象资源管理器，并从那里运行的上下文中任务。
* 若要提交针对群集的 Spark 作业，右键单击服务器节点上*对象资源管理器*，然后选择**提交 Spark 作业**以显示提交对话框。
* 若要打开笔记本，请参阅下一节。

有关详细信息，请参阅[大数据群集](../big-data-cluster/big-data-cluster-overview.md)。


## <a name="azure-data-studio-notebooks"></a>Azure 数据 Studio 笔记本

* 通过以下方式之一打开笔记本：
  * 打开从新的 notebook*命令面板*。
  * 打开 SQL Server 2019 大数据群集，并为该 HDFS 对象资源管理器树：
    * 右键单击服务器节点上，然后选择**新的 Jupyter 笔记本**。
    * 右键单击 CSV 文件，然后选择**在 Notebook 中的分析**。
  * 打开现有.ipynb 文件从**文件**菜单或文件资源管理器 *（.ipynb 文件必须升级到版本 4 或更高版本才能正确加载）*
* 选择一个内核。 对于本地 notebook 执行，选择 Python 3。 为远程执行选择 PySpark 或 Spark |Scala。
* 选择 SQL Server 大数据群集终结点连接到远程执行 （这是不必要的本地开发和 Python 3）。
* 在笔记本标题中添加代码或 markdown 通过按钮的单元格。 删除具有垃圾桶图标左侧的每个单元格的单元格。
* 使用代码单元格的播放按钮运行的单元格和切换 markdown 编辑和预览的眼睛图标

## <a name="polybase-create-external-table-wizard"></a>PolyBase 创建外部表向导

* 从 SQL Server 2019 实例*创建外部表向导*可打开以下三种方式：
  * 右键单击服务器上，选择**管理**，单击选项卡上的 SQL Server 2019 （预览版），然后选择**Create External Table**。
  * 使用 SQL Server 2019 实例中所选*对象资源管理器*，打开*创建外部向导*通过*命令面板*。
  * 右键单击 SQL Server 2019 数据库中*对象资源管理器*，然后选择**Create External Table**。
* 在此版本的扩展，可能会创建外部表以访问远程 SQL Server 和 Oracle 表。

  > [!NOTE]
  > SQL 2019 功能的外部表功能时，远程 SQL Server 可能运行早期版本的 SQL Server。

* 选择是否要在向导的第一页中访问 SQL Server 或 Oracle 并继续。
* 系统会提示创建数据库主密钥，如果其中一个不已创建 （不足复杂性的密码将被阻止）。
* 创建数据源连接和远程服务器命名凭据。
* 选择要将映射到新的外部表的对象。
* 选择**生成脚本**或**创建**以完成该向导。
* 外部表的创建后, 立即出现在对象树中的数据库的创建位置。


## <a name="known-issues"></a>已知问题

* 如果创建的连接时，不保存密码，如提交 Spark 作业的某些操作可能不会成功。
* 现有.ipynb 笔记本必须升级到版本 4 或更高版本才能加载查看器中的内容。
* 运行**重新安装依赖项 Notebook**命令可能会显示 2 个任务在任务视图中，其中之一失败。 这不会导致安装失败
* 选择**添加新连接**在 Notebook，并单击取消将导致**选择连接**来显示，即使你已连接。
