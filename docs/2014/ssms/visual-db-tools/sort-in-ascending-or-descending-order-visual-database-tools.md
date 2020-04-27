---
title: 按升序或降序进行排序 (Visual Database Tools) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- descending sorts
- ascending sorts
ms.assetid: d61cc55b-9ee8-4ecf-a32f-6459ae43910b
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: cdf37ab5b61e74ab04b9b58162325b580675c493
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/26/2020
ms.locfileid: "63070777"
---
# <a name="sort-in-ascending-or-descending-order-visual-database-tools"></a>按升序或降序进行排序 (Visual Database Tools)
  通过在 `ASC` 子句中使用 `DESC` 或 `ORDER BY` 关键字，可以按结果集中的一列或多列以升序或降序对查询结果进行排序。  
  
> [!NOTE]  
>  排序顺序在一定程度上由列的排序规则顺序来决定。 可以在 [“排序规则”对话框](visual-database-tools.md)中更改排序规则顺序。  
  
 下面的过程假设您已在查询和视图设计器中打开了一个查询，该查询使用 ORDER BY 子句对一列或多列进行排序。  
  
### <a name="to-specify-or-change-the-order-in-which-results-are-sorted"></a>指定或更改结果的排序顺序  
  
1.  在[“条件”窗格](criteria-pane-visual-database-tools.md)中，单击要重新排序的列的“排序类型”  字段。  
  
2.  选择“升序”  或“降序”  以指定该列的排序顺序。  
  
 请注意，在“条件”窗格中操作时，查询的 UNION 子句将随之更改以反映最近执行的操作。  
  
> [!NOTE]  
>  按多列对结果进行排序时，可使用“排序顺序”列指定要搜索的各列的相对顺序。 有关详细信息，请参阅[对查询中的多个列进行排序 (Visual Database Tools)](sort-multiple-columns-in-queries-visual-database-tools.md)。  
  
## <a name="see-also"></a>另请参阅  
 [对查询结果进行排序和分组 &#40;Visual Database Tools&#41;](sort-and-group-query-results-visual-database-tools.md)   
 [&#40;Visual Database Tools&#41;汇总查询结果](summarize-query-results-visual-database-tools.md)   
 [设计查询和视图操作指南主题 (Visual Database Tools)](design-queries-and-views-how-to-topics-visual-database-tools.md)  
  
  
