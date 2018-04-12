---
title: 教程： 启用表空间使用情况示例见解小组件，在 SQL Operations Studio (preview) |Microsoft 文档
description: 本教程演示如何启用表空间使用情况示例见解小组件，在 SQL Operations Studio (preview) 数据库仪表板。
ms.custom: tools|sos
ms.date: 03/19/2018
ms.prod: sql-non-specified
ms.reviewer: alayu; erickang; sstein
ms.suite: sql
ms.prod_service: sql-tools
ms.component: sos
ms.tgt_pltfrm: ''
ms.topic: tutorial
author: erickangMSFT
ms.author: erickang
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 09a1ebe6fda1baf546923887f28b51d416a80b59
ms.sourcegitcommit: 6bd21109abedf64445bdb3478eea5aaa7553fa46
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/20/2018
---
# <a name="tutorial-enable-the-table-space-usage-sample-insight-widget-using-includename-sosincludesname-sos-shortmd"></a>教程： 启用表空间使用使用情况示例见解小组件 [!INCLUDE[name-sos](../includes/name-sos-short.md)]

本教程演示如何启用数据库中的所有表中提供的空间使用情况有关的一览式视图的数据库仪表板见解小组件。 在本教程中，你学习如何：

> [!div class="checklist"]
> * 快速开启使用内置的见解小组件示例见解小组件
> * 查看表空间使用情况的详细信息
> * 筛选数据，并在见解图表上查看标签的详细信息

## <a name="prerequisites"></a>必要條件

本教程需要安装 SQL Server 或 Azure SQL 数据库*TutorialDB*。 若要创建*TutorialDB*数据库，请完成以下快速入门之一：

- [连接和查询 SQL Server 使用 [!INCLUDE[name-sos-short](../includes/name-sos-short.md)]](quickstart-sql-server.md)
- [连接和查询使用 Azure SQL 数据库 [!INCLUDE[name-sos-short](../includes/name-sos-short.md)]](quickstart-sql-database.md)


## <a name="turn-on-a-management-insight-on-includename-sosincludesname-sos-shortmds-database-dashboard"></a>开启的管理见解[!INCLUDE[name-sos](../includes/name-sos-short.md)]的数据库仪表板
[!INCLUDE[name-sos](../includes/name-sos-short.md)] 具有内置示例小组件监视数据库的表中所用的空间。

1. 打开*用户设置*按**Ctrl + Shift + P**以打开*命令控制板*。
2. 类型*设置*在搜索框中，选择**首选项： 打开用户设置**。
2. 类型*仪表板*中设置搜索输入框中，找到**dashboard.database.widgets**。

3. 若要自定义**dashboard.database.widgets**需要编辑的设置**dashboard.database.widgets**中的条目**用户设置**部分 (中的列右侧）。 如果没有任何**dashboard.database.widgets**中**用户设置**部分中，将鼠标悬停在**dashboard.database.widgets**默认设置列和单击中的文本显示该文本，然后单击左侧的铅笔图标**复制到设置**。 如果弹出的窗口中显示**在设置中替换**，而不是单击 ！ 转到**用户设置**列添加到右侧并找到**dashboard.database.widgets**部分，并前进到下一步。

4. 在**dashboard.database.widgets**部分中，添加以下：

   ```json
        {
            "name": "Space Used by Tables",
            "gridItemConfig": {
                "sizex": 2,
                "sizey": 1
            },
            "widget": {
                "table-space-db-insight": null
            }
        },
    ```
**Dashboard.database.widgets**部分应类似于以下映像：

   ![搜索设置](./media/tutorial-table-space-sql-server/insight-table-space.png)

5. 按**Ctrl + S**以保存设置。

6. 通过右键单击打开的数据库仪表板**TutorialDB**单击**管理**。

7. 视图*表空间*见解小组件在下图中所示： 

   ![小组件](./media/tutorial-table-space-sql-server/insight-table-space-result.png)


## <a name="working-with-the-insight-chart"></a>使用见解图表

[!INCLUDE[name-sos](../includes/name-sos-short.md)]见解图表提供筛选和鼠标悬停时的详细信息。 若要尝试以下步骤：

1. 单击并切换*row_count*图表上的图例。 [!INCLUDE[name-sos](../includes/name-sos-short.md)] 显示和隐藏数据序列，如打开或关闭切换图例。
    
2. 鼠标指针悬停在图表中。 [!INCLUDE[name-sos](../includes/name-sos-short.md)] 显示有关数据序列标签以及其值，如下面的屏幕截图中所示的详细信息。

   ![图表切换和图例](./media/tutorial-table-space-sql-server/insight-table-space-toggle.png)


## <a name="next-steps"></a>后续步骤
在本教程中，您学习了如何：
> [!div class="checklist"]
> * 快速开启使用内置的见解小组件示例见解小组件。
> * 查看表空间使用情况的详细信息。
> * 筛选数据，并在见解图表上查看标签的详细信息

若要了解如何构建自定义见解小组件，请完成下一教程：

> [!div class="nextstepaction"]
> [生成自定义见解小组件](tutorial-build-custom-insight-sql-server.md)。