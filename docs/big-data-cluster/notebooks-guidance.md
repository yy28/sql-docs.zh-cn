---
title: 如何在 SQL Server 2019 预览版中使用笔记本 |Microsoft Docs
description: ''
author: rothja
ms.author: jroth
manager: craigg
ms.date: 10/05/2018
ms.topic: conceptual
ms.prod: sql
ms.openlocfilehash: 989ee419406d0f69cd7bda26485d3d44cbf56550
ms.sourcegitcommit: c7d3a903eb7f410db3a0230101d24de0af17621a
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/05/2018
ms.locfileid: "48827328"
---
# <a name="how-to-use-notebooks-in-sql-server-2019-preview"></a>如何在 SQL Server 2019 预览版中使用笔记本

本文介绍如何启动 SQL Server 2019 大数据群集上的笔记本。 它还显示如何开始创作自己的笔记本以及如何将针对群集的作业提交。

## <a name="prerequisites"></a>必要條件

若要使用笔记本，必须安装以下先决条件：

- [SQL Server 2019 大数据群集](deployment-guidance.md)
- [Azure 数据 Studio](../azure-data-studio/what-is.md)
- [SQL Server 2019 扩展 （预览版）](../azure-data-studio/sql-server-2019-extension.md)。

[!INCLUDE [Limited public preview note](../includes/big-data-cluster-preview-note.md)]

## <a name="connect-to-the-sql-server-big-data-cluster-end-point"></a>连接到 SQL Server 大数据群集终结点

你可以连接到群集中的不同终结点。 您可以连接到 Microsoft SQL Server 连接类型或 SQL Server 大数据群集终结点。

在 Azure 数据 Studio （预览版） 中，键入**F1** > **新连接**，并连接到在 SQL Server 大数据群集终结点。

![image1](media/notebooks-guidance/image1.png)

## <a name="browse-hdfs"></a>浏览 HDFS
连接后，你将能够浏览 HDFS 文件夹。 在完成部署，并且你将能够启动 WebHDFS**刷新**，添加**的新目录**，**上载**文件，和**删除**.

![image2](media/notebooks-guidance/image2.png)

这些简单的操作，让您能够将你自己的数据带到 HDFS。

## <a name="launch-new-notebooks"></a>启动新的笔记本

有多种方法来启动新的 notebook。

1. 从管理仪表板。 在进行新连接时，会看到仪表板。 单击新的 Notebook 从仪表板的任务。

  ![image3](media/notebooks-guidance/image3.png)

1. 右键单击 HDFS/Spark 连接和上下文菜单中有新的 Notebook

![image4](media/notebooks-guidance/image4.png)

提供笔记本的名称 (示例： *Test.ipynb*)，单击**保存**。

![image5](media/notebooks-guidance/image5.png)

## <a name="supported-kernels-and-attach-to-context"></a>支持的内核和将附加到上下文

在我们 Notebook 安装中，我们支持 PySpark 和 Spark，Spark Magic 内核，使用户可以编写使用 Spark 的 Python 和 Scala 代码。 我们还允许用户选择 Python 用于其本地开发。

![image6](media/notebooks-guidance/image6.png)

当你选择其中一个这些内核时，我们将在虚拟环境中安装该内核，您可以开始在受支持的语言中编写代码。

| 内核 | 描述
|---- |----
|PySpark 内核| 有关编写使用 Spark 的 Python 代码，将计算与该群集。
|Spark 内核|有关编写使用 Spark Scala 代码，将计算与该群集。
|Python 内核|用于写入 Python 代码进行本地开发。

附加到所选内容提供了附加的内核的上下文。 当连接到 SQL Server 大数据群集终结点时，默认附加到选择将该终结点的群集。

![image7](media/notebooks-guidance/image7.png)

## <a name="hello-world-in-the-different-contexts"></a>不同的上下文中的 hello world

### <a name="pyspark-kernel"></a>Pyspark 内核

选择 PySpark 内核在下面的代码中的单元格类型：

![image8](media/notebooks-guidance/image8.png)

单击运行和你应启动 Spark 应用程序，请参阅，您将看到以下输出：

![image9](media/notebooks-guidance/image9.png)

输出应类似于下图类似。

![Image10](media/notebooks-guidance/image10.png)

### <a name="spark-kernel"></a>Spark 内核
通过单击来添加新的代码单元格 + 的代码在工具栏中的命令。

![Image11](media/notebooks-guidance/image11.png)

选择 Spark 内核的内核的下拉列表中，然后在中单元格类型/粘贴 

![Image12](media/notebooks-guidance/image12.png)

单击**运行**应该看到正在启动 Spark 应用程序，这将创建 Spark 会话**spark** ，并将定义**HelloWorld**对象。

笔记本应类似于下图。

![Image13](media/notebooks-guidance/image13.png)

一次定义对象然后在下一步的 Notebook 单元格中键入下面的代码中：

![Image14](media/notebooks-guidance/image14.png)

单击**运行**笔记本中菜单，您应看到"Hello，world ！" 在输出中。

![Image15](media/notebooks-guidance/image15.png)

### <a name="local-python-kernel"></a>本地 python 内核
选择本地 Python 内核中的单元格类型在 * *

![Image16](media/notebooks-guidance/image16.png)

您应看到下列输出：

![Image17](media/notebooks-guidance/image17.png)

### <a name="markdown-text"></a>Markdown 文本
通过单击来添加新的文本单元格 + 工具栏中的文本命令。

![Image18](media/notebooks-guidance/image18.png)

单击预览图标以添加 markdown

![Image19](media/notebooks-guidance/image19.png)

单击预览图标再次以切换以查看只需 markdown

![Image20](media/notebooks-guidance/image20.png)

## <a name="manage-packages"></a>管理包
我们针对本地 Python 开发优化的项目之一是包括安装包的客户将需要为其方案的能力。 默认情况下，我们包括常用的程序包像 pandas、 numpy 等，但如果希望不包括的包然后编写以下代码的 Notebook 单元格中

```python
import <package-name>
```

当运行此命令时，您将收到`Module not found`错误。 如果您的包存在，然后将未收到错误。

如果您发现`Module not Found`错误，然后单击**管理包**以标识您 Virtualenv 启动终端中的路径。 现在可以安装本地包。 使用以下命令以安装包：

```
./pip install <package-name>
```

安装此包后，您应能够在笔记本单元格并键入以下命令：

```python
import <package-name>
```

现在，当您运行该单元格，应不再获得`Module not found`错误。

如果你想要卸载包，使用从终端运行以下命令：

```
./pip uninstall <package-name>
```

## <a name="next-steps"></a>后续步骤

若要了解如何使用现有 notebook，请参阅[如何管理 Azure Data Studio 中的笔记本](notebooks-how-to-manage.md)。