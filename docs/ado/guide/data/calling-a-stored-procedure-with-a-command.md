---
title: 调用存储的过程使用命令 |Microsoft 文档
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
- calling stored procedures [ADO]
- stored procedures [ADO]
- commands [ADO]
ms.assetid: 685f7652-2271-4ede-b552-2eeb8c756b4c
caps.latest.revision: 15
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 63e2b0c1958f680b85bfe8b1df99442cc588b291
ms.sourcegitcommit: 62826c291db93c9017ae219f75c3cfeb8140bf06
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/11/2018
ms.locfileid: "35270446"
---
# <a name="calling-a-stored-procedure-with-a-command"></a>调用存储的过程使用命令
命令可用于调用存储的过程。 本主题末尾处的代码示例是指在 Northwind 示例数据库中，调用 CustOrdersOrders，按以下方式定义的存储过程。  
  
```  
CREATE PROCEDURE CustOrdersOrders @CustomerID nchar(5) AS  
SELECT OrderID, OrderDate, RequiredDate, ShippedDate  
FROM Orders  
WHERE CustomerID = @CustomerID  
ORDER BY OrderID  
```  
  
 请参阅 SQL Server 文档详细了解如何定义和调用存储过程。  
  
 此存储的过程是类似于命令中使用[命令对象参数](../../../ado/guide/data/command-object-parameters.md)。 它采用客户 ID 参数，并返回有关该客户的订单的信息。 下面的代码示例使用此存储的过程作为源 ADO**记录集**。  
  
 使用存储的过程允许你访问的 ADO 另一个功能：**参数**集合**刷新**方法。 通过使用此方法，ADO 可以自动填写该命令在运行时所需的参数有关的所有信息。 存在使用此技术，是对性能产生负面影响，因为 ADO 必须查询的参数的信息的数据源。  
  
 下面的代码示例和中的代码之间存在一些其他重要的差异[命令对象参数](../../../ado/guide/data/command-object-parameters.md)，后者手动输入参数。 首先，此代码不会设置**已准备**属性**True**因为它是 SQL Server 存储过程，通过定义预编译。 第二个， **CommandType**属性**命令**对象更改为**adCmdStoredProc**在第二个示例中，以通知 ADO 命令是存储的过程。  
  
 最后，在第二个示例参数必须是通过索引引用时设置值，因为你可能不在设计时知道参数的名称。 如果您知道参数的名称，则可以设置新[NamedParameters](../../../ado/reference/ado-api/namedparameters-property-ado.md)属性**命令**对象为 True，并引用该属性的名称。 你可能想知道的第一个参数的位置中存储过程所述的原因 (@CustomerID) 为 1 而不是 0 (`objCmd(1) = "ALFKI"`)。 这是因为参数 0 包含的 SQL Server 存储过程的返回值。  
  
```  
'BeginAutoParamCmd  
    On Error GoTo ErrHandler:  
  
    Dim objConn As New ADODB.Connection  
    Dim objCmd As New ADODB.Command  
    Dim objParm1 As New ADODB.Parameter  
    Dim objRs As New ADODB.Recordset  
  
    ' Set CommandText equal to the stored procedure name.  
    objCmd.CommandText = "CustOrdersOrders"  
    objCmd.CommandType = adCmdStoredProc  
  
    ' Connect to the data source.  
    Set objConn = GetNewConnection  
    objCmd.ActiveConnection = objConn  
  
    ' Automatically fill in parameter info from stored procedure.  
    objCmd.Parameters.Refresh  
  
    ' Set the param value.  
    objCmd(1) = "ALFKI"  
  
    ' Execute once and display...  
    Set objRs = objCmd.Execute  
  
    Debug.Print objParm1.Value  
    Do While Not objRs.EOF  
        Debug.Print vbTab & objRs(0) & vbTab & objRs(1) & vbTab & _  
                    objRs(2) & vbTab & objRs(3)  
        objRs.MoveNext  
    Loop  
  
    ' ...then set new param value, re-execute command, and display.  
    objCmd(1) = "CACTU"  
    Set objRs = objCmd.Execute  
  
    Debug.Print objParm1.Value  
    Do While Not objRs.EOF  
        Debug.Print vbTab & objRs(0) & vbTab & objRs(1) & vbTab & _  
                    objRs(2) & vbTab & objRs(3)  
        objRs.MoveNext  
    Loop  
  
    'clean up  
    objRs.Close  
    objConn.Close  
    Set objRs = Nothing  
    Set objConn = Nothing  
    Set objCmd = Nothing  
    Set objParm1 = Nothing  
    Exit Sub  
  
ErrHandler:  
    'clean up  
    If objRs.State = adStateOpen Then  
        objRs.Close  
    End If  
  
    If objConn.State = adStateOpen Then  
        objConn.Close  
    End If  
  
    Set objRs = Nothing  
    Set objConn = Nothing  
    Set objCmd = Nothing  
    Set objParm1 = Nothing  
  
    If Err <> 0 Then  
        MsgBox Err.Source & "-->" & Err.Description, , "Error"  
    End If  
'EndAutoParamCmd  
  
'BeginNewConnection  
Private Function GetNewConnection() As ADODB.Connection  
    Dim oCn As New ADODB.Connection  
    Dim sCnStr As String  
  
    sCnStr = "Provider='SQLOLEDB';Data Source='MySqlServer';" & _  
             "Integrated Security='SSPI';Initial Catalog='Northwind';"  
    oCn.Open sCnStr  
  
    If oCn.State = adStateOpen Then  
        Set GetNewConnection = oCn  
    End If  
  
End Function  
'EndNewConnection  
```  
  
## <a name="see-also"></a>请参阅  
 [知识库文章 117500](http://go.microsoft.com/fwlink/?LinkId=117500)
