---
title: "打开查询和视图设计器 (Visual Database Tools) | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- tools-ssms
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- opening View Designer
- View Designer, opening
- Query Designer [SQL Server], opening
- opening Query Designer
ms.assetid: b473f258-d53c-41c0-9ad9-528a2ff141f4
caps.latest.revision: 4
author: stevestein
ms.author: sstein
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: 6d4b09ac45528392c55f47ab7b62ed7881a1ebc9
ms.contentlocale: zh-cn
ms.lasthandoff: 06/22/2017

---
# <a name="open-the-query-and-view-designer-visual-database-tools"></a>打开查询和视图设计器 (Visual Database Tools)
当您打开视图的定义、显示查询或视图的结果或者创建或打开查询时，查询和视图设计器将会打开。 它由四个不同的窗格组成：  
  
-   “关系图”窗格以图形形式显示了您通过数据连接选择的表或表值对象。 同时也会显示它们之间的联接关系。  
  
-   “条件”窗格用于指定查询选项（例如要显示哪些数据列、如何对结果进行排序以及选择哪些行等），您可以通过将选择输入到一个类似电子表格的网格中来进行指定。  
  
-   您可以使用 SQL 窗格创建自己的 SQL 语句，也可以使用“条件”窗格和“关系图”窗格创建语句，在后面这种情况下将在 SQL 窗格中相应地创建 SQL 语句。 生成查询时，SQL 窗格将自动更新并重新设置格式以便于阅读。  
  
-   “结果”窗格显示最近执行的“选择”查询的结果。 （其他类型查询的结果会在消息框中显示。）  
  
-   这些窗格对于处理查询和视图非常有用。  
  
-   当您打开一个视图或查询时，以上部分或全部窗格将随之打开。 所打开的窗格取决于“选项”对话框中的设置以及你所连接的数据库管理系统。 默认设置是四个窗格全都打开。  
  
### <a name="to-open-the-query-and-view-designer-for-a-view"></a>为视图打开查询和视图设计器  
  
1.  在对象资源管理器中，右键单击要打开的视图，然后单击“设计”或“打开视图”。  
  
    如果选择“设计”，查询和视图设计器窗格将按照在“选项”对话框中选定的选项设置打开。 如果选择“打开视图”，默认情况下仅打开“结果”窗格。  
  
### <a name="to-open-the-query-and-view-designer-for-an-existing-query"></a>为现有查询打开查询和视图设计器  
  
1.  在解决方案资源管理器中，展开“查询”文件夹。  
  
2.  双击要打开的查询。  
  
3.  突出显示相应的查询语句，右键单击突出显示的区域，再单击“在编辑器中设计查询”。  
  
## <a name="see-also"></a>另请参阅  
[设计查询和视图操作指南主题 (Visual Database Tools)](../../ssms/visual-db-tools/design-queries-and-views-how-to-topics-visual-database-tools.md)  
[查询和视图设计器工具 (Visual Database Tools)](../../ssms/visual-db-tools/query-and-view-designer-tools-visual-database-tools.md)  
  

