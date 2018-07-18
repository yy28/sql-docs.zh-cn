---
title: 手动联接表 (Visual Database Tools) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.component: ssms-visual-db
ms.reviewer: ''
ms.suite: sql
ms.technology: ssms
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- manual joins [SQL Server]
- joins [SQL Server], manual
- joins [SQL Server], creating
ms.assetid: 9c785356-646b-4c87-82d4-25efd6051d9d
caps.latest.revision: 4
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 905c551cd4e9aa9e58900a58b9d9399a3c662a7c
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
ms.locfileid: "33051294"
---
# <a name="join-tables-manually-visual-database-tools"></a>手动联接表 (Visual Database Tools)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
向查询中添加两个或多个表时， [查询和视图设计器](../../ssms/visual-db-tools/query-and-view-designer-tools-visual-database-tools.md) 将尝试根据公共数据或数据库中存储的关于这些表如何相关的信息来联接这些表。 有关详细信息，请参阅[自动联接表 (Visual Database Tools)](../../ssms/visual-db-tools/join-tables-automatically-visual-database-tools.md)。 但是，如果查询和视图设计器未自动联接这些表，或者您希望在这些表之间创建其他联接条件，则可手动联接这些表。  
  
除基于包含相同信息的列之外，还可以基于任意两列之间的比较创建联接。 例如，如果数据库包含 `titles` 和 `roysched`两个表，则可将 `ytd_sales` 表的 `titles` 列中的值与 `lorange` 表的 `hirange` 和 `roysched` 列中的值相比较。 创建此联接将允许您查找特定的书名，这些书籍截止到目前为止的年销售额介于版税的最高和最低范围之内。  
  
> [!TIP]  
> 如果联接条件中的列已建立索引，则联接的速度最快。 在某些情况下，对没有建立索引的列进行联接会导致查询速度缓慢。  
  
### <a name="to-manually-join-tables-or-table-structured-objects"></a>手动联接表或表结构对象  
  
1.  将要联接的对象添加到 [“关系图”窗格](../../ssms/visual-db-tools/diagram-pane-visual-database-tools.md) 中。  
  
2.  拖动第一个表或表结构对象中的联接列的名称，并将其拖放到第二个表或表结构对象中的相关列上。 不能基于 **text**、 **ntext**、或**image** 列建立联接。  
  
    > [!NOTE]  
    > 联接列必须具有相同（或兼容）的数据类型。 例如，如果第一个表中的联接列是日期，则必须将其与第二个表中的日期列相关。 另一方面，如果第一个联接列是整数，则相关联接列也必须是整数数据类型，但它的大小可以不同。 查询和视图设计器不检查要用来创建联接的列的数据类型，但当您执行查询时，如果数据类型不兼容，数据库将显示错误。  
  
3.  如果需要，请更改联接运算符；默认情况下，该运算符是等号 (=)。 有关详细信息，请参阅[修改联接运算符 (Visual Database Tools)](../../ssms/visual-db-tools/modify-join-operators-visual-database-tools.md)。  
  
查询和视图设计器将在 [SQL 窗格](../../ssms/visual-db-tools/sql-pane-visual-database-tools.md)内的 SQL 语句中添加 INNER JOIN 子句。 您可以将其类型更改为外部联接。 有关详细信息，请参阅[创建外部联接 (Visual Database Tools)](../../ssms/visual-db-tools/create-outer-joins-visual-database-tools.md)。  
  
## <a name="see-also"></a>另请参阅  
[使用联接进行查询 (Visual Database Tools)](../../ssms/visual-db-tools/query-with-joins-visual-database-tools.md)  
  
