---
title: "状态属性示例 （字段） (VB) |Microsoft 文档"
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: ado
ms.technology: drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.topic: article
dev_langs: VB
helpviewer_keywords: Status property [ADO Field], Visual Basic example
ms.assetid: fdd09b60-39c7-44be-8008-e891a031f80e
caps.latest.revision: "10"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 6e1abe338e6034fec34d1576b52af6df43970ea9
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/21/2017
---
# <a name="status-property-example-field-vb"></a>状态属性示例 （字段） (VB)
下面的示例从读/写文件夹使用打开文档[Internet 发布提供商](../../../ado/guide/appendixes/microsoft-ole-db-provider-for-internet-publishing.md)。 [状态](../../../ado/reference/ado-api/status-property-ado-field.md)属性[字段](../../../ado/reference/ado-api/field-object.md)对象[记录](../../../ado/reference/ado-api/record-object-ado.md)首先将设置为**adFieldPendingInsert**，则将更新到**adFieldOk**。  
  
```  
'BeginStatusFieldVB  
  
 ' to integrate this code replace the values in the source string  
  
Sub Main()  
  
   Dim File As ADODB.Record  
   Dim strFile As String  
   Dim Cnxn As ADODB.Connection  
   Dim strCnxn As String  
  
   Set Cnxn = New ADODB.Connection  
   strCnxn = "url=http://MyServer/"  
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
  
 以下示例将删除已知**字段**从**记录**从文档打开。 **状态**首先将属性设置为**adFieldOK**，然后**adFieldPendingUnknown**。  
  
```  
Attribute VB_Name = "StatusField"  
```  
  
 下面的代码删除**字段**从**记录**上只读的文档打开。 **状态**将设置为**adFieldPendingDelete**。 在[更新](../../../ado/reference/ado-api/update-method.md)，删除将失败并**状态**将**adFieldPendingDelete**加上**adFieldPermissionDenied**。 [正在执行](../../../ado/reference/ado-api/cancelupdate-method-ado.md)清除挂起**状态**设置。  
  
```  
Attribute VB_Name = "StatusField"  
```  
  
## <a name="see-also"></a>另请参阅  
 [字段对象](../../../ado/reference/ado-api/field-object.md)   
 [记录对象 (ADO)](../../../ado/reference/ado-api/record-object-ado.md)   
 [Status 属性（ADO 字段）](../../../ado/reference/ado-api/status-property-ado-field.md)
