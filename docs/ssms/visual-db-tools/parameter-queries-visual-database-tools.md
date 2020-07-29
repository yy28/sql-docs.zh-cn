---
title: 参数查询
ms.custom: seo-lt-2019
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- parameter queries [SQL Server]
ms.assetid: 4897c41a-324a-47b8-a30b-cbc9e9e19a8b
author: markingmyname
ms.author: maghan
ms.reviewer: ''
ms.openlocfilehash: f0cfe484f628040bf419738f79e6500cc6911f83
ms.sourcegitcommit: f3321ed29d6d8725ba6378d207277a57cb5fe8c2
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/06/2020
ms.locfileid: "86003233"
---
# <a name="parameter-queries-visual-database-tools"></a>参数查询 (Visual Database Tools)
[!INCLUDE[SQL Server Azure SQL Database Synapse Analytics PDW ](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]
在某些情况下，您需要创建可以使用多次但每次使用不同值的查询。 例如，可能经常运行一个查询以查找某位作者编写的所有 `title_ids` 。 可以为每次请求运行相同的查询，只是每次使用的作者 ID 或姓名不同。  
  
若要创建每次使用不同值的查询，可以在查询中使用参数。 参数是在运行查询时提供的值的占位符。 带有参数的 SQL 语句可能类似于以下形式，其中“?”表示代表作者 ID 的参数：  
  
```  
SELECT title_id  
FROM titleauthor  
WHERE (au_id = ?)  
```  
  
## <a name="where-you-can-use-parameters"></a>可以使用参数的位置  
可以将参数用作文本值（文本值或数值）的占位符。 最常见的情况是，在单个行或组的搜索条件中（即在 SQL 语句的 WHERE 或 HAVING 子句中）使用参数作为占位符。  
  
您可以在表达式中使用参数作为占位符。 例如，可能希望在每次运行查询时，通过提供不同的折扣值来计算打折价格。 为此，可以指定以下表达式：  
  
```  
(price * ?)  
```  
  
## <a name="specifying-unnamed-and-named-parameters"></a>指定未命名参数和命名参数  
可以指定两种类型的参数：未命名参数和命名参数。 未命名参数是可放在查询中的任意位置的问号 (?)，用于提示输入值或以文本值替代。 例如，如果在 `titleauthor` 表中使用未命名参数搜索某个作者的 ID，则在 [SQL 窗格](../../ssms/visual-db-tools/sql-pane-visual-database-tools.md) 中生成的语句可能类似于以下形式：  
  
```  
SELECT title_id  
FROM titleauthor  
WHERE (au_id = ?)  
```  
  
在 [查询和视图设计器](../../ssms/visual-db-tools/query-and-view-designer-tools-visual-database-tools.md)中运行查询时，将显示带有“?”（作为参数名称）的 [查询参数对话框](../../ssms/visual-db-tools/query-parameters-dialog-box-visual-database-tools.md) 。  
  
此外，您也可以为参数分配一个名称。 如果查询中存在多个参数，此时命名参数将非常有用。 例如，如果在 `authors` 表中使用命名参数搜索某作者的姓氏和名称，则在 SQL 窗格中生成的语句可能类似于以下形式：  
  
```  
SELECT au_id  
FROM authors  
WHERE au_fname = %first name% AND  
      au_lname = %last name%  
```  
  
> [!TIP]  
> 在创建命名参数查询之前，必须定义前缀和后缀字符。  
  
在查询和视图设计器中运行查询时，将显示 [查询参数对话框](../../ssms/visual-db-tools/query-parameters-dialog-box-visual-database-tools.md) 和命名参数列表。  
  
## <a name="see-also"></a>另请参阅  
[使用参数进行查询 (Visual Database Tools)](../../ssms/visual-db-tools/query-with-parameters-visual-database-tools.md)  
[支持的查询类型 (Visual Database Tools)](../../ssms/visual-db-tools/supported-query-types-visual-database-tools.md)  
[设计查询和视图操作指南主题 (Visual Database Tools)](../../ssms/visual-db-tools/design-queries-and-views-how-to-topics-visual-database-tools.md)  
  
