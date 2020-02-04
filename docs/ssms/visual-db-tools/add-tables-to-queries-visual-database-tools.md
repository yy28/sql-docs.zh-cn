---
title: 向查询添加表
ms.prod: sql
ms.prod_service: sql-tools
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- inserting tables
- adding tables
- queries [SQL Server], tables
ms.assetid: 6551aa7e-31a1-4636-852a-819bc53d658b
author: markingmyname
ms.author: maghan
ms.manager: jroth
ms.reviewer: ''
ms.custom: seo-lt-2019
ms.date: 01/19/2017
ms.openlocfilehash: 3f333e275441f211457e14800cae14d19bd83b2a
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2020
ms.locfileid: "75245373"
---
# <a name="add-tables-to-queries-visual-database-tools"></a>向查询中添加表 (Visual Database Tools)

[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
创建查询时，实际是在从表或其他表结构对象（视图和某些用户定义的函数）中检索数据。 若要在查询中使用这些对象中的任何对象，可将其添加到“关系图”  窗格中。  
  
### <a name="to-add-a-table-or-table-valued-object-to-a-query"></a>向查询中添加表或表值对象  
  
1.  在查询和视图设计器的“关系图”  窗格中，右键单击背景，然后从快捷菜单中选择“添加表”  。  
  
2.  在“添加表”  对话框中，选择与要添加到查询中的对象类型相应的选项卡。  
  
3.  在项的列表中，双击要添加的每一项。  
  
4.  完成添加项后，单击“关闭”  。  
  
    查询和视图设计器会相应地更新“关系图窗格”  、“条件窗格”  和“SQL 窗格”  。  
  
在 SQL 窗格内的语句中引用表和视图时，所引用的表和视图将自动添加到查询中。  
  
如果您对表或表结构对象没有足够的访问权限，或者提供程序无法返回其相关信息，则查询和视图设计器将不显示该表或表结构对象的数据列。 在这种情况下，仅显示该表或表值对象的标题栏和“*(所有列)”复选框。  
  
### <a name="to-add-an-existing-query-to-a-new-query"></a>将现有查询添加到新查询中  
  
1.  确保在创建的新查询中显示“SQL 窗格”  。  
  
2.  在“SQL 窗格”  中，在单词 FROM 后键入左括号和右括号 ()。  
  
3.  为现有的查询打开查询设计器。 （现在当您打开了两个查询设计器。）  
  
4.  显示内部查询的“SQL 窗格”，内部查询是指要包括在新的外部查询中的现有查询  。  
  
5.  选中“SQL 窗格”  中的所有文本，然后将其复制到剪贴板中。  
  
6.  单击新查询的“SQL 窗格”  ，将光标置于添加的括号之间，然后粘贴剪贴板中的内容。  
  
7.  仍然是在“SQL 窗格”  中，在右括号的后面添加别名。  
  
## <a name="see-also"></a>另请参阅  
[创建表别名 (Visual Database Tools)](../../ssms/visual-db-tools/create-table-aliases-visual-database-tools.md)  
[从查询中删除表 (Visual Database Tools)](../../ssms/visual-db-tools/remove-tables-from-queries-visual-database-tools.md)  
[指定搜索条件 (Visual Database Tools)](../../ssms/visual-db-tools/specify-search-criteria-visual-database-tools.md)  
[汇总查询结果 (Visual Database Tools)](../../ssms/visual-db-tools/summarize-query-results-visual-database-tools.md)  
[执行基本的查询操作 (Visual Database Tools)](../../ssms/visual-db-tools/perform-basic-operations-with-queries-visual-database-tools.md)  
  
