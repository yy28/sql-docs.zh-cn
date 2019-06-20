---
title: 数据库实验助手中面向 SQL Server 升级查看分析报告
description: 查看分析报告中数据库实验助手
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
manager: jroth
ms.openlocfilehash: da99a24ab6729e78220aeed3d18819e7b075603f
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/15/2019
ms.locfileid: "66794439"
---
# <a name="view-analysis-reports-in-database-experimentation-assistant"></a>查看分析报告中数据库实验助手

检查完[创建分析报表](database-experimentation-assistant-create-report.md)中数据库实验助手 (DEA) 完成在查看报表和获取性能见解提供您的这篇文章中所述的步骤 / B 测试。

## <a name="select-a-server"></a>选择一个服务器

在 DEA，选择菜单图标。 在展开的菜单中，选择**分析报表**旁边清单图标以打开分析报告窗口。

下**分析报表**，输入运行了分析的数据库的 SQL Server 的计算机的名称。 选择“连接”  。 

![连接到现有报表](./media/database-experimentation-assistant-view-report/dea-view-report-connect.png)

如果您遗漏了任何依赖项**先决条件**页面提示你安装它们的链接。 安装必备组件，并选择**再试一次**。

![先决条件页](./media/database-experimentation-assistant-view-report/dea-view-report-prereq.png)

## <a name="select-an-analysis-report-to-view"></a>选择要查看分析报告

在的分析报告列表中，双击一个报表以打开它。

![查看现有报表](./media/database-experimentation-assistant-view-report/dea-view-report-view-existing.png)

您可以深入程度表示你的工作负荷，在此示例图中所示：

![工作负荷 Rep 图表](./media/database-experimentation-assistant-view-report/dea-view-report-workload-compare.png)

## <a name="view-and-understand-the-analysis-report"></a>查看并了解分析报表

本节将指导你通过分析报表。

### <a name="query-categories"></a>查询类别

选择左侧饼图以显示仅属于该类别的查询的不同切片。

![报表饼图扇区](./media/database-experimentation-assistant-view-report/dea-view-report-pie-slices.png)

- **降级的查询**:A 比 b 中的更好地执行查询  
- **错误**:查询错误显示在实例 B 但不是在实例 a。  
- **改进了查询**:A.实例中运行更好地与实例 B 中的查询  
- **不确定查询**:更改查询的不确定的性能。  
- **同一**:查询中的性能条件不变跨实例 A 和 b。

### <a name="individual-query-drill-down"></a>单个查询向下钻取

您可以选择以查看有关特定查询的更多详细的信息的查询模板链接。

![查询向下钻取](./media/database-experimentation-assistant-view-report/dea-view-report-drilldown.png)

选择特定的查询，以打开摘要查询的比较。

![比较摘要](./media/database-experimentation-assistant-view-report/dea-view-report-comparison-summary.png)

您可以看到 A 和 B 实例运行的查询。 此外可以查看的查询可能如下所示的模板。 显示一个表，查询信息特定于实例 A 和 b。

### <a name="error-queries"></a>错误的查询

比较摘要报表具有可扩展**错误信息**并**查询计划信息**部分。 部分显示错误，并计划为两个实例的信息。

选择错误 （红色） 饼图显示这些类型的错误：
- **现有错误**:A.中的错误
- **新的错误**:B.中的错误
- **已解决的错误**:已在一个但不是在 B.错误

![错误图表](./media/database-experimentation-assistant-view-report/dea-view-report-error-charts.png)

## <a name="next-steps"></a>后续步骤

- 若要了解如何生成分析报告，在命令提示符下，请参阅[在命令提示符下运行](database-experimentation-assistant-run-command-prompt.md)。

- DEA 和演示的 19 分钟介绍，请观看以下视频：

  > [!VIDEO https://channel9.msdn.com/Shows/Data-Exposed/Introducing-the-Database-Experimentation-Assistant/player]
