---
title: 调试和诊断的 Spark 应用程序在 Spark History Server 中的 SQL Server 大数据群集上
description: 调试和诊断的 Spark 应用程序在 Spark History Server 中的 SQL Server 大数据群集上
services: SQL Server 2019 big data cluster spark
ms.service: SQL Server 2019 big data cluster spark
author: jejiang
ms.author: jejiang
ms.reviewer: jroth
ms.custom: ''
ms.topic: conceptual
ms.date: 10/01/2018
ms.openlocfilehash: 1e154ccfca46430f4ab96e620ac450e3c213313d
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/02/2018
ms.locfileid: "48795922"
---
# <a name="debug-and-diagnose-spark-applications-on-sql-server-big-data-clusters-in-spark-history-server"></a>调试和诊断的 Spark 应用程序在 Spark History Server 中的 SQL Server 大数据群集上

本文提供有关如何使用扩展的 Spark History Server 来调试和诊断 SQL Server 2019 （预览版） 大数据群集中的 Spark 应用程序的指南。 这些调试和诊断功能是内置于 Spark History Server 且由 Microsoft 提供支持。 扩展插件包括数据和关系图选项卡和诊断选项卡。在数据选项卡上，用户可以检查 Spark 作业的输入和输出数据。 用户可在关系图选项卡上，检查数据流和重播作业图。 在诊断选项卡上，用户可以引用数据偏斜、 时间偏差和执行器使用情况分析。

## <a name="get-access-to-spark-history-server"></a>有权访问 Spark History Server

开放源代码 Spark 历史记录服务器用户体验得到了增强的信息，包括特定于作业的数据和大数据群集的作业关系图和数据流的交互式可视化效果。 

### <a name="open-the-spark-history-server-web-ui-by-url"></a>打开 Spark 历史记录服务器 Web 用户界面的 URL
打开 Spark History Server 通过浏览到以下 URL 中，替换`<Ipaddress>`和`<Port>`与大数据群集特定的信息。 可以引用的详细信息：[部署 SQL Server 大数据群集](quickstart-big-data-cluster-deploy.md)

```
https://<Ipaddress>:<Port>/gateway/default/sparkhistory
```

Spark History Server web UI 如下所示：

![Spark History Server](./media/apache-azure-spark-history-server/spark-history-server.png)


## <a name="data-tab-in-spark-history-server"></a>Spark History Server 中的数据选项卡
选择作业 ID，然后单击**数据**在工具菜单上，若要获取的数据视图。

+ 检查**输入**，**输出**，并**表操作**通过单独选择这些选项卡。

    ![数据选项卡](./media/apache-azure-spark-history-server/sparkui-data-tabs.png)

+ 通过单击按钮来复制所有行**都复制**。

    ![数据复制](./media/apache-azure-spark-history-server/sparkui-data-copy.png)

+ 通过单击按钮将所有数据都保存为 CSV 文件**csv**。

    ![保存数据](./media/apache-azure-spark-history-server/sparkui-data-save.png)

+ 通过在字段中输入关键字搜索**搜索**，将立即显示搜索结果。

    ![数据搜索](./media/apache-azure-spark-history-server/sparkui-data-search.png)

+ 单击列标题以对表进行排序，单击加号以展开的行以显示更多详细信息，或单击减号可折叠行。

    ![数据表](./media/apache-azure-spark-history-server/sparkui-data-table.png)

+ 通过单击按钮下载单个文件**部分下载**，将在右侧，那么所选的文件下载到本地位置。 如果文件不存在任何更多的情况下，它将打开新选项卡以显示错误消息。

    ![数据下载行](./media/apache-azure-spark-history-server/sparkui-data-download-row.png)

+ 通过选择复制完整路径或相对路径**复制完整路径**，**复制相对路径**这从下载菜单会展开。 有关 azure 数据湖存储文件中，**在 Azure 存储资源管理器中打开**将启动 Azure 存储资源管理器。 并在登录时找到到确切的文件夹。

    ![数据复制路径](./media/apache-azure-spark-history-server/sparkui-data-copy-path.png)

+ 单击在表下面的编号，以导航页时过许多行以在一页上显示。 

    ![数据页](./media/apache-azure-spark-history-server/sparkui-data-page.png)

