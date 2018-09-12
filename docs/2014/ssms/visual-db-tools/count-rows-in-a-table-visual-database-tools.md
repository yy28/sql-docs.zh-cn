---
title: 计算表中的行数 (Visual Database Tools) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- totals [SQL Server], row counts
- row counts [SQL Server]
- column values [SQL Server]
- number of rows
- number of values
- counting rows
ms.assetid: dda4296a-1d16-4e77-8d6f-e295f6dd4e87
caps.latest.revision: 10
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 1dc91e9be0b517966eb0cea9ded88b07685c1f2a
ms.sourcegitcommit: 8ae6e6618a7e9186aab3c6a37ea43776aa9a382b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/06/2018
ms.locfileid: "43808253"
---
# <a name="count-rows-in-a-table-visual-database-tools"></a>计算表中的行数 (Visual Database Tools)
  您可对表中的行进行计数以确定以下信息：  
  
-   表中的总行数，例如 `titles` 表中所有书籍的数量。  
  
-   表中满足特定条件的行数，例如， `titles` 表中某出版商出版的书籍数量。  
  
-   特定列中的值的数量。  
  
 当对列中的值进行计数时，空值将不包含在计数中。 例如，假设要计算 `titles` 表中在 `advance` 列具有值的书籍的数量。 默认情况下，该计数包含所有值，而不仅仅是唯一值。  
  
 以上所有三种类型的计数过程都是类似的。  
  
### <a name="to-count-all-the-rows-in-a-table"></a>对表中的所有行进行计数  
  
1.  确保您要汇总的表已经包含在“关系图”窗格中。  
  
2.  右键单击“关系图”窗格的背景，再从快捷菜单中选择“添加分组依据”。 [查询和视图设计器](visual-database-tools.md)会在“条件”窗格的网格中添加一个“分组依据”列。  
  
3.  选择 **\* （所有列）** 表示表值对象的矩形中。  
  
     查询和视图设计器会自动在“条件”窗格的“分组依据”列中填充 **Count** 一词，并为要汇总的列分配列别名。 您可以用更有意义的名称替换这一自动生成的别名。 有关详细信息，请参阅[创建列别名 (Visual Database Tools)](create-column-aliases-visual-database-tools.md)。  
  
4.  运行查询。  
  
### <a name="to-count-all-the-rows-that-meet-a-condition"></a>对满足条件的所有行进行计数  
  
1.  确保您要汇总的表已经包含在“关系图”窗格中。  
  
2.  右键单击“关系图”窗格的背景，再从快捷菜单中选择“添加分组依据”。 查询和视图设计器会在“条件”窗格的网格中添加一个“分组依据”列。  
  
3.  选择 **\*（所有列）** 表示表结构对象的矩形中。  
  
     查询和视图设计器会自动在“条件”窗格的“分组依据”列中填充 **Count** 一词，并为要汇总的列分配列别名。 若要在查询输出中创建更实用的列标题，请参阅[创建列别名 (Visual Database Tools)](create-column-aliases-visual-database-tools.md)。  
  
4.  添加要搜索的数据列，再清除“输出”列中的复选框。  
  
     查询和视图设计器会自动在网格的“分组依据”列中填充 **Group By** 一词。  
  
5.  将“分组依据”列中的 **Group By** 改为 **Where**。  
  
6.  在要搜索的数据列的“筛选器”列中，输入搜索条件。  
  
7.  运行查询。  
  
### <a name="to-count-the-values-in-a-column"></a>对列中的值进行计数  
  
1.  确保您要汇总的表已经包含在“关系图”窗格中。  
  
2.  右键单击“关系图”窗格的背景，再从快捷菜单中选择“添加分组依据”。 查询和视图设计器会在“条件”窗格的网格中添加一个“分组依据”列。  
  
3.  将要计数的列添加到“条件”窗格中。  
  
     查询和视图设计器会自动在网格的“分组依据”列中填充 **Group By** 一词。  
  
4.  将“分组依据”列中的 **Group By** 改为 **Count**。  
  
    > [!NOTE]  
    >  若要只计算唯一值的数目，请选择 **Count Distinct**。  
  
5.  运行查询。  
  
## <a name="see-also"></a>请参阅  
 [排序和分组查询结果&#40;可视化数据库工具&#41;](sort-and-group-query-results-visual-database-tools.md)   
 [汇总查询结果 (Visual Database Tools)](summarize-query-results-visual-database-tools.md)  
  
  
