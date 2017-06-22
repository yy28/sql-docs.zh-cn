---
title: "向关系图中添加表 (Visual Database Tools) | Microsoft Docs"
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
- inserting tables
- adding tables
ms.assetid: 5440fdf7-ac04-4325-9f32-181f4cd402e5
caps.latest.revision: 5
author: stevestein
ms.author: sstein
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: ae6c38826ce111508e88de0948ffe8e1ecb35c24
ms.contentlocale: zh-cn
ms.lasthandoff: 06/22/2017

---
# <a name="add-tables-to-diagrams-visual-database-tools"></a>向关系图中添加表 (Visual Database Tools)
可以将表添加到数据库关系图中，以编辑其结构或使其与关系图中的其他表相关。 可以向关系图中添加现有的数据库表，或者插入尚未在数据库中定义的新表。  
  
### <a name="to-insert-a-new-table-into-a-diagram"></a>向关系图中插入新表  
  
1.  确保已连接到要在其中创建表的数据库。  
  
    若要在当前关系图中创建表，请单击工具栏上的“新建表”按钮。  
  
    - 或 -  
  
    在关系图中右键单击，然后选择“新建表”。  
  
2.  在“选择名称”对话框中修改或接受系统分配的表名，然后选择“确定”。  
  
    此时，将在关系图中以标准视图显示一个新表。  
  
3.  在新表的第一个单元格中，键入列名。 然后按 Tab 键移动到下一个单元格。  
  
4.  在“数据类型”下，选择列的数据类型。 每个列都必须具有名称和数据类型。  
  
    您可以在表设计器中设置列的其他属性。  
  
5.  对于要添加到表中的每一列重复第 3 和第 4 步。  
  
> [!NOTE]  
> 在保存数据库关系图时，新表将添加到数据库中。  
  
### <a name="to-add-an-existing-table-to-a-diagram"></a>向关系图中添加现有的表  
  
1.  确保已连接到要编辑其表的数据库。  
  
2.  在“表”文件夹中选择表。  
  
3.  将该表拖动到数据库关系图中。  
  
4.  释放鼠标按钮。  
  
> [!NOTE]  
> 如果选定的表与关系图中的其他表之间存在关系，则自动绘制关系线。  
  
### <a name="to-add-related-tables-to-a-diagram"></a>向关系图中添加相关表  
  
1.  在数据库关系图中，选择一个或多个具有外键约束的表。  
  
2.  右键单击任何选定的表，再选择“添加相关表”。  
  
> [!NOTE]  
> 选定表的外键约束所引用的表以及引用具有外键约束的选定表的表都将添加到关系图中。  
  
## <a name="see-also"></a>另请参阅  
[使用数据库关系图 (Visual Database Tools)](../../ssms/visual-db-tools/work-with-database-diagrams-visual-database-tools.md)  
[使用数据库关系图中的表 (Visual Database Tools)](../../ssms/visual-db-tools/work-with-tables-in-database-diagram-visual-database-tools.md)  
  

