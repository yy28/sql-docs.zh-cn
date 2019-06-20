---
title: 教程：生成自定义见解小组件
titleSuffix: Azure Data Studio
description: 本教程演示如何生成自定义见解小组件并将其添加到 Azure Data Studio 中的数据库和服务器仪表板。
ms.prod: sql
ms.technology: azure-data-studio
ms.topic: tutorial
author: markingmyname
ms.author: maghan
manager: jroth
ms.reviewer: alayu; sstein
ms.custom: seodec18
ms.date: 09/24/2018
ms.openlocfilehash: 20b8bb332f2b8910d533407e79799dab162ac217
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/15/2019
ms.locfileid: "66797977"
---
# <a name="tutorial-build-a-custom-insight-widget"></a>教程：生成自定义见解小组件

本教程演示如何使用你自己的见解查询以生成自定义见解小组件。

本教程期间，你学习如何：
> [!div class="checklist"]
> * 运行您自己的查询，并在图表中查看
> * 生成从图表的自定义见解小组件
> * 将图表添加到服务器或数据库仪表板
> * 添加到自定义见解小组件的详细信息

## <a name="prerequisites"></a>必备条件

本教程需要安装 SQL Server 或 Azure SQL 数据库*TutorialDB*。 若要创建*TutorialDB*数据库，请完成以下快速入门之一：

- [使用 SQL Server 连接和查询 [!INCLUDE[name-sos-short](../includes/name-sos-short.md)]](quickstart-sql-server.md)
- [Azure SQL 数据库使用连接和查询 [!INCLUDE[name-sos-short](../includes/name-sos-short.md)]](quickstart-sql-database.md)


## <a name="run-your-own-query-and-view-the-result-in-a-chart-view"></a>运行您自己的查询和图表视图中查看结果
在此步骤中，运行 sql 脚本来查询当前活动会话。

1. 若要打开新的编辑器，请按**Ctrl + N**。 

2. 更改到的连接上下文**TutorialDB**。

3. 将以下查询粘贴到查询编辑器：

   ```sql
   SELECT count(session_id) as [Active Sessions]
   FROM sys.dm_exec_sessions
   WHERE status = 'running'
   ```

4. 将查询保存到在编辑器中\*.sql 文件。 本教程中，将保存该脚本作为*activeSession.sql*。

5. 若要执行查询时，按**F5**。

6. 查询结果显示后，单击**视图为图表**，然后单击**图表查看器**选项卡。

7. 更改**图表类型**到**计数**。 这些设置呈现计数图表。

## <a name="add-the-custom-insight-to-the-database-dashboard"></a>将自定义见解添加到数据库仪表板

1. 若要打开见解小组件配置，请单击**创建见解**上*图表查看器*:

   ![配置](./media/tutorial-build-custom-insight-sql-server/create-insight.png)
   
2. 将见解配置 （JSON 数据） 的复制。 

3. 按**Ctrl + 逗号**以打开*用户设置*。

4. 类型*仪表板*中*搜索设置*。

5. 单击**编辑**有关*dashboard.database.widgets*。

   ![仪表板设置](./media/tutorial-build-custom-insight-sql-server/dashboard-settings.png)

6. 将见解配置 JSON 粘贴到*dashboard.database.widgets*。 数据库仪表板设置看起来如下所示：

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

7. 保存*用户设置*文件，然后打开*TutorialDB*数据库仪表板以查看活动会话小组件：

   ![activesession 见解](./media/tutorial-build-custom-insight-sql-server/insight-activesession-dashboard.png)

## <a name="add-details-to-custom-insight"></a>将详细信息添加到自定义见解

1. 若要打开新的编辑器，请按**Ctrl + N**。

2. 更改到的连接上下文**TutorialDB**。

3. 将以下查询粘贴到查询编辑器：

   ```sql
    SELECT session_id AS [SID], login_time AS [Login Time], host_name AS [Host Name], program_name AS [Program Name], login_name AS [Login Name]
    FROM sys.dm_exec_sessions
    WHERE status = 'running'
   ```

4. 将查询保存到在编辑器中\*.sql 文件。 本教程中，将保存该脚本作为*activeSessionDetail.sql*。

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

7. 保存*用户设置*文件，然后打开*TutorialDB*数据库仪表板。 单击省略号 （...） 按钮旁边*我小组件*显示详细信息：

    ![activesession 见解](./media/tutorial-build-custom-insight-sql-server/insight-activesession-detail.png)

## <a name="next-steps"></a>后续步骤
在本教程中，你将了解：
> [!div class="checklist"]
> * 运行您自己的查询，并在图表中查看
> * 生成从图表的自定义见解小组件
> * 将图表添加到服务器或数据库仪表板
> * 添加到自定义见解小组件的详细信息

若要了解如何备份和还原数据库，请完成下一教程：

> [!div class="nextstepaction"]
> [备份和还原数据库](tutorial-backup-restore-sql-server.md)。
