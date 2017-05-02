---
title: "在查询中指定 TOP 子句 (Visual Database Tools) | Microsoft Docs"
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
- TOP clause, queries
- percentage of rows returned [SQL Server]
- number of rows
- search conditions [SQL Server], TOP clause
- restricting rows returned
- search criteria [SQL Server], limiting rows returned
- inspecting portion of results
- limiting rows returned
- search criteria [SQL Server], TOP clause
ms.assetid: ba7d7c10-9bb3-4d9b-90b0-5fa94ecae59b
caps.latest.revision: 4
author: stevestein
ms.author: sstein
manager: jhubbard
translationtype: Human Translation
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: fd92acc6387cf67dd4b2a75b83e0e69b97a2ed3e
ms.lasthandoff: 04/11/2017

---
# <a name="specify-the-top-clause-in-queries-visual-database-tools"></a>在查询中指定 TOP 子句 (Visual Database Tools)
TOP 子句仅返回查询的前 *n* 行或 *n percent* 的行。 在需要检查部分结果以核实查询是否按预期执行时，TOP 子句十分有用，这样就不会占用返回所有查询结果所需的资源。  
  
### <a name="to-specify-the-top-clause-in-queries"></a>在查询中指定 TOP 子句  
  
1.  在解决方案资源管理器中打开一个查询或创建新的查询。  
  
2.  在“视图”****菜单中，单击“属性窗口”****。  
  
3.  在“属性”****窗口中，找到并展开“Top 规范”****属性。  
  
4.  单击“(最前面)”****子属性并将其设置为“是”****。  
  
5.  在“表达式”****子属性中，键入结果为数值的表达式（例如，“10”或“2*5”）。  
  
6.  单击“百分比”****子属性，并指示将“表达式”****属性视为所有返回行的百分比（是）还是返回行的绝对数值（否）。  
  
7.  如果查询使用 ORDER BY 子句，请单击“With Ties”****子属性，然后选择“是”****在只包含组中部分行时显示该组中的所有行，或选择“否”****截断这些行。  
  
执行以上过程时，请注意 SQL 窗格中显示的 TOP 子句会随之更改，以反映属性的最新设置。  
  
> [!NOTE]  
> 还可以通过在 SQL 窗格中编辑 TOP 子句来更改“Top 规范”****的子属性的值。  
  
## <a name="see-also"></a>另请参阅  
[设计查询和视图操作指南主题 (Visual Database Tools)](../../ssms/visual-db-tools/design-queries-and-views-how-to-topics-visual-database-tools.md)  
[查询属性 (Visual Database Tools)](../../ssms/visual-db-tools/query-properties-visual-database-tools.md)  
  

