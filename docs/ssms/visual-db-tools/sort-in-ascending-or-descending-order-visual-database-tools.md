---
title: 按升序或降序排序
ms.custom: seo-lt-2019
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- descending sorts
- ascending sorts
ms.assetid: d61cc55b-9ee8-4ecf-a32f-6459ae43910b
author: markingmyname
ms.author: maghan
ms.manager: jroth
ms.reviewer: ''
ms.openlocfilehash: fbef85b0211b49319298b29f7e935d6c2bc51db4
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/29/2020
ms.locfileid: "75255031"
---
# <a name="sort-in-ascending-or-descending-order-visual-database-tools"></a>按升序或降序进行排序 (Visual Database Tools)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
通过在 **ORDER BY** 子句中使用 **ASC** 或 **DESC** 关键字，可以按结果集中的一列或多列以升序或降序对查询结果进行排序。  
  
> [!NOTE]  
> 排序顺序在一定程度上由列的排序规则顺序来决定。 可以在 [“排序规则”对话框](../../ssms/visual-db-tools/collation-dialog-box-visual-database-tools.md)中更改排序规则顺序。  
  
下面的过程假设您已在查询和视图设计器中打开了一个查询，该查询使用 ORDER BY 子句对一列或多列进行排序。  
  
### <a name="to-specify-or-change-the-order-in-which-results-are-sorted"></a>指定或更改结果的排序顺序  
  
1.  在[“条件”窗格](../../ssms/visual-db-tools/criteria-pane-visual-database-tools.md)中，单击要重新排序的列的“排序类型”  字段。  
  
2.  选择“升序”  或“降序”  以指定该列的排序顺序。  
  
请注意，在“条件”窗格中操作时，查询的 UNION 子句将随之更改以反映最近执行的操作。  
  
> [!NOTE]  
> 按多列对结果进行排序时，可使用“排序顺序”列指定要搜索的各列的相对顺序。 有关详细信息，请参阅[对查询中的多个列进行排序 (Visual Database Tools)](../../ssms/visual-db-tools/sort-multiple-columns-in-queries-visual-database-tools.md)。  
  
## <a name="see-also"></a>另请参阅  
[对查询结果进行排序和分组 (Visual Database Tools)](../../ssms/visual-db-tools/sort-and-group-query-results-visual-database-tools.md)  
[汇总查询结果 (Visual Database Tools)](../../ssms/visual-db-tools/summarize-query-results-visual-database-tools.md)  
[设计查询和视图操作指南主题 (Visual Database Tools)](../../ssms/visual-db-tools/design-queries-and-views-how-to-topics-visual-database-tools.md)  
  
