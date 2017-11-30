---
title: "创建表别名 (Visual Database Tools) | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology: tools-ssms
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- table aliases [SQL Server]
- aliases [SQL Server], tables
ms.assetid: 49e61e85-8abf-4ca7-8c70-7e9f8f1078bd
caps.latest.revision: "4"
author: stevestein
ms.author: sstein
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 2e7c4230e0e72e3de7a636e822a6f89b94b379fb
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/09/2017
---
# <a name="create-table-aliases-visual-database-tools"></a>创建表别名 (Visual Database Tools)
别名可使表名的使用更为方便。 在以下情况下，使用别名很有帮助：  
  
-   希望使 [SQL](../../ssms/visual-db-tools/sql-pane-visual-database-tools.md) 窗格中的语句更简短、更容易阅读。  
  
-   经常在查询中引用表名（如在限定列名时），并希望确保查询不超过特定的字符长度限制。 （一些数据库对查询进行了最大长度限制。）  
  
-   使用同一个表的多个实例（如在自联接中），并需要一种引用其中的一个实例或其他实例的方法。  
  
例如，可以为表名 `employee_information` 创建别名 `"e"`，然后在查询的其余部分使用 `"e"` 引用该表。  
  
### <a name="to-create-an-alias-for-a-table-or-table-valued-object"></a>为表或表值对象创建别名  
  
1.  将表或表值对象添加到查询中。  
  
2.  在“关系图”窗格中，右键单击要为其创建别名的对象，然后从快捷菜单中选择“属性”。  
  
3.  在“属性”窗口的“别名”字段中输入别名。  
  
## <a name="see-also"></a>另请参阅  
[向查询中添加表 (Visual Database Tools)](../../ssms/visual-db-tools/add-tables-to-queries-visual-database-tools.md)  
[对查询结果进行排序和分组 (Visual Database Tools)](../../ssms/visual-db-tools/sort-and-group-query-results-visual-database-tools.md)  
[汇总查询结果 (Visual Database Tools)](../../ssms/visual-db-tools/summarize-query-results-visual-database-tools.md)  
[执行基本的查询操作 (Visual Database Tools)](../../ssms/visual-db-tools/perform-basic-operations-with-queries-visual-database-tools.md)  
  
