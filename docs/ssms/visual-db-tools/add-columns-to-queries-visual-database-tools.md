---
title: 向查询中添加列 (Visual Database Tools) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- inserting columns
- columns [SQL Server], adding
- queries [SQL Server], columns
- adding columns
ms.assetid: 82f3ba72-3d72-4fb1-8179-2a953a782787
author: markingmyname
ms.author: maghan
manager: craigg
ms.openlocfilehash: 2ae2ace318d49ff524379c3f825d8da272674755
ms.sourcegitcommit: bb5484b08f2aed3319a7c9f6b32d26cff5591dae
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/06/2019
ms.locfileid: "65088842"
---
# <a name="add-columns-to-queries-visual-database-tools"></a>向查询中添加列 (Visual Database Tools)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
若要在查询中使用列，必须将其添加到查询中。 您可以添加某个列，以在查询输出中显示该列，使用该列进行排序，搜索该列的内容或对其内容进行汇总。 您可以决定在运行查询时，“结果”窗格中将包括查询中使用的哪些列。 有关详细信息，请参阅[从查询结果中删除列 (Visual Database Tools)](../../ssms/visual-db-tools/remove-columns-from-query-results-visual-database-tools.md)  
  
> [!NOTE]  
> 若要在查询和视图设计器中查看列的数据类型，请在“关系图”窗格中选择表或表值对象，然后在“属性”窗口中单击“列列表”。 再单击省略号“(…)”以打开“列列表”对话框。  
  
无论在查询中的任何位置使用列，都还可使用由列、文本、运算符和函数的任意组合组成的表达式。  
  
### <a name="to-add-an-individual-column"></a>添加单个列  
  
-   在“关系图”窗格中，选中要包括的列旁边的复选框。  
  
    -或 -  
  
-   在“条件”窗格中移动到第一个空白网格行，单击“列”列中的字段，然后从下拉列表中选择一个列名。  
  
### <a name="to-add-all-columns-for-one-table-or-table-valued-object"></a>添加一个表或表值对象的所有列  
  
-   在“关系图”窗格中，选中“&#42;(所有列)”旁边的复选框。  
  
### <a name="to-add-all-columns-for-all-tables-and-table-structured-objects"></a>添加所有表和表结构对象的所有列  
  
1.  确保没有选定“表操作”窗格中的任何联接线。  
  
2.  右键单击“设计”窗口的空白位置，然后从快捷菜单中选择“属性”。  
  
3.  在“属性”窗口中，单击“输出所有列”，然后从下拉列表中选择“是”或“否”。  
  
## <a name="see-also"></a>另请参阅  
[从查询结果中删除列 (Visual Database Tools)](../../ssms/visual-db-tools/remove-columns-from-query-results-visual-database-tools.md)  
[从查询中删除列 (Visual Database Tools)](../../ssms/visual-db-tools/remove-columns-from-queries-visual-database-tools.md)  
[指定搜索条件 (Visual Database Tools)](../../ssms/visual-db-tools/specify-search-criteria-visual-database-tools.md)  
[汇总查询结果 (Visual Database Tools)](../../ssms/visual-db-tools/summarize-query-results-visual-database-tools.md)  
[执行基本的查询操作 (Visual Database Tools)](../../ssms/visual-db-tools/perform-basic-operations-with-queries-visual-database-tools.md)  
  
