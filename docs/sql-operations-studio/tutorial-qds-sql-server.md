---
title: "教程： 启用五个最慢的查询示例小组件的 SQL 操作 Studio （预览版） |Microsoft 文档"
description: "本教程演示如何启用五个最慢的查询示例上的小组件数据库仪表板。"
ms.custom: tools|sos
ms.date: 11/16/2017
ms.prod: sql-non-specified
ms.reviewer: alayu; erickang; sstein
ms.suite: sql
ms.prod_service: sql-tools
ms.component: sos
ms.tgt_pltfrm: 
ms.topic: tutorial
author: erickangMSFT
ms.author: erickang
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: fc30051dff2bef07ac3e7d06aa98d92d4e05e79e
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/21/2017
---
# <a name="tutorial-add-the-five-slowest-queries-sample-widget-to-the-database-dashboard"></a>教程： 添加*五个最慢的查询*示例小组件设为数据库仪表板

本教程演示的过程将其中一个添加[!INCLUDE[name-sos](../includes/name-sos-short.md)]的内置示例小组件到*数据库仪表板*可以快速查看数据库的五个最慢查询。 你还了解了如何查看速度慢的查询的详细信息和查询计划使用[!INCLUDE[name-sos](../includes/name-sos-short.md)]的功能。 在本教程中，你学习如何：

> [!div class="checklist"]
> * 在数据库上启用 Query Store
> * 将预建的见解小组件添加到数据库仪表板
> * 查看有关数据库的速度最慢的查询详细信息
> * 查看速度慢的查询的查询执行计划

[!INCLUDE[name-sos](../includes/name-sos-short.md)]包括几个见解小组件的-现成。 本教程演示如何将添加*查询的数据的存储区-db-见解*小组件中，但步骤是基本上相同的添加任何小组件。

## <a name="prerequisites"></a>必备条件

本教程需要安装 SQL Server 或 Azure SQL 数据库*TutorialDB*。 若要创建*TutorialDB*数据库，请完成以下快速入门之一：

- [连接和查询 SQL Server 使用[!INCLUDE[name-sos-short](../includes/name-sos-short.md)]](quickstart-sql-server.md)
- [连接和查询使用 Azure SQL 数据库[!INCLUDE[name-sos-short](../includes/name-sos-short.md)]](quickstart-sql-database.md)



## <a name="turn-on-query-store-for-your-database"></a>为你的数据库启用 Query Store

在此示例中的小组件需要*Query Store*要启用针对你的数据库的因此运行以下 TRANSACT-SQL (T-SQL) 语句：

   ```sql
    ALTER DATABASE TutorialDB SET QUERY_STORE = ON
   ```

## <a name="add-an-insight-widget-to-your-database-dashboard"></a>将见解小组件添加到你的数据库仪表板

若要将见解小组件添加到你的仪表板中，编辑*dashboard.database.widgets*中设置你*用户设置*文件。

1. 打开*用户设置*按**Ctrl + Shift + P**以打开*命令控制板*。
2. 类型*设置*的搜索框中，并从可用的设置文件，请选择**首选项： 打开用户设置**。

   ![打开用户设置命令](./media/tutorial-qds-sql-server/open-user-settings.png)

2. 类型*仪表板*中设置搜索框中，找到**dashboard.database.widgets**。

   ![搜索设置](./media/tutorial-qds-sql-server/search-settings.png)

3. 若要自定义**dashboard.database.widgets**设置，将鼠标悬停在左侧的铅笔图标**dashboard.database.widgets**文本，单击**编辑** > **复制到设置**。

4. 复制的设置后**dashboard.database.widgets**，将光标置于行的末尾后的左括号，按**Enter**，并添加如下所示使用大括号 （右大括号将自动出现）：

   ```json
   "dashboard.database.widgets": [
   {}
   ```
5. 将光标位于大括号内，按**Ctrl + Space**和选择**名称**。 
6. 完成该小组件的设置，使其外观如下所示：

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
        }
    ...
    ```

5. 按**Ctrl + S**以保存已修改**用户设置**。

6. 打开*数据库仪表板*通过导航到**TutorialDB**中*服务器*栏中，右键单击，并选择**管理**。

   ![打开仪表板](./media/tutorial-qds-sql-server/insight-open-dashboard.png)

7. 在仪表板上显示见解小组件： 

   ![QDS 小组件](./media/tutorial-qds-sql-server/insight-qds-result.png)


## <a name="view-insight-details-for-more-information"></a>有关详细信息视图了解详细信息

1. 若要查看见解小组件的其他信息，请单击省略号 (**...**) 正确，然后选择右上**显示详细信息**。
2. 若要显示的项的更多详细信息，请选择中的任意项**图表数据**列表。

   ![了解详细信息对话框](./media/tutorial-qds-sql-server/insight-details-dialog.png)

3. 右键单击**query_sql_txt**中**项详细信息**单击**复制单元格**。

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

5. 按**Ctrl + S**保存该文件，并更改文件扩展名为*.s q l*。 为本教程中，命名该文件*slowquery.sqlplan*。

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