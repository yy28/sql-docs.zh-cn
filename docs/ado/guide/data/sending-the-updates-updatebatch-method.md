---
title: 发送更新：UpdateBatch 方法 |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
ms.assetid: 87123797-831f-48e0-94b5-f669f9ca194a
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 6759f007e652a6a52a1633b021553faa2978f6b7
ms.sourcegitcommit: 074d44994b6e84fe4552ad4843d2ce0882b92871
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/05/2019
ms.locfileid: "66706646"
---
# <a name="sending-the-updates-updatebatch-method"></a>发送更新：UpdateBatch 方法
下面的代码通过 LockType 属性设置为 adLockBatchOptimistic 和到 adUseClient CursorLocation 在批处理模式下打开的记录集。 它将添加两个新记录和保存的原始值的现有记录中的字段的值更改，然后调用 UpdateBatch 将所做的更改回数据源。  
  
## <a name="remarks"></a>备注  
  
```  
'BeginBatchUpdate  
    strConn = "Provider=SQLOLEDB;Initial Catalog=Northwind;" & _  
              "Data Source=MySQLServer;Integrated Security=SSPI;"  
  
    strSQL = "SELECT ShipperId, CompanyName, Phone FROM Shippers"  
  
    Set objRs1 = New ADODB.Recordset  
    objRs1.CursorLocation = adUseClient  
    objRs1.Open strSQL, strConn, adOpenStatic, adLockBatchOptimistic, adCmdText  
  
    ' Change value of Phone field for first record in Recordset, saving value  
    ' for later restoration.  
    intId = objRs1("ShipperId")  
    sPhone = objRs1("Phone")  
  
    objRs1("Phone") = "(111) 555-1111"  
  
    'Add two new records  
    For i = 0 To 1  
        objRs1.AddNew  
        objRs1(1) = "New Shipper #" & CStr((i + 1))  
        objRs1(2) = "(nnn) 555-" & i & i & i & i  
    Next i  
  
    ' Send the updates  
    objRs1.UpdateBatch  
'EndBatchUpdate  
```  
  
 如果正在编辑当前记录或添加新记录时调用 UpdateBatch 方法时，ADO 将自动调用 Update 方法将再传输到提供程序的批处理的更改保存到当前记录的任何挂起的更改。  
  
## <a name="see-also"></a>请参阅  
 [批处理模式](../../../ado/guide/data/batch-mode.md)
