---
title: 查询和视图设计器工具 (Visual Database Tools) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
f1_keywords:
- vdt.querydesigner
- vdt.pane.diagram
- vdt.pane.grid
- vdt.dlgbox.querybuilder
- vdt.pane.sql
- vdt.pane.results
helpviewer_keywords:
- Query Designer [SQL Server], panes
- View Designer, panes
- Query Designer [SQL Server], components
- View Designer, components
ms.assetid: 12e4b5a5-b793-4b6c-a0e5-c450c49bf26f
author: markingmyname
ms.author: maghan
ms.openlocfilehash: d8a1cbdc010f614c9b3cc72c1d3f9549b00ec8b2
ms.sourcegitcommit: e7d921828e9eeac78e7ab96eb90996990c2405e9
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/16/2019
ms.locfileid: "68266330"
---
# <a name="query-and-view-designer-tools-visual-database-tools"></a>查询和视图设计器工具 (Visual Database Tools)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
在设计查询、视图、内嵌函数或单语句存储过程时，所使用的设计器由四个窗格组成：“关系图”窗格、“条件”窗格、SQL 窗格和“结果”窗格。  
  
![查询设计器](../../ssms/visual-db-tools/media/vs_queryviewdsgpanes.gif "查询设计器")  
  
-   “关系图”窗格显示正在查询的表和其他表值对象。 每个矩形代表一个表或表值对象，并显示可用的数据列。 联接用矩形之间的连线来表示。 有关详细信息，请参阅[“关系图”窗格 (Visual Database Tools)](../../ssms/visual-db-tools/diagram-pane-visual-database-tools.md)。  
  
-   “条件”窗格包含一个类似于电子表格的网格，在该网格中可以指定相应的选项，例如要显示的数据列、要选择的行、行的分组方式等。 有关详细信息，请参阅[“条件”窗格 (Visual Database Tools)](../../ssms/visual-db-tools/criteria-pane-visual-database-tools.md)。  
  
-   SQL 窗格显示查询或视图的 SQL 语句。 您可以对由设计器创建的 SQL 语句进行编辑，也可以输入自己的 SQL 语句。 对于输入不能用“关系图”窗格和“条件”窗格创建的 SQL 语句（例如联合查询），此窗格尤其有用。 有关详细信息，请参阅 [ SQL 窗格 (Visual Database Tools)](../../ssms/visual-db-tools/sql-pane-visual-database-tools.md)。  
  
-   “结果”窗格显示一个网格，用来包含查询或视图检索到的数据。 在查询和视图设计器中，该窗格显示最近执行的 SELECT 查询的结果。 可以通过编辑网格单元格中的值来修改数据库，并可以添加或删除行。 有关详细信息，请参阅 [“结果”窗格 (Visual Database Tools)](../../ssms/visual-db-tools/results-pane-visual-database-tools.md)。  
  
可以通过在任意一个窗格中进行操作来创建查询或视图：通过以下方法可以指定要显示的列，在“关系图”窗格中选择该列，在“条件”窗格中输入该列，或者在 SQL 窗格中使其成为 SQL 语句的一部分。  
  
## <a name="displaying-and-hiding-panes"></a>显示和隐藏窗格  
若要隐藏窗格或显示不可见的窗格，请右键单击设计图面，指向“窗格”  ，再单击窗格的名称。 如果在查询设计器模式下打开了查询和视图设计器，则不会显示“结果”  窗格。  
  
## <a name="see-also"></a>另请参阅  
[设计查询和视图操作指南主题 (Visual Database Tools)](../../ssms/visual-db-tools/design-queries-and-views-how-to-topics-visual-database-tools.md)  
[打开查询和视图设计器 (Visual Database Tools)](../../ssms/visual-db-tools/open-the-query-and-view-designer-visual-database-tools.md)  
[SQL 编辑器 (Visual Database Tools)](../../ssms/visual-db-tools/sql-editor-visual-database-tools.md)  
  
