---
title: 步骤 3：字段列表框中填充 |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
ms.assetid: 315c32dc-aeb1-4629-b30e-87b44e8f84d1
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: f69ab97a522e148d8027042ff7e2c6b09a690424
ms.sourcegitcommit: 074d44994b6e84fe4552ad4843d2ce0882b92871
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/05/2019
ms.locfileid: "66704825"
---
# <a name="step-3-populate-the-fields-list-box"></a>步骤 3：填充字段列表框
若要填充的字段列表框中，将以下代码插入的单击事件处理程序`lstMain`:  
  
```  
Private Sub lstMain_Click()  
    Dim rec As Record  
    Dim rs As Recordset  
    Set rec = New Record  
    Set rs = New Recordset  
    grs.MoveFirst  
    grs.Move lstMain.ListIndex  
    lstDetails.Clear  
    rec.Open grs  
    Select Case rec.RecordType  
        Case adCollectionRecord:  
            Set rs = rec.GetChildren  
            While Not rs.EOF  
                lstDetails.AddItem rs(0)  
                rs.MoveNext  
            Wend  
        Case adSimpleRecord:  
            recFields rec, lstDetails, txtDetails  
  
        Case adStructDoc:  
    End Select  
  
End Sub  
```  
  
 此代码声明并实例化本地记录和记录集对象，`rec`和`rs`分别。  
  
 在选定的资源相对应的行`lstMain`进行的当前行`grs`。 然后清除的详细信息列表框并`rec`使用的当前行打开`grs`作为源。  
  
 如果资源是集合记录，由指定[RecordType](../../../ado/reference/ado-api/recordtype-property-ado.md)，本地记录集`rs`rec 子级上打开。然后`lstDetails`中的行的值填充`rs`。  
  
 如果资源是一个简单的记录，`recFields`调用。 有关详细信息`recFields`，请参阅下一步。  
  
 如果资源是结构化的文档，不实现任何代码。  
  
## <a name="see-also"></a>请参阅  
 [Internet 发布方案](../../../ado/guide/data/internet-publishing-scenario.md)   
 [步骤 2：初始化主列表框](../../../ado/guide/data/step-2-initialize-the-main-list-box.md)   
 [步骤 4：填充详细信息文本框中](../../../ado/guide/data/step-4-populate-the-details-text-box.md)
