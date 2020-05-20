---
title: 步骤4：填充 "详细信息" 文本框 |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
ms.assetid: cb4273e2-c907-4a86-a621-3bf110088228
author: rothja
ms.author: jroth
ms.openlocfilehash: 2110384afa66e74e17d4e3c9a8600b5825cc412e
ms.sourcegitcommit: 6037fb1f1a5ddd933017029eda5f5c281939100c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/04/2020
ms.locfileid: "82760783"
---
# <a name="step-4-populate-the-details-text-box"></a>步骤 4：填充详细信息文本框
若要填充 "详细信息" 文本框，请创建名为**recFields**的新子程序，并插入以下代码：  
  
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
  
 此代码将填充 `lstDetails` 传递到的简单记录的字段和值 `recFields` 。 如果资源是文本文件，则从资源记录中打开一个文本流。 此代码确定字符集是否为 ASCII，并将流内容复制到中 `txtDetails` 。  
  
## <a name="see-also"></a>另请参阅  
 [Internet 发布方案](../../../ado/guide/data/internet-publishing-scenario.md)   
 [步骤 3：填充字段列表框](../../../ado/guide/data/step-3-populate-the-fields-list-box.md)
