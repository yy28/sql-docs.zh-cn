---
title: 教程：启用五个最慢查询示例小组件
titleSuffix: Azure Data Studio
description: 本教程演示如何在数据库仪表板上启用五个最慢查询示例小组件。
ms.prod: sql
ms.technology: azure-data-studio
ms.topic: tutorial
author: markingmyname
ms.author: maghan
ms.reviewer: alayu; sstein
ms.custom: seodec18
ms.date: 09/24/2018
ms.openlocfilehash: 5c94d2cf8b80ad7724cc1f710dc67d3f4a13c59e
ms.sourcegitcommit: db9bed6214f9dca82dccb4ccd4a2417c62e4f1bd
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/25/2019
ms.locfileid: "67959068"
---
# <a name="tutorial-add-the-five-slowest-queries-sample-widget-to-the-database-dashboard"></a>教程：将*五个最慢查询*示例小组件添加到数据库仪表板

本教程演示了将 [!INCLUDE[name-sos](../includes/name-sos-short.md)] 内置示例小组件之一添加到*数据库仪表板*以快速查看数据库的五个最慢查询的过程。 你还将学习如何使用 [!INCLUDE[name-sos](../includes/name-sos-short.md)] 的功能查看慢速查询和查询计划的详细信息。 在本教程中，你将学习如何执行以下操作：

> [!div class="checklist"]
> * 在数据库上启用查询存储
> * 向数据库仪表板添加预生成的见解小组件
> * 查看有关数据库最慢查询的详细信息
> * 查看慢速查询的查询执行计划

[!INCLUDE[name-sos](../includes/name-sos-short.md)] 包含几个现成的见解小组件。 本教程介绍如何添加 *query-data-store-db-insight* 小组件，但所有小组件的添加步骤都基本相同。

## <a name="prerequisites"></a>必备条件

本教程需要 SQL Server 或 Azure SQL 数据库 *TutorialDB*。 若要创建 *TutorialDB* 数据库，请完成以下快速入门之一：

- [使用 [!INCLUDE[name-sos-short](../includes/name-sos-short.md)] 连接并查询 SQL Server](quickstart-sql-server.md)
- [使用 [!INCLUDE[name-sos-short](../includes/name-sos-short.md)] 连接并查询 Azure SQL 数据库](quickstart-sql-database.md)



## <a name="turn-on-query-store-for-your-database"></a>为数据库启用查询存储

本示例中的小组件需要启用*查询存储*。

1. 右键单击“TutorialDB”数据库（在“服务器”侧栏中），然后选择“新建查询”    。
2. 在查询编辑器中粘贴以下 Transact-SQL (T-SQL) 语句，然后单击“运行”  ：

   ```sql
    ALTER DATABASE TutorialDB SET QUERY_STORE = ON
   ```

## <a name="add-the-slow-queries-widget-to-your-database-dashboard"></a>将慢速查询小组件添加到数据库仪表板

若要将*慢速查询小组件*添加到仪表板，请编辑*用户设置*文件中的 *dashboard.database.widgets* 设置。

1. 按“Ctrl+Shift+P”打开“命令面板”，以打开“用户设置”    。
2. 在搜索框中键入“设置”，然后选择“首选项:打开用户设置”   。

   ![打开用户设置命令](./media/tutorial-qds-sql-server/open-user-settings.png)

2. 在设置搜索框中键入“仪表板”，然后找到“dashboard.database.widgets”   。

   ![搜索设置](./media/tutorial-qds-sql-server/search-settings.png)

3. 若要自定义“dashboard.database.widgets”设置，需编辑“用户设置”部分（右侧列）中的“dashboard.database.widgets”条目    。 如果“用户设置”部分中没有“dashboard.database.widgets”，请将鼠标悬停在“默认设置”列中的“dashboard.database.widgets”文本上，单击显示在文本左侧的铅笔图标，然后单击“复制到设置”     。 如果弹出窗口显示“在设置中替换”，请勿单击它  ！ 转到右侧的“用户设置”列，找到“dashboard.database.widgets”部分，然后进入下一步   。

