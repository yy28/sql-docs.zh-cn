---
title: ADO 事件实例化：Visual Basic |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
dev_langs:
- VB
ms.assetid: dce0a2a3-326f-4aaf-a822-6c5549833afa
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 590a3c282492fd07a86eae1715ffc9b027764fac
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/15/2019
ms.locfileid: "66702420"
---
# <a name="ado-event-instantiation-visual-basic"></a>ADO 事件实例化：Visual Basic
若要处理 Microsoft® Visual Basic® 中的 ADO 事件，必须声明模块级变量 using **WithEvents**关键字。 变量可以声明仅为类模块的一部分，且必须在模块级别声明。 这不是限制性最高，因为它看上去，但是，因为 Visual Basic**窗体**对象也是类。 处理 ADO 事件的最简单方法是声明变量的使用**WithEvents**。 下面的示例处理**ConnectComplete**事件**连接**对象：  
  
```  
' BeginEventExampleVB02  
Dim WithEvents connEvent As Connection  
Attribute connEvent.VB_VarHelpID = -1  
  
Private Sub Form_Load()  
Dim strConn As String  
  
   ' Create a new object with event  
   ' handling enabled.  
   strConn = "Provider=sqloledb;" & _  
      "Data Source=MyServer;" & _  
      "Initial Catalog=Northwind;" & _  
      "Integrated Security=SSPI;"  
   Set connEvent = New ADODB.Connection  
   connEvent.Open strConn  
End Sub  
  
Private Sub connEvent_ConnectComplete(ByVal pError As ADODB.Error, _  
    adStatus As ADODB.EventStatusEnum, _  
    ByVal pConnection As ADODB.Connection)  
Dim strMsg As String  
  
   If adStatus = adStatusErrorsOccurred Then  
      Select Case pError.Number  
         Case adErrOperationCancelled  
            ' The operation was cancelled in the  
            ' Will event. Notify the user and exit.  
            strMsg = "I'm sorry you can't connect right now." & vbCrLf  
            strMsg = strMsg & "Click OK to exit."  
            Unload Me  
         Case Else  
            strMsg = "Error " & Format(pError.Number) & vbCrLf  
            strMsg = strMsg & pError.Description  
            strMsg = strMsg & "Click OK to exit."  
            Unload Me  
      End Select  
   End If  
   frmWait.btnOK.Enabled = True  
End Sub  
' EndEventExampleVB02  
```  
  
 **连接**处声明对象**窗体**级别使用**WithEvents**关键字来启用事件处理。 Form_Load 事件处理程序实际上会通过将分配一个新创建对象**连接**对象传递给*connEvent*信息，然后打开该连接。 当然，实际的应用程序可以实现更多的处理在 Form_Load 事件处理程序与此处所示。
