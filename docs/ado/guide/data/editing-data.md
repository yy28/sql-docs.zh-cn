---
description: 编辑数据
title: 编辑数据 |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- ADO, editing data
- AdUseClient [ADO]
- editing data [ADO]
ms.assetid: ef514f85-c446-4f05-824e-c9313b2ffae1
author: rothja
ms.author: jroth
ms.openlocfilehash: b7fc5d177b05447637d635a9f132c9f9da086ef2
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/17/2020
ms.locfileid: "88453459"
---
# <a name="editing-data"></a>编辑数据
我们介绍了如何使用 ADO 连接到数据源、执行命令、获取 **记录集** 对象中的结果，以及在 **记录集中**导航。 本部分重点介绍下一基本 ADO 操作：编辑数据。  
  
 此部分继续使用[检查数据](../../../ado/guide/data/examining-data.md)时引入的示例**记录集**，其中一项重要更改。 以下代码用于打开 **记录集**：  
  
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
  
 代码的重要变化涉及到在*GetNewConnection*函数中设置等于**adUseClient**的**连接**对象的**CursorLocation**属性 (在下一个示例) 中显示，指示客户端游标的使用。 有关客户端和服务器端游标之间的差异的详细信息，请参阅 [了解游标和锁定](../../../ado/guide/data/understanding-cursors-and-locks.md)。  
  
 **CursorLocation**属性的**adUseClient**设置会将数据源中光标的位置移 (SQL Server，在这种情况下)  (桌面工作站) 的客户端代码的位置。 此设置强制 ADO 调用客户端上的 OLE DB 客户端游标引擎，以便创建和管理游标。  
  
 你可能还注意到， **Open**方法的**LockType**参数已更改为**adLockBatchOptimistic**。 这将在批处理模式下打开光标。  (提供程序缓存多个更改并仅在调用**updatebatch**方法时将这些更改写入基础数据源 ) 。在调用**updatebatch**方法之前，将不会在数据库中更新对**记录集**所做的更改。  
  
 最后，本部分中的代码使用 GetNewConnection 函数的修改版本。 此版本的函数现在返回客户端游标。 该函数如下所示：  
  
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
