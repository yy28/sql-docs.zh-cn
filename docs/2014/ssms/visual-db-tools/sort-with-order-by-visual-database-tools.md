---
title: 使用 ORDER BY 排序 (Visual Database Tools) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- dbe-cross-instance
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- ORDER BY clause [Visual Database Tools]
ms.assetid: 459f5640-8058-4c24-97e7-7bbd6168bc39
caps.latest.revision: 11
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: c8ad8958c102821c123a15217faea03478f6f4a2
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/02/2018
ms.locfileid: "37268041"
---
# <a name="sort-with-order-by-visual-database-tools"></a>使用 ORDER BY 排序 (Visual Database Tools)
  可以使用 ORDER BY 子句按返回行中的一个或多个列对查询结果进行排序。 通过选择“条件详细信息”窗格中的选项可以定义 ORDER BY 子句。  
  
### <a name="to-sort-a-query-using-an-order-by-clause"></a>使用 ORDER BY 子句对查询进行排序  
  
1.  打开一个查询或创建一个新查询。  
  
2.  在[“条件”窗格](visual-database-tools.md)中，单击与对查询结果进行排序所依据的列相对应的行的“排序类型”列。  
  
3.  从下拉列表中选择升序或降序。  
  
> [!NOTE]  
>  清除某列的“排序类型”项将从 ORDER BY 子句中删除该列。  
  
 请注意，在“条件”窗格中操作时，查询的 UNION 子句将随之更改以反映最近执行的操作。  
  
> [!NOTE]  
>  按多列对结果进行排序时，可使用“排序顺序”列指定要搜索的各列的相对顺序。 有关详细信息，请参阅**如何对查询中的多个列进行排序**。  
  
## <a name="see-also"></a>请参阅  
 [排序和分组查询结果&#40;可视化数据库工具&#41;](sort-and-group-query-results-visual-database-tools.md)   
 [汇总查询结果&#40;可视化数据库工具&#41;](summarize-query-results-visual-database-tools.md)   
 [设计查询和视图操作指南主题 (Visual Database Tools)](design-queries-and-views-how-to-topics-visual-database-tools.md)  
  
  
