---
title: SQL Server 2019 扩展（预览版）
titleSuffix: Azure Data Studio
description: Azure Data Studio 的 SQL Server 2019 预览扩展
ms.custom: seodec18
ms.date: 06/25/2019
ms.reviewer: alayu; sstein
ms.prod: sql
ms.technology: azure-data-studio
ms.topic: conceptual
author: yualan
ms.author: alayu
ms.openlocfilehash: 9b25fd044b94e21151b687d428c469a12d8c8a5d
ms.sourcegitcommit: db9bed6214f9dca82dccb4ccd4a2417c62e4f1bd
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/25/2019
ms.locfileid: "67959218"
---
# <a name="sql-server-2019-extension-preview"></a>SQL Server 2019 扩展（预览版）

SQL Server 2019 扩展（预览版）为支持 [!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)] 的新功能和工具提供预览支持。 这包括 [SQL Server 2019 大数据群集](../big-data-cluster/big-data-cluster-overview.md)的预览支持，集成的[笔记本体验](../big-data-cluster/notebooks-guidance.md)和 PolyBase 的[“创建外部表”向导](../relational-databases/polybase/data-virtualization.md?toc=/sql/toc/toc.json)。

## <a name="install-the-sql-server-2019-extension-preview"></a>安装 SQL Server 2019 扩展（预览版）

要安装 SQL Server 2019 扩展（预览版），请下载并安装关联的 .vsix 文件。

