---
title: 创建更新查询 (Visual Database Tools) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.service: ''
ms.component: ssms-visual-db
ms.reviewer: ''
ms.suite: sql
ms.technology:
- tools-ssms
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- tables [SQL Server], updating
- queries [SQL Server], types
- Update query
- updating tables
ms.assetid: 178b7b75-8078-4e61-b2a8-4719b9d8033d
caps.latest.revision: 4
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: d5b40a79039017062464f530a422821420069b12
ms.sourcegitcommit: a85a46312acf8b5a59a8a900310cf088369c4150
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/26/2018
---
# <a name="create-update-queries-visual-database-tools"></a>创建更新查询 (Visual Database Tools)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
可以使用“更新”查询在一次操作中更改多个行中的内容。 例如，在 `titles` 表中，可以使用“更新”查询将特定出版商出版的所有书籍都加价 10%。  
  
在创建“更新”查询时，需要指定：  
  
-   要更新的表。  
  
-   要更新其内容的列。  
  
-   用来更新单个列的值或表达式。  
  
-   定义要更新的行的搜索条件。  
  
例如，以下查询通过将一个出版商出版的所有书籍都加价 10% 来更新 `titles` 表：  
  
```  
UPDATE titles  
SET price = price * 1.1  
WHERE (pub_id = '0766')  
```  
  
> [!CAUTION]  
> 无法撤消执行“更新”查询的操作。 作为预防措施，可在执行该查询前备份数据。  
  
### <a name="to-create-an-update-query"></a>创建“更新”查询  
  
1.  将要更新的表添加到“关系图”窗格中。  
  
2.  在“查询设计器”菜单中，指向“更改类型”，再单击“更新”。  
  
    > [!NOTE]  
    > 如果启动“更新”查询时“关系图”窗格中显示有多个表，则查询和视图设计器将显示“[选择插入值的目标表](../../ssms/visual-db-tools/choose-target-table-for-insert-values-dialog-box-visual-database-tools.md)”对话框，以提示你输入要更新的表名。  
  
3.  在“关系图”窗格中，单击要为其提供新值的每个列的复选框。 这些列将显示在“条件”窗格中。 列只有在添加到查询后才能更新。  
  
4.  在“条件”窗格的“新建值”列中，输入列的更新值。 可以输入文字值、列名或表达式。 该值必须与要更新的列的数据类型相匹配（或兼容）。  
  
    > [!CAUTION]  
    > 查询和视图设计器无法检查值是否适合要更新的列的长度。 如果所提供的值太长，那么可能会在不提出警告的情况下截断该值。 例如，如果 `name` 列的长度为 20 个字符，但您指定的更新值为 25 个字符，那么可能会截断后 5 个字符。  
  
5.  在“筛选器”列中输入搜索条件，定义要更新的行。 有关详细信息，请参阅[指定搜索条件 (Visual Database Tools)](../../ssms/visual-db-tools/specify-search-criteria-visual-database-tools.md)。  
  
    如果未指定搜索条件，将更新指定表中的所有行。  
  
    > [!NOTE]  
    > 当向“条件”窗格中添加要在搜索条件中使用的列时，查询和视图设计器也会将其添加到要更新的列的列表中。 若要在搜索条件中使用某列但不更新该列，请在表示表或表值对象的矩形中，清除该列名旁边的复选框。  
  
在执行“更新”查询时，不会在 [“结果”窗格](../../ssms/visual-db-tools/results-pane-visual-database-tools.md)中报告任何结果。 但是，会显示一条消息，指示已更改的行数。  
  
## <a name="see-also"></a>另请参阅  
[支持的查询类型 (Visual Database Tools)](../../ssms/visual-db-tools/supported-query-types-visual-database-tools.md)  
[设计查询和视图操作指南主题 (Visual Database Tools)](../../ssms/visual-db-tools/design-queries-and-views-how-to-topics-visual-database-tools.md)  
[执行基本的查询操作 (Visual Database Tools)](../../ssms/visual-db-tools/perform-basic-operations-with-queries-visual-database-tools.md)  
  
