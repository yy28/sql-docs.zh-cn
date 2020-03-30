---
title: 对输出列进行重新排序
ms.custom: seo-lt-2019
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- reordering output columns [SQL Server]
- output columns [SQL Server]
ms.assetid: 76462885-de4a-4290-a26b-90696d3671f4
author: markingmyname
ms.author: maghan
ms.manager: jroth
ms.reviewer: ''
ms.openlocfilehash: 33739ef70de87ece117d57a9091dda83d60138fb
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/29/2020
ms.locfileid: "75255193"
---
# <a name="reorder-output-columns-visual-database-tools"></a>重新排列输出列 (Visual Database Tools)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
向“选择”查询中添加数据列的顺序决定了这些列在结果中显示的顺序。 向查询中添加的第一列显示在结果的最左边，接下来是第二列，依此类推。  
  
如果创建的是“更新”或“插入”查询，则添加列的顺序将影响数据的处理顺序。  
  
若要控制数据列在结果集中显示的位置或控制数据列的使用顺序，可以对列重新排序。  
  
### <a name="to-reorder-columns-for-output"></a>对输出列重新排序  
  
1.  在“ [条件](../../ssms/visual-db-tools/criteria-pane-visual-database-tools.md)”窗格中，通过单击行左侧的行选择器按钮来选择包含该列的行。  
  
2.  指向行选择器按钮，然后将该行拖动到新位置。  
  
    -或-  
  
    在 [“SQL”窗格](../../ssms/visual-db-tools/sql-pane-visual-database-tools.md)中编辑列名的顺序。  
  
> [!TIP]  
> 您可以在“条件”窗格中的特定位置添加数据行，方法是：通过向“条件”窗格中插入空白行，再指定要插入的数据列。 有关详细信息，请参阅[向查询中添加列 (Visual Database Tools)](../../ssms/visual-db-tools/add-columns-to-queries-visual-database-tools.md)。  
  
## <a name="see-also"></a>另请参阅  
[对查询结果进行排序和分组 (Visual Database Tools)](../../ssms/visual-db-tools/sort-and-group-query-results-visual-database-tools.md)  
[汇总查询结果 (Visual Database Tools)](../../ssms/visual-db-tools/summarize-query-results-visual-database-tools.md)  
[执行基本的查询操作 (Visual Database Tools)](../../ssms/visual-db-tools/perform-basic-operations-with-queries-visual-database-tools.md)  
  
