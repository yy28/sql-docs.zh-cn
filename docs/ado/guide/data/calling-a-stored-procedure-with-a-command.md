---
title: 调用带有命令的存储的过程 |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- calling stored procedures [ADO]
- stored procedures [ADO]
- commands [ADO]
ms.assetid: 685f7652-2271-4ede-b552-2eeb8c756b4c
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 35c1fce22e700ddd7ca2e738449a7b8b4ce4a63a
ms.sourcegitcommit: 63b4f62c13ccdc2c097570fe8ed07263b4dc4df0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/13/2018
ms.locfileid: "51601468"
---
# <a name="calling-a-stored-procedure-with-a-command"></a>使用命令调用存储过程
命令可用于调用存储的过程。 在本主题末尾的代码示例引用名为 CustOrdersOrders，按如下所示定义 Northwind 示例数据库中的存储过程。  
  
```  
CREATE PROCEDURE CustOrdersOrders @CustomerID nchar(5) AS  
SELECT OrderID, OrderDate, RequiredDate, ShippedDate  
FROM Orders  
WHERE CustomerID = @CustomerID  
ORDER BY OrderID  
```  
  
 请参阅 SQL Server 文档中的详细了解如何定义和调用存储过程。  
  
 此存储的过程是类似于在所使用的命令[命令对象参数](../../../ado/guide/data/command-object-parameters.md)。 它获取客户 ID 参数并返回有关该客户的订单信息。 下面的代码示例使用此存储的过程作为源 ADO**记录集**。  
  
 使用存储的过程可访问的 ADO 另一个功能：**参数**集合**刷新**方法。 通过使用此方法，ADO 可以自动填充该命令在运行时所需的参数有关的所有信息。 存在使用此技术，是对性能产生负面影响，因为 ADO 必须查询的参数信息的数据源。  
  
 下面的代码示例和中的代码之间存在其他重要的区别[命令对象参数](../../../ado/guide/data/command-object-parameters.md)，后者手动输入参数。 首先，此代码不会设置**已准备**属性设置为**True**因为它是 SQL Server 存储过程，通过定义预编译。 第二个， **CommandType**的属性**命令**对象更改为**adCmdStoredProc**在第二个示例中，以通知 ADO 命令已存储的过程。  
  
 最后，在第二个示例中该参数必须引用按索引时设置值，因为可能不知道在设计时的参数的名称。 如果您知道参数的名称，则可以设置新[NamedParameters](../../../ado/reference/ado-api/namedparameters-property-ado.md)的属性**命令**对象为 True，并引用该属性的名称。 您可能想知道为什么的第一个参数的位置所述的存储过程 (@CustomerID) 为 1 而不是 0 (`objCmd(1) = "ALFKI"`)。 这是因为参数 0 包含的 SQL Server 存储过程的返回值。  
  
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
 [知识库文章 117500](https://go.microsoft.com/fwlink/?LinkId=117500)
