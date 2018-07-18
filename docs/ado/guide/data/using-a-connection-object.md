---
title: 使用连接对象 |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
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
ms.openlocfilehash: e04067cda6fad31ebd07f5d887e387139c7739b1
ms.sourcegitcommit: c7a98ef59b3bc46245b8c3f5643fad85a082debe
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/12/2018
ms.locfileid: "38979769"
---
# <a name="using-a-connection-object"></a>使用连接对象
打开之前**连接**对象，必须定义数据源和连接类型的特定信息。 此信息大多数由*ConnectionString*的参数[Open 方法](../../../ado/reference/ado-api/open-method-ado-connection.md)上**连接**对象，或由[ConnectionString属性](../../../ado/reference/ado-api/connectionstring-property-ado.md)上**连接**对象。 连接字符串包含以分号分隔包含在单引号中的值的参数/值对的列表。 例如：  
  
```  
Dim sConn As String  
sConn = "Provider='SQLOLEDB';Data Source='MySqlServer';" & _  
             "Initial Catalog='Northwind';Integrated Security='SSPI';"  
```  
  
> [!NOTE]
>  此外可以指定 ODBC 数据源名称 (DSN) 或数据链接 (UDL) 文件中的连接字符串。 有关 Dsn 的详细信息，请参阅[管理数据源](../../../odbc/admin/managing-data-sources.md)中的 ODBC 程序员参考。 有关 Udl 的详细信息，请参阅[数据链接 API 概述](http://msdn.microsoft.com/95c180ea-bd4f-4dca-b95a-576afd135bbc)中的 OLE DB 程序员参考。  
  
 通常情况下，通过调用建立的连接**Connection.Open**相应方法*连接字符串*作为其参数。 在下面的 Visual Basic 代码段中显示一个示例：  
  
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
  
 这里**oRs.Open**采用**连接**对象 (*oConn*) 变量的值作为其*ActiveConnection*参数。 此外， **Connection.CursorLocation**属性假定的默认值**adUseServer**。 相比之下[HelloData](../../../ado/guide/data/hellodata-a-simple-ado-application.md)前一部分中的示例。 以下指令将导致运行时错误。  
  
```  
oRs.MarshalOptions = adMarshalModifiedOnly  
' Disconnect the Recordset.  
Set oRs.ActiveConnection = Nothing  
```
