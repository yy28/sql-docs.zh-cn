---
title: "筛选更新记录 |Microsoft 文档"
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
- filtering for updated records [ADO]
ms.assetid: 4a798921-d7bb-47c9-a252-550fd9463ec9
caps.latest.revision: 4
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: b633f10b4bac5ec6347879510e1867e7d5d14741
ms.contentlocale: zh-cn
ms.lasthandoff: 09/09/2017

---
# <a name="filtering-for-updated-records"></a>筛选更新的记录
在调用 UpdateBatch 之前，你可以使用要查看自该记录集打开后已更改的那些记录的记录集筛选器属性或 UpdateBatch 上次调用。 若要执行此操作，将筛选器设置为等于 adFilterPendingRecords 以确定将更新多少条记录下, 一节中的代码示例中所示。  
  
## <a name="remarks"></a>注释  
 此示例将 UpdateBatch 上例扩展通过筛选记录集，它调用 UpdateBatch 之前，显示用户的记录将更改，并允许她可以取消更新 （使用执行方法）。  
  
```  
'BeginFilterPend  
    '...  
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
  
    objRs1.Filter = adFilterPendingRecords  
  
    MsgBox "There are " & objRs1.RecordCount & " records pending.", _  
            , "Filter Pending"  
  
    ' Cancel the updates  
    objRs1.CancelBatch  
'EndFilterPend  
```  
  
## <a name="see-also"></a>另请参阅  
 [批处理模式](../../../ado/guide/data/batch-mode.md)

