---
title: 开始使用数据库实验助手进行 SQL Server 升级
description: 开始使用数据库实验助手
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
manager: craigg
ms.openlocfilehash: 45cd72d4383b0bae756b7b8f59502c981dfd6622
ms.sourcegitcommit: 45a9d7ffc99502c73f08cb937cbe9e89d9412397
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/22/2019
ms.locfileid: "66015127"
---
# <a name="get-started-with-database-experimentation-assistant"></a>开始使用数据库实验助手

数据库实验助手 (DEA) 是 A / B 测试解决方案的更改在 SQL Server 环境中，例如升级或新的索引。 DEA 可帮助你评估源服务器 （在当前环境） 中的工作负荷将如何在新环境中执行。 DEA 将引导您完成运行 A / B 测试通过完成三个步骤： 

- 捕获
- 重播
- 分析

本文指导完成这些步骤。

## <a name="capture"></a>捕获

第一步的 SQL Server A / B 测试是捕获源服务器上的跟踪。 源服务器通常是生产服务器。 跟踪文件捕获该服务器，包括时间戳的整个查询工作负荷。 更高版本，此跟踪重播分析在目标服务器上。 分析报表提供了两个目标服务器之间的差异中的工作负荷性能的见解。

注意事项：

- 在开始跟踪捕获之前，请确保备份您要从中捕获跟踪的数据库。
- DEA 用户必须配置为使用 Windows 身份验证连接到数据库。
- SQL Server 服务帐户需要访问源跟踪文件路径。

若要捕获的跟踪源服务器上：

1. 在 DEA，转到**所有捕获**在左侧菜单中选择照相机图标。

   ![左侧的导航菜单](./media/database-experimentation-assistant-get-started/dea-get-started-leftnav.png)

1. 输入或选择以下信息：

   - **跟踪名称**:要创建新的跟踪文件的文件名。 避免使用滚动更新文件命名约定，例如，CaptureName 跟踪名称\_NNN。
   - **持续时间**:捕获持续时间。
   - **SQL Server 实例名称**:想要捕获的跟踪的 SQL Server 实例。
   - **数据库名称**:运行 SQL Server 的计算机上的数据库的名称要捕获的跟踪。 如果为空，则从服务器上的所有数据库捕获跟踪。
   - **用于存储 SQL Server 计算机上的源跟踪文件路径**:你想要保存跟踪文件文件夹路径。

1. 请确保备份目标数据库。 然后，选择数据库复选框。
1. 选择**启动**来启动捕获。

您可以查看您捕获，包括开始时间、 持续时间，以及剩余时间的进度。 等待完成此捕获时，您还可以启动新的捕获。 完成捕获后，使用输出跟踪文件启动第二个阶段： 重播跟踪文件在目标服务器上的。

