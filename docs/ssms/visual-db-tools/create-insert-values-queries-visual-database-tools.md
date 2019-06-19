---
title: 创建“插入值”查询 (Visual Database Tools) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- inserting values
- queries [SQL Server], types
- adding values
- row additions [SQL Server], Insert Values query
- inserting rows
- Insert Values query
- adding rows
- table values [SQL Server]
ms.assetid: 2d4b2f6d-cc09-434b-8a0e-ccce40628064
author: markingmyname
ms.author: maghan
manager: craigg
ms.openlocfilehash: 5f1fb77b9664de6806a5dd49420267919be28c59
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/15/2019
ms.locfileid: "65105892"
---
# <a name="create-insert-values-queries-visual-database-tools"></a>创建“插入值”查询 (Visual Database Tools)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
可以使用“插入值”查询在当前表中创建新行。 在创建“插入值”查询时，需要指定：  
  
-   要向其中添加行的数据库表。  
  
-   要添加其内容的列。  
  
-   要插入到各个列中的值或表达式。  
  
例如，下面的查询将向 `titles` 表中添加一行，指定书名、类型、出版商和价格的值：  
  
```  
INSERT INTO titles  
         (title_id, title, type, pub_id, price)  
VALUES   ('BU9876', 'Creating Web Pages', 'business', '1389', '29.99')  
```  
  
在创建“插入值”查询时，“条件”窗格将发生相应变化以仅反映可用于插入新行的选项：要插入的列名和值。  
  
> [!CAUTION]  
> 无法撤消执行“插入值”查询的操作。 作为预防措施，可在执行该查询前备份数据。  
  
### <a name="to-create-an-insert-values-query"></a>创建“插入值”查询  
  
1.  将要更新的表添加到“关系图”窗格中。  
  
2.  在“查询设计器”菜单中，指向“更改类型”，再单击“插入值”。  
  
    > [!NOTE]  
    > 如果启动“插入值”查询时“关系图”窗格中显示有多个表，则查询和视图设计器将显示[“选择插入值的目标表”对话框](../../ssms/visual-db-tools/choose-target-table-for-insert-values-dialog-box-visual-database-tools.md)，以提示你输入要更新的表名。  
  
3.  在“关系图”窗格中，单击要为其提供新值的每个列的复选框。 这些列将显示在“条件”窗格中。 列只有在添加到查询后才能更新。  
  
4.  在“条件”窗格的“新建值”列中，为列输入新值。 可以输入文字值、列名或表达式。 该值必须与要更新的列的数据类型相匹配（或兼容）。  
  
    > [!CAUTION]  
    > 查询和视图设计器无法检查值是否适合要插入的列的长度。 如果所提供的值太长，那么可能会在不提出警告的情况下截断该值。 例如，如果 `name` 列的长度为 20 个字符，但您指定的插入值为 25 个字符，那么可能会截断后 5 个字符。  
  
在执行“插入值”查询时，不会在 [“结果”窗格](../../ssms/visual-db-tools/results-pane-visual-database-tools.md)中报告任何结果。 但是，会显示一条消息，指示已更改的行数。  
  
## <a name="see-also"></a>另请参阅  
[支持的查询类型 (Visual Database Tools)](../../ssms/visual-db-tools/supported-query-types-visual-database-tools.md)  
[设计查询和视图操作指南主题 (Visual Database Tools)](../../ssms/visual-db-tools/design-queries-and-views-how-to-topics-visual-database-tools.md)  
[执行基本的查询操作 (Visual Database Tools)](../../ssms/visual-db-tools/perform-basic-operations-with-queries-visual-database-tools.md)  
  
