---
title: 如何在 Azure Data Studio 中使用 SQL Notebook
titleSuffix: Azure Data Studio
description: 了解如何在 Azure Data Studio 中使用 SQL Notebook
ms.custom: seodec18
ms.date: 03/17/2019
ms.prod: sql
ms.technology: azure-data-studio
ms.reviewer: achatter; alayu; sstein
ms.topic: conceptual
author: yualan
ms.author: alayu
manager: jroth
ms.openlocfilehash: 6ac15dcd6b440a8c3bcca0c468a79548469fe059
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/15/2019
ms.locfileid: "66798039"
---
# <a name="how-to-use-notebooks-in-azure-data-studio"></a>如何在 Azure Data Studio 中使用 notebook

本文介绍如何启动 Azure 数据 Studio 中的笔记本体验以及如何开始创作自己的笔记本。 它还演示如何编写使用不同的内核的笔记本。


## <a name="connect-to-sql-server"></a>连接到 SQL Server

您可以连接到 Azure Data Studio 中的 Microsoft SQL Server 连接类型。
在 Azure 数据 Studio 中，您可以还按 F1，并单击**新的连接** 并连接到 SQL Server。

![image1](media/sql-notebooks/connection-info.png)

## <a name="launch-notebooks"></a>启动笔记本

有多种方法来启动新的 notebook。

1. 转到**文件菜单**在 Azure Data Studio，然后单击**新的 Notebook**。

    ![image3](media/sql-notebooks/file-new-notebook.png)

3. 右键单击**SQL Server**连接，然后启动**新的 Notebook**。 
    ![image3](media/sql-notebooks/server-new-notebook.png)

4. 打开命令面板 (**Ctrl + Shift + P**))，然后键入**新的 Notebook**。 名为的新文件`Notebook-1.ipynb`随即打开。

## <a name="supported-kernels-and-attach-to-context"></a>支持的内核和将附加到上下文

Azure Data Studio 中的 Notebook 安装以本机方式支持 SQL 内核。 如果是 SQL 开发人员并且想要使用笔记本，则这将是你所选择的内核。 

SQL 内核还可用来连接到 PostgreSQL 服务器实例。 如果您是 PostgreSQL 开发人员，并且想要连接到 PostgreSQL 服务器，然后下载[ **PostgreSQL 扩展**](postgres-extension.md) Azure Data Studio 扩展应用商店中。

![image7](media/sql-notebooks/sql-kernel-dropdown.png)

### <a name="sql-kernel"></a>SQL Kernel

笔记本，类似于我们的查询编辑器中的代码单元中，我们支持现代 SQL 编码的内置功能，例如丰富的 SQL 编辑器、 IntelliSense 和内置代码段简化日常任务的体验。 代码片段，可生成正确的 SQL 语法来创建数据库、 表、 视图、 存储的过程、 等，并更新现有数据库对象。 使用代码片段来快速创建开发或测试用途的数据库的副本并生成和执行脚本。

单击**运行**执行每个单元格。

若要连接到 SQL Server 实例的 SQL 内核

![image7](media/sql-notebooks/intellisense-code-cell.png)

查询结果

![image19](media/sql-notebooks/sql-cell-results.png)

若要连接到 PostgreSQL 服务器实例的 SQL 内核 

![image18](media/sql-notebooks/pgsql-code-cell.png)

查询结果

![image20](media/sql-notebooks/pgsql-cell-results.png)

### <a name="configure-python-for-notebooks"></a>适用于笔记本中配置 Python

当您选择任何除了 SQL 之外的其他内核的内核下拉列表中时，这会提示您**配置 Python 笔记本的**。 Notebook 依赖项安装在指定的位置，但您可以决定是否设置的安装位置。 此安装可能需要一些时间，建议在安装完成之前不关闭应用程序。 安装完成后，可以开始在受支持的语言中编写代码。

![image21](media/sql-notebooks/configure-python.png)

安装成功后，您会发现通知任务历史记录以及在输出终端中运行的 Jupyter 后端服务器的位置中。

![image22](media/sql-notebooks/jupyter-backend.png)

