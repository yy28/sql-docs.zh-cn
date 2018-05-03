---
title: 编辑数据 |Microsoft 文档
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: ado
ms.technology:
- drivers
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- ADO, editing data
- AdUseClient [ADO]
- editing data [ADO]
ms.assetid: ef514f85-c446-4f05-824e-c9313b2ffae1
caps.latest.revision: 16
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: e669880691cd61db355bdceb9323f51ebef1a6f6
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
---
# <a name="editing-data"></a>编辑数据
我们已介绍了如何使用 ADO 连接到数据源、 执行命令和获取结果中**记录集**对象，并在中导航**记录集**。 本部分重点介绍下一步的基本 ADO 操作： 编辑数据。  
  
 本部分将继续使用示例**记录集**中引入[检查数据](../../../ado/guide/data/examining-data.md)，与一个重要的更改。 下面的代码用于打开**记录集**:  
  
```  
'BeginEditIntro  
    Dim strSQL As String  
    Dim objRs1 As ADODB.Recordset  
  
    strSQL = "SELECT * FROM Shippers"  
  
    Set objRs1 = New ADODB.Recordset  
  
    objRs1.Open strSQL, GetNewConnection, adOpenStatic, _  
                adLockBatchOptimistic, adCmdText  
  
    ' Disconnect the Recordset from the Connection object.  
    Set objRs1.ActiveConnection = Nothing  
'EndEditIntro  
```  
  
 对代码的重要的更改包括设置**CursorLocation**属性**连接**对象等于**adUseClient**中*GetNewConnection*函数 （在下一步的示例中显示），这表示客户端游标的使用。 有关客户端和服务器端游标之间的差异的详细信息，请参阅[了解游标和锁定](../../../ado/guide/data/understanding-cursors-and-locks.md)。  
  
 **CursorLocation**属性的**adUseClient**设置将数据源 (SQL Server，在此情况下) 中的光标的位置移动到客户端代码 （桌面工作站） 的位置。 此设置将强制 ADO 以创建和管理光标在客户端上调用 OLE DB 客户端游标引擎。  
  
 你可能还具有注意到， **LockType**参数**打开**方法更改为**adLockBatchOptimistic**。 这将在批处理模式下打开光标。 (提供程序缓存多个更改，并将其写入到基础数据源仅在调用**UpdateBatch**方法。)对所做的更改**记录集**将不会更新在数据库中，直到**UpdateBatch**调用方法。  
  
 最后，本部分中的代码使用 GetNewConnection 函数的修改的版本。 此版本的函数现在可返回客户端游标。 该函数如下所示：  
  
```  
'BeginNewConnection  
Public Function GetNewConnection() As ADODB.Connection  
    On Error GoTo ErrHandler:  
  
    Dim objConn As New ADODB.Connection  
    Dim strConnStr As String  
  
    strConnStr = "Provider='SQLOLEDB';Initial Catalog='Northwind';" & _  
                 "Data Source='MySqlServer';Integrated Security='SSPI';"  
  
    objConn.ConnectionString = strConnStr  
    objConn.CursorLocation = adUseClient  
    objConn.Open  
  
    Set GetNewConnection = objConn  
  
    Exit Function  
  
ErrHandler:  
    Set objConn = Nothing  
    Set GetNewConnection = Nothing  
  
    If Err <> 0 Then  
        MsgBox Err.Source & "-->" & Err.Description, , "Error"  
    End If  
End Function  
'EndNewConnection  
```  
  
 本部分包含以下主题。  
  
-   [编辑现有记录](../../../ado/guide/data/editing-existing-records.md)  
  
-   [添加记录](../../../ado/guide/data/adding-records.md)  
  
-   [确定支持的功能](../../../ado/guide/data/determining-what-is-supported.md)  
  
-   [使用 Delete 方法删除记录](../../../ado/guide/data/deleting-records-using-the-delete-method.md)  
  
-   [替代方法：使用 SQL 语句](../../../ado/guide/data/alternatives-using-sql-statements.md)
