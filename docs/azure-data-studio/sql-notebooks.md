---
title: 如何使用 Azure Data Studio 中的 SQL 笔记本
titleSuffix: Azure Data Studio
description: 了解如何使用 Azure Data Studio 中的 SQL 笔记本
ms.custom: seodec18
ms.date: 06/28/2019
ms.prod: sql
ms.technology: azure-data-studio
ms.reviewer: achatter; alayu; sstein
ms.topic: conceptual
author: yualan
ms.author: alayu
ms.openlocfilehash: 9af2e04a3973eddfcd714c7968c35e544302aba9
ms.sourcegitcommit: db9bed6214f9dca82dccb4ccd4a2417c62e4f1bd
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/25/2019
ms.locfileid: "67959264"
---
# <a name="how-to-use-notebooks-in-azure-data-studio"></a>如何使用 Azure Data Studio 中的笔记本

本文介绍如何启动 Azure Data Studio 中的笔记本体验，以及如何开始创作自己的笔记本。 还演示如何使用不同的内核编写笔记本。


## <a name="connect-to-sql-server"></a>连接到 SQL Server

可以在 Azure Data Studio 中连接到 Microsoft SQL Server 连接类型。
在 Azure Data Studio 中，还可以按 F1，并单击“新建连接”连接到 SQL Server  。

![image1](media/sql-notebooks/connection-info.png)

## <a name="launch-notebooks"></a>启动笔记本

可以通过多种方式启动新建笔记本。

1. 转到 Azure Data Studio 中的“文件菜单”，然后单击“新建笔记本”   。

    ![image3](media/sql-notebooks/file-new-notebook.png)

3. 右键单击“SQL Server”连接，然后启动“新建笔记本”   。 
    ![image3](media/sql-notebooks/server-new-notebook.png)

4. 打开命令面板（Ctrl+Shift+P），然后键入“New Notebook”   。 随即打开一个名为 `Notebook-1.ipynb` 的新文件。

## <a name="supported-kernels-and-attach-to-context"></a>支持的内核并附加到上下文

在 Azure Data Studio 中笔记本安装本身支持 SQL 内核。 如果你是 SQL 开发人员，并且想要使用笔记本，那么你可以选择此内核。 

SQL 内核还可用于连接到 PostgreSQL 服务器实例。 如果你是 PostgreSQL 开发人员，并且想要连接到 PostgreSQL 服务器，请在 Azure Data Studio 扩展商城中下载 [PostgreSQL 扩展](postgres-extension.md)  。

![image7](media/sql-notebooks/sql-kernel-dropdown.png)

### <a name="sql-kernel"></a>SQL 内核

在笔记本内的代码单元格中，与查询编辑器类似，我们支持新式 SQL 编码体验，通过丰富的 SQL 编辑器、IntelliSense 和内置代码段等内置功能，使日常任务更加轻松。 借助代码段可以生成正确的 SQL 语法以创建数据库、表格、视图、存储过程等等，并更新现有的数据库对象。 使用代码片段快速创建用于开发或测试的数据库副本，然后生成并执行脚本。

单击“运行”以执行每个单元格  。

连接到 SQL Server 实例的 SQL 内核

![image7](media/sql-notebooks/intellisense-code-cell.png)

查询结果

![image19](media/sql-notebooks/sql-cell-results.png)

连接到 PostgreSQL 服务器实例的 SQL 内核 

![image18](media/sql-notebooks/pgsql-code-cell.png)

查询结果

![image20](media/sql-notebooks/pgsql-cell-results.png)

### <a name="configure-python-for-notebooks"></a>为笔记本配置 Python

如果从内核下拉列表中选择除 SQL 之外的任何其他内核，则会提示“为笔记本配置 Python”  。 笔记本依赖项将安装在指定位置，但你可以决定是否设置安装位置。 此安装可能需要一些时间，建议在安装完成之前，不要关闭应用程序。 安装完成后，可以开始使用支持的语言编写代码。

![image21](media/sql-notebooks/configure-python.png)

安装成功后，在任务历史记录中将找到通知，以及在输出终端中运行的 Jupyter 后端服务器的位置。

![image22](media/sql-notebooks/jupyter-backend.png)

