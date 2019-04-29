---
title: 筛选更新的记录 |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- filtering for updated records [ADO]
ms.assetid: 4a798921-d7bb-47c9-a252-550fd9463ec9
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 74ea4a208cad079933b27a7305a5ce0462e08515
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63161371"
---
# <a name="filtering-for-updated-records"></a>筛选更新的记录
在调用 UpdateBatch 之前，可以使用记录集筛选器属性，若要查看已打开记录集后已更改的记录或到 UpdateBatch 的最后一个调用。 若要执行此操作，请将筛选器设置为 adFilterPendingRecords 来确定将更新多少条记录下, 一节中的代码示例中所示。  
  
## <a name="remarks"></a>备注  
 此示例将上例 UpdateBatch 扩展通过筛选记录集，只需调用 UpdateBatch 之前，显示用户的记录将更改并允许用户取消更新 （使用 CancelBatch 方法）。  
  
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
  
## <a name="see-also"></a>请参阅  
 [批处理模式](../../../ado/guide/data/batch-mode.md)