+ 将鼠标悬停在数据显示工具提示，旁边的问号，或单击问号来获取详细信息。

    ![数据的详细信息](./media/apache-azure-spark-history-server/sparkui-data-more-info.png)

+ 通过单击发送反馈的问题**向我们提供反馈**。

    ![图表反馈](./media/apache-azure-spark-history-server/sparkui-graph-feedback.png)

## <a name="graph-tab-in-spark-history-server"></a>Spark History Server 中的关系图选项卡

选择作业 ID，然后单击**Graph**工具菜单上，若要获取作业关系图视图上。

+ 生成的作业图来检查作业的概述。 

+ 默认情况下，它将显示所有作业，并且它可以通过筛选**作业 ID**。

    ![关系图作业 ID](./media/apache-azure-spark-history-server/sparkui-graph-jobid.png)

+ 我们将保留**进度**作为默认值。 用户可以通过选择检查数据流**读**或 * * 写入 * * * 在下拉列表中的**显示**。

    ![关系图显示](./media/apache-azure-spark-history-server/sparkui-graph-display.png)

    显示热度地图的颜色中的关系图节点显示。

    ![关系图热度地图](./media/apache-azure-spark-history-server/sparkui-graph-heatmap.png)

+ 通过单击播放作业**播放**按钮，然后通过单击停止按钮随时停止。 颜色以在播放时显示不同状态中的任务显示：

    + 绿色表示成功： 作业已成功完成。
    + 橙色试： 任务已失败但不是会影响作业最终结果的实例。 这些任务必须复制或重试实例可能稍后会成功。
    + 蓝色表示运行： 在任务运行。
    + 白色等待或已跳过： 该任务正在等待运行，或已跳过阶段。
    + 红色失败： 该任务失败。

    ![关系图颜色样本运行](./media/apache-azure-spark-history-server/sparkui-graph-color-running.png)
 
    已跳过的阶段以白色显示。
    ![图形颜色样本，跳过](./media/apache-azure-spark-history-server/sparkui-graph-color-skip.png)

    ![关系图颜色样本失败](./media/apache-azure-spark-history-server/sparkui-graph-color-failed.png)
 
    > [!NOTE]
    > 允许为每个作业播放。 对于不完整作业，不支持播放。


+ 鼠标滚动以缩放输入/输出作业图，或单击**缩放到合适大小**以使其适应屏幕。
 
    ![图形缩放到合适大小](./media/apache-azure-spark-history-server/sparkui-graph-zoom2fit.png)

+ 将鼠标悬停在图形节点以查看工具提示时有失败的任务，并单击阶段，以打开阶段页。

    ![图形工具提示](./media/apache-azure-spark-history-server/sparkui-graph-tooltip.png)

+ 阶段将在作业关系图选项卡上，有工具提示和小图标显示如果他们有任务满足以下条件：
    + 数据倾斜： 读取的数据大小 > 平均数据读取的此阶段内的所有任务的大小 * 2 和读取的数据大小 > 10 MB
    + 时间偏差： 执行时间 > 在此阶段内的所有任务的平均执行时间 * 2 和执行时间 > 2 分钟

    ![倾斜图标](./media/apache-azure-spark-history-server/sparkui-graph-skew-icon.png)

+ 作业关系图节点将显示每个阶段的以下信息：
    + ID。
    + 名称或说明。
    + 总的任务数。
    + 读取的数据： 输入的大小和无序播放的总和读取大小。
    + 数据写入： 输出大小和无序播放的总和写入大小。
    + 执行时间： 第一次尝试开始时间和完成时间的最后一次尝试之间的时间。
    + 行计数： 输入记录的总和将输出记录、 无序播放读取的记录和无序播放写入记录。
    + 进度。

    > [!NOTE]
    > 默认情况下，作业图形节点将显示上次尝试中 （除阶段执行时间），每个阶段的信息，但在播放图形节点将显示每次尝试的信息。

    > [!NOTE]
    > 数据大小的读取和写入，我们使用 1 MB = 1000 KB = 1000 * 1000 个字节。

+ 通过单击发送反馈的问题**向我们提供反馈**。

    ![图表反馈](./media/apache-azure-spark-history-server/sparkui-graph-feedback.png)


