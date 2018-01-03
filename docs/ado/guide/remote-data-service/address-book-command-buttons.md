---
title: "通讯簿命令按钮 |Microsoft 文档"
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: ado
ms.technology: drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- address book application scenario [ADO], command buttons
- RDS scenarios [ADO], command buttons
ms.assetid: 80676831-6488-4dad-a558-c47c52256a22
caps.latest.revision: "16"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 878878f11c6d1083d261e592a57a6b28ae793b56
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/21/2017
---
# <a name="address-book-command-buttons"></a>通讯簿命令按钮
通讯簿应用程序包括以下的命令按钮：  
  
-   A**查找**按钮以提交到数据库的查询。  
  
-   A**清除**按钮以启动新的搜索之前清除文本框。  
  
-   **更新配置文件**按钮以保存对雇员记录的更改。  
  
-   A**取消更改**按钮以放弃更改。  
  
> [!IMPORTANT]
>  从 Windows 8 和 Windows Server 2012 开始，不再在 Windows 操作系统中包含 RDS 服务器组件 (请参阅 Windows 8 和[Windows Server 2012 兼容性手册](https://www.microsoft.com/en-us/download/details.aspx?id=27416)有关详细信息)。 将 Windows 的未来版本中删除 RDS 客户端组件。 请避免在新的开发工作中使用该功能，并着手修改当前还在使用该功能的应用程序。 使用 RDS 的应用程序应迁移到[WCF 数据服务](http://go.microsoft.com/fwlink/?LinkId=199565)。  
  
## <a name="find-button"></a>查找按钮  
 单击**查找**按钮激活 VBScript Find_OnClick Sub 过程，用于生成和发送 SQL 查询。 单击此按钮将填充数据网格。  
  
## <a name="building-the-sql-query"></a>生成 SQL 查询  
 Find_OnClick Sub 过程的第一部分通过将文本字符串追加到全局 SQL SELECT 语句生成 SQL 查询，一次一个短语。 它首先会通过设置变量`myQuery`到请求的数据的所有行从数据源表的 SQL SELECT 语句。 接下来，Sub 过程扫描每个页上的四个输入框。  
  
 因为该程序使用 word`like`在生成 SQL 语句，查询是子字符串搜索，而不是完全匹配。  
  
 例如，如果**姓氏**框中包含的条目"高"和**标题**框包含条目的 SQL 语句"程序管理员"(值`myQuery`) 将读取：  
  
```  
Select FirstName, LastName, Title, Email, Building, Room, Phone from Employee where lastname like 'Berge%' and title like 'Program Manager%'  
```  
  
 如果查询成功，最后一个名称包含的文本 （例如高和高阳） 的"高"，且职务中包含单词"项目经理"（例如，项目经理，高级技术） 的所有人员 HTML 数据网格中都显示。  
  
## <a name="preparing-and-sending-the-query"></a>准备和发送查询  
 Find_OnClick Sub 过程的最后部分由两个语句组成。 第一个语句将赋[SQL](../../../ado/reference/rds-api/sql-property.md)属性[rds.DataControl](../../../ado/reference/rds-api/datacontrol-object-rds.md)等于动态生成的 SQL 查询的对象。 第二个语句会导致**rds.DataControl**对象 (`DC1`) 并将检索查询数据库，然后在网格中显示新查询的结果。  
  
```  
Sub Find_OnClick  
   '...  
   DC1.SQL = myQuery  
   DC1.Refresh  
End Sub  
```  
  
## <a name="update-profile-button"></a>更新配置文件按钮  
 单击**更新配置文件**按钮激活 VBScript Update_OnClick Sub 过程中，执行[rds.DataControl](../../../ado/reference/rds-api/datacontrol-object-rds.md)对象的 (`DC1`) [SubmitChanges](../../../ado/reference/rds-api/submitchanges-method-rds.md)和[刷新](../../../ado/reference/rds-api/refresh-method-rds.md)方法。  
  
```  
Sub Update_OnClick  
   DC1.SubmitChanges  
   DC1.Refresh  
End Sub  
```  
  
 当`DC1.SubmitChanges`执行，远程数据服务包更新的所有信息并将其发送到通过 HTTP 服务器。 此更新是全盘接受或者全盘;如果成功更新的一部分，进行任何更改，并返回一条状态消息。 `DC1.Refresh`不需要后**SubmitChanges**与远程数据服务，但可确保刷新的数据。  
  
## <a name="cancel-changes-button"></a>取消更改按钮  
 单击**取消更改**激活 VBScript Cancel_OnClick Sub 过程中，执行[rds.DataControl](../../../ado/reference/rds-api/datacontrol-object-rds.md)对象的 (`DC1)` [正在执行](../../../ado/reference/rds-api/cancelupdate-method-rds.md)方法。  
  
```  
Sub Cancel_OnClick  
   DC1.CancelUpdate  
End Sub  
```  
  
 当`DC1.CancelUpdate`执行，则会丢弃自最后一个查询或更新用户对在数据网格上的员工记录所做的任何编辑。 它会还原原始值。  
  
## <a name="see-also"></a>另请参阅  
 [通讯簿导航按钮](../../../ado/guide/remote-data-service/address-book-navigation-buttons.md)   
 [DataControl 对象 (RDS)](../../../ado/reference/rds-api/datacontrol-object-rds.md)


