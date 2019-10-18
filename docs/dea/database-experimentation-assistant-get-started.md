---
title: 数据库实验助手 SQL Server 升级入门
description: 数据库实验助手入门
ms.custom: ''
ms.date: 10/22/2018
ms.prod: sql
ms.prod_service: dea
ms.suite: sql
ms.technology: dea
ms.tgt_pltfrm: ''
ms.topic: conceptual
author: HJToland3
ms.author: ajaykar
ms.reviewer: mathoma
ms.openlocfilehash: 9fe162b2a9bc0db4a2a49648eecb76c5802f57c0
ms.sourcegitcommit: 4c75b49599018124f05f91c1df3271d473827e4d
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/16/2019
ms.locfileid: "72381773"
---
# <a name="get-started-with-database-experimentation-assistant"></a>数据库实验助手入门

数据库实验助手（DEA）是一种用于在 SQL Server 环境中进行更改的 A/B 测试解决方案，如升级或新索引。 DEA 可帮助你评估源服务器上的工作负荷（在当前环境中）在你的新环境中将如何执行。 DEA 指导你完成三个步骤来运行 A/B 测试： 

- 捕获
- 重播
- 分析

本文将指导你完成这些步骤。

## <a name="capture"></a>捕获

SQL Server A/B 测试的第一步是在源服务器上捕获跟踪。 源服务器通常是生产服务器。 跟踪文件将捕获该服务器上的整个查询工作负荷，包括时间戳。 稍后，将在目标服务器上重播此跟踪以进行分析。 分析报告提供两个目标服务器之间工作负荷的性能差异。

注意事项：

- 在开始跟踪捕获之前，请确保备份要从中捕获跟踪的数据库。
- DEA 用户必须配置为使用 Windows 身份验证连接到数据库。
- SQL Server 服务帐户需要访问源跟踪文件路径。
- 要使 DEA 能够确定查询的性能是否有所提高或是否降级，该查询必须在捕获期间至少执行15次。  

在源服务器上捕获跟踪：

1. 在 DEA 中，通过选择左侧菜单中的相机图标，中转到**所有捕获**。

   ![左侧导航菜单](./media/database-experimentation-assistant-get-started/dea-get-started-leftnav.png)

1. 输入或选择以下信息：

   - **跟踪名称**：正在创建的新跟踪文件的文件名。 避免使用滚动更新文件命名约定的跟踪名称，例如，CaptureName \_NNN。
   - **持续**时间：捕获的持续时间。
   - **SQL Server 实例名称**：要从中捕获跟踪的 SQL Server 实例。
   - **数据库名称**：运行 SQL Server 的计算机上要捕获其跟踪的数据库的名称。 如果留空，将从服务器上的所有数据库中捕获跟踪。
   - **SQL Server 计算机上存储源跟踪文件的路径**：要保存跟踪文件的文件夹路径。

1. 请确保已备份目标数据库。 然后，选中 "数据库" 复选框。
1. 选择 "**启动**" 以启动捕获。

你可以查看捕获进度，包括开始时间、持续时间和剩余时间。 在等待此捕获完成时，还可以启动新的捕获。 捕获完成后，使用输出跟踪文件开始第二阶段：在目标服务器上重播跟踪文件。

