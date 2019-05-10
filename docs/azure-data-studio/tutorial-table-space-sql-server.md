---
title: 教程：启用表空间使用情况示例见解小组件
titleSuffix: Azure Data Studio
description: 本教程演示如何启用表空间使用情况示例见解小组件，在 Azure Data Studio 数据库仪表板。
ms.prod: sql
ms.technology: azure-data-studio
ms.topic: tutorial
author: markingmyname
ms.author: maghan
manager: craigg
ms.reviewer: alayu; sstein
ms.custom: seodec18
ms.date: 09/24/2018
ms.openlocfilehash: 6594aea6a618e2b9c4bd28368462f85c94a5ff0a
ms.sourcegitcommit: bb5484b08f2aed3319a7c9f6b32d26cff5591dae
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/06/2019
ms.locfileid: "65089671"
---
# <a name="tutorial-enable-the-table-space-usage-sample-insight-widget-using-includename-sosincludesname-sos-shortmd"></a>教程：启用表空间使用情况示例见解小组件使用 [!INCLUDE[name-sos](../includes/name-sos-short.md)]

本教程演示如何能够在数据库仪表板，提供数据库中的所有表有关的空间使用情况的一眼视图见解小组件。 在本教程中，你了解如何：

> [!div class="checklist"]
> * 快速开启使用内置的见解小组件示例见解小组件
> * 查看表空间使用情况的详细信息
> * 筛选数据和见解图表上查看标签的详细信息

## <a name="prerequisites"></a>必要條件

本教程需要安装 SQL Server 或 Azure SQL 数据库*TutorialDB*。 若要创建*TutorialDB*数据库，请完成以下快速入门之一：

- [使用 SQL Server 连接和查询 [!INCLUDE[name-sos-short](../includes/name-sos-short.md)]](quickstart-sql-server.md)
- [Azure SQL 数据库使用连接和查询 [!INCLUDE[name-sos-short](../includes/name-sos-short.md)]](quickstart-sql-database.md)


## <a name="turn-on-a-management-insight-on-includename-sosincludesname-sos-shortmds-database-dashboard"></a>在管理见解上开启[!INCLUDE[name-sos](../includes/name-sos-short.md)]的数据库仪表板
[!INCLUDE[name-sos](../includes/name-sos-short.md)] 具有内置的示例小组件来监视数据库的表中使用的空间。

1. 打开*用户设置*通过按**Ctrl + Shift + P**以打开*命令面板*。
2. 类型*设置*在搜索框中，选择**首选项：打开用户设置**。
2. 类型*仪表板*中设置搜索输入框，找到**dashboard.database.widgets**。

3. 若要自定义**dashboard.database.widgets**设置，需要编辑**dashboard.database.widgets**中的条目**用户设置**部分 (中的列右侧）。 如果没有任何**dashboard.database.widgets**中**用户设置**部分中，将鼠标悬停**dashboard.database.widgets**中默认设置列并单击文本显示的文本并单击左侧的铅笔图标**复制到设置**。 如果弹出窗口中显示**替换为在设置**，不要单击它 ！ 转到**用户设置**右侧的列并找到**dashboard.database.widgets**部分并转到下一步。

4. 在中**dashboard.database.widgets**部分中，添加以下：

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

6. 通过右键单击打开的数据库仪表板**TutorialDB**然后单击**管理**。

7. 视图*表空间*见解小组件在下图中所示： 

   ![小组件](./media/tutorial-table-space-sql-server/insight-table-space-result.png)


## <a name="working-with-the-insight-chart"></a>使用见解图表

[!INCLUDE[name-sos](../includes/name-sos-short.md)]见解图表提供了筛选和鼠标悬停时的详细信息。 若要尝试以下步骤：

1. 单击，然后切换*row_count*图表上的图例。 [!INCLUDE[name-sos](../includes/name-sos-short.md)] 显示和隐藏数据序列，如打开或关闭切换图例。
    
2. 鼠标指针悬停在图表中。 [!INCLUDE[name-sos](../includes/name-sos-short.md)] 显示有关数据序列标签和其值如以下屏幕截图中所示的详细信息。

   ![图表切换和图例](./media/tutorial-table-space-sql-server/insight-table-space-toggle.png)


## <a name="next-steps"></a>后续步骤
在本教程中，你将了解：
> [!div class="checklist"]
> * 快速启用使用内置的见解小组件示例见解小组件。
> * 查看表空间使用情况的详细信息。
> * 筛选数据和见解图表上查看标签的详细信息

若要了解如何构建自定义见解小组件，完成下一教程：

> [!div class="nextstepaction"]
> [生成自定义见解小组件](tutorial-build-custom-insight-sql-server.md)。
