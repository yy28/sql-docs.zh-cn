---
title: “条件”窗格 (Visual Database Tools) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- Query Designer [SQL Server], Criteria pane
- View Designer, Criteria pane
- entering query options into grid [SQL Server]
- Criteria pane
- inserting query options into grid
- grid showing query options [SQL Server]
- adding query options into grid
ms.assetid: 6291affe-580e-482f-a7ff-45ce3837956a
author: markingmyname
ms.author: maghan
manager: craigg
ms.openlocfilehash: 8a4df3e9ed712975aa6d372dbc9afc3ce76bbeaa
ms.sourcegitcommit: bb5484b08f2aed3319a7c9f6b32d26cff5591dae
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/06/2019
ms.locfileid: "65095199"
---
# <a name="criteria-pane-visual-database-tools"></a>“条件”窗格 (Visual Database Tools)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
“条件”窗格用于指定查询选项（例如要显示哪些数据列、如何对结果进行排序以及选择哪些行等），可以通过将选择输入到一个类似电子表格的网格中来进行指定。 在“条件”窗格中，可以指定：  
  
-   要显示的列以及列名别名。  
  
-   列所属的表。  
  
-   计算列的表达式。  
  
-   查询的排序顺序。  
  
-   搜索条件。  
  
-   分组条件，包括用于摘要报告的聚合函数。  
  
-   UPDATE 或 INSERT INTO 查询的新值。  
  
-   INSERT FROM 查询的目标列名。  
  
在“条件”窗格中所做的更改将自动反映到“关系图”窗格和 SQL 窗格中。 同样，“条件”窗格也会自动更新以反映在其他窗格中所做的更改。  
  
## <a name="about-the-criteria-pane"></a>关于“条件”窗格  
“条件”窗格中的行显示查询中所用的数据列；“条件”窗格中的列显示查询选项。  
  
在“条件”窗格中显示的特定信息取决于所创建查询的类型。  
  
如果“条件”窗格不可见，则右键单击设计器，指向“窗格”，再单击“条件”。  
  
## <a name="options"></a>选项  
  
|**列**|**查询类型**|**Description**|  
|--------------|------------------|-------------------|  
|“列”|All|显示用于查询的数据列名或计算列的表达式。 该列将被锁定，以便当水平滚动屏幕时，始终可以看到该列。|  
|别名|SELECT、INSERT FROM、UPDATE 和 MAKE TABLE|指定列的可选名称或可以为计算列使用的名称。|  
|表|SELECT、INSERT FROM、UPDATE 和 MAKE TABLE|指定关联数据列的表名或表结构对象名。 对于计算列，该列是空白的。|  
|“输出”|SELECT、INSERT FROM 和 MAKE TABLE|指定某个数据列是否出现在查询输出中。<br /><br />注意：如果数据库允许，可以将某个数据列用于排序子句或搜索子句，但不在结果集内显示该数据列。|  
|排序类型|SELECT 和 INSERT FROM|指定关联的数据列用于对查询结果进行排序，并指定排序是升序还是降序。|  
|“排序顺序”|SELECT 和 INSERT FROM|指定用于对结果集进行排序的数据列的排序优先级。 当更改某个数据列的排序顺序时，所有其他列的排序顺序都将相应更新。|  
|分组依据|SELECT、INSERT FROM 和 MAKE TABLE|指定关联的数据列用于创建聚合查询。 只有从“工具”菜单中选择“分组依据”或向 SQL 窗格中添加了 GROUP BY 子句时，才会显示此网格列。<br /><br />默认情况下，该列的值设置为“分组依据”，而且该列也将成为 GROUP BY 子句的一部分。<br /><br />当移动到该列的某个单元格中，并选择一个聚合函数以应用到关联的数据列时，在默认情况下所得到的表达式将作为结果集的输出列添加。|  
|条件|All|为关联数据列指定搜索条件（筛选器）。 请输入运算符（默认为“=”）和要搜索的值。 用单引号将文本值括起来。<br /><br />如果关联的数据列是 GROUP BY 子句的一部分，则输入的表达式将用于 HAVING 子句。<br /><br />如果为“条件”网格列的多个单元格输入值，则所得到的搜索条件将自动以逻辑 AND 链接。<br /><br />若要为单个数据库列指定多个搜索条件表达式（例如，(fname > 'A') AND (fname < 'M')），请将该数据列添加到“条件”窗格中两次，并在“条件”网格列中为该数据列的每个实例输入不同的值。|  
|或...|All|指定数据列的附加搜索条件表达式，并用逻辑 OR 链接到前面的表达式。 通过在最右边的“或...”列中按 Tab 键可以添加更多的“或...”网格列。|  
|追加|INSERT FROM|指定关联数据列的目标数据列名称。 在创建“插入源”查询时，查询和视图设计器将尝试将源与相应的目标数据列相匹配。 如果查询和视图设计器无法选择匹配项，则必须提供列名。|  
|新值|UPDATE 和 INSERT INTO|指定要放入关联列中的值。 请输入文本值或表达式。|  
  
## <a name="see-also"></a>另请参阅  
[设计查询和视图操作指南主题 (Visual Database Tools)](../../ssms/visual-db-tools/design-queries-and-views-how-to-topics-visual-database-tools.md)  
[“关系图”窗格 (Visual Database Tools)](../../ssms/visual-db-tools/diagram-pane-visual-database-tools.md)  
[输入搜索值的规则 (Visual Database Tools)](../../ssms/visual-db-tools/rules-for-entering-search-values-visual-database-tools.md)  
[对查询结果进行排序和分组 (Visual Database Tools)](../../ssms/visual-db-tools/sort-and-group-query-results-visual-database-tools.md)  
[“结果”窗格 (Visual Database Tools)](../../ssms/visual-db-tools/results-pane-visual-database-tools.md)  
[SQL 窗格 (Visual Database Tools)](../../ssms/visual-db-tools/sql-pane-visual-database-tools.md)  
  
