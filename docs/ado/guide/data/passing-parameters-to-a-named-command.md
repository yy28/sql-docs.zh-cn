---
title: "将参数传递给命名命令 |Microsoft 文档"
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: guide
ms.technology:
- drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- named commands [ADO]
- commands [ADO], passing parameters to a named command
ms.assetid: 36e0cdbe-7f50-40f5-af0d-700f5d8dc75a
caps.latest.revision: 12
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 33d1ee3fe4e24695deccd0615f17868bfdfd988c
ms.contentlocale: zh-cn
ms.lasthandoff: 09/09/2017

---
# <a name="passing-parameters-to-a-named-command"></a>将参数传递给命名命令
就像该命令的结果作为传递*出*变量命名的命令中，参数来参数化的命令可以被传入的作为*中*命名命令的变量。  
  
 下面的代码示例尝试检索所有订单放置客户其**CustomerID**是来自 Northwind 数据库的"ALKFI"。 值**CustomerID**在调用命名的命令时提供。  
  
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
  
 请注意所有输入的参数必须优先于任何输出变量，并且参数的数据类型必须匹配，或可以转换为与相应的字段。 下面的语句-  
  
```  
objConn.GetOrdersOf 12345, objRs  
```  
  
 -将导致错误的不匹配的数据类型，因为所需的输入的参数属于**字符串**类型，不是**整数**类型。  
  
 以下调用-  
  
```  
objConn.GetOrdersOf "12345", objRs  
```  
  
 -有效，但会产生任何设置，因为数据库中不存在任何此类记录了空结果。  
  
## <a name="see-also"></a>另请参阅  
 [连接对象 (ADO)](../../../ado/reference/ado-api/connection-object-ado.md)