|内核|Description
|:-----|:-----
| SQL Kernel | 编写针对关系数据库的 SQL 代码。
|PySpark3 和 PySpark 内核| 编写使用 Spark 计算群集中的 Python 代码。
|Spark 内核|编写使用 Spark 计算群集中的 Scala 和 R 代码。
|Python Kernel|编写 Python 代码进行本地开发。

`Attach to` 提供要附加的内核的上下文。 如果使用的 SQL 内核，然后，你可以`Attach to`任何 SQL Server 实例。

如果使用 Python3 内核`Attach to`是`localhost`。 为本地 Python 开发，可以使用此内核。

当连接到 SQL Server 2019 大数据群集，默认值`Attach to`群集该终结点，让你提交 Python、 Scala 和 R 代码中使用 Spark 群集的计算。

### <a name="code-cells-and-markdown-cells"></a>代码单元格和 Markdown 单元格

通过单击来添加新的代码单元格 **+ Code**命令工具栏中。

通过单击来添加新的文本单元格 **+ 文本**命令工具栏中。

![image8](media/sql-notebooks/notebook-toolbar.png)

单元格更改编辑模式，现在键入 markdown 和你将看到在同一时间的预览

![image9](media/sql-notebooks/notebook-markdown-cell.png)

文本单元格外单击，则会显示 markdown 文本。

![image10](media/sql-notebooks/notebook-markdown-preview.png)

### <a name="trusted-and-non-trusted"></a>受信任和非受信任

在 Azure Data Studio 中打开笔记本，则进行默认**受信任**。

如果从某个其他源中打开笔记本，它将在中打开**非受信任**模式，然后你可以使其**受信任**。

### <a name="save"></a>保存 

您可以保存通过笔记本**Ctrl + S**或单击**文件将保存**，**文件另存为...** 并**文件将保存所有**从文件菜单命令和**文件：保存**在命令面板中输入的命令。

### <a name="pyspark3pyspark-kernel"></a>Pyspark3/PySpark 内核

选择`PySpark Kernel`和在下面的代码中的单元格类型。

单击 **“运行”** 。

Spark 应用程序启动，并返回以下输出：

![image12](media/sql-notebooks/pyspark.png)

### <a name="spark-kernel--scala-language"></a>Spark 内核 |Scala 语言

选择`Spark|Scala Kernel`和在下面的代码中的单元格类型。

![image13](media/sql-notebooks/spark-scala.png)

单击下 – 的选项图标上时，还可以查看"单元格选项"

![image14](media/sql-notebooks/scala-cell-options.png)

### <a name="spark-kernel--r-language"></a>Spark 内核 |R 语言

选择 Spark |R 内核在下拉列表中。 在单元格中，键入或粘贴代码。 单击**运行**看到以下输出。

![image15](media/sql-notebooks/spark-r.png)

### <a name="local-python-kernel"></a>本地 Python 内核

选择本地 Python 内核在-中的单元格类型

![image16](media/sql-notebooks/local-python.png)

## <a name="manage-packages"></a>管理包
我们针对本地 Python 开发优化的项目之一是包括安装包的客户将需要为其方案的能力。 默认情况下，我们包括等常用的程序包`pandas`，`numpy`等，但如果您希望不包括的包然后在笔记本单元中编写以下代码： 

```python
import <package-name>
```

运行此命令时`Module not found`返回。 如果您的包存在，然后将未收到错误。

如果它返回`Module not Found`错误，然后单击**管理包**启动终端。 现在可以安装本地包。 使用以下命令以安装包：

```bash
./pip install <package-name>
```

   > [!Tip]
   > 在 Mac 上请按照在终端窗口中安装包的说明。 

安装此包后，您应能够处于 Notebook 单元中，并键入以下命令：

```python
import <package-name>
```

若要卸载包，请使用从终端运行以下命令：

```bash
./pip uninstall <package-name>
```

## <a name="next-steps"></a>后续步骤

若要了解如何使用现有 notebook，请参阅[如何管理 Azure Data Studio 中的笔记本](https://docs.microsoft.com/sql/big-data-cluster/notebooks-how-to-manage?view=sqlallproducts-allversions)。