---
description: 从查询中删除列 (Visual Database Tools)
title: 从查询中删除列
ms.custom: seo-lt-2019
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- removing columns
- queries [SQL Server], columns
- deleting columns
- dropping columns
ms.assetid: 6d9819b8-ee2f-4838-9713-c5e3ad37ab46
author: markingmyname
ms.author: maghan
ms.reviewer: ''
ms.openlocfilehash: 05a761620a0acb4bc799c0163b69a75881425f62
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/17/2020
ms.locfileid: "88313893"
---
# <a name="remove-columns-from-queries-visual-database-tools"></a>从查询中删除列 (Visual Database Tools)
[!INCLUDE[SQL Server Azure SQL Database Synapse Analytics PDW ](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]
如果不希望再在查询中使用某列，则可以可移除该列。 如果执行此操作，“查询和视图设计器”将从选择列表、排序规范、搜索条件、“SQL”窗格**** 以及所有分组规范中删除对该列的引用。  
  
> [!NOTE]  
> 如果只希望从“选择”查询的输出中移除某列，则可以直接从输出中移除该列，而不必同时从查询中移除该列。 有关详细信息，请参阅[从查询结果中删除列 (Visual Database Tools)](../../ssms/visual-db-tools/remove-columns-from-query-results-visual-database-tools.md)  
  
### <a name="to-remove-a-column-from-the-query"></a>从查询中移除列  
  
-   在“条件”**** 窗格中，选择包含要移除的列的网格行，然后按 Delete。  
  
    - 或 -  
  
-   在 [“SQL”窗格](../../ssms/visual-db-tools/sql-pane-visual-database-tools.md)中移除对该列的所有引用。  
  
## <a name="see-also"></a>另请参阅  
[向查询中添加列 (Visual Database Tools)](../../ssms/visual-db-tools/add-columns-to-queries-visual-database-tools.md)  
[对查询结果进行排序和分组 (Visual Database Tools)](../../ssms/visual-db-tools/sort-and-group-query-results-visual-database-tools.md)  
[汇总查询结果 (Visual Database Tools)](../../ssms/visual-db-tools/summarize-query-results-visual-database-tools.md)  
[执行基本的查询操作 (Visual Database Tools)](../../ssms/visual-db-tools/perform-basic-operations-with-queries-visual-database-tools.md)  
  
