---
title: "创建和更新表 (SSMS) | Microsoft Docs"
ms.custom: 
ms.date: 08/25/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- tools-ssms
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- Visual Database Tools [SQL Server], Table Designer
- Table Designer, designing tables
- opening tables
- opening Table Designer
- tables [SQL Server], opening
- Table Designer, opening
ms.assetid: c49e0155-5dcb-481f-9538-e1bde77105e2
caps.latest.revision: 3
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: Inactive
ms.translationtype: HT
ms.sourcegitcommit: 21f0cfd102a6fcc44dfc9151750f1b3c936aa053
ms.openlocfilehash: ca37946fadb30837e21255ae67b862a61bd6f68e
ms.contentlocale: zh-cn
ms.lasthandoff: 08/28/2017

---
# <a name="create-and-update-database-tables"></a>创建和更新数据库表

表设计器是一种可视化工具，用于设计和直观呈现[数据库表](../../relational-databases/tables/tables.md)。 使用 SQL Server Management Studio (SSMS) 表设计器创建、编辑或删除表、列、键、索引、关系和约束。  

  
## <a name="create-a-table"></a>创建表  
  
1. 右键单击数据库中的“表”节点，然后选择“新建” > “表”：  
  
    ![新建表](../media/design-tables/new-table.png)
  
1. 向表添加[列](column-properties-visual-database-tools.md)：
  
    ![设计表](../media/design-tables/new-table2.png)

1. 关闭设计器并保存更改。
  
## <a name="update-a-table"></a>更新表  
  
1. 右键单击数据库的“表”节点下的表，并选择“设计”：  
  
   ![更新表](../media/design-tables/update-table.png)

1. 更新所需的表设置：

   ![](../media/design-tables/update-table2.png)

1. 关闭设计器并保存更改。

## <a name="see-also"></a>另请参阅

[表](http://msdn.microsoft.com/82d7819c-b801-4309-a849-baa63083e83f)  
[表属性 (Visual Database Tools)](../../ssms/visual-db-tools/table-properties-visual-database-tools.md)  
[列属性](column-properties-visual-database-tools.md)  
[向表中添加列](../../relational-databases/tables/add-columns-to-a-table-database-engine.md)  
[主键和外键](../../relational-databases/tables/primary-and-foreign-key-constraints.md)  
[索引](../../relational-databases/indexes/indexes.md)  
[数据类型 (Transact-SQL)](../../t-sql/data-types/data-types-transact-sql.md)  
[下载 SQL Server Management Studio (SSMS)](../download-sql-server-management-studio-ssms.md)  

