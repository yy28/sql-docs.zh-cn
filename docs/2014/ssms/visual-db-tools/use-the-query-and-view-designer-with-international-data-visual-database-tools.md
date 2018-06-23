---
title: 对国际数据 (Visual Database Tools) 使用的查询和视图设计器 |Microsoft 文档
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- dbe-cross-instance
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- Visual Database Tools [SQL Server], international data
- queries [SQL Server], international data
- languages [SQL Server], Query and View Designer
- international considerations [SQL Server], Query and View Designer
- Criteria pane
- View Designer, international data
- Query Designer [SQL Server], international data
- localized information in Query and View Designer [SQL Server]
- global considerations [SQL Server], Query and View Designer
- SQL pane [Visual Database Tools]
- multiple language support [SQL Server], Query and View Designer
ms.assetid: 4b51c56f-f902-4e72-b919-e36127369b63
caps.latest.revision: 10
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: 5ab3f1bbc7708b40243269724f949df4693dd488
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/19/2018
ms.locfileid: "36027127"
---
# <a name="use-the-query-and-view-designer-with-international-data-visual-database-tools"></a>对国际数据使用查询和视图设计器 (Visual Database Tools)
  在[查询和视图设计器](visual-database-tools.md)中，可以使用任何语言的数据，也可以在任何 Windows 操作系统版本中使用查询和视图设计器。 以下准则概括介绍了需要注意的一些差异，并提供有关管理国际应用程序中的数据的信息。  
  
## <a name="localized-information-in-the-criteria-and-sql-panes"></a>“条件”窗格和 SQL 窗格中的本地化信息  
 如果使用“条件”窗格创建查询，则可以使用与计算机中的 Windows 区域设置相应的格式输入信息。 例如，如果要搜索数据，则可以在“条件”列中采用您所习惯的格式输入数据，但以下情况除外：  
  
-   不支持长数据格式。  
  
-   不能在“条件”窗格中输入货币符号。  
  
-   货币符号将不会显示在“结果”窗格中。  
  
    > [!NOTE]  
    >  在“结果”窗格中，实际上可以输入与计算机的 Windows 区域设置相应的货币符号，但该符号将被移除，并且不会显示在“结果”窗格中。  
  
-   一元负号始终显示在左侧（例如 -1），与区域设置选项无关。  
  
 相反，SQL 窗格中的数据和关键字必须始终为 ANSI（美国）格式。 例如，查询和视图设计器在生成查询时，会插入所有 SQL 关键字（如 SELECT 和 FROM）的 ANSI 格式。 如果将元素添加到 SQL 窗格内的语句中，则一定要使用这些元素的 ANSI 标准格式。  
  
 在“条件”窗格中以本地特定格式输入数据时，查询和视图设计器会在 SQL 窗格中将其自动转换为 ANSI 格式。 例如，如果区域设置设置为“标准德语”，则可以在“条件”窗格中以类似于“31.12.96”的格式输入数据。 但是，该日期在 SQL 窗格中将以 ANSI 日期时间格式显示为 `{ ts '1996-12-31 00:00:00' }.` ，如果直接在 SQL 窗格中输入数据，则必须以 ANSI 格式输入。  
  
## <a name="sort-order"></a>“排序顺序”  
 查询中数据的排序顺序由数据库决定。 Windows“区域设置”对话框中设置的选项不影响查询的排序顺序。 但是，在任何特定查询中，可以请求以特定的顺序返回行。  
  
## <a name="using-double-byte-characters"></a>使用双字节字符  
 可以输入 DBCS 字符作为文字或数据库对象名称（例如表和视图的名称或别名）。 也可以使用 DBCS 字符作为参数名和参数标记字符。 但是，不能在 SQL 语言元素（如函数名或 SQL 关键字）中使用 DBCS 字符。  
  
## <a name="see-also"></a>请参阅  
 [设计查询和视图操作指南主题 (Visual Database Tools)](design-queries-and-views-how-to-topics-visual-database-tools.md)  
  
  