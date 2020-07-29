---
title: SQL 窗格
ms.custom: seo-lt-2019
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- Query Designer [SQL Server], SQL pane
- View Designer, SQL pane
- SQL pane [Visual Database Tools]
ms.assetid: dbabab18-0614-415b-a2ef-9bcd0d320d5c
author: markingmyname
ms.author: maghan
ms.reviewer: ''
ms.openlocfilehash: 5b9136e9f24447f57bc375a8ff9d8ec83ef17bd9
ms.sourcegitcommit: f3321ed29d6d8725ba6378d207277a57cb5fe8c2
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/06/2020
ms.locfileid: "86008198"
---
# <a name="sql-pane-visual-database-tools"></a>SQL 窗格 (Visual Database Tools)
[!INCLUDE[SQL Server Azure SQL Database Synapse Analytics PDW ](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]
您可以使用 SQL 窗格创建自己的 SQL 语句，也可以使用“条件”窗格和“关系图”窗格创建语句，在后面这种情况下将在 SQL 窗格中相应地创建 SQL 语句。 生成查询时，SQL 窗格将自动更新并重新设置格式以便于阅读。  
  
若要打开 SQL 窗格，请首先打开查询和视图设计器（在服务器资源管理器中选择相应的数据库对象后，在“数据库”  菜单中单击“新建查询”  ）。 然后在“查询设计器”  菜单中指向“窗格”  ，再单击“SQL”  。  
  
在 SQL 窗格中，可以进行以下操作：  
  
-   通过输入 SQL 语句创建新查询。  
  
-   根据在“关系图”窗格和“条件”窗格中进行的设置，对查询和视图设计器创建的 SQL 语句进行修改。  
  
-   输入语句以利用所使用数据库的特有功能。  
  
> [!NOTE]  
> 请务必了解所用数据库中数据库对象的标识规则。 有关详细信息，请参阅数据库管理系统文档。  
  
## <a name="statements-in-the-sql-pane"></a>SQL 窗格中的语句  
您可以直接在 SQL 窗格中编辑当前查询。 当移动到另一窗格时，查询和视图设计器会自动设置语句格式，再更改“关系图”窗格和“条件”窗格以同语句匹配。  
  
如果语句不能在“关系图”窗格和“条件”窗格中表示出来，并且这两个窗格是可见的，则查询和视图设计器将显示一条错误信息，然后提供两种选择：  
  
-   忽略无法在“关系图”窗格和“条件”窗格中表示的语句。  
  
-   撤销无法表示的更改，并恢复到最近的 SQL 语句版本。  
  
如果选择忽略无法在“关系图”窗格和“条件”窗格中表示的语句，查询和视图设计器将使其他窗格变成灰色，指示它们不再反映 SQL 窗格的内容。  
  
您可以继续编辑语句，并像执行任何 SQL 语句一样执行该语句。  
  
> [!NOTE]  
> 如果输入 SQL 语句，但随后通过更改“关系图”窗格和“条件”窗格对查询做进一步更改，则查询和视图设计器将重新生成和显示 SQL 语句。 在某些情况下，此操作产生的 SQL 语句在构造上和原先输入的 SQL 语句将有所不同（尽管该语句始终会产生相同的结果）。 当使用的搜索条件涉及用 AND 和 OR 链接的多个子句时，尤其可能产生这种差异。  
  
## <a name="see-also"></a>另请参阅  
[创建查询 (Visual Database Tools)](../../ssms/visual-db-tools/create-queries-visual-database-tools.md)  
[运行查询 (Visual Database Tools)](../../ssms/visual-db-tools/run-queries-visual-database-tools.md)  
[设计查询和视图操作指南主题 (Visual Database Tools)](../../ssms/visual-db-tools/design-queries-and-views-how-to-topics-visual-database-tools.md)  
[“关系图”窗格 (Visual Database Tools)](../../ssms/visual-db-tools/diagram-pane-visual-database-tools.md)  
[“条件”窗格 (Visual Database Tools)](../../ssms/visual-db-tools/criteria-pane-visual-database-tools.md)  
[“结果”窗格 (Visual Database Tools)](../../ssms/visual-db-tools/results-pane-visual-database-tools.md)  
  
