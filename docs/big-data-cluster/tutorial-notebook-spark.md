---
title: 在 SQL Server 2019 大数据群集上运行的示例笔记本 |Microsoft Docs
description: 本教程演示如何可以加载 SQL Server 2019 大数据群集 （预览版） 上的示例 Spark 笔记本将运行。
author: rothja
ms.author: jroth
manager: craigg
ms.date: 10/17/2018
ms.topic: tutorial
ms.prod: sql
ms.openlocfilehash: 811c94615f0d69886f0f538357529ad3125e2925
ms.sourcegitcommit: 38f35b2f7a226ded447edc6a36665eaa0376e06e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/23/2018
ms.locfileid: "49644111"
---
# <a name="tutorial-run-a-sample-notebook-on-a-sql-server-2019-big-data-cluster"></a>教程： SQL Server 2019 大数据群集上运行的示例笔记本

本教程演示如何加载和笔记本在 Azure 数据 Studio 中运行 SQL Server 2019 大数据群集 （预览版） 上。 这允许数据科学家和数据工程师针对群集中运行 Python、 R 或 Scala 代码。

> [!TIP]
> 如果您愿意，可以下载并运行本教程中的所有命令的脚本。 有关说明，请参阅[Spark 示例](https://github.com/Microsoft/sql-server-samples/tree/master/samples/features/sql-big-data-cluster/spark)GitHub 上。

## <a id="prereqs"></a> 先决条件

* [部署 Kubernetes 上的大数据群集](deployment-guidance.md)。
* [安装 Azure Data Studio 和 SQL Server 2019 扩展](deploy-big-data-tools.md)。
* [将示例数据加载到群集](#sampledata)。

[!INCLUDE [Load sample data](../includes/big-data-cluster-load-sample-data.md)]

## <a name="download-the-sample-notebook-file"></a>下载示例 notebook 文件

使用以下说明示例 notebook 文件加载**spark sql.ipynb**到 Azure Data Studio。

1. 打开 bash 命令提示符 (Linux) 或 Windows PowerShell。

1. 导航到想要下载的示例 notebook 文件的目录。

1. 运行以下**curl**命令，从 GitHub 下载笔记本文件：

   ```bash
   curl 'https://raw.githubusercontent.com/Microsoft/sql-server-samples/master/samples/features/sql-big-data-cluster/spark/spark-sql.ipynb' -o spark-sql.ipynb
   ```

## <a name="open-the-notebook"></a>打开 notebook

以下步骤演示如何在 Azure Data Studio 中打开笔记本文件：

1. 在 Azure Data Studio，连接到你的大数据群集的 HDFS/Spark 网关。 有关详细信息，请参阅[连接到 HDFS/Spark 网关](deploy-big-data-tools.md#hdfs)。

1. 中的 HDFS/Spark 网关连接上双击**服务器**窗口。 然后选择**打开 Notebook**。

   ![打开 notebook](media/tutorial-notebook-spark/azure-data-studio-open-notebook.png)

1. 等待**内核**和目标上下文 (**附加到**) 填充。 设置**内核**到**PySpark3**，并设置**将附加到**到大数据群集终结点的 IP 地址。

   ![设置的内核并将附加到](media/tutorial-notebook-spark/set-kernel-and-attach-to.png)

## <a name="run-the-notebook-cells"></a>运行 notebook 单元

通过按播放按钮的单元格的左侧，可以运行每个 notebook 单元格中。 该单元格完成运行后结果显示在 notebook 中。

![运行 notebook 单元格](media/tutorial-notebook-spark/run-notebook-cell.png)

在连续示例笔记本中运行每个单元格。 笔记本中使用的 SQL Server 大数据群集的详细信息，请参阅以下资源：

- [如何在 SQL Server 2019 预览版中使用笔记本](notebooks-guidance.md)
- [如何管理 Azure Data Studio 中的笔记本](notebooks-how-to-manage.md)

## <a name="next-steps"></a>后续步骤

了解有关笔记本的详细信息：
> [!div class="nextstepaction"]
> [了解有关笔记本](notebooks-guidance.md)