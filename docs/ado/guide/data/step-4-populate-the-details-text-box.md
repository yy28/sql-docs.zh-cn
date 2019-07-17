---
title: 步骤 4：详细信息文本框中填充 |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
ms.assetid: cb4273e2-c907-4a86-a621-3bf110088228
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 90748ca7f725ddbf947d9686b846695da0c6626c
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/15/2019
ms.locfileid: "67924069"
---
# <a name="step-4-populate-the-details-text-box"></a>步骤 4：填充详细信息文本框
若要填充详细信息文本框中，创建名为一个新的子例程**recFields**并插入以下代码：  
  
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
  
 这段代码填入`lstDetails`使用的字段和值的简单记录传递给`recFields`。 如果资源是一个文本文件，文本 Stream 打开从该资源记录。 该代码确定的字符集是 ASCII 并将复制到 Stream 内容`txtDetails`。  
  
## <a name="see-also"></a>请参阅  
 [Internet 发布方案](../../../ado/guide/data/internet-publishing-scenario.md)   
 [步骤 3：填充字段列表框](../../../ado/guide/data/step-3-populate-the-fields-list-box.md)
