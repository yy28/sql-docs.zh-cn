---
title: 放弃对查询所做的更改
ms.custom: seo-lt-2019
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- reverting queries
- queries [SQL Server], discarding changes
- discarding query changes
ms.assetid: 7bb17ece-1222-4622-b476-5789d7641c64
author: markingmyname
ms.author: maghan
ms.reviewer: ''
ms.openlocfilehash: 895bc5a3f68d36b4948d5697a901e6b4711025ec
ms.sourcegitcommit: f3321ed29d6d8725ba6378d207277a57cb5fe8c2
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/06/2020
ms.locfileid: "85999701"
---
# <a name="discard-changes-made-to-queries-visual-database-tools"></a>放弃对查询所做的更改 (Visual Database Tools)
[!INCLUDE[SQL Server Azure SQL Database Synapse Analytics PDW ](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]
在保存之前，可以放弃对查询定义所做的更改。 在保存之后，查询将无法还原到先前的状态。  
  
> [!NOTE]  
> 若要撤消对“结果”窗格中的值所做的更改，请在离开该记录之前按 Esc 键。 如果在离开记录时收到更改无法提交到数据库的通知，您也可以按 Esc 键恢复到先前的值。  
  
### <a name="to-discard-changes-made-to-a-query-definition"></a>放弃对查询定义所做的更改  
  
1.  如果该查询已经在查询和视图设计器中打开，请在“文件”  菜单中，单击“关闭”  。  
  
2.  在“Microsoft SQL Server Management Studio”  对话框中，单击“否”  。  
  
    查询定义将返回到上次保存时的状态。  
  
## <a name="see-also"></a>另请参阅  
[保存查询](../../ssms/visual-db-tools/save-queries-visual-database-tools.md)  
[设计查询和查看操作说明主题](../../ssms/visual-db-tools/design-queries-and-views-how-to-topics-visual-database-tools.md)  
[执行基本的查询操作](../../ssms/visual-db-tools/perform-basic-operations-with-queries-visual-database-tools.md)  
[使用“结果”窗格中的数据](../../ssms/visual-db-tools/work-with-data-in-the-results-pane-visual-database-tools.md)  
  
