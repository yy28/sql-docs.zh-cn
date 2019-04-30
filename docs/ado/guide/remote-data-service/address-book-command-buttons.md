---
title: 通讯簿命令按钮 |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 11/09/2018
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- address book application scenario [ADO], command buttons
- RDS scenarios [ADO], command buttons
ms.assetid: 80676831-6488-4dad-a558-c47c52256a22
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 5e3b29fd5f4fab7e487be5be18752ac7de892537
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63222022"
---
# <a name="address-book-command-buttons"></a>通讯簿命令按钮
通讯簿应用程序包括以下的命令按钮：  
  
-   一个**查找**按钮以提交到数据库的查询。  
  
-   一个**清除**按钮以启动新的搜索之前清除文本框。  
  
-   **更新配置文件**按钮将更改保存到员工记录。  
  
-   一个**取消更改**按钮可放弃更改。  
  
> [!IMPORTANT]
>  从 Windows 8 和 Windows Server 2012 开始，不再在 Windows 操作系统中包含 RDS 服务器组件 (请参阅 Windows 8 和[Windows Server 2012 兼容性指南](https://www.microsoft.com/download/details.aspx?id=27416)以了解详细信息)。 将 Windows 的未来版本中删除 RDS 客户端组件。 请避免在新的开发工作中使用该功能，并着手修改当前还在使用该功能的应用程序。 使用 RDS 的应用程序应迁移到[WCF 数据服务](https://go.microsoft.com/fwlink/?LinkId=199565)。  
  
## <a name="find-button"></a>查找按钮  
 单击**查找**按钮激活 VBScript Find_OnClick Sub 过程，用于生成和发送的 SQL 查询。 单击此按钮将填充数据网格。  
  
## <a name="building-the-sql-query"></a>生成 SQL 查询  
 Find_OnClick Sub 过程的第一部分通过将文本字符串追加到全球的 SQL SELECT 语句生成的 SQL 查询，一次一个短语。 它首先设置变量`myQuery`请求数据的所有行从数据源的表的 SQL SELECT 语句。 接下来，Sub 过程会扫描每个页上的四个输入框。  
  
 因为该程序使用 word`like`在构建 SQL 语句，查询是子字符串搜索，而不是完全匹配项。  
  
 例如，如果**姓氏**框包含条目"高"和**标题**框包含"经理"，SQL 语句的条目 (值为`myQuery`) 将读取：  
  
```sql
Select FirstName, LastName, Title, Email, Building, Room, Phone from Employee where lastname like 'Berge%' and title like 'Program Manager%'  
```  
  
 如果查询成功，HTML 数据网格中显示包含文本 （例如高和 Berger） 的"高"的最后一个名称和标题包含单词"项目经理"（例如，项目经理、 高级技术） 的所有人员。  
  
## <a name="preparing-and-sending-the-query"></a>准备并发送查询  
 Find_OnClick Sub 过程的最后一个部分包含两个语句。 第一条语句将分配[SQL](../../../ado/reference/rds-api/sql-property.md)属性的[rds。DataControl](../../../ado/reference/rds-api/datacontrol-object-rds.md)等于动态生成的 SQL 查询的对象。 第二个语句会导致**rds。DataControl**对象 (`DC1`) 来查询数据库，并在网格中然后显示新查询的结果。  
  
```vb
Sub Find_OnClick  
   '...  
   DC1.SQL = myQuery  
   DC1.Refresh  
End Sub  
```  
  
## <a name="update-profile-button"></a>更新配置文件按钮  
 单击**更新配置文件**按钮将激活 VBScript Update_OnClick Sub 过程中，执行[rds。DataControl](../../../ado/reference/rds-api/datacontrol-object-rds.md)对象的 (`DC1`) [SubmitChanges](../../../ado/reference/rds-api/submitchanges-method-rds.md)并[刷新](../../../ado/reference/rds-api/refresh-method-rds.md)方法。  
  
```vb
Sub Update_OnClick  
   DC1.SubmitChanges  
   DC1.Refresh  
End Sub  
```  
  
 当`DC1.SubmitChanges`执行时，远程数据服务包更新的所有信息并将其发送到通过 HTTP 服务器。 更新是要么;如果在更新过程不成功，进行任何更改，并返回一条状态消息。 `DC1.Refresh` 没有必要后**SubmitChanges**与远程数据服务，但它会确保新数据。  
  
## <a name="cancel-changes-button"></a>更改取消按钮  
 单击**取消更改**激活 VBScript Cancel_OnClick Sub 过程中，执行[rds。DataControl](../../../ado/reference/rds-api/datacontrol-object-rds.md)对象的 (`DC1)` [CancelUpdate](../../../ado/reference/rds-api/cancelupdate-method-rds.md)方法。  
  
```vb
Sub Cancel_OnClick  
   DC1.CancelUpdate  
End Sub  
```  
  
 当`DC1.CancelUpdate`执行时，它将放弃自上次查询或更新用户对数据网格上的员工记录所做的任何编辑。 它会还原原始值。  
  
## <a name="see-also"></a>请参阅  
 [通讯簿导航按钮](../../../ado/guide/remote-data-service/address-book-navigation-buttons.md)   
 [DataControl 对象 (RDS)](../../../ado/reference/rds-api/datacontrol-object-rds.md)


