---
title: 教程： 生成 SQL 操作 Studio （预览版） 中的自定义见解小组件 |Microsoft 文档
description: 本教程演示如何生成自定义见解小组件并将其添加到 SQL 操作 Studio （预览版） 中的数据库和服务器仪表板。
ms.custom: tools|sos
ms.date: 11/15/2017
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
ms.openlocfilehash: fc57d6abd04a4672aad1026701489f15dfd69d66
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
---
# <a name="tutorial-build-a-custom-insight-widget"></a>教程： 构建自定义见解小组件

本教程演示如何使用您自己的见解查询来生成自定义见解小组件。

在本教程，你学习如何：
> [!div class="checklist"]
> * 运行自己的查询并在图表中查看它
> * 生成从图表的自定义见解小组件
> * 将图表添加到服务器或数据库仪表板
> * 添加到自定义见解小组件的详细信息

## <a name="prerequisites"></a>必备条件

本教程需要安装 SQL Server 或 Azure SQL 数据库*TutorialDB*。 若要创建*TutorialDB*数据库，请完成以下快速入门之一：

- [连接和查询 SQL Server 使用 [!INCLUDE[name-sos-short](../includes/name-sos-short.md)]](quickstart-sql-server.md)
- [连接和查询使用 Azure SQL 数据库 [!INCLUDE[name-sos-short](../includes/name-sos-short.md)]](quickstart-sql-database.md)


## <a name="run-your-own-query-and-view-the-result-in-a-chart-view"></a>运行自己的查询和图表视图中查看结果
在此步骤中，运行查询当前的活动会话的 sql 脚本。

1. 若要打开新的编辑器，请按**Ctrl + N**。 

2. 将连接上下文更改为**TutorialDB**。

3. 将以下查询粘贴到查询编辑器中：

   ```sql
   SELECT count(session_id) as [Active Sessions]
   FROM sys.dm_exec_sessions
   WHERE status = 'running'
   ```

4. 将查询保存到编辑器中\*.sql 文件。 本教程中，将保存该脚本作为*activeSession.sql*。

5. 若要执行查询时，按**F5**。

6. 显示查询结果后，单击**以图表形式查看**，然后单击**图表查看器**选项卡。

7. 更改**图表类型**到**计数**。 这些设置呈现 count 图表。

## <a name="add-the-custom-insight-to-the-database-dashboard"></a>将自定义见解添加到数据库仪表板

1. 若要打开见解小组件配置，请单击**创建见解**上*图表查看器*:

   ![配置](./media/tutorial-build-custom-insight-sql-server/create-insight.png)
   
2. 将复制的见解配置 （JSON 数据）。 

3. 按**Ctrl + 逗号**以打开*用户设置*。

4. 类型*仪表板*中*搜索设置*。

5. 单击**编辑**为*dashboard.database.widgets*。

   ![仪表板设置](./media/tutorial-build-custom-insight-sql-server/dashboard-settings.png)

6. 粘贴见解配置 JSON 到*dashboard.database.widgets*。 数据库仪表板设置类似于以下内容：

   ```json
    "dashboard.database.widgets": [
        {
            "name": "My-Widget",
            "gridItemConfig": {
                "sizex": 2,
                "sizey": 1
            },
            "widget": {
                "insights-widget": {
                    "type": {
                        "count": {
                            "dataDirection": "vertical",
                            "dataType": "number",
                            "legendPosition": "none",
                            "labelFirstColumn": false,
                            "columnsAsLabels": false
                        }
                    },
                    "queryFile": "{your file folder}/activeSession.sql"
                }
            }
        }
    ]
   ```

7. 保存*用户设置*文件，并打开*TutorialDB*数据库仪表板以查看活动会话小组件：

   ![activesession 见解](./media/tutorial-build-custom-insight-sql-server/insight-activesession-dashboard.png)

## <a name="add-details-to-custom-insight"></a>将详细信息添加到自定义见解

1. 若要打开新的编辑器，请按**Ctrl + N**。

2. 将连接上下文更改为**TutorialDB**。

3. 将以下查询粘贴到查询编辑器中：

   ```sql
    SELECT session_id AS [SID], login_time AS [Login Time], host_name AS [Host Name], program_name AS [Program Name], login_name AS [Login Name]
    FROM sys.dm_exec_sessions
    WHERE status = 'running'
   ```

4. 将查询保存到编辑器中\*.sql 文件。 本教程中，将保存该脚本作为*activeSessionDetail.sql*。

5. 按**Ctrl + 逗号**以打开*用户设置*。

6. 编辑现有*dashboard.database.widgets*设置文件中的节点：

   ```json
    "dashboard.database.widgets": [
        {
            "name": "My-Widget",
            "gridItemConfig": {
                "sizex": 2,
                "sizey": 1
            },
            "widget": {
                "insights-widget": {
                    "type": {
                        "count": {
                            "dataDirection": "vertical",
                            "dataType": "number",
                            "legendPosition": "none",
                            "labelFirstColumn": false,
                            "columnsAsLabels": false
                        }
                    },
                    "queryFile": "{your file folder}/activeSession.sql",
                    "details": {
                        "queryFile": "{your file folder}/activeSessionDetail.sql",
                        "label": "SID",
                        "value": "Login Name"
                    }
                }
            }
        }
    ]
   ```

7. 保存*用户设置*文件，并打开*TutorialDB*数据库仪表板。 单击省略号 （…） 按钮旁边*我小组件*以显示详细信息：

    ![activesession 见解](./media/tutorial-build-custom-insight-sql-server/insight-activesession-detail.png)

## <a name="next-steps"></a>后续步骤
在本教程中，您学习了如何：
> [!div class="checklist"]
> * 运行自己的查询并在图表中查看它
> * 生成从图表的自定义见解小组件
> * 将图表添加到服务器或数据库仪表板
> * 添加到自定义见解小组件的详细信息

若要了解如何备份和还原数据库，请完成下一步教程：

> [!div class="nextstepaction"]
> [备份和还原数据库](tutorial-backup-restore-sql-server.md)。