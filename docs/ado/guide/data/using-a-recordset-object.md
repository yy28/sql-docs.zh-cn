---
description: 使用记录集对象
title: 使用记录集对象 |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- connections [ADO]
ms.assetid: 01c630d8-eb35-4bd0-a99f-7c0f85316cc1
author: rothja
ms.author: jroth
ms.openlocfilehash: a9f75190ae5375b357d6baba93aac7aa2959e188
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/27/2020
ms.locfileid: "88979098"
---
# <a name="using-a-recordset-object"></a>使用记录集对象
或者，可以使用 " **记录集" 打开** 来隐式建立连接，并在单个操作中通过该连接发出命令。 例如，在 Visual Basic 中：  
  
```  
Dim oRs As ADODB.Recordset  
Dim sConn As String  
Dim sSQL as String  
  
sConn = "Provider='SQLOLEDB';Data Source='MySqlServer';" & _             "Initial Catalog='Northwind';Integrated Security='SSPI';"  
  
sSQL = "SELECT ProductID, ProductName, CategoryID, UnitPrice " & _  
             "FROM Products"  
  
' Create and Open the Recordset object.  
Set oRs = New ADODB.Recordset  
oRs.CursorLocation = adUseClient  
oRs.Open sSQL, sConn, adOpenStatic, _  
               adLockBatchOptimistic, adCmdText  
  
MsgBox oRs.RecordCount  
  
oRs.MarshalOptions = adMarshalModifiedOnly  
' Disconnect the Recordset.  
Set oRs.ActiveConnection = Nothing  
oRs.Close          
Set oRs = Nothing  
```  
  
 请注意， **or** 采用 (*sConn*) 的连接字符串来代替 **连接** 对象 (*oConn*) ，作为其 **ActiveConnection** 参数的值。 此外，通过在**Recordset**对象上设置**CursorLocation**属性来强制实施客户端游标类型。 同样，这与 **HelloData** 示例相反。
