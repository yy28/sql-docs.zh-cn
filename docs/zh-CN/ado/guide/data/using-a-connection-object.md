---
title: 使用连接对象 |Microsoft 文档
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
- connections [ADO]
ms.assetid: 4b34f971-5699-43e7-9b15-137d334fa66e
caps.latest.revision: 16
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 70342452aa10935b48e6698cd989a0be30fe5858
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
---
# <a name="using-a-connection-object"></a>使用连接对象
在打开之前**连接**对象，你必须定义有关的数据源和连接的类型的某些信息。 大部分此信息由持有*ConnectionString*参数[Open 方法](../../../ado/reference/ado-api/open-method-ado-connection.md)上**连接**对象，或通过[ConnectionString属性](../../../ado/reference/ado-api/connectionstring-property-ado.md)上**连接**对象。 连接字符串包含用分号分隔括在单引号内的值的参数/值对的列表。 例如：  
  
```  
Dim sConn As String  
sConn = "Provider='SQLOLEDB';Data Source='MySqlServer';" & _  
             "Initial Catalog='Northwind';Integrated Security='SSPI';"  
```  
  
> [!NOTE]
>  此外可以指定 ODBC 数据源名称 (DSN) 或数据链接 (UDL) 文件中的连接字符串。 有关 Dsn 的详细信息，请参阅[管理数据源](../../../odbc/admin/managing-data-sources.md)ODBC 程序员参考中。 Udl 有关的详细信息，请参阅[数据链接 API 概述](http://msdn.microsoft.com/en-us/95c180ea-bd4f-4dca-b95a-576afd135bbc)OLE DB 程序员参考中。  
  
 通常情况下，通过调用建立的连接**Connection.Open**与相应的方法*连接字符串*作为其参数。 在下面的 Visual Basic 代码段显示一个示例：  
  
```  
Dim oConn As ADODB.Connection  
Dim oRs As ADODB.Recordset  
Dim sConn As String  
Dim sSQL as String  
  
' Open a connection.  
Set oConn = New ADODB.Connection  
.Open   
  
' Make a query over the connection.  
sSQL = "SELECT ProductID, ProductName, CategoryID, UnitPrice " & _  
             "FROM Products"  
Set oRs = New ADODB.Recordset  
oRs.Open sSQL, , adOpenStatic, adLockBatchOptimistic, adCmdText  
  
MsgBox oRs.RecordCount  
  
' Close the connection.  
oConn.Close  
Set oConn = Nothing  
  
```  
  
 此处**oRs.Open**采用**连接**对象 (*oConn*) 变量的值作为其*ActiveConnection*参数。 此外， **Connection.CursorLocation**属性假定的默认值**adUseServer**。 相比之下[HelloData](../../../ado/guide/data/hellodata-a-simple-ado-application.md)在上一部分中的示例。 以下指令将导致运行时错误。  
  
```  
oRs.MarshalOptions = adMarshalModifiedOnly  
' Disconnect the Recordset.  
Set oRs.ActiveConnection = Nothing  
```