有关跟踪捕获的常见问题，请参阅[捕获常见问题](database-experimentation-assistant-capture-trace.md#frequently-asked-questions-about-trace-capture)。

## <a name="replay"></a>重播

第二个步骤的 SQL Server A / B 测试是若要重播的跟踪文件中捕获到目标服务器。 然后，从分析重播收集大量的跟踪。 

重播跟踪文件在两个目标服务器上： 一个，以模拟你的源服务器 (Target 1)，另一个，以模拟你建议的更改 (目标 2)。 目标 1 和目标 2 的硬件配置应尽可能类似，因此 SQL Server 可以准确地分析建议的更改对性能产生影响。

注意事项：

- 若要运行重播，计算机必须进行设置以运行分布式重播 (DReplay) 跟踪。 有关详细信息，请参阅[Distributed Replay 控制器和客户端安装程序](https://blogs.msdn.microsoft.com/datamigration/distributed-replay-controller-and-client-setup/)。
- 请确保在目标服务器上使用的源服务器从备份还原数据库。
- 在 SQL Server 中查询缓存可能会影响评估结果。 我们建议在服务应用程序，以提高一致性评估结果中的重新启动 SQL Server 服务 (MSSQLSERVER)。

若要重播跟踪文件：

1. 在 DEA，选择在左侧菜单中，转到播放图标**所有重播**。 如果任何，出现在会话期间运行的过去重播的列表。 若要启动新的重播，选择**新重播**。

1. 输入或选择以下信息：

   - **重播名称**:重播跟踪的文件名称。
   - **控制器计算机的名称**:Distributed Replay 控制器计算机的名称。
   - **在控制器上的源跟踪文件的路径**:中的源跟踪文件的文件路径[捕获](#capture)。
   - **SQL Server 实例名称**:在其重播跟踪源上的 SQL Server 实例的名称。
   - **用于存储 SQL Server 计算机上的目标跟踪文件路径**:生成重播跟踪文件的文件夹路径。

1. 选择该复选框可以将备份还原的第一步。

1. 选择**启动**若要启动重播。 

可以查看在重播的状态。 重播源跟踪在这两个目标服务器上的后，就可以用于生成分析报告。

有关重播的常见问题，请参阅[重播常见问题解答](database-experimentation-assistant-replay-trace.md#frequently-asked-questions-about-trace-replay)。

## <a name="analysis"></a>分析

最后一步是使用来生成分析报告，重播跟踪。 分析报表可以帮助您深入了解所建议的更改的性能影响。

注意事项：

- 如果缺少一个或多个组件，系统必备组件页面包含一个有关下载链接将显示当你尝试生成新的分析报告 （需要 internet 连接） 时。
- 若要查看该工具的早期版本中生成的报表，必须先更新架构。

若要生成的分析报表：

1. 在左侧菜单中，转到**分析报表**。 连接到运行你在其中存储报表数据库的 SQL Server 的计算机。 将显示在服务器中的所有报表的列表。 若要创建新的报表，请选择**新的报表**。

1. 输入或选择生成报表所需的信息：

   - **报表名称**:要创建的分析报表的名称。
   - **目标 1 SQL Server 的跟踪**:从目标 1 上重播跟踪文件的路径。
   - **目标 2 SQL Server 的跟踪**:从目标 2 上重播跟踪文件的路径。

1. 选择**启动**生成报表。 新的报表显示在列表的顶部。 生成报告，该报表旁边的图标将变为绿色复选标记。

现在，查看分析报告，以获得您的提供的见解 / B 测试。

分析报表有关的常见问题，请参阅[分析常见问题](database-experimentation-assistant-create-report.md#frequently-asked-questions-about-analysis-reports)。

### <a name="analysis-report"></a>分析报告

在报表的第一页，会显示在其运行该实验的目标服务器的版本和生成信息。 可用阈值来调整敏感度或容差为 A / B 测试分析。 默认情况下，阈值设置为 5%。 很多或等于 5%的性能有任何改进是否属于**改进了**。 若要使用不同的性能阈值评估报表的下拉列表菜单中选择选项。

![阈值](https://msdnshared.blob.core.windows.net/media/2017/03/threshold.jpg)

两个饼图演示工作负荷的两个目标服务器之间的差异的性能影响。 左侧的图表根据执行计数。 不同查询所需的图表为基础。 有五个可能类别：

- **改进了**:据统计，查询在比目标 1 上的目标 2 上运行更好。
- **降级**:据统计，查询可运行更糟的是比目标 1 上的目标 2 上。
- **同一**:没有任何查询目标 1 与目标 2 之间的统计差异。
- **无法计算**:查询的示例大小是进行统计分析太小。 对于 A / B 测试分析，DEA 所需的每个目标上具有至少 30 次执行的相同查询。
- **错误**：出错的至少一次在其中一个目标查询。

![饼图](./media/database-experimentation-assistant-get-started/dea-get-started-piechart.png)

选择向下钻取到特定的类别并获取性能指标，包括一个切片**不能评估**饼图扇区。

性能的向下钻取页更改类别显示该类别中的查询的列表。 **错误**页具有三个选项卡：

- **新的错误**:出现目标 2 上但不是在目标 1 上的错误。
- **现有错误**:目标 1 和目标 2 出现的错误。
- **已解决的错误**:出现目标 1 上但不是在目标 2 的错误。

   ![错误页](./media/database-experimentation-assistant-get-started/dea-get-started-errorpage.png)

选择一个查询，若要转到**Comparison Summary**页为该查询。

**比较摘要**页显示为该查询的摘要统计信息。 摘要包括执行数量、 平均持续时间、 平均 CPU、 平均读取/写入和错误计数。

![摘要统计信息](./media/database-experimentation-assistant-get-started/dea-get-started-summarystats.png)

如果查询是错误查询中，**错误信息**选项卡显示有关错误的详细信息。 **查询计划信息**选项卡显示有关用于在目标 1 和目标 2 查询的查询计划的信息。

![查询计划](./media/database-experimentation-assistant-get-started/dea-get-started-queryplan.png)

在分析报表的任何页上，选择**打印**顶部的按钮打印权限的所有内容可见。

## <a name="next-steps"></a>后续步骤

- 若要了解如何生成具有在服务器上发生的事件日志的跟踪文件，请参阅[跟踪捕获](database-experimentation-assistant-capture-trace.md)。

- DEA 和演示的 19 分钟介绍，请观看以下视频：

  > [!VIDEO https://channel9.msdn.com/Shows/Data-Exposed/Introducing-the-Database-Experimentation-Assistant/player]
