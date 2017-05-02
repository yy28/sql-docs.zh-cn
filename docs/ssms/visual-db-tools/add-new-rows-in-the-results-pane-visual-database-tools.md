---
title: "在“结果”窗格中添加新行 (Visual Database Tools) | Microsoft Docs"
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
- View Designer, Results pane
- inserting rows
- Query Designer [SQL Server], Results pane
- Results pane
- adding rows
- row additions [SQL Server], Results pane
ms.assetid: 59891c84-3f54-4ab9-8b86-72c59627b480
caps.latest.revision: 3
author: stevestein
ms.author: sstein
manager: jhubbard
translationtype: Human Translation
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: 0ba11f05536a52023c382e040738b8d9f9a4a215
ms.lasthandoff: 04/11/2017

---
# <a name="add-new-rows-in-the-results-pane-visual-database-tools"></a>在“结果”窗格中添加新行 (Visual Database Tools)
若要添加新数据，既可以在其中键入数据也可以从其他程序（如“记事本”或 Excel）粘贴数据。 要粘贴的行必须与要粘贴到的表中列的数目和类型完全一致。 可以在“结果”窗格中一次粘贴多行。  
  
有关如何输入数据的信息，请参阅[更新结果的规则 (Visual Database Tools)](../../ssms/visual-db-tools/rules-for-updating-results-visual-database-tools.md)。  
  
### <a name="to-add-a-new-data-row"></a>添加新数据行  
  
1.  定位到“结果”窗格底部，此处有一个可用于添加新数据行的空白行。  
  
    所有列的初始值都将为 NULL**。  
  
    > [!TIP]  
    > 若要直接转到第一个空行，请使用“结果”窗格底部的导航栏。  
  
2.  如果从剪贴板中粘贴多行，请通过单击新行左侧的按钮选择新行。  
  
    > [!NOTE]  
    > 如果所粘贴的一行或多行无法提交到数据库，则您将收到消息，指示哪些行不能提交。  
  
3.  为新行输入数据。 如果要粘贴数据，请从“编辑”****菜单中选择“粘贴”****。  
  
4.  离开该行可以将其提交到数据库。  
  
如果在保存行时出错，查询和视图数据库设计器将显示一条消息，然后返回到您所编辑的行。 然后，您可以：  
  
-   通过对该行进行进一步的编辑以解决错误。  
  
-   按 Esc 取消编辑。 如果在已经进行了更改的某个单元格中按 Esc，则将取消对该单元格所做的更改。 如果在未进行更改的单元格中按 Esc，则将取消对整个行所做的更改。  
  
## <a name="see-also"></a>另请参阅  
[使用“结果”窗格中的数据 (Visual Database Tools)](../../ssms/visual-db-tools/work-with-data-in-the-results-pane-visual-database-tools.md)  
[执行基本的查询操作 (Visual Database Tools)](../../ssms/visual-db-tools/perform-basic-operations-with-queries-visual-database-tools.md)  
  

