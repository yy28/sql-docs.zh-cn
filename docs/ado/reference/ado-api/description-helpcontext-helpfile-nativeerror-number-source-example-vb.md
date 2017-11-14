---
title: "错误对象属性示例 (VB) |Microsoft 文档"
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: reference
ms.technology:
- drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.topic: article
dev_langs:
- VB
helpviewer_keywords:
- Number property [ADO], Visual Basic example
- Source property [ADO], Visual Basic example
- NativeError property [ADO], Visual Basic example
- Description property [ADO], Visual Basic example
- HelpFile property [ADO], Visual Basic example
- SQLState property [ADO], Visual Basic example
- HelpContext property [ADO], Visual Basic example
ms.assetid: 5c728458-d85c-497c-afcf-2cfa36c3342a
caps.latest.revision: 10
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 43385a04975c36109c420d3137c205bd184b121f
ms.contentlocale: zh-cn
ms.lasthandoff: 09/09/2017

---
# <a name="description-helpcontext-helpfile-nativeerror-number-source-and-sqlstate-properties-example-vb"></a>描述、 HelpContext、 HelpFile、 NativeError、 数量、 源和 SQLState 属性示例 (VB)
此示例将触发错误、 捕获它，并显示[说明](../../../ado/reference/ado-api/description-property.md)， [HelpContext](../../../ado/reference/ado-api/helpcontext-helpfile-properties.md)， [HelpFile](../../../ado/reference/ado-api/helpcontext-helpfile-properties.md)， [NativeError](../../../ado/reference/ado-api/nativeerror-property-ado.md)， [数](../../../ado/reference/ado-api/number-property-ado.md)，[源](../../../ado/reference/ado-api/source-property-ado-error.md)，和[SQLState](../../../ado/reference/ado-api/sqlstate-property.md)的生成属性[错误](../../../ado/reference/ado-api/error-object.md)对象。  
  
```  
'BeginDescriptionVB  
Public Sub Main()  
  
    Dim Cnxn As ADODB.Connection  
    Dim Err As ADODB.Error  
    Dim strError As String  
  
    On Error GoTo ErrorHandler  
  
    ' Intentionally trigger an error  
    Set Cnxn = New ADODB.Connection  
    Cnxn.Open "nothing"  
  
    Set Cnxn = Nothing  
    Exit Sub  
  
ErrorHandler:  
  
    ' Enumerate Errors collection and display  
    ' properties of each Error object  
    For Each Err In Cnxn.Errors  
        strError = "Error #" & Err.Number & vbCr & _  
            "   " & Err.Description & vbCr & _  
            "   (Source: " & Err.Source & ")" & vbCr & _  
            "   (SQL State: " & Err.SQLState & ")" & vbCr & _  
            "   (NativeError: " & Err.NativeError & ")" & vbCr  
        If Err.HelpFile = "" Then  
            strError = strError & "   No Help file available"  
        Else  
            strError = strError & _  
               "   (HelpFile: " & Err.HelpFile & ")" & vbCr & _  
               "   (HelpContext: " & Err.HelpContext & ")" & _  
               vbCr & vbCr  
        End If  
  
        Debug.Print strError  
    Next  
  
    Resume Next  
End Sub  
'EndDescriptionVB  
```  
  
## <a name="see-also"></a>另请参阅  
 [Description 属性](../../../ado/reference/ado-api/description-property.md)   
 [错误对象](../../../ado/reference/ado-api/error-object.md)   
 [HelpContext，HelpFile 属性](../../../ado/reference/ado-api/helpcontext-helpfile-properties.md)   
 [HelpContext，HelpFile 属性](../../../ado/reference/ado-api/helpcontext-helpfile-properties.md)   
 [NativeError 属性 (ADO)](../../../ado/reference/ado-api/nativeerror-property-ado.md)   
 [Number 属性 (ADO)](../../../ado/reference/ado-api/number-property-ado.md)   
 [源属性 （ADO 错误）](../../../ado/reference/ado-api/source-property-ado-error.md)   
 [SQLState 属性](../../../ado/reference/ado-api/sqlstate-property.md)