## <a name="diagnosis-tab-in-spark-history-server"></a>Spark History Server 中的诊断选项卡
选择作业 ID，然后单击**诊断**在工具菜单上，若要获取作业诊断视图。 诊断选项卡包括**的数据偏斜**，**时间偏差**，并**执行器使用情况分析**。
    
+ 检查**的数据偏斜**，**时间偏差**，并**执行器使用情况分析**通过分别选择选项卡。

    ![诊断选项卡](./media/apache-azure-spark-history-server/sparkui-diagnosis-tabs.png)

### <a name="data-skew"></a>数据偏斜
单击**的数据偏斜**选项卡上，相应显示偏斜的任务基于指定的参数。 

+ **指定参数**-第一部分显示的参数，用于检测数据偏斜。 内置的规则是： 大于三次平均任务读取的数据，读取的任务数据，读取的任务数据是超过 10 MB。 如果你想要定义自己的规则的偏斜的任务，则可以选择你的参数，**偏斜阶段**，并**倾斜 Char**部分将进行相应地刷新。 

+ **倾斜阶段**-第二部分显示阶段，已倾斜符合上面指定的条件的任务。 如果阶段中有多个偏斜的任务，偏斜的阶段表仅显示最偏斜的任务 （例如，数据偏斜的最大数据）。 

    ![数据倾斜 section2](./media/apache-azure-spark-history-server/sparkui-diagnosis-dataskew-section2.png)

+ **倾斜图**– 选中偏斜阶段表中的行后，偏斜的图表显示多个任务分布区的详细信息基于读取的数据和执行时间。 倾斜的任务标记为红色和蓝色标记的常规任务。 出于性能考虑，图表仅显示最多 100 个示例任务。 任务详细信息将显示在右下面板。

    ![数据倾斜 section3](./media/apache-azure-spark-history-server/sparkui-diagnosis-dataskew-section3.png)

### <a name="time-skew"></a>时间偏差
**时间差**选项卡显示基于任务的执行时间的偏斜的任务。 

+ **指定参数**-第一部分显示的参数，用于检测时间偏差。 若要检测的时间差的默认条件是： 任务执行时间是否大于三次的平均执行时间和任务执行时间大于 30 秒。 你可以根据需要的参数。 **偏斜阶段**并**倾斜图表**一样显示相应的阶段和任务信息**的数据偏斜**上面的选项卡。

+ 单击**时间差**，则已筛选的结果显示在**偏斜阶段**根据部分中设置的参数部分**指定参数**。 单击中的一项**偏斜阶段**部分，则相应的图表在 section3，开发阶段和任务详细信息显示在面板中靠右下对齐。

    ![时间倾斜 section2](./media/apache-azure-spark-history-server/sparkui-diagnosis-timeskew-section2.png)

### <a name="executor-usage-analysis"></a>执行器使用情况分析
执行器使用情况图直观显示 Spark 作业实际的执行器分配和运行状态。  

+ 单击**执行器使用情况分析**，然后我们草稿执行器使用情况有关的四个类型曲线。 它们包括**分配执行器**，**运行的执行器**，**空闲执行器**，以及**最大执行器实例**。 有关已分配执行器，每个"执行器添加"或"执行器已删除"事件将增加或减少分配执行器。 在"作业"选项卡中进行详细比较，可以检查"事件时间线"。

    ![执行器选项卡](./media/apache-azure-spark-history-server/sparkui-diagnosis-executors.png)

+ 单击颜色图标以选中或取消选中所有草稿中的相应内容。

    ![选择图表](./media/apache-azure-spark-history-server/sparkui-diagnosis-select-chart.png)


## <a name="known-issues"></a>已知问题
Spark History Server 具有以下已知的问题：

+ 目前，它仅适用于 Spark 2.3 群集。

+ 使用 RDD 的输入/输出数据将不会显示在选项卡中的数据。

## <a name="next-steps"></a>后续步骤

* [管理 HDInsight 上的 Spark 群集的资源](https://docs.microsoft.com/en-us/azure/hdinsight/spark/apache-spark-resource-manager)
* [配置 Spark 设置](https://docs.microsoft.com/en-us/azure/hdinsight/spark/apache-spark-settings)
