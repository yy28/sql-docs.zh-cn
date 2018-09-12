---
title: 创建列别名 (Visual Database Tools) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- columns [SQL Server], aliases
- aliases [SQL Server], columns
ms.assetid: e2e1c166-8ea7-47a2-b6a7-e419bf0fa3bb
caps.latest.revision: 9
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 04b12ad83b60d2e1953af7ecc0dbadbc1169b926
ms.sourcegitcommit: 8ae6e6618a7e9186aab3c6a37ea43776aa9a382b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/06/2018
ms.locfileid: "43811183"
---
# <a name="create-column-aliases-visual-database-tools"></a>创建列别名 (Visual Database Tools)
  您可为列名创建别名，以更方便地使用列名、计算和汇总值。 例如，您可以创建列别名以实现以下目的：  
  
-   为诸如 `(quantity * unit_price)` 之类的表达式或为聚合函数创建列名，如“Total Amount”。  
  
-   为列名创建简写形式，如用 `"d_id"` 代表 `"discounts.stor_id."`  
  
 定义列别名后，可在“选择”查询中使用该别名以指定查询输出。  
  
### <a name="to-create-a-column-alias"></a>创建列别名  
  
1.  在“条件”窗格中，找到包含要为其创建别名的数据列的行，如果需要，还可将其标记为输出。 如果该数据列不在网格中，则将其添加到网格中。  
  
2.  在该行的“别名”列中，输入别名。 别名必须遵循 SQL 的所有命名约定。 如果输入的别名包含空格，则查询和视图设计器将自动在其两旁放置分隔符。  
  
## <a name="see-also"></a>请参阅  
 [向查询中添加列&#40;可视化数据库工具&#41;](visual-database-tools.md)   
 [排序和分组查询结果&#40;可视化数据库工具&#41;](sort-and-group-query-results-visual-database-tools.md)   
 [汇总查询结果&#40;可视化数据库工具&#41;](summarize-query-results-visual-database-tools.md)   
 [执行基本的查询操作 (Visual Database Tools)](perform-basic-operations-with-queries-visual-database-tools.md)  
  
  
