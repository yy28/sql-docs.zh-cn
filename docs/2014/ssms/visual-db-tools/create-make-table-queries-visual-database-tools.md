---
title: 创建“生成表”查询 (Visual Database Tools) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- queries [SQL Server], types
- table creation [SQL Server], Make Table query
- inserting tables
- Make Table query
- adding tables
ms.assetid: 4493cffa-7b2d-4c24-8ef0-d49329198972
author: stevestein
ms.author: sstein
ms.openlocfilehash: f44097ef41a4dc1a115dbdad9f9ff7940a1c2880
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/18/2020
ms.locfileid: "85058151"
---
# <a name="create-make-table-queries-visual-database-tools"></a>创建“生成表”查询 (Visual Database Tools)
  可以使用“生成表”查询将行复制到一个新表中，“生成表”查询对创建要使用的数据子集或在数据库之间复制表的内容非常有用。 “生成表”查询与“插入结果”查询类似，但它会创建要向其中复制行的新表。  
  
 在创建“生成表”查询时，需要指定：  
  
-   新数据库表的名称（目标表）。  
  
-   从中复制行的一个或多个表（源表）。 您可以从单个表或联接的表中复制行。  
  
-   源表中要复制其内容的列。  
  
-   排序顺序（如果您希望按特定顺序复制行）。  
  
-   定义要复制的行的搜索条件。  
  
-   “分组依据”选项（如果您希望仅复制摘要信息）。  
  
 例如，下面的查询将创建一个名为 `uk`_`customers` 的新表，并将 `customers` 表中的信息复制到该表中：  
  
```  
SELECT *   
INTO uk_customers  
FROM customers  
WHERE country = 'UK'  
```  
  
 为了成功使用“生成表”查询：  
  
-   数据库必须支持 SELECT...INTO 语法。  
  
-   必须具有在目标数据库中创建表的权限。  
  
### <a name="to-create-a-make-table-query"></a>创建“生成表”查询  
  
1.  将一个或多个源表添加到“关系图”窗格中。  
  
2.  在“查询设计器”  菜单中，指向“更改类型”  ，再单击“生成表”  。  
  
3.  在“生成表”  对话框中，键入目标表的名称。 查询和视图设计器不会检查该名称是否已使用，也不会检查您是否具有创建表的权限。  
  
     若要在另一个数据库中创建目标表，请指定完全限定表名，包括目标数据库的名称、所有者（如果需要）以及表名。  
  
4.  通过将其添加到查询中来指定要复制的列。 有关详细信息，请参阅[向查询中添加列 (Visual Database Tools)](visual-database-tools.md)。 列只有在添加到查询后才能复制。 若要复制整行，请选择 " ** \* （所有列）**"。  
  
     “查询和视图设计器”会将选择的列添加到“条件”窗格的“列”  列中。  
  
5.  如果希望按特定顺序复制行，请指定排序顺序。 有关详细信息，请参阅“对查询结果进行排序和分组”  。  
  
6.  通过输入搜索条件指定要复制的行。 有关详细信息，请参阅[指定搜索条件 (Visual Database Tools)](specify-search-criteria-visual-database-tools.md)。  
  
     如果未指定搜索条件，则源表中的所有行都会复制到目标表中。  
  
    > [!NOTE]  
    >  当向“条件”窗格添加要搜索的列时，查询和视图设计器也会将该列添加到要复制的列的列表中。 若要在搜索中使用某列但不复制该列，请在表示表或表结构对象的矩形中，清除该列名旁边的复选框。  
  
7.  如果希望复制摘要信息，请指定“分组依据”选项。 有关详细信息，请参阅[汇总查询结果 (Visual Database Tools)](summarize-query-results-visual-database-tools.md)。  
  
 在执行“生成表”查询时，不会在 [“结果窗格”](results-pane-visual-database-tools.md)中报告任何结果。 但是，会显示一条消息，指出已复制的行数。  
  
## <a name="see-also"></a>另请参阅  
 [&#40;Visual Database Tools 的设计查询和视图操作指南主题&#41;](design-queries-and-views-how-to-topics-visual-database-tools.md)   
 [查询类型 (Visual Database Tools)](types-of-queries-visual-database-tools.md)  
  
  
