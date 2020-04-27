---
title: 向查询中添加列 (Visual Database Tools) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- inserting columns
- columns [SQL Server], adding
- queries [SQL Server], columns
- adding columns
ms.assetid: 82f3ba72-3d72-4fb1-8179-2a953a782787
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: aef64ed8031664dcbefa7d0e30bf9f63435b292c
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/26/2020
ms.locfileid: "63015698"
---
# <a name="add-columns-to-queries-visual-database-tools"></a>向查询中添加列 (Visual Database Tools)
  若要在查询中使用列，必须将其添加到查询中。 您可以添加某个列，以在查询输出中显示该列，使用该列进行排序，搜索该列的内容或对其内容进行汇总。 您可以决定在运行查询时，“结果”窗格中将包括查询中使用的哪些列。 有关详细信息，请参阅[从查询结果中删除列 (Visual Database Tools)](visual-database-tools.md)  
  
> [!NOTE]  
>  若要在查询和视图设计器中查看列的数据类型，请在“关系图”  窗格中选择表或表值对象，然后在“属性”窗口中单击“列列表”。 再单击省略号“(…)”以打开“列列表”对话框   。  
  
 无论在查询中的任何位置使用列，都还可使用由列、文本、运算符和函数的任意组合组成的表达式。  
  
### <a name="to-add-an-individual-column"></a>添加单个列  
  
-   在“关系图”  窗格中，选中要包括的列旁边的复选框。  
  
     -或-  
  
-   在“条件”  窗格中移动到第一个空白网格行，单击“列”  列中的字段，然后从下拉列表中选择一个列名。  
  
### <a name="to-add-all-columns-for-one-table-or-table-valued-object"></a>添加一个表或表值对象的所有列  
  
-   在 "**关系图" 窗格**中，选择 " ** \*（所有列）**" 旁边的复选框。  
  
### <a name="to-add-all-columns-for-all-tables-and-table-structured-objects"></a>添加所有表和表结构对象的所有列  
  
1.  确保没有选定“表操作”  窗格中的任何联接线。  
  
2.  右键单击“设计”窗口的空白位置，然后从快捷菜单中选择“属性”  。  
  
3.  在“属性”窗口中，单击“输出所有列”  ，然后从下拉列表中选择“是”  或“否”  。  
  
## <a name="see-also"></a>另请参阅  
 [从查询结果中删除列 &#40;Visual Database Tools&#41;](visual-database-tools.md)   
 [&#40;Visual Database Tools&#41;从查询中删除列](remove-columns-from-queries-visual-database-tools.md)   
 [指定 Visual Database Tools &#40;搜索条件&#41;](specify-search-criteria-visual-database-tools.md)   
 [&#40;Visual Database Tools&#41;汇总查询结果](summarize-query-results-visual-database-tools.md)   
 [执行基本的查询操作 (Visual Database Tools)](perform-basic-operations-with-queries-visual-database-tools.md)  
  
  
