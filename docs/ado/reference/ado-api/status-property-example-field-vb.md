---
title: Status 属性示例（字段）（VB） |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
dev_langs:
- VB
helpviewer_keywords:
- Status property [ADO Field], Visual Basic example
ms.assetid: fdd09b60-39c7-44be-8008-e891a031f80e
author: MightyPen
ms.author: genemi
ms.openlocfilehash: c28a0b615a9f250c8539e87abf9fefbc11f513ee
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/26/2020
ms.locfileid: "67916830"
---
# <a name="status-property-example-field-vb"></a>Status 属性示例（字段）(VB)
下面的示例使用[Internet 发布提供程序](../../../ado/guide/appendixes/microsoft-ole-db-provider-for-internet-publishing.md)从读/写文件夹打开文档。 [记录](../../../ado/reference/ado-api/record-object-ado.md)的[Field](../../../ado/reference/ado-api/field-object.md)对象的[Status](../../../ado/reference/ado-api/status-property-ado-field.md)属性将首先设置为**AdFieldPendingInsert**，然后将其更新为**adFieldOk**。  
  
```  
'BeginStatusFieldVB  
  
 ' to integrate this code replace the values in the source string  
  
Sub Main()  
  
   Dim File As ADODB.Record  
   Dim strFile As String  
   Dim Cnxn As ADODB.Connection  
   Dim strCnxn As String  
  
   Set Cnxn = New ADODB.Connection  
   strCnxn = "url=https://MyServer/"  
   Cnxn.Open strCnxn  
  
   Set File = New ADODB.Record  
   strFile = "Folder/FileName"  
   ' Open a read/write document  
   File.Source = strFile  
   File.ActiveConnection = Cnxn  
   File.Mode = adModeReadWrite  
   File.Open  
  
   Debug.Print "Append a couple of fields"  
  
   File.Fields.Append "chektest:fld1", adWChar, 42, adFldUpdatable, "fld1"  
   File.Fields.Append "chektest:fld2", adWChar, 42, adFldUpdatable, "fld2"  
  
   Debug.Print "status for the fields"  
   Debug.Print File.Fields("chektest:fld1").Status 'adfldpendinginsert  
   Debug.Print File.Fields("chektest:fld2").Status 'adfldpendinginsert  
  
    'turn off error-handling to verify field status  
   On Error Resume Next  
  
   File.Fields.Update  
  
   Debug.Print "Update succeeds"  
   Debug.Print File.Fields("chektest:fld1").Status 'adfldpendinginsert + adFieldUnavailable  
   Debug.Print File.Fields("chektest:fld2").Status 'adfldpendinginsert + adFieldUnavailable  
  
    ' resume default error-handling  
   On Error GoTo 0  
  
     ' clean up  
    File.Close  
    Cnxn.Close  
    Set File = Nothing  
    Set Cnxn = Nothing  
  
End Sub  
'EndStatusFieldVB  
```  
  
 下面的示例从文档中打开的**记录**中删除已知**字段**。 **Status**属性将首先设置为**adFieldOK**，然后设置为**adFieldPendingUnknown**。  
  
```  
Attribute VB_Name = "StatusField"  
```  
  
 下面的代码从在只读文档上打开的**记录**中删除**字段**。 **状态**将设置为**adFieldPendingDelete**。 在[更新](../../../ado/reference/ado-api/update-method.md)时，删除将失败，并且**状态**将为**adFieldPendingDelete** + **adFieldPermissionDenied**。 [CancelUpdate](../../../ado/reference/ado-api/cancelupdate-method-ado.md)清除挂起**状态**设置。  
  
```  
Attribute VB_Name = "StatusField"  
```  
  
## <a name="see-also"></a>另请参阅  
 [Field 对象](../../../ado/reference/ado-api/field-object.md)   
 [Record 对象（ADO）](../../../ado/reference/ado-api/record-object-ado.md)   
 [Status 属性（ADO 字段）](../../../ado/reference/ado-api/status-property-ado-field.md)
