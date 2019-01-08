---
title: 在 Azure Data Studio 中运行 notebook
titleSuffix: SQL Server 2019 big data clusters
description: 此文章介绍了如何对 SQL Server 2019 大数据群集在 Azure Data Studio conneected 中运行的 Jupyter 笔记本。
author: rothja
ms.author: jroth
manager: craigg
ms.date: 12/06/2018
ms.topic: conceptual
ms.prod: sql
ms.custom: seodec18
ms.openlocfilehash: af1393b38b297e451903d5a39942a3e878c88ee6
ms.sourcegitcommit: edf7372cb674179f03a330de5e674824a8b4118f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/11/2018
ms.locfileid: "53246606"
---
# <a name="how-to-use-notebooks-in-sql-server-2019-preview"></a>如何在 SQL Server 2019 预览版中使用笔记本

本文介绍如何在大数据群集上启动 Jupyter 笔记本以及如何开始创作自己的笔记本。 它还演示如何将针对群集的作业提交。

## <a name="prerequisites"></a>先决条件

若要使用笔记本，必须安装以下先决条件：

- [SQL Server 2019 大数据群集](deployment-guidance.md)
- [SQL Server 2019 大数据工具](deploy-big-data-tools.md):
   - **Azure Data Studio**
   - **SQL Server 2019 扩展**
   - **Kubectl**

[!INCLUDE [Limited public preview note](../includes/big-data-cluster-preview-note.md)]

## <a name="connect-to-the-hadoop-gateway-knox-end-point"></a>连接到 Hadoop 网关 Knox 终结点

你可以连接到群集中的不同终结点。 您可以连接到 Microsoft SQL Server 连接类型或 HDFS/Spark 网关终结点。
在 Azure 数据 Studio （预览版） 中，按 F1，并单击**新的连接** 并且可以连接到你的 HDFS/Spark 网关终结点。

![image1](media/notebooks-guidance/image1.png)

## <a name="browse-hdfs"></a>浏览 HDFS

连接后，你将能够浏览 HDFS 文件夹。 在完成部署，并且你将能够启动 WebHDFS**刷新**，添加**的新目录**，**上载**文件，和**删除**.

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

  例如，提供的笔记本中，名称`Test.ipynb`。 单击“保存” 。

![image6](media/notebooks-guidance/image6.png)

## <a name="supported-kernels-and-attach-to-context"></a>支持的内核和将附加到上下文

Notebook 安装支持使用 PySpark 和 Spark，Spark Magic 内核时，可用于编写使用 Spark 的 Python 和 Scala 代码。 （可选） 你可以选择 Python 用于本地开发。

![image7](media/notebooks-guidance/image7.png)

当你选择其中一个这些内核时，我们将在虚拟环境中安装该内核，您可以开始在受支持的语言中编写代码。

|内核|Description
|:-----|:-----
|PySpark 内核|有关编写使用 Spark 计算群集中的 Python 代码。
|Spark 内核|有关编写使用 Spark 计算群集中的 Scala 代码。
|Python 内核|用于写入 Python 代码进行本地开发。

`Attach to`提供附加的内核的上下文。 当您连接到 HDFS/Spark 网关 (Knox) 结束时点默认`Attach to`群集该终结点。

![image8](media/notebooks-guidance/image8.png)

## <a name="hello-world-in-different-contexts"></a>不同的上下文中的 hello world

### <a name="pyspark-kernel"></a>Pyspark 内核

选择 PySpark 内核在下面的代码中的单元格类型：

![image9](media/notebooks-guidance/image9.png)

单击运行和你应启动 Spark 应用程序，请参阅，您将看到以下输出：

![Image10](media/notebooks-guidance/image10.png)

输出应类似于下图类似。

![Image11](media/notebooks-guidance/image11.png)

### <a name="spark-kernel"></a>Spark 内核
通过单击来添加新的代码单元格 **+ Code**命令工具栏中。

![Image12](media/notebooks-guidance/image12.png)

单击下方的选项图标上时，还可以查看"单元格选项"

![Image13](media/notebooks-guidance/image13.png)

以下是有关每个单元格的选项

![Image14](media/notebooks-guidance/image14.png)-

现在，选择 Spark 内核，内核在下拉列表中，然后在中的单元格类型/粘贴

![Image15](media/notebooks-guidance/image15.png)

单击**运行**和你应看到正在启动 Spark 应用程序和这将创建与 Spark 会话**spark** ，并将定义**HelloWorld**对象。

笔记本应类似于下图。

![Image16](media/notebooks-guidance/image16.png)

一次定义的对象，然后在下一步的 Notebook 单元中，键入下面的代码中：

![Image17](media/notebooks-guidance/image17.png)

单击**运行**笔记本中菜单，您应看到"Hello，world ！" 在输出中。

![Image18](media/notebooks-guidance/image18.png)

### <a name="local-python-kernel"></a>本地 python 内核
选择本地 Python 内核在-中的单元格类型

![Image19](media/notebooks-guidance/image19.png)

您应看到下列输出：

![Image20](media/notebooks-guidance/image20.png)

### <a name="markdown-text"></a>Markdown 文本
通过单击来添加新的文本单元格 **+ 文本**命令工具栏中。

![Image21](media/notebooks-guidance/image21.png)

单击预览图标以添加 markdown

![Image22](media/notebooks-guidance/image22.png)

单击预览图标再次以切换以查看只需 markdown

![Image23](media/notebooks-guidance/image23.png)

## <a name="manage-packages"></a>管理包
我们针对本地 Python 开发优化的项目之一是包括安装包的客户将需要为其方案的能力。 默认情况下，我们包括常用的程序包像 pandas、 numpy 等，但如果希望不包括的包然后编写以下代码的 Notebook 单元格中： 

```python
import <package-name>
```

当运行此命令时，您将收到`Module not found`错误。 如果您的包存在，然后将未收到错误。

如果您发现`Module not Found`错误，然后单击**管理包**以标识您 Virtualenv 启动终端中的路径。 现在可以安装本地包。 使用以下命令以安装包：

```bash
./pip install <package-name>
```

安装此包后，您应能够处于 Notebook 单元中，并键入以下命令：

```python
import <package-name>
```

现在，当您运行该单元格，应不再获得`Module not found`错误。

若要卸载包，请使用从终端运行以下命令：

```bash
./pip uninstall <package-name>
```

## <a name="next-steps"></a>后续步骤

若要了解如何使用现有 notebook，请参阅[如何管理 Azure Data Studio 中的笔记本](notebooks-how-to-manage.md)。