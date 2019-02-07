---
title: 在 Azure Data Studio 中运行 notebook
titleSuffix: SQL Server 2019 big data clusters
description: 此文章介绍了如何对 SQL Server 2019 大数据群集在 Azure Data Studio conneected 中运行的 Jupyter 笔记本。
author: rothja
ms.author: jroth
manager: craigg
ms.date: 12/12/2018
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.custom: seodec18
ms.openlocfilehash: e4f1c945bd09c4d2878ebb441027e32898f24c56
ms.sourcegitcommit: f8ad5af0f05b6b175cd6d592e869b28edd3c8e2c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/07/2019
ms.locfileid: "55807467"
---
# <a name="how-to-use-notebooks-in-sql-server-2019-preview"></a>如何在 SQL Server 2019 预览版中使用笔记本

本文介绍如何在大数据群集上启动 Jupyter 笔记本以及如何开始创作自己的笔记本。 它还演示如何将针对群集的作业提交。

## <a name="prerequisites"></a>先决条件

若要使用笔记本，必须安装以下先决条件：

- [SQL Server 2019 大数据群集](deployment-guidance.md)
- [SQL Server 2019 大数据工具](deploy-big-data-tools.md):
   - **Azure Data Studio**
   - **SQL Server 2019 扩展**
   - **kubectl**

[!INCLUDE [Limited public preview note](../includes/big-data-cluster-preview-note.md)]

## <a name="connect-to-the-sql-server-big-data-cluster-end-point"></a>连接到 SQL Server 大数据群集终结点

你可以连接到群集中的不同终结点。 您可以连接到 Microsoft SQL Server 连接类型或 SQL Server 大数据群集终结点。
在 Azure 数据 Studio （预览版） 中，按 F1，并单击**新的连接** 并且可以连接到你的 SQL Server 大数据群集终结点。

![image1](media/notebooks-guidance/image1.png)

## <a name="browse-hdfs"></a>浏览 HDFS

连接后，你将能够浏览 HDFS 文件夹。 部署完成后，SQL Server 开始 WebHDFS 才开始。 使用 WebHDFS，你可以**刷新**，添加**的新目录**，**上载**文件，并**删除**。

![image2](media/notebooks-guidance/image2.png)

这些简单的操作，让您能够将你自己的数据带到 HDFS。

## <a name="launch-new-notebooks"></a>启动新的笔记本

>[!NOTE]
>如果有多个环境中运行的 Python 进程，首先删除`.scaleoutdata`安装目录下的文件夹。 这应触发`Reinstall Notebook dependencies`Azure Data Studio 中的任务。 它将需要几分钟来安装的所有依赖项。

如果有安装笔记本依赖项的问题，请单击 Ctrl + Shift + P 或 Macintosh Cmd + Shift + P，和类型`Reinstall Notebook dependencies`在命令面板中。

![image3](media/notebooks-guidance/image3.png)

有多种方法来启动新的 notebook。

1. 从**管理仪表板**。 新的连接后，您将看到仪表板。 单击**新的 Notebook**从仪表板的任务。
  
    ![image4](media/notebooks-guidance/image4.png)

1. 右键单击 HDFS/Spark 连接，然后单击**新的 Notebook**的上下文菜单中。

    ![image5](media/notebooks-guidance/image5.png)

    名为的新文件`Notebook-0.ipynb`随即打开。

    ![image6](media/notebooks-guidance/image6.png)

当从命令托盘打开笔记本时，笔记本将作为打开`Untitled-0.ipynb`。

## <a name="supported-kernels-and-attach-to-context"></a>支持的内核和将附加到上下文

Notebook 安装支持使用 PySpark 和 Spark，Spark Magic 内核时，可用于编写使用 Spark 的 Python 和 Scala 代码。 （可选） 你可以选择 Python 用于本地开发。

![image7](media/notebooks-guidance/image7.png)

当你选择其中一个这些内核时，安装在虚拟环境中配置该内核，您可以开始在受支持的语言中编写代码。

|内核|Description
|:-----|:-----
|PySpark3 和 PySpark 内核| 编写使用 Spark 计算群集中的 Python 代码。
|Spark 内核|编写使用 Spark 计算群集中的 Scala 和 R 代码。
|Python Kernel|编写 Python 代码进行本地开发。

`Attach to` 提供要附加的内核的上下文。 当连接到 SQL Server 大数据群集终结点，默认值`Attach to`群集该终结点。

在您未连接到 SQL Server 大数据群集终结点，默认内核是 Python 和`Attach to`是`localhost`。

## <a name="hello-world-in-different-contexts"></a>不同的上下文中的 hello world

### <a name="pyspark3pyspark-kernel"></a>Pyspark3/PySpark 内核

选择 PySpark 内核在下面的代码中的单元格类型。

单击 **“运行”**。

Spark 应用程序启动，并返回以下输出：

![image8](media/notebooks-guidance/image8.png)

### <a name="spark-kernel--scala-language"></a>Spark 内核 |Scala 语言

选择 Spark |Scala 内核和在下面的代码中的单元格类型。

![image9](media/notebooks-guidance/image9.png)

通过单击来添加新的代码单元格 **+ Code**命令工具栏中。

现在，选择 Spark |Scala 内核在下拉列表中和在 – 在单元格中键入/粘贴

![image10](media/notebooks-guidance/image10.png)

单击下 – 的选项图标上时，还可以查看"单元格选项"

![image11](media/notebooks-guidance/image11.png)

### <a name="spark-kernel--r-language"></a>Spark 内核 |R 语言

选择 Spark |R 内核在下拉列表中。 在单元格中，键入或粘贴代码。 单击**运行**看到以下输出。

![image13](media/notebooks-guidance/image13.png)

### <a name="local-python-kernel"></a>本地 Python 内核

选择本地 Python 内核在-中的单元格类型

![image14](media/notebooks-guidance/image14.png)

### <a name="markdown-text"></a>Markdown 文本

通过单击来添加新的文本单元格 **+ 文本**命令工具栏中。

![image15](media/notebooks-guidance/image15.png)

若要更改编辑视图的文本单元格内双击 

![image16](media/notebooks-guidance/image16.png)

要编辑模式的单元格更改

![image17](media/notebooks-guidance/image17.png)

现在类型 markdown 和你将看到在同一时间的预览

![image18](media/notebooks-guidance/image18.png)

单击 **“运行”**。 在 Spark 应用程序启动创建 Spark 会话，作为**spark** ，并定义**HelloWorld**对象。

笔记本应类似于下图。

文本单元格外单击将改为预览模式下，隐藏 markdown。

![image19](media/notebooks-guidance/image19.png)


## <a name="manage-packages"></a>管理包
我们针对本地 Python 开发优化的项目之一是包括安装包的客户将需要为其方案的能力。 默认情况下，我们包括等常用的程序包`pandas`，`numpy`等，但如果您希望不包括的包然后在笔记本单元中编写以下代码： 

```python
import <package-name>
```

运行此命令时`Module not found`返回。 如果您的包存在，然后将未收到错误。

如果它返回`Module not Found`错误，然后单击**管理包**以标识您 Virtualenv 启动终端中的路径。 现在可以安装本地包。 使用以下命令以安装包：

```bash
./pip install <package-name>
```

安装此包后，您应能够处于 Notebook 单元中，并键入以下命令：

```python
import <package-name>
```

若要卸载包，请使用从终端运行以下命令：

```bash
./pip uninstall <package-name>
```

## <a name="next-steps"></a>后续步骤

若要了解如何使用现有 notebook，请参阅[如何管理 Azure Data Studio 中的笔记本](notebooks-how-to-manage.md)。