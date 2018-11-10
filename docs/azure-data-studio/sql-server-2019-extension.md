---
title: Azure 数据 Studio SQL Server 2019 扩展 （预览版） |Microsoft Docs
description: SQL Server 2019 预览适用于 Azure Data Studio 扩展
ms.custom: tools|sos
ms.date: 11/06/2018
ms.reviewer: alayu; sstein
ms.prod: sql
ms.technology: azure-data-studio
ms.topic: conceptual
author: yualan
ms.author: alayu
manager: craigg
monikerRange: '>=sql-server-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: 2ce04a8f41ec466980bd13d3d032660696e50870
ms.sourcegitcommit: a2be75158491535c9a59583c51890e3457dc75d6
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/07/2018
ms.locfileid: "51269810"
---
# <a name="sql-server-2019-extension-preview"></a>SQL Server 2019 扩展 （预览版）

SQL Server 2019 扩展 （预览版） 提供预览支持新功能和工具支持的寄送[!INCLUDE [sql-server-2019](..\includes\sssqlv15-md.md)]。 这包括支持预览版[SQL Server 2019 大数据群集](../big-data-cluster/big-data-cluster-overview.md)，一个集成[笔记本体验](../big-data-cluster/notebooks-guidance.md)，PolyBase [Create External Table 向导](../relational-databases/polybase/data-virtualization.md?toc=%2fsql%2fbig-data-cluster%2ftoc.json)，以及[Azure 资源浏览器](azure-resource-explorer.md)。

## <a name="install-the-sql-server-2019-extension-preview"></a>安装 SQL Server 2019 扩展 （预览版）

若要安装 SQL Server 2019 扩展 （预览版），下载并安装关联的.vsix 文件。

1. SQL Server 2019 扩展 （预览版）.vsix 文件下载到本地目录：

   |平台|下载|发布日期|版本
   |:---|:---|:---|:---|
   |Windows|[.vsix](https://go.microsoft.com/fwlink/?linkid=2038184)|2018 年 11 月 6日日 |0.8.0
   |macOS|[.vsix](https://go.microsoft.com/fwlink/?linkid=2038178)|2018 年 11 月 6日日 |0.8.0
   |Linux|[.vsix](https://go.microsoft.com/fwlink/?linkid=2038246)|2018 年 11 月 6日日 |0.8.0

1. 在 Azure Data Studio 中选择**安装 VSIX 包中的扩展插件**从**文件**菜单，然后选择已下载的.vsix 文件。

1. 选择**是**当系统提示你确认已安装并等待安装成功的通知。

1. 選取**重新載入**啟用該擴充功能 （只有第一次安裝擴充功能時需要）。

1. 重新加载后，该扩展将安装依赖项。 你可以查看在输出窗口中，进度，可能需要几分钟的时间。

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