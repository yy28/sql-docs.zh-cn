---
title: 教程： 启用五个最慢的查询示例小组件的 SQL 操作 Studio （预览版） |Microsoft 文档
description: 本教程演示如何启用五个最慢的查询示例上的小组件数据库仪表板。
ms.custom: tools|sos
ms.date: 03/15/2018
ms.prod: sql
ms.reviewer: alayu; erickang; sstein
ms.suite: sql
ms.prod_service: sql-tools
ms.component: sos
ms.tgt_pltfrm: ''
ms.topic: tutorial
author: erickangMSFT
ms.author: erickang
manager: craigg
ms.openlocfilehash: d06bd752b0cdd07d87d8e5816a74d6e2d43d31ef
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
---
# <a name="tutorial-add-the-five-slowest-queries-sample-widget-to-the-database-dashboard"></a>教程： 添加*五个最慢的查询*示例小组件设为数据库仪表板

本教程演示的过程将其中一个添加[!INCLUDE[name-sos](../includes/name-sos-short.md)]的内置示例小组件到*数据库仪表板*可以快速查看数据库的五个最慢查询。 你还了解了如何查看速度慢的查询的详细信息和查询计划使用[!INCLUDE[name-sos](../includes/name-sos-short.md)]的功能。 在本教程中，你学习如何：

> [!div class="checklist"]
> * 在数据库上启用 Query Store
> * 将预建的见解小组件添加到数据库仪表板
> * 查看有关数据库的速度最慢的查询详细信息
> * 查看速度慢的查询的查询执行计划

[!INCLUDE[name-sos](../includes/name-sos-short.md)] 包括几个见解小组件的-现成。 本教程演示如何将添加*查询的数据的存储区-db-见解*小组件中，但步骤是基本上相同的添加任何小组件。

## <a name="prerequisites"></a>必要條件

本教程需要安装 SQL Server 或 Azure SQL 数据库*TutorialDB*。 若要创建*TutorialDB*数据库，请完成以下快速入门之一：

- [连接和查询 SQL Server 使用 [!INCLUDE[name-sos-short](../includes/name-sos-short.md)]](quickstart-sql-server.md)
- [连接和查询使用 Azure SQL 数据库 [!INCLUDE[name-sos-short](../includes/name-sos-short.md)]](quickstart-sql-database.md)



## <a name="turn-on-query-store-for-your-database"></a>为你的数据库启用 Query Store

在此示例中的小组件需要*Query Store*启用。

1. 右键单击**TutorialDB**数据库 (在**服务器**侧栏)，然后选择**新查询**。
2. 在查询编辑器中，粘贴以下 TRANSACT-SQL (T-SQL) 语句，然后单击**运行**:

   ```sql
    ALTER DATABASE TutorialDB SET QUERY_STORE = ON
   ```

## <a name="add-the-slow-queries-widget-to-your-database-dashboard"></a>将速度慢的查询小组件添加到你的数据库仪表板

若要添加*缓慢查询小组件*到仪表板，编辑*dashboard.database.widgets*中设置你*用户设置*文件。

1. 打开*用户设置*按**Ctrl + Shift + P**以打开*命令控制板*。
2. 类型*设置*在搜索框中，选择**首选项： 打开用户设置**。

   ![打开用户设置命令](./media/tutorial-qds-sql-server/open-user-settings.png)

2. 类型*仪表板*中设置搜索框中，找到**dashboard.database.widgets**。

   ![搜索设置](./media/tutorial-qds-sql-server/search-settings.png)

3. 若要自定义**dashboard.database.widgets**需要编辑的设置**dashboard.database.widgets**中的条目**用户设置**部分 (中的列右侧）。 如果没有任何**dashboard.database.widgets**中**用户设置**部分中，将鼠标悬停在**dashboard.database.widgets**默认设置列和单击中的文本显示该文本，然后单击左侧的铅笔图标**复制到设置**。 如果弹出的窗口中显示**在设置中替换**，而不是单击 ！ 转到**用户设置**列添加到右侧并找到**dashboard.database.widgets**部分，并前进到下一步。

4. 在**dashboard.database.widgets**部分中，添加以下：

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

1. 如果这是添加新的小组件中，第一次**dashboard.database.widgets**部分应类似于此：

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

1. 按**Ctrl + S**以保存已修改**用户设置**。

6. 打开*数据库仪表板*通过导航到**TutorialDB**中**服务器**栏中，右键单击，并选择**管理**。

   ![打开仪表板](./media/tutorial-qds-sql-server/insight-open-dashboard.png)

7. 在仪表板上显示见解小组件： 

   ![QDS 小组件](./media/tutorial-qds-sql-server/insight-qds-result.png)


## <a name="view-insight-details-for-more-information"></a>有关详细信息视图了解详细信息

1. 若要查看见解小组件的其他信息，请单击省略号 (**...**) 正确，然后选择右上**显示详细信息**。
2. 若要显示的项的更多详细信息，请选择中的任意项**图表数据**列表。

   ![了解详细信息对话框](./media/tutorial-qds-sql-server/insight-details-dialog.png)

3. 右键单击右侧的单元格**query_sql_txt**中**项详细信息**单击**复制单元格**。

4. 关闭**Insights**窗格。

## <a name="view-the-query-plan"></a>查看查询计划 

1. 打开一个新的查询编辑器按**Ctrl + N**。

2. 将前面步骤中的查询文本粘贴到编辑器。

3. 单击**解释**。

   ![见解 QDS 说明](./media/tutorial-qds-sql-server/insight-qds-explain.png)

4. 查看查询的执行计划：

   ![显示计划 (Showplan)](./media/tutorial-qds-sql-server/showplan.png)

## <a name="save-and-open-a-query-plan"></a>保存并打开查询计划 

1. 打开了解详细信息对话框中。
2. 选择某一查询项。
2. 右键单击**query_plan**值，然后选择**复制单元格**

   ![Insights QDS 计划](./media/tutorial-qds-sql-server/insight-qds-plan.png)

3. 按**Ctrl + N**以打开新的编辑器。

4. 粘贴到编辑器中复制的计划。

5. 按**Ctrl + S**保存该文件，并更改文件扩展名为 *.s q l*。 *.s q l*未出现在文件扩展名下拉列表中，因此只需键入中。 为本教程中，命名该文件*slowquery.sqlplan*。

6. 在中打开查询计划[!INCLUDE[name-sos](../includes/name-sos-short.md)]的查询计划查看器：

   ![Insights QDS 计划](./media/tutorial-qds-sql-server/sqlplan.png)


## <a name="next-steps"></a>后续步骤
在本教程中，您学习了如何：
> [!div class="checklist"]
> * 在数据库上启用 Query Store
> * 将见解小组件添加到数据库仪表板
> * 查看有关数据库的速度最慢的查询详细信息
> * 查看速度慢的查询的查询执行计划


若要了解如何启用**表空间使用情况**示例见解，请完成下一步教程：

> [!div class="nextstepaction"]
> [启用表空间示例见解小组件](tutorial-table-space-sql-server.md)