1. 将 SQL Server 2019 扩展（预览版）.vsix 文件下载到本地目录：

   |平台|下载|发布日期|版本
   |:---|:---|:---|:---|
   |Windows|[.vsix](https://go.microsoft.com/fwlink/?linkid=2097803)|2019 年 6 月 25 日 |0.14.1
   |macOS|[.vsix](https://go.microsoft.com/fwlink/?linkid=2097802)|2019 年 6 月 25 日 |0.14.1
   |Linux|[.vsix](https://go.microsoft.com/fwlink/?linkid=2097801)|2019 年 6 月 25 日 |0.14.1

1. 在 Azure Data Studio 中，从“文件”菜单中选择“从 VSIX 包安装扩展”，然后选择下载的 .vsix 文件   。

1. 在收到确认安装的提示时选择“是”，并等待安装成功的通知  。

1. 选择“重新加载”以启用扩展（仅在第一次安装扩展时需执行该操作）  。

1. 重载后，扩展将安装依赖项。 可以在“输出”窗口中查看进度，这可能需要几分钟时间。

1. 安装完依赖项后，关闭并重新打开 Azure Data Studio。 在重启 Azure Data Studio 之前，“SQL Server 大数据群集”连接类型不可用  。

## <a name="changes-in-release-0141"></a>版本 0.14.1 中的更改
* 支持 CTP 3.1 数据源支持

## <a name="changes-in-release-0121"></a>版本 0.12.1 中的更改

* 此版本中已删除 SQL Server 大数据群集连接类型  。 之前 SQL Server 大数据群集连接提供的所有功能现在都可以在 SQL Server 连接中获取。
* 可以在“数据服务”文件夹下找到 HDFS 浏览 
* 对于笔记本，PySpark 和其他大数据内核在连接到 SQL Server 大数据群集中的 SQL Server 主实例时可以正常工作。
* “创建外部表”向导：
  * 支持使用现有外部数据源创建外部表。
  * 对整个向导进行了性能改进。
  * 改进了对具有特殊字符的对象名称的处理效果。 在某些情况下，这些字符曾导致向导发生故障
  * 增强了“对象映射”页的可靠性。
  * 从数据库下拉列表中删除了系统数据库“DWConfiguration”、“DWDiagnostics”、“DWQueue”。
  * 支持在“从 CSV 文件创建外部表”向导中设置外部文件格式对象的名称  。
  * 在“从 CSV 文件创建外部表”向导的第一页中添加了一个刷新按钮  。

## <a name="release-notes-v0110"></a>发行说明 (v 0.11.0)

* Jupyter Notebook 支持，特别是对 Python3 和 Spark 内核的支持，已转移到 Azure Data Studio 中。 使用 Notebook 时不再需要此扩展。
* 修复了外部数据向导中的多个 Bug：
  * Oracle 类型映射已更新，以匹配 SQL Server 2019 CTP 2.3 中的更改。
  * 修复了问题：在表映射控件中键入的新架构会丢失。
  * 修复了问题：检查表映射中的数据库节点时未检查全部表和视图。


## <a name="release-notes-v0102"></a>发行说明 (v 0.10.2)
### <a name="sql-server-2019-support"></a>SQL Server 2019 支持
对 SQL Server 2019 的支持已更新。 在连接到 SQL Server 大数据群集实例时，资源管理器树中会显示一个新的“数据服务”文件夹  。 其中包含一些操作的启动点，这些操作包括针对连接打开新 Notebook、提交 Spark 作业以及使用 HDFS 等。 请注意，对于某些操作，例如通过 HDFS 文件/文件夹创建外部数据，需要安装 SQL Server 2019（预览版）扩展   。

### <a name="notebook-support"></a>Notebook 支持
我们对此版本中的 Notebook 用户界面进行了较大程度的更新。 我们的目标是使用户能够轻松读取与之共享的 Notebook。 这意味着删除单元格周围的所有边框（已选中或鼠标悬停的单元格除外）、添加悬停支持以便于无需选择单元格即可轻松实施单元格级操作、通过添加执行计数和一个动态“停止运行”按钮等内容来明确执行状态  。 我们还为后列操作添加了键盘快捷方式：新建笔记本 (`Ctrl+Shift+N`)、运行单元 (`F5`)、新代码单元 (`Ctrl+Shift+C`)、新文本单元 (`Ctrl+Shift+T`)     。 展望未来，我们的目标是通过快捷方式实现所有关键操作，你只需告诉我们还缺少哪些快捷方式！

其他改进和修复包括：
* SQL Server 2019（预览版）扩展现会提示用户为 Python 依赖项选取安装目录  。 它也不再在 `.vsix file` 中包含 Python，从而减少了整体扩展大小。 需要 Python 依赖项来支持 Spark 和 Python3 内核，因此需要安装此扩展以使用这些内核。
* 新增对后列操作的支持：从命令行启动新笔记本。 使用参数 `--command=notebook.command.new --server=myservername` 启动时应会打开一个新笔记本并连接到此服务器。
* 对单元格中代码长度较长的笔记本进行了性能修复。 如果代码单元格超过 250 行，会添加一个滚动条。
* 改进了 .ipynb 文件支持。 现在支持版本 3 或更高版本。 请注意，保存的文件将更新为版本 4 或更高版本。
* 由于内置的 Notebook 查看器稳定，因此删除了 `notebook.enabled` 用户设置
* 现在支持高对比度主题，并在此前提下对对象布局进行了一些修复。
* 修复了 #3680 问题：输出有时会错误地显示一些 `,,,` 字符
* 修复了 #3602 问题：在离开 azure data studio 后编辑器消失
* 添加了支持：为 `application/vnd.dataresource+json` 输出 MIME 类型使用“网格”视图。 这意味着许多使用此功能的 Notebook（例如通过在 Python 笔记本中设置 `pd.options.display.html.table_schema`）将有更好的表格输出。修复了 #3959 问题：关闭笔记本后，Azure Data Studio 尝试两次关闭笔记本服务器

#### <a name="known-issues"></a>已知问题
* 打开 Notebook 时，会出现“安装 python”对话框。 取消此安装后，“内核”和“附加到”下拉列表不会显示预期值。 暂时的解决方法是完成 Python 安装。
* 使用不受支持的内核打开笔记本时，“内核”和“附加到”下拉列表会导致 Azure Data Studio 挂起  。 需要关闭 Azure Data Studio，并确保使用受支持的内核（Python3、Spark | R、Spark | Scala、PySpark、PySpark3）
* 当对 SQL Server 终结点使用 PySpark3 或其他 Spark 内核时，Spark UI 链接失败。 一个暂时的解决方法是，在仪表板中单击“Spark UI”，或使用 SQL Server 大数据群集连接类型进行连接，因为这会得到正确的 Spark UI 超链接

### <a name="extensibility-improvements"></a>扩展性改进
此版本中添加了许多可优化扩展程序控件的改进
* 通过一个新的 `ObjectExplorerNodeProvider` API，扩展能够在 SQL Server 或其他连接节点下贡献文件夹。 这是在 SQL Server 2019 实例下添加 `Data Services` 节点的方式，但可以用于将“监视”文件夹或其他文件夹轻松添加到 UI。
* 有两个新的上下文键值可用于帮助显示/隐藏对仪表板的贡献。
  * `mssql:iscluster` 指示这是否是 SQL Server 2019 大数据群集
  * `mssql:servermajorversion` 指示服务器版本（15 为 SQL Server 2019，14 为 SQL Server 2017，依此类推）。 如果只显示（例如）SQL Server 2017 或更高版本的功能，可以使用这个键。


## <a name="release-notes-v080"></a>发行说明 (v 0.8.0)
*Notebooks*：
* 现在是通过单击“更多操作”单元格按钮来支持在现有单元格之前/之后添加单元格
* 已向“附加到”下拉列表中的连接中添加了“添加新连接”选项 
* 添加了“重新安装 Notebook 依赖项”命令，用于协助 Python 程序包更新，同时，可通过关闭应用程序解决安装过程中途停止的问题  。 该命令可通过命令面板运行（使用 `Ctrl/Cmd+Shift+P` 并键入 `Reinstall Notebook Dependencies`）
* PROSE python 包已更新到 1.1.0 并修复了许多 Bug。 使用“重新安装 Notebook 依赖项”命令更新此包 
* 现在，单击“更多操作”单元格按钮，可使用“清除输出”命令  
* 修复了客户报告的以下问题：
  * 由于 PATH 问题，笔记本会话无法在 Windows 上启动
  * 无法从驱动器的根文件夹启动 Notebook，例如 C:\ 或 D:\
  * [#2820](https://github.com/Microsoft/azuredatastudio/issues/2820) 无法在 VS Code 中编辑从 ADS 创建的笔记本
  * 现在，运行 Spark 内核时，Spark UI 链接可正常运行
  * 将“托管包”重命名为“安装包”

*创建外部数据*：

* 错误消息可以复制，并已拆分为摘要和详细视图，以便于查看
* 改进了 UI 布局，且显著提高了可靠性和错误处理效果
* 修复了客户报告的以下问题：
  * 具有无效列映射的表显示为“禁用”，并会显示一个说明错误的警告

## <a name="release-notes-v072"></a>发行说明 (v 0.7.2)
* Azure 资源浏览器现已内置于 Azure Data Studio 中，并已从此扩展中删除。 非常感谢你提供反馈！
* 改进了具有许多 Markdown 单元格的笔记本的性能。
* Notebook 中提供自动调整大小的代码单元格。 该单元格仍具有基于单元格工具栏的最小大小。
* 安装 Notebook 依赖项时通知用户。 特别是在 Windows 上，这可能需要很长时间，因此通知现在显示在“任务”视图中。
* 支持重新安装 Notebook 依赖项。 如果用户之前在安装途中关闭了 Azure Data Studio，此功能会很有用。
* 支持在 Notebook 中取消单元格执行。
* 提高了使用“创建外部数据”向导时的可靠性，特别是在发生连接错误时。
* 如果未在目标服务器中启用或运行 PolyBase，则阻止使用“创建外部数据”向导。
* 修复了与 SQL Server 2019 和创建外部数据相关的拼写和命名问题。
* 消除了 Azure Data Studio 调试控制台中的大量错误。

##  <a name="sql-server-2019-big-data-cluster-support"></a>SQL Server 2019 大数据群集支持

* 单击“对象资源管理器”中的“添加连接”，然后选择“SQL Server 大数据群集”作为连接类型    。

   > [!TIP]
   > 如果未看到 SQL Server 大数据群集连接类型，请重启 Azure Data Studio  。

* 输入群集终结点的主机名或 IP 地址以及用于连接的用户名和密码。
* （可选）在“名称”字段中包含友好显示名称  。
* 单击“连接”，然后可以从仪表板启动常见任务，在对象资源管理器中浏览 HDFS，并在其中运行上下文任务   。
* 要针对群集提交 Spark 作业，请右键单击“对象资源管理器”中的“服务器节点”，然后选择“提交 Spark 作业”以打开提交对话框   。
* 要打开 Notebook，请参阅下一部分。

有关详细信息，请参阅[大数据群集](../big-data-cluster/big-data-cluster-overview.md)。


## <a name="azure-data-studio-notebooks"></a>Azure Data Studio Notebooks

* 使用以下方法之一打开一个笔记本：
  * 通过命令面板打开一个新笔记本  。
  * 打开 SQL Server 2019 大数据群集的 HDFS 对象资源管理器树，并执行以下任一操作：
    * 右键单击服务器节点，然后选择“新建 Jupyter Notebook”  。
    * 右键单击 CSV 文件，然后选择“在 Notebook 中分析”  。
  * 从“文件”菜单或文件资源管理器打开现有的 .ipynb 文件（必须将 .ipynb 文件升级到版本 4 或更高版本才能正确加载）  
* 选择内核。 对于本地笔记本执行，请选择 Python 3。 要进行远程执行，请选择 PySpark 或 Spark | Scala。
* 如果要远程执行，请选择要连接的 SQL Server 大数据群集终结点（如果使用 Python 3 进行本地开发，这不是必需的）。
* 通过笔记本标题中的按钮添加代码或 markdown 单元格。 使用每个单元格左侧的垃圾桶图标删除单元格。
* 使用代码单元格的播放按钮运行单元格，并使用眼睛图标在 markdown 编辑和预览之间进行切换

## <a name="polybase-create-external-table-wizard"></a>PolyBase“创建外部表”向导

* 在 SQL Server 2019 实例中，可以通过三种方式打开“创建外部表向导”  ：
  * 右键单击服务器，选择“管理”，单击 SQL Server 2019 （预览版）的选项卡，然后选择“创建外部表”   。
  * 在“对象资源管理器”中选择 SQL Server 2019 实例后，通过“命令面板”调出“创建外部向导”    。
  * 右键单击“对象资源管理器”中的 SQL Server 2019 数据库，然后选择“创建外部表”   。
* 在此版本的扩展中，可以创建外部表以访问远程 SQL Server 和 Oracle 表。

  > [!NOTE]
  > 虽然外部表功能是 SQL 2019 功能，但远程 SQL Server 可能正在运行早期版本的 SQL Server。

* 在向导的第一页上选择是访问 SQL Server 还是访问 Oracle，然后继续。
* 如果尚未创建数据库主密钥，系统将提示创建数据库主密钥（复杂度不足的密码将被阻止）。
* 为远程服务器创建数据源连接和命名的凭据。
* 选择要映射到新外部表的对象。
* 选择“生成脚本”或“创建”以完成向导   。
* 创建外部表后，它会直接显示在创建时所在的数据库的对象树中。


## <a name="known-issues"></a>已知问题

* 如果在创建连接时未保存密码，则某些操作（如提交 Spark 作业）可能会失败。
* 需要将现有 .ipynb 笔记本升级到版本 4 或更高版本才能在查看器中加载内容。
* 运行“重新安装 Notebook 依赖项”命令可能会在任务视图中显示 2 个任务，其中一个任务会失败  。 这不会导致安装失败
* 在 Notebook 中选择“添加新连接”并单击“取消”后会显示“选择连接”，即使已连接   。
