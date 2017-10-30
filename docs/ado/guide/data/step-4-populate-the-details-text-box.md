---
title: "步骤 4： 填充详细信息文本框中 |Microsoft 文档"
ms.prod: sql-non-specified
ms.technology:
- drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: 
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: cb4273e2-c907-4a86-a621-3bf110088228
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 512ad22b6529adcf065cacb219d1f0acc025c306
ms.contentlocale: zh-cn
ms.lasthandoff: 09/09/2017

---
# <a name="step-4-populate-the-details-text-box"></a>步骤 4： 填充详细信息文本框中
若要填充详细信息文本框中，创建一个名为的新子例程**recFields**并插入以下代码：  
  
```  
Sub recFields(r As Record, l As ListBox, t As TextBox)  
    Dim f As Field  
    Dim s As Stream  
    Set s = New Stream  
    Dim str As String  
  
    For Each f In r.Fields  
        l.AddItem f.Name & ": " & f.Value  
    Next  
    t.Text = ""  
    If r!RESOURCE_CONTENTCLASS = "text/plain" Then  
        s.Open r, adModeRead, adOpenStreamFromRecord  
        str = s.ReadText(1)  
        s.Position = 0  
        If Asc(Mid(str, 1, 1)) = 63 Then '//63 = "?"  
            s.Charset = "ascii"  
            s.Type = adTypeText  
        End If  
        t.Text = s.ReadText(adReadAll)  
    End If  
End Sub  
```  
  
 此代码用来填充`lstDetails`与字段和值传递到的简单记录`recFields`。 如果资源是一个文本文件，文本流被打开从该资源记录。 代码将确定是否为 ASCII 字符集，并将复制到的流内容`txtDetails`。  
  
## <a name="see-also"></a>另请参阅  
 [Internet 发布方案](../../../ado/guide/data/internet-publishing-scenario.md)   
 [步骤 3： 在字段列表框中填充](../../../ado/guide/data/step-3-populate-the-fields-list-box.md)