4. 在“dashboard.database.widgets”部分中，添加以下内容  ：

   ```json
        {
            "name": "slow queries widget",
            "gridItemConfig": {
                "sizex": 2,
                "sizey": 1
            },
            "widget": {
                "query-data-store-db-insight": null
            }
        },
    ```

1. 如果这是第一次添加新的小组件，“dashboard.database.widgets”部分应如下所示  ：

   ```json
   "dashboard.database.widgets": [
       {
           "name": "slow queries widget",
           "gridItemConfig": {
               "sizex": 2,
               "sizey": 1
           },
           "widget": {
               "query-data-store-db-insight": null
           }
       },
       {
           "name": "Tasks",
           "gridItemConfig": {
               "sizex": 1,
               "sizey": 1
           },
           "widget": {
               "tasks-widget": {}
           }
       },
       {
           "gridItemConfig": {
               "sizex": 1,
               "sizey": 2
           },
           "widget": {
               "explorer-widget": {}
           }
       }
   ]
   ```

1. 按“Ctrl+S”保存修改后的“用户设置”   。

6. 通过导航到“服务器”侧栏中的“TutorialDB”打开*数据库仪表板*，右键单击并选择“管理”    。

   ![打开仪表板](./media/tutorial-qds-sql-server/insight-open-dashboard.png)

7. 见解小组件显示在仪表板上： 

   ![QDS 小组件](./media/tutorial-qds-sql-server/insight-qds-result.png)


## <a name="view-insight-details-for-more-information"></a>查看见解详细信息以了解更多信息

1. 若要查看见解小组件的其他信息，请单击右上角的省略号 ( **...** )，然后选择“显示详细信息”  。
2. 若要显示某个项目的更多详细信息，请选择“图表数据”列表中的任意项目  。

   ![见解详细信息对话框](./media/tutorial-qds-sql-server/insight-details-dialog.png)

3. 右键单击“项目详细信息”中“query_sql_txt”右侧的单元格，然后单击“复制单元格”    。

4. 关闭“见解”窗格  。

## <a name="view-the-query-plan"></a>查看查询计划 

1. 按“Ctrl+N”打开新的查询编辑器  。

2. 将前面步骤中的查询文本粘贴到编辑器中。

3. 单击“说明”  。

   ![见解 QDS 说明](./media/tutorial-qds-sql-server/insight-qds-explain.png)

4. 查看查询的执行计划：

   ![显示计划 (Showplan)](./media/tutorial-qds-sql-server/showplan.png)

## <a name="save-and-open-a-query-plan"></a>保存并打开查询计划 

1. 打开见解详细信息对话框。
2. 选择其中一个查询项。
2. 右键单击“query_plan”值，选择“复制单元格”  

   ![见解 QDS 计划](./media/tutorial-qds-sql-server/insight-qds-plan.png)

3. 按“Ctrl+N”打开新的编辑器  。

4. 将复制的计划粘贴到编辑器中。

5. 按“Ctrl+S”保存文件，并将文件扩展名更改为 *.sqlplan*  。 *.sqlplan* 不会出现在文件扩展名下拉列表中，因此直接键入即可。 在本教程中，将文件命名为 *slowquery.sqlplan*。

6. 查询计划在 [!INCLUDE[name-sos](../includes/name-sos-short.md)] 的查询计划查看器中打开：

   ![见解 QDS 计划](./media/tutorial-qds-sql-server/sqlplan.png)


## <a name="next-steps"></a>后续步骤
在本教程中，你已学习如何执行以下操作：
> [!div class="checklist"]
> * 在数据库上启用查询存储
> * 向数据库仪表板添加见解小组件
> * 查看有关数据库最慢查询的详细信息
> * 查看慢速查询的查询执行计划


若要了解如何启用“表空间使用情况”示例见解，请完成下一教程  ：

> [!div class="nextstepaction"]
> [启用表空间示例见解小组件](tutorial-table-space-sql-server.md)
