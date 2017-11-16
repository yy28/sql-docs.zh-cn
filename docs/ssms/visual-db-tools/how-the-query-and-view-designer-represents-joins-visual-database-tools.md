---
title: "查询和视图设计器如何表示联接 | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology: tools-ssms
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- SQL pane [Visual Database Tools]
- joins [SQL Server], Query and View Designer
- Diagram pane [Visual Database Tools]
ms.assetid: 20a99dcb-83bd-4aa6-9139-92e2e5ba4887
caps.latest.revision: "4"
author: stevestein
ms.author: sstein
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 2231538d858cf69c6275c00458ebfa97561bd303
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/09/2017
---
# <a name="how-the-query-and-view-designer-represents-joins-visual-database-tools"></a>查询和视图设计器如何表示联接 (Visual Database Tools)
如果对表进行了联接，[查询和视图设计器](../../ssms/visual-db-tools/query-and-view-designer-tools-visual-database-tools.md)将在“[关系图](../../ssms/visual-db-tools/diagram-pane-visual-database-tools.md)”窗格中以图形方式表示联接，并在 [SQL 窗格](../../ssms/visual-db-tools/sql-pane-visual-database-tools.md)中使用 SQL 语法表示联接。  
  
## <a name="diagram-pane"></a>“关系图”窗格  
在“关系图”窗格中，查询和视图设计器在联接所涉及的数据列之间显示一条联接线。 查询和视图设计器为每个联接条件显示一条联接线。 例如，下图阐释两个联接的表之间的联接线：  
  
![联接线显示两个表之间的关系](../../ssms/visual-db-tools/media/dv3wbig.gif "联接线显示两个表之间的关系")  
  
如果用多个联接条件联接表，则查询和视图设计器将显示多条联接线，如下例所示：  
  
![使用多个联接条件联接的表](../../ssms/visual-db-tools/media/dv3w9n1.gif "使用多个联接条件联接的表")  
  
如果没有显示联接的数据列（例如，表示表或表结构对象的矩形已最小化，或者联接涉及表达式），则查询和视图设计器会将联接线放到表示表或表结构对象的矩形的标题栏中。  
  
联接线中间的图标形状指示表或表结构对象的联接方式。 如果联接子句使用等号 (=) 以外的运算符，则该运算符将出现在联接线图标中。 下表列出了在联接线上显示的图标。  
  
|**联接线图标**|**说明**|  
|----------------------|-------------------|  
|![Visual Database Tools 图标](../../ssms/visual-db-tools/media/dv3wbih.gif "Visual Database Tools 图标")|内部联接（用等号创建）。|  
|![Visual Database Tools 图标](../../ssms/visual-db-tools/media/dv3wbii.gif "Visual Database Tools 图标")|基于“大于”运算符的内部联接。|  
|![Visual Database Tools 图标](../../ssms/visual-db-tools/media/dv3wbij.gif "Visual Database Tools 图标")|外部联接，其中包括左侧表示的表中的所有行，即使它们在相关表中没有匹配行。|  
|![Visual Database Tools 图标](../../ssms/visual-db-tools/media/dv3wbik.gif "Visual Database Tools 图标")|外部联接，其中包括右侧表示的表中的所有行，即使它们在相关表中没有匹配行。|  
|![Visual Database Tools 图标](../../ssms/visual-db-tools/media/dv3wbil.gif "Visual Database Tools 图标")|完全外部联接，其中包括两个表中的所有行，即使它们在相关表中没有匹配行。|  
  
联接线末端的符号指示联接类型。 下表列出联接类型和在联接线末端显示的图标。  
  
|**联接线末端的图标**|**联接类型**|  
|---------------------------------|--------------------|  
|![Visual Database Tools 图标](../../ssms/visual-db-tools/media/dv3wbim.gif "Visual Database Tools 图标")|一对一联接。|  
|![Visual Database Tools 图标](../../ssms/visual-db-tools/media/dv3wbin.gif "Visual Database Tools 图标")|一对多联接。|  
|![Visual Database Tools 图标](../../ssms/visual-db-tools/media/dv3wbio.gif "Visual Database Tools 图标")|查询和视图设计器无法确定联接类型。 这种情况最常发生在手动创建联接时。|  
  
## <a name="sql-pane"></a>SQL 窗格  
在 SQL 语句中，可以采用许多方式表达联接。 确切的语法取决于所使用的数据库以及定义联接的方式。  
  
联接表的语法选项包括：  
  
-   **FROM 子句的 JOIN 限定符**。   关键字 INNER 和 OUTER 指定联接类型。 此语法是 ANSI 92 SQL 的标准语法。  
  
    例如，如果基于每个表中的 `publishers` 列联接 `pub_info` 和 `pub_id` 表，所得到的 SQL 语句可能类似于以下形式：  
  
    ```  
    SELECT *  
    FROM publishers INNER JOIN pub_info ON  
       publishers.pub_id = pub_info.pub_id  
    ```  
  
    如果创建外部联接，将显示关键字 LEFT OUTER 或 RIGHT OUTER 来代替关键字 INNER。  
  
-   **WHERE 子句比较两个表中的列**。   如果数据库不支持 JOIN 语法（或用户自己输入该语法），将显示 WHERE 子句。 如果联接是在 WHERE 子句中创建的，则两个表名都出现在 FROM 子句中。  
  
    例如，下面的语句联接 `publishers` 和 `pub_info` 表。  
  
    ```  
    SELECT *  
    FROM publishers, pub_info  
    WHERE publishers.pub_id = pub_info.pub_id  
    ```  
  
## <a name="see-also"></a>另请参阅  
[使用联接进行查询 (Visual Database Tools)](../../ssms/visual-db-tools/query-with-joins-visual-database-tools.md)  
[“联接”对话框 (Visual Database Tools)](../../ssms/visual-db-tools/join-dialog-box-visual-database-tools.md)  
  