有关跟踪捕获的常见问题，请参阅[捕获常见问题解答](database-experimentation-assistant-capture-trace.md#frequently-asked-questions-about-trace-capture)。

## <a name="replay"></a>重播

SQL Server A/B 测试的第二步是重播已捕获到目标服务器的跟踪文件。 然后，从重播收集大量跟踪以进行分析。 

您将在两个目标服务器上重播跟踪文件：一个模拟源服务器（目标1），另一个用于模拟您建议的更改（目标2）。 目标1和目标2的硬件配置应尽可能相似，因此 SQL Server 可以准确地分析所建议更改的性能影响。

注意事项：

- 若要运行重播，你的计算机必须设置为运行 Distributed Replay （DReplay）跟踪。 有关详细信息，请参阅[Distributed Replay 控制器和客户端设置](https://blogs.msdn.microsoft.com/datamigration/distributed-replay-controller-and-client-setup/)。
- 请确保通过使用源服务器中的备份来还原目标服务器上的数据库。
- SQL Server 中的查询缓存可能会影响评估结果。 建议在服务应用程序中重新启动 SQL Server 服务（MSSQLSERVER），以提高评估结果的一致性。

重播跟踪文件：

1. 在 DEA 中，选择左侧菜单中的 "播放" 图标以打开**所有重播**。 在会话期间运行的过去重播的列表（如果有）将出现。 若要开始新重播，请选择 "**新建重播**"。

1. 输入或选择以下信息：

   - **重播名称**：重播跟踪的文件名。
   - **控制器计算机名称**： Distributed Replay 控制器计算机的名称。
   - **控制器上的源跟踪文件的路径**：[捕获](#capture)的源跟踪文件的文件路径。
   - **SQL Server 实例名称**：在其上重播源跟踪的 SQL Server 实例的名称。
   - **用于存储 SQL Server 机上的目标跟踪文件的路径**：生成的重播跟踪文件的文件夹路径。

1. 选中此复选框可从第一步还原备份。

1. 选择 "**开始**" 以开始重播。 

您可以查看重播的状态。 在这两个目标服务器上重播源跟踪后，便可以生成分析报表了。

有关重播的常见问题，请参阅[重播常见问题解答](database-experimentation-assistant-replay-trace.md#frequently-asked-questions-about-trace-replay)。

## <a name="analysis"></a>分析

最后一步是使用重播跟踪生成分析报告。 分析报告可以帮助您深入了解建议的更改的性能影响。

注意事项：

- 如果缺少一个或多个组件，则当你尝试生成新的分析报表（需要 internet 连接）时，会显示包含下载链接的 "先决条件" 页面。
- 若要查看在工具的早期版本中生成的报表，必须先更新该架构。

生成分析报告：

1. 在左侧菜单中，请参阅 "**分析报表**"。 连接到运行 SQL Server 存储报表数据库的计算机。 此时将显示服务器中所有报表的列表。 若要创建新报表，请选择 "**新建报表**"。

1. 输入或选择生成报表所需的信息：

   - **报表名称**：要创建的分析报表的名称。
   - **目标 1 SQL Server 的跟踪**：从目标1重播的跟踪文件的路径。
   - **目标 2 SQL Server 的跟踪**：在目标2上重播的跟踪文件的路径。

1. 选择 "**启动**" 以生成报表。 新报表将显示在列表的顶部。 生成报表后，该报表旁边的图标变为绿色复选标记。

现在，查看分析报告以获取 A/B 测试提供的见解。

有关分析报告的常见问题，请参阅[分析常见问题解答](database-experimentation-assistant-create-report.md#frequently-asked-questions-about-analysis-reports)。

### <a name="analysis-report"></a>分析报告

在报表的第一页上，将显示运行实验的目标服务器的版本和生成信息。 您可以使用阈值调整 A/B 测试分析的灵敏度或容差。 默认情况下，阈值设置为5%。 大于或等于5% 的性能改进会分类为已**改进**。 选择下拉菜单中的选项，以便使用不同的性能阈值来评估报表。

![阈值](https://msdnshared.blob.core.windows.net/media/2017/03/threshold.jpg)

两个饼图演示了工作负荷的两个目标服务器之间的差异的性能影响。 左图基于执行计数。 右图基于不同查询。 有五种可能的类别：

- **改进**：从统计的角度来来，查询在目标2上运行得比在目标1上更好。
- **降级**：统计，查询在目标2上运行的比目标1更糟。
- **相同**：目标1和目标2之间的查询没有统计差异。
- **无法计算**：查询的样本大小太小，无法进行统计分析。 对于 A/B 测试分析，DEA 要求执行相同的查询，才能在每个目标上至少执行30次。
- **错误**：查询在一个目标上至少误码一次。

![饼图](./media/database-experimentation-assistant-get-started/dea-get-started-piechart.png)

选择要向下钻取到特定类别的切片并获取性能指标，其中包括 "**无法评估**饼图扇区"。

"性能更改" 类别的深化页面显示该类别中的查询列表。 **错误**页包含三个选项卡：

- **新错误**：出现在目标2上但在目标1上不存在的错误。
- **现有错误**：在目标1和目标2上出现的错误。
- **已解决的错误**：出现在目标1上但在目标2上未出现的错误。

   ![错误页](./media/database-experimentation-assistant-get-started/dea-get-started-errorpage.png)

选择一个查询以前往该查询的**比较摘要**页。

"**比较摘要**" 页显示该查询的摘要统计信息。 该摘要包括执行次数、平均持续时间、平均 CPU、平均读取/写入次数和错误计数。

![摘要统计信息](./media/database-experimentation-assistant-get-started/dea-get-started-summarystats.png)

如果查询是错误查询，则 "**错误信息**" 选项卡将显示有关错误的详细信息。 "**查询计划信息**" 选项卡显示有关在目标1和目标2上用于查询的查询计划的信息。

![查询计划](./media/database-experimentation-assistant-get-started/dea-get-started-queryplan.png)

在分析报表的任何页上，选择右上方的 "**打印**" 按钮以打印所有可见内容。

## <a name="next-steps"></a>后续步骤

- 若要了解如何生成具有在服务器上发生的事件日志的跟踪文件，请参阅[捕获跟踪](database-experimentation-assistant-capture-trace.md)。

- 有关 DEA 和演示的19分钟简介，请观看以下视频：

  > [!VIDEO https://channel9.msdn.com/Shows/Data-Exposed/Introducing-the-Database-Experimentation-Assistant/player]
