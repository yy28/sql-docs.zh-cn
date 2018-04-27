---
title: 汇总查询结果 (Visual Database Tools) | Microsoft Docs
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
- summarizing query results
- queries [SQL Server], results
- aggregate queries [SQL Server]
ms.assetid: c9e15350-ed57-4d95-814d-815fbebfd86b
caps.latest.revision: 3
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: bf1e57b23b8a8442e7bd74f96c7046c75fee9564
ms.sourcegitcommit: a85a46312acf8b5a59a8a900310cf088369c4150
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/26/2018
---
# <a name="summarize-query-results-visual-database-tools"></a>汇总查询结果 (Visual Database Tools)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
当您创建聚合查询时，需要符合某些逻辑原则。 例如，在汇总查询中不能显示单个行的内容。 查询和视图设计器可帮助你遵循 [“关系图”窗格](../../ssms/visual-db-tools/diagram-pane-visual-database-tools.md) 和 [“条件”窗格](../../ssms/visual-db-tools/criteria-pane-visual-database-tools.md) 的行为原则。  
  
通过理解聚合查询的原则以及查询和视图设计器的行为，可以创建逻辑关系正确的聚合查询。 最重要的原则是聚合查询只能生成汇总信息。 因此，以下大多数原则都介绍可以在聚合查询中引用单个数据列的方法。  
  
## <a name="in-this-section"></a>本节内容  
[在聚合查询中使用列 (Visual Database Tools)](../../ssms/visual-db-tools/work-with-columns-in-aggregate-queries-visual-database-tools.md)  
介绍有关使用 GROUP BY、WHERE 和 HAVING 子句对列进行分组和汇总的概念。  
  
[计算表中的行数 (Visual Database Tools)](../../ssms/visual-db-tools/count-rows-in-a-table-visual-database-tools.md)  
介绍计算表中行数或表中符合一组条件的行数的步骤。  
  
[汇总或聚合表中所有行的值 (Visual Database Tools)](../../ssms/visual-db-tools/summarize-or-aggregate-values-for-all-rows-in-a-table-visual-database-tools.md)  
介绍汇总所有行而不是一些分组行的步骤。  
  
[使用自定义表达式汇总或聚合值 (Visual Database Tools)](../../ssms/visual-db-tools/summarize-or-aggregate-values-using-custom-expressions-visual-database-tools.md)  
介绍使用表达式而不是预定义子句进行汇总或聚合的步骤。  
  
## <a name="related-sections"></a>相关章节  
[设计查询和视图操作指南主题 (Visual Database Tools)](../../ssms/visual-db-tools/design-queries-and-views-how-to-topics-visual-database-tools.md)  
提供指向介绍如何使用查询和视图设计器的主题的链接。  
  
