---
title: 使用连接对象 |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- connections [ADO]
ms.assetid: 4b34f971-5699-43e7-9b15-137d334fa66e
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 4f1b867e1870b81641c7cea09d9a8fb3accfcc01
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/08/2020
ms.locfileid: "67923648"
---
# <a name="using-a-connection-object"></a>使用连接对象
在打开**连接**对象之前，必须定义有关数据源和连接类型的某些信息。 此信息中的大部分信息由**connection**对象上[Open 方法](../../../ado/reference/ado-api/open-method-ado-connection.md)的*connectionstring*参数或**连接**对象的[connectionstring 属性](../../../ado/reference/ado-api/connectionstring-property-ado.md)保存。 连接字符串包含由分号分隔的参数/值对列表，其值括在单引号内。 例如：  
  
```  
Dim sConn As String  
sConn = "Provider='SQLOLEDB';Data Source='MySqlServer';" & _  
             "Initial Catalog='Northwind';Integrated Security='SSPI';"  
```  
  
> [!NOTE]
>  你还可以在连接字符串中指定 ODBC 数据源名称（DSN）或数据链接（UDL）文件。 有关 Dsn 的详细信息，请参阅 ODBC 程序员参考中的[管理数据源](../../../odbc/admin/managing-data-sources.md)。 有关 Udl 的详细信息，请参阅 OLE DB 程序员参考中的[数据链接 API 概述](https://msdn.microsoft.com/95c180ea-bd4f-4dca-b95a-576afd135bbc)。  
  
 通常，通过调用**连接. Open**方法并使用适当的*连接字符串*作为参数，建立连接。 以下 Visual Basic 代码片段显示了一个示例：  
  
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
  
 此处**or**使用**连接**对象（*OConn*）变量作为其*ActiveConnection*参数的值。 此外， **CursorLocation**属性采用**adUseServer**的默认值。 与上一节中的[HelloData](../../../ado/guide/data/hellodata-a-simple-ado-application.md)示例相反。 以下指令将导致运行时错误。  
  
```  
oRs.MarshalOptions = adMarshalModifiedOnly  
' Disconnect the Recordset.  
Set oRs.ActiveConnection = Nothing  
```
