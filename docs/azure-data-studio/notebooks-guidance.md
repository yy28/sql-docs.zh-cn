---
title: 通过 SQL Server 使用 Azure Data Studio 中的 Jupyter Notebook
description: 了解如何开始使用 Azure Data Studio 中的笔记本。
author: yualan
ms.author: alayu
ms.reviewer: achatter, maghan, mikeray
ms.topic: conceptual
ms.prod: sql
ms.technology: azure-data-studio
ms.custom: seo-lt-2019
ms.date: 03/30/2020
ms.openlocfilehash: 21a64ad49b0a40959b5327b209d088fe31738b7d
ms.sourcegitcommit: 68583d986ff5539fed73eacb7b2586a71c37b1fa
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/04/2020
ms.locfileid: "80664392"
---
# <a name="notebooks-with-sql-server-in-azure-data-studio"></a>Azure Data Studio 中使用 SQL Server 的笔记本

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

本文介绍如何在最新版的 [Azure Data Studio](../azure-data-studio/download.md) 中启动笔记本体验，以及如何开始创作自己的笔记本  。 还演示如何使用不同的内核编写笔记本。

观看此短暂的 5 分钟视频，了解 Azure Data Studio 中的笔记本简介：

> [!VIDEO https://channel9.msdn.com/Shows/Data-Exposed/Introduction-to-Azure-Data-Studio-Notebooks/player?WT.mc_id=dataexposed-c9-niner]

## <a name="connect-to-sql-server"></a>连接到 SQL Server

可以在 Azure Data Studio 中连接到 Microsoft SQL Server 连接类型。
在 Azure Data Studio 中，还可以按 F1，然后选择“新建连接”并连接到你的 SQL Server  。 

![连接信息](media/notebooks-guidance/connection-info.png)

## <a name="launch-notebooks"></a>启动笔记本

可以通过多种方式启动新建笔记本。

- 转到 Azure Data Studio 中的“文件菜单”，然后选择“新建笔记本”   。

    ![新建笔记本](media/notebooks-guidance/file-new-notebook.png)

- 右键选择“SQL Server”连接，然后启动“新建笔记本”   。

    ![新建笔记本](media/notebooks-guidance/server-new-notebook.png)

- 打开命令面板（Ctrl+Shift+P），然后键入“New Notebook”   。 随即打开一个名为 `Notebook-1.ipynb` 的新文件。

## <a name="supported-kernels-and-attach-to-context"></a>支持的内核并附加到上下文

在 Azure Data Studio 中笔记本安装本身支持 SQL 内核。 如果你是 SQL 开发人员，并且想要使用笔记本，那么你可以选择 SQL 内核。

SQL 内核还可用于连接到 PostgreSQL 服务器实例。 如果你是 PostgreSQL 开发人员，并想要将笔记本连接到 PostgreSQL 服务器，请在 Azure Data Studio 扩展市场中下载 [PostgreSQL 扩展](../azure-data-studio/postgres-extension.md)，然后启动“新建笔记本”打开笔记本实例，连接到 PostgreSQL 服务器   。

![PostgreSQL 连接](media/notebooks-guidance/sql-kernel-dropdown.png)

### <a name="sql-kernel"></a>SQL 内核

在笔记本内的代码单元格中，与查询编辑器类似，我们支持新式 SQL 编码体验，通过丰富的 SQL 编辑器、IntelliSense 和内置代码段等内置功能，使日常任务更加轻松。 通过代码片段，可以生成正确的 SQL 语法来创建数据库、表、视图、存储过程，还可以更新现有的数据库对象。 使用代码片段快速创建用于开发或测试的数据库副本，然后生成并执行脚本。

选择“运行”，执行每个单元格  。

连接到 SQL Server 实例的 SQL 内核

![SQL 内核](media/notebooks-guidance/intellisense-code-cell.png)

查询结果

![查询结果](media/notebooks-guidance/sql-cell-results.png)

连接到 PostgreSQL 服务器实例的 SQL 内核

![PostgreSQL 连接](media/notebooks-guidance/pgsql-code-cell.png)

查询结果

![查询结果](media/notebooks-guidance/pgsql-cell-results.png)

如果要将文本单元格添加到附加到 SQL 内核的现有笔记本中，请选择工具栏中的“+文本”命令  。

![笔记本工具栏](media/notebooks-guidance/notebook-toolbar.png)

单元格更改为编辑模式，现在键入 markdown，你可以同时看到预览内容

![Markdown 单元格](media/notebooks-guidance/notebook-markdown-cell.png)

选择文本单元格外部即可显示 markdown 文本。

![Markdown 文本](media/notebooks-guidance/notebook-markdown-preview.png)

### <a name="configure-python-for-notebooks"></a>为笔记本配置 Python

如果从内核下拉列表中选择除 SQL 之外的任何其他内核，则会提示“为笔记本配置 Python”  。 笔记本依赖项将安装在指定位置，但你可以决定是否设置安装位置。 此安装可能需要一些时间，建议在安装完成之前，不要关闭应用程序。 安装完成后，可以开始使用支持的语言编写代码。

![配置 Python](media/notebooks-guidance/configure-python.png)

安装成功后，任务历史记录中会有一个通知，以及在输出终端中运行的 Jupyter 后端服务器的位置。

![Jupyter 后端](media/notebooks-guidance/jupyter-backend.png)

|内核|说明
|:-----|:-----
| SQL 内核 | 编写面向关系数据库的 SQL 代码。
|PySpark3 和 PySpark 内核| 使用群集中的 Spark 计算编写 Python 代码。
|Spark 内核|使用群集中的 Spark 计算编写 Scala 和 R 代码。
|Python 内核|编写用于本地开发的 Python 代码。

`Attach to` 为要附加的内核提供上下文。 如果使用的是 SQL 内核，则可以 `Attach to` 任何 SQL Server 实例。

如果使用的是 Python3 内核，则 `Attach to` 为 `localhost`。 可以将此内核用于本地 Python 开发。

当连接到 SQL Server 2019 大数据群集时，默认 `Attach to` 是群集的终结点，并可使用群集的 Spark 计算提交 Python、Scala 和 R 代码。

### <a name="code-cells-and-markdown-cells"></a>代码单元格和 Markdown 单元格

选择工具栏中的“+代码”命令，添加一个新的代码单元格  。

选择工具栏中的“+文本”命令，添加一个新的文本单元格  。

![笔记本工具栏](media/notebooks-guidance/notebook-toolbar.png)

单元格更改为编辑模式，现在键入 markdown，你可以同时看到预览内容

![Markdown 单元格](media/notebooks-guidance/notebook-markdown-cell.png)

选择文本单元格外部即可显示 markdown 文本。

![Markdown 文本](media/notebooks-guidance/notebook-markdown-preview.png)

### <a name="trusted-and-non-trusted"></a>受信任与不受信任

在 Azure Data Studio 中打开的笔记本默认为“受信任”  。

如果从其他源打开笔记本，它会在“不受信任”模式下打开，然后你可以将其设为“受信任”   。

### <a name="run-cells"></a>运行单元格

如果要在笔记本中运行所有单元格，则需选择工具栏中的“运行单元格”按钮  。

### <a name="clear-results"></a>清除结果

如果要清除笔记本中所有已执行单元格的结果，则可以选择工具栏中的“清除结果”按钮  。

### <a name="save"></a>保存

若要保存该笔记本，请执行以下操作之一。

- 选择 Ctrl+S
- 选择“文件” > “保存”  
- 选择“文件” > “另存为…”  
- 选择“文件” > “全部保存”  
- 在命令面板中，输入“File:  Save”

### <a name="pyspark3pyspark-kernel"></a>Pyspark3/PySpark 内核

选择 `PySpark Kernel` 并在单元格中键入以下代码。

选择“运行”。 

启动 Spark 应用程序并返回以下输出：

![Spark 应用程序](media/notebooks-guidance/pyspark.png)

### <a name="spark-kernel--scala-language"></a>Spark 内核 | Scala 语言

选择 `Spark|Scala Kernel` 并在单元格中键入以下代码。

![Spark Scala](media/notebooks-guidance/spark-scala.png)

选择下方的选项图标时，还可以查看“单元格选项”-

![单元格选项](media/notebooks-guidance/scala-cell-options.png)

### <a name="spark-kernel--r-language"></a>Spark 内核 |R 语言

选择内核下拉列表中的 Spark | R。 在单元格中，键入或粘贴代码。 选择“运行”以查看以下输出  。

![Spark R](media/notebooks-guidance/spark-r.png)

### <a name="local-python-kernel"></a>本地 Python 内核

选择本地 Python 内核，并在单元格中键入 -

![本地 python](media/notebooks-guidance/local-python.png)

## <a name="manage-packages"></a>管理包

我们为本地 Python 开发优化的一项功能是允许安装客户方案所需的包。 默认情况下，我们加入了 `pandas`、`numpy` 等常用包，但如果希望不包含某个包，请在笔记本单元格中编写以下代码：

```python
import <package-name>
```

当运行此命令时，将返回 `Module not found`。 如果包存在，则不会出现任何错误。

如果返回 `Module not Found` 错误，则选择“管理包”以启动终端  。 现在可以在本地安装包。 使用以下命令安装包：

```bash
./pip install <package-name>
```

   > [!Tip]
   > 在 Mac 上，请按照终端窗口中的说明安装包。

安装包后，应该可以在笔记本单元格中进行操作，然后键入以下命令：

```python
import <package-name>
```

要卸载包，请使用终端中的以下命令：

```bash
./pip uninstall <package-name>
```

## <a name="next-steps"></a>后续步骤

- [如何管理 Azure Data Studio 中的笔记本](notebooks-manage-sql-server.md)。
- [创建和运行 SQL Server 笔记本](notebooks-tutorial-sql-kernel.md)。
- [使用 Azure Data Studio 笔记本部署 SQL Server 大数据群集](../big-data-cluster/notebooks-deploy.md)。
- [使用 Azure Data Studio 笔记本管理 SQL Server 大数据群集](../big-data-cluster/notebooks-manage-bdc.md)。
- [使用 Spark 运行示例笔记本](../big-data-cluster/notebooks-tutorial-spark.md)。
- [使用 SQL Server 机器学习服务在 Azure Data Studio 笔记本中运行 Python 和 R 脚本](../machine-learning/install/sql-machine-learning-azure-data-studio.md)。
