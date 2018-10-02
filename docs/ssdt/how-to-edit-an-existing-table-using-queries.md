---
title: 如何：使用查询编辑现有表 | Microsoft Docs
ms.custom:
- SSDT
ms.date: 02/09/2017
ms.prod: sql
ms.technology: ssdt
ms.reviewer: ''
ms.topic: conceptual
ms.assetid: 58f4de8e-97b4-4bcb-953f-f3d428432491
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: b9687226caec47161fb42038994be279a89becc4
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/01/2018
ms.locfileid: "47659575"
---
# <a name="how-to-edit-an-existing-table-using-queries"></a>如何使用查询编辑现有表
可以通过编写 Transact\-SQL 查询编辑表或其数据的定义。 若要以直观方式查看或输入表中的数据，请使用[连接的数据库开发](../ssdt/connected-database-development.md)中介绍的数据编辑器。  
  
> [!WARNING]  
> 下面的过程利用在[连接的数据库开发](../ssdt/connected-database-development.md)一节的前面的过程中创建的实体。  
  
### <a name="to-edit-the-definition-of-an-existing-table"></a>编辑现有表的定义  
  
1.  在“SQL Server 对象资源管理器”中展开 Trade 数据库的“表”节点，然后右键单击 dbo.Suppliers。  
  
2.  选择“视图设计器”以便在表设计器中查看表架构。  
  
3.  为 Address 列选中“允许 Null 值”框。 请注意，脚本窗格中的相应代码将立即更改为 `NULL`。  
  
4.  按照[如何：使用 Power Buffer 更新连接的数据库](../ssdt/how-to-update-a-connected-database-with-power-buffer.md)主题中的步骤更新数据库。  
  
### <a name="to-populate-data-in-new-tables-using-a-transact-sql-query"></a>使用 Transact\-SQL 查询在新表中填充数据  
  
1.  右键单击 Trade 数据库节点并选择“新建查询”。  
  
2.  在脚本窗格中，粘贴以下代码。  
  
    ```  
    insert into dbo.Suppliers values  
    (1, 'NorthWind Traders', 'Seattle, WA'),  
    (2, 'Contoso', 'Tacoma, WA')  
    GO  
  
    insert dbo.Customer values  
    (1, 'Fourth Coffee')  
    GO  
  
    insert dbo.Products values  
    (1, 'Apples', 0, 1, 1),  
    (2, 'Instant Coffee', 1, 2, 1)  
    GO  
    ```  
  
3.  单击“执行查询”按钮以运行该查询。 “消息”窗格中的以下内容指示这些行已成功添加到表中。  
  
（2 行受影响）（1 行受影响）（2 行受影响）  
  
4.  用下面部分中的代码替换脚本窗格中的代码并且执行该查询。 这将尝试向 `Products` 表中添加 `ShelfLife` 为 6 的一个新行。  
  
    ```  
    insert dbo.Products values  
    (3, 'Potato Chips', 6, 1, 1)  
    GO  
    ```  
  
5.  “消息”窗格指示 `INSERT` 语句与现有 CHECK 约束冲突，这会将 `ShelfLife` 的值限制为低于 5。 由于该语句未能满足现有约束，因此将不更新 Products 表。  
  
6.  用以下代码更改该代码并且再次运行该查询。 请注意，此时该行成功更新。  
  
    ```  
    insert dbo.Products values  
    (3, 'Potato Chips', 2, 1, 1)  
    GO  
    ```  
  
## <a name="see-also"></a>另请参阅  
[管理表、关系和修复错误](../ssdt/manage-tables-relationships-and-fix-errors.md)  
[使用 Transact-SQL 编辑器编辑和执行脚本](../ssdt/use-transact-sql-editor-to-edit-and-execute-scripts.md)  
  
