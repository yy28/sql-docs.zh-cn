---
title: 查看 SQL Server 升级的分析报告
description: 在数据库实验助手中查看分析报表
ms.custom: seo-lt-2019
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
ms.openlocfilehash: fddc71bf7cdf7686154b4f9b5612cf671ca64fce
ms.sourcegitcommit: d00ba0b4696ef7dee31cd0b293a3f54a1beaf458
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/13/2019
ms.locfileid: "74056664"
---
# <a name="view-analysis-reports-in-database-experimentation-assistant"></a>在数据库实验助手中查看分析报表

在数据库实验助手（DEA）中[创建分析报表](database-experimentation-assistant-create-report.md)后，请完成本文中所述的步骤以查看报表并获得 A/B 测试提供的性能见解。

## <a name="select-a-server"></a>选择服务器

在 DEA 中，选择菜单图标。 在展开的菜单中，选择 "清单" 图标旁边的 "**分析报表**" 以打开 "分析报表" 窗口。

在 "**分析报表**" 下，输入运行包含分析数据库 SQL Server 的计算机的名称。 选择“连接”。 

![连接到现有报表](./media/database-experimentation-assistant-view-report/dea-view-report-connect.png)

如果缺少任何依赖项，则 "**先决条件**" 页将提示你提供用于安装这些依赖项的链接。 安装必备组件，然后选择 "**重试**"。

![必备页](./media/database-experimentation-assistant-view-report/dea-view-report-prereq.png)

## <a name="select-an-analysis-report-to-view"></a>选择要查看的分析报告

在分析报表列表中，双击报表将其打开。

![查看现有报表](./media/database-experimentation-assistant-view-report/dea-view-report-view-existing.png)

您可以深入了解工作负荷的表示方式，如以下示例图表所示：

![工作负荷代表图](./media/database-experimentation-assistant-view-report/dea-view-report-workload-compare.png)

## <a name="view-and-understand-the-analysis-report"></a>查看和了解分析报告

本部分将指导你完成分析报表。

### <a name="query-categories"></a>查询类别

选择左侧饼图的不同切片，以便仅显示属于该类别的查询。

![报表饼图切片](./media/database-experimentation-assistant-view-report/dea-view-report-pie-slices.png)

- **降级的查询**：比 B 中更好地执行的查询。  
- **错误**：在实例 B 中显示错误但在实例 A 中不存在的查询。  
- **改进的查询**：在实例 B 中运行得更好的查询，在实例 a 中运行。  
- 不**确定的查询**：性能更改不确定的查询。  
- **相同**：在实例 A 和 B 上性能保持相同的查询。

### <a name="individual-query-drill-down"></a>单个查询向下钻取

您可以选择 "查询模板" 链接以查看有关特定查询的更多详细信息。

![查询向下钻取](./media/database-experimentation-assistant-view-report/dea-view-report-drilldown.png)

选择特定查询以打开查询的比较摘要。

![比较摘要](./media/database-experimentation-assistant-view-report/dea-view-report-comparison-summary.png)

您可以看到运行查询的 A 和 B 实例。 你还可以查看查询的外观的模板。 表显示特定于实例 A 和 B 的查询信息。

### <a name="error-queries"></a>错误查询

"比较摘要" 报表包含可扩充的**错误信息**和**查询计划信息**部分。 部分显示了两个实例的错误和计划信息。

选择错误（红色）饼图以显示以下类型的错误：
- **现有错误**：中的错误。
- **新错误**： B 中的错误。
- **已解决的错误**：在中但不在 B 中的错误。

![错误图表](./media/database-experimentation-assistant-view-report/dea-view-report-error-charts.png)

## <a name="next-steps"></a>后续步骤

- 若要了解如何在命令提示符下生成分析报告，请参阅[在命令提示符下运行](database-experimentation-assistant-run-command-prompt.md)。

- 有关 DEA 和演示的19分钟简介，请观看以下视频：

  > [!VIDEO https://channel9.msdn.com/Shows/Data-Exposed/Introducing-the-Database-Experimentation-Assistant/player]
