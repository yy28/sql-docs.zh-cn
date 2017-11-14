---
title: "将更新发送： UpdateBatch 方法 |Microsoft 文档"
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
ms.assetid: 87123797-831f-48e0-94b5-f669f9ca194a
caps.latest.revision: 3
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 6cad1bfd63ffafd32d0621f6142717cd7175ccd0
ms.contentlocale: zh-cn
ms.lasthandoff: 09/09/2017

---
# <a name="sending-the-updates-updatebatch-method"></a>将更新发送： UpdateBatch 方法
下面的代码将 LockType 属性设置为 adLockBatchOptimistic 和到 adUseClient CursorLocation，在批处理模式下打开记录集。 它将添加两条新记录和更改中保存的原始值的现有记录的字段的值，然后调用 UpdateBatch 将所做的更改回数据源。  
  
## <a name="remarks"></a>注释  
  
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
  
 如果你正在编辑当前记录或添加新记录时在调用 UpdateBatch 方法时，ADO 将自动调用更新方法来传输到提供程序的批处理的更改前将所有挂起的更改保存到当前记录。  
  
## <a name="see-also"></a>另请参阅  
 [批处理模式](../../../ado/guide/data/batch-mode.md)

