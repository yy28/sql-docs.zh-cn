---
title: “结果”窗格 (Visual Database Tools) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- View Designer, Results pane
- result sets [SQL Server], queries
- synchronization [SQL Server], query results with definition
- displaying query results in grid
- grid showing query results [SQL Server]
- showing query results in grid
- Query Designer [SQL Server], Results pane
- results [SQL Server], query
- viewing query results
- queries [SQL Server], results
- Results pane
ms.assetid: 6309a1bc-a628-4141-8bb5-b35924bd19f9
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 65221627169e524b53eed7965ec6ec2f7c677b8d
ms.sourcegitcommit: e7d921828e9eeac78e7ab96eb90996990c2405e9
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/16/2019
ms.locfileid: "68255807"
---
# <a name="results-pane-visual-database-tools"></a>“结果”窗格 (Visual Database Tools)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
“结果”窗格显示最近执行的 SELECT 查询的结果。 （其他类型查询的结果会在消息框中显示。）若要打开“结果”窗格，请打开或创建一个查询或视图，或者返回某个表的数据。 如果默认情况下不显示“结果”窗格，请在 **“查询设计器”** 菜单中，指向 **“窗格”**，再单击 **“结果”**。  
  
## <a name="what-you-can-do-in-the-results-pane"></a>可以在“结果”窗格中执行的操作  
  
-   在类似于电子表格的网格中查看最近执行的 SELECT 查询的结果集。  
  
-   对于显示单个表或视图中的数据的查询或视图，您可以编辑结果集中各个列的值、添加新行以及删除现有的行。  
  
## <a name="limitations-in-the-results-pane"></a>“结果”窗格中的限制  
  
-   表值函数返回的结果只有在某些情况下才能更新。  
  
-   如果查询或视图所包括的列来自多个表或视图，则不能更新这些查询或视图。  
  
-   不能更新存储过程返回的结果。  
  
-   不能更新使用 GROUP BY 或 DISTINCT 子句的查询或视图。  
  
## <a name="navigating-in-the-results-pane"></a>在“结果”窗格中导航  
您可以使用“结果”窗格底部的导航栏在记录之间快速导航。  
  
导航栏中提供了多个按钮，可分别用于跳转到第一个记录、最后一个记录、下一个记录、上一个记录以及某个特定记录。  
  
若要转到特定的记录，请在导航栏的文本框中键入行号，然后按 Enter。  
  
有关在查询和视图设计器中使用键盘快捷方式的信息，请参阅[在查询和视图设计器中导航 (Visual Database Tools)](../../ssms/visual-db-tools/navigate-in-the-query-and-view-designer-visual-database-tools.md)。  
  
## <a name="keeping-the-results-set-synchronized-with-the-query-definition"></a>使结果集与查询定义保持同步  
当您处理查询或视图的结果时，可能会出现“结果”窗格中的记录与查询定义不同步的情况。 例如，如果您用查询搜索出表的五列中的四列，然后使用“关系图”窗格将第五列添加到查询的定义中，则第五列的数据不会自动添加到“结果”窗格中。 若要使“结果”窗格反映新的查询定义，请再次运行该查询。  
  
如果某个查询发生更改，则在“结果”窗格的右下角会出现一个警报图标和文本“查询已更改”。 该图标在窗格的左上角反复出现。  
  
## <a name="see-also"></a>另请参阅  
[创建查询 (Visual Database Tools)](../../ssms/visual-db-tools/create-queries-visual-database-tools.md)  
[运行查询 (Visual Database Tools)](../../ssms/visual-db-tools/run-queries-visual-database-tools.md)  
[设计查询和视图操作指南主题 (Visual Database Tools)](../../ssms/visual-db-tools/design-queries-and-views-how-to-topics-visual-database-tools.md)  
[“关系图”窗格 (Visual Database Tools)](../../ssms/visual-db-tools/diagram-pane-visual-database-tools.md)  
[“条件”窗格 (Visual Database Tools)](../../ssms/visual-db-tools/criteria-pane-visual-database-tools.md)  
[使用“结果”窗格中的数据 (Visual Database Tools)](../../ssms/visual-db-tools/work-with-data-in-the-results-pane-visual-database-tools.md)  
  
