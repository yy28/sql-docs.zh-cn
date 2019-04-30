---
title: 将参数传递给命名命令 |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- named commands [ADO]
- commands [ADO], passing parameters to a named command
ms.assetid: 36e0cdbe-7f50-40f5-af0d-700f5d8dc75a
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 4c221030b54aef21ffa0a2df891561976aacff76
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63302368"
---
# <a name="passing-parameters-to-a-named-command"></a>将参数传递给命名命令
只需命令的结果作为传递*出*变量的已命名的命令参数已参数化的命令可为传入的*中*命名命令的变量。  
  
 下面的代码示例尝试检索所有订单放置客户通过其**CustomerID**是来自 Northwind 数据库的"ALKFI"。 值**CustomerID**在调用已命名的命令时提供。  
  
```  
Const DS = "MySqlServer"  
Const DB = "Northwind"  
Const DP = "SQLOLEDB"  
  
Dim objConn As New ADODB.Connection  
Dim objRs As New ADODB.Recordset  
Dim objComm As New ADODB.Command  
  
CommandText = "SELECT OrderID, OrderDate, " & _  
                     "RequiredDate, ShippedDate " & _  
                     "FROM Orders " & _  
                     "WHERE CustomerID = ? " & _  
                     "ORDER BY OrderID"  
  
ConnectionString = "Provider=" & DP & _  
                   ";Data Source=" & DS & _  
                   ";Initial Catalog=" & DB & _  
                   ";Integrated Security=SSPI;"  
  
' Connect to the data source.  
objConn.Open ConnectionString  
  
' Set a named command.  
objComm.CommandText = CommandText  
objComm.CommandType = adCmdText  
objComm.Name = "GetOrdersOf"  
Set objComm.ActiveConnection = objConn  
  
' Call the named command, passing a CustomerID value  
' as the input parameter.   
'    "ALFKI" is the required input parameter,  
'    objRs is the resultant output variable.  
objConn.GetOrdersOf "ALKFI", objRs  
  
' Display the result.  
Debug.Print "All orders by ALFKI:"  
Do While Not objRs.EOF  
    Debug.Print vbTab & objRs(0) & vbTab & objRs(1) & vbTab & _  
                objRs(2) & vbTab & objRs(3)  
    objRs.MoveNext  
Loop  
  
' Clean up.  
objRs.Close  
objConn.Close  
Set objRs = Nothing  
Set objConn = Nothing  
Set objComm = Nothing  
```  
  
 请注意，所有输入的参数必须在之前的任何输出变量和参数的数据类型必须匹配或可以转换为与相应的字段。 以下语句-  
  
```  
objConn.GetOrdersOf 12345, objRs  
```  
  
 -将导致错误的数据类型不匹配，因为必需的输入的参数的**字符串**类型，不是**整数**类型。  
  
 以下调用-  
  
```  
objConn.GetOrdersOf "12345", objRs  
```  
  
 -虽然有效，但会产生空结果集，因为在数据库中不存在任何此类记录。  
  
## <a name="see-also"></a>请参阅  
 [连接对象 (ADO)](../../../ado/reference/ado-api/connection-object-ado.md)