|内核|描述
|:-----|:-----
| SQL 内核 | 编写面向关系数据库的 SQL 代码。
|PySpark3 和 PySpark 内核| 使用群集中的 Spark 计算编写 Python 代码。
|Spark 内核|使用群集中的 Spark 计算编写 Scala 和 R 代码。
|Python 内核|编写用于本地开发的 Python 代码。

`Attach to` 为要附加的内核提供上下文。 如果使用的是 SQL 内核，则可以 `Attach to` 任何 SQL Server 实例。

如果使用的是 Python3 内核，则 `Attach to` 为 `localhost`。 可以将此内核用于本地 Python 开发。

当连接到 SQL Server 2019 大数据群集时，默认 `Attach to` 为该群集的终结点，并允许使用群集的 Spark 计算提交 Python、Scala 和 R 代码。

### <a name="code-cells-and-markdown-cells"></a>代码单元格和 Markdown 单元格

单击工具栏中的“+代码”命令，添加一个新的代码单元格  。

单击工具栏中的“+文本”命令，添加一个新的文本单元格  。

![image8](media/sql-notebooks/notebook-toolbar.png)

单元格更改为编辑模式，现在键入 markdown，你将同时看到预览内容

![image9](media/sql-notebooks/notebook-markdown-cell.png)

单击文本单元格外部将显示 markdown 文本。

![image10](media/sql-notebooks/notebook-markdown-preview.png)

### <a name="trusted-and-non-trusted"></a>受信任与不受信任

在 Azure Data Studio 中打开的笔记本默认为“受信任”  。

如果从其他源打开笔记本，它将在“不受信任”模式下打开，然后你可以将其设为“受信任”   。

### <a name="save"></a>保存 

可以通过按 Ctrl+S 或单击“文件”菜单中的“保存文件”、“文件另存为...”和“保存所有文件”命令      以及在命令面板中输入 File: Save 命令可以保存笔记本。

### <a name="pyspark3pyspark-kernel"></a>Pyspark3/PySpark 内核

选择 `PySpark Kernel` 并在单元格中键入以下代码。

单击 **“运行”** 。

启动 Spark 应用程序并返回以下输出：

![image12](media/sql-notebooks/pyspark.png)

### <a name="spark-kernel--scala-language"></a>Spark 内核 | Scala 语言

选择 `Spark|Scala Kernel` 并在单元格中键入以下代码。

![image13](media/sql-notebooks/spark-scala.png)

单击下面的选项图标时，还可以查看“单元格选项”-

![image14](media/sql-notebooks/scala-cell-options.png)

### <a name="spark-kernel--r-language"></a>Spark 内核 |R 语言

选择内核下拉列表中的 Spark | R。 在单元格中，键入或粘贴代码。 单击“运行”查看以下输出  。

![image15](media/sql-notebooks/spark-r.png)

### <a name="local-python-kernel"></a>本地 Python 内核

选择本地 Python 内核，并在单元格中键入 -

![image16](media/sql-notebooks/local-python.png)

## <a name="manage-packages"></a>管理包
我们为本地 Python 开发优化的一项功能是允许安装客户方案所需的包。 默认情况下，我们加入了 `pandas``numpy` 等常用包，但如果希望不包含某个包，请在笔记本单元格中编写以下代码： 

```python
import <package-name>
```

当运行此命令时，将返回 `Module not found`。 如果包存在，则不会收到错误。

如果返回 `Module not Found` 错误，则单击“管理包”以启动向导体验  。 

![image17](media/sql-notebooks/manage-packages.png)

在此向导中，你将能够看到“已安装”的包  。 可以搜索列表以及每个包的关联版本。 如果需要“卸载”这些包中的任何一个，则可以单击其中一个包，然后单击“卸载所选程序包”选项   。

还可以单击“新增”包以“搜索”特定包，然后选择相关版本并单击“安装”    。 默认情况下，选择最新版本的搜索包。 

安装包后，应该可以在笔记本单元格中进行操作，然后键入以下命令：

```python
import <package-name>
```

如果需要“卸载”这些包中的任何一个，则可以单击其中一个或多个包，然后单击“卸载所选包”选项   。

## <a name="next-steps"></a>后续步骤

若要了解如何使用现有笔记本，请参阅[如何管理 Azure Data Studio 中的笔记本](https://docs.microsoft.com/sql/big-data-cluster/notebooks-how-to-manage?view=sqlallproducts-allversions)。