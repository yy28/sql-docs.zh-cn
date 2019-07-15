---
title: 创建插入结果查询 (Visual Database Tools) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- queries [SQL Server], types
- result sets [SQL Server], queries
- results [SQL Server], query
- Insert Results query
- queries [SQL Server], results
ms.assetid: 8770d630-09cc-47ec-a0e9-e9de2d7bbc89
author: markingmyname
ms.author: maghan
manager: jroth
ms.openlocfilehash: b7b13e67c7c67e96516fd64f0dcd4a9bcddf0488
ms.sourcegitcommit: 5d839dc63a5abb65508dc498d0a95027d530afb6
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/09/2019
ms.locfileid: "67682543"
---
# <a name="create-insert-results-queries-visual-database-tools"></a>创建插入结果查询 (Visual Database Tools)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
您可以使用“插入结果”查询将行从一个表复制到另一个表或在同一个表内复制行。 例如，在 `titles` 表中，您可使用“插入结果”查询将某个出版商的所有书名信息复制到另一个可用于该出版商的表中。 “插入结果”查询与“生成表”查询类似，但前者是将行复制到现有表中。  
  
> [!TIP]  
> 您也可以使用剪切和粘贴功能将行从一个表复制到另一个表中。 还可以为每个表创建一个查询，然后运行这些查询。 将所需的行从一个结果网格复制到另一个结果网格中。  
  
当创建“插入结果”查询时，需要指定：  
  
-   要将行复制到其中的数据库表（目标表）。  
  
-   从中复制行的一个或多个表（源表）。 指定的源表将成为子查询的一部分。 如果在同一个表内复制，则源表就是目标表。  
  
-   源表中要复制其内容的列。  
  
-   目标表中要向其中复制数据的目标列。  
  
-   定义要复制的行的搜索条件。  
  
-   排序顺序（如果您希望按特定顺序复制行）。  
  
-   “分组依据”选项（如果您希望仅复制摘要信息）。  
  
例如，下面的查询将书名信息从 `titles` 表复制到名为 `archivetitles`的存档表。 该查询将复制属于特定出版商的所有书名的四列内容：  
  
```  
INSERT INTO archivetitles   
   (title_id, title, type, pub_id)  
SELECT title_id, title, type, pub_id  
FROM titles  
WHERE (pub_id = '0766')  
```  
  
> [!NOTE]  
> 若要在新行中插入值，请使用“插入值”查询。  
  
您可复制某行中所选列或全部列的内容。 不论是哪种情况，您要复制的数据都必须与要复制到其中的行内的列兼容。 例如，如果复制某列（如 `price`）中的内容，则要复制到其中的行内的列必须能够接受带小数点的数字数据。 若要复制整个行，目标表与源表的相同物理位置的列必须要相互兼容。  
  
当您创建“插入结果”查询时，“条件”窗格将相应变化以反映可用于复制数据的选项。 使用增加的“追加”列，您可以指定应将数据复制到其中的列。  
  
> [!CAUTION]  
> 无法撤消执行“插入结果”查询的操作。 作为预防措施，可在执行该查询前备份数据。  
  
### <a name="to-create-an-insert-results-query"></a>创建“插入结果”查询  
  
1.  创建一个新查询并添加要从其中复制行的表（源表）。 若要在同一个表内复制行，则可将源表作为目标表添加。  
  
2.  在 **“查询设计器”** 菜单中，指向 **“更改类型”** ，再单击 **“插入结果”** 。  
  
3.  在“ [选择插入结果的目标表](../../ssms/visual-db-tools/choose-target-table-for-insert-results-dialog-box-visual-database-tools.md)”对话框中，选择要将行复制到其中的表（目标表）。  
  
    > [!NOTE]  
    > 查询和视图设计器无法预先确定您可更新哪些表和视图。 因此，“从查询选择插入的表”  对话框中的“表名称”  列表将显示所查询的数据连接中的所有可用表和视图，甚至包括不能将行复制到其中的表和视图。  
  
4.  在表示表或表值对象的矩形中，选择要复制其内容的列的名称。 若要复制全部行，请选择“&#42; (所有列)”  。  
  
    查询和视图设计器会将选择的列添加到“条件”窗格的“列”  列中。  
  
5.  在“条件”窗格的“追加”  列中，为要复制的每个列选择目标表中的相应目标列。 如果要复制全部行，请选择“tablename.&#42;”  。 目标表中的列必须与源表中的列具有相同（或兼容）的数据类型。  
  
6.  如果希望按特定顺序复制行，请指定排序顺序。 有关详细信息，请参阅[对查询结果进行排序和分组 (Visual Database Tools)](../../ssms/visual-db-tools/sort-and-group-query-results-visual-database-tools.md)。  
  
7.  通过在“筛选器”  列中输入搜索条件来指定要复制的行。 有关详细信息，请参阅[指定搜索条件 (Visual Database Tools)](../../ssms/visual-db-tools/specify-search-criteria-visual-database-tools.md)。  
  
    如果未指定搜索条件，则源表中的所有行都会复制到目标表中。  
  
    > [!NOTE]  
    > 当向“条件”窗格添加要搜索的列时，查询和视图设计器也会将该列添加到要复制的列的列表中。 如果希望在搜索中使用某列但不复制该列，请在表示表或表值对象的矩形中，清除该列名旁边的复选框。  
  
8.  如果希望复制摘要信息，请指定“分组依据”选项。 有关详细信息，请参阅[汇总查询结果 (Visual Database Tools)](../../ssms/visual-db-tools/summarize-query-results-visual-database-tools.md)。  
  
在执行“插入结果”查询时，不会在[“结果”窗格](../../ssms/visual-db-tools/results-pane-visual-database-tools.md)中报告任何结果。 但是，会显示一条消息，指出已复制的行数。  
  
## <a name="see-also"></a>另请参阅  
[查询类型 (Visual Database Tools)](../../ssms/visual-db-tools/types-of-queries-visual-database-tools.md)  
[设计查询和视图操作指南主题 (Visual Database Tools)](../../ssms/visual-db-tools/design-queries-and-views-how-to-topics-visual-database-tools.md)  
  
