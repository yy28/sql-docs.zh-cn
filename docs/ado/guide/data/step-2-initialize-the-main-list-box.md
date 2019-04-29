---
title: 第 2 步：初始化主列表框 |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
ms.assetid: a1454493-1c86-46c2-ada8-d3c6fcdaf3c1
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 90b7d50d6cb0a6fd8c0814d1b4bcbb631e5e8376
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63062793"
---
# <a name="step-2-initialize-the-main-list-box"></a>第 2 步：初始化主列表框
若要声明全局记录和记录集对象，请插入 （常规） （声明） 为 Form1 的以下代码：  
  
```  
Option Explicit  
Dim grec As Record  
Dim grs As Recordset  
```  
  
 此代码声明用于将更高版本在此方案中使用的记录和记录集对象的全局对象引用。  
  
## <a name="to-connect-to-a-url-and-populate-lstmain"></a>若要连接到的 URL，并填充 lstMain  
 Form1 到窗体加载事件处理程序中插入以下代码：  
  
```  
Private Sub Form_Load()  
    Set grec = New Record  
    Set grs = New Recordset  
    grec.Open "", "URL=https://servername/foldername/", , _  
        adOpenIfExists Or adCreateCollection  
    Set grs = grec.GetChildren  
    While Not grs.EOF  
        lstMain.AddItem grs(0)  
        grs.MoveNext  
    Wend  
End Sub  
```  
  
 此代码实例化的全局的记录和记录集对象。 记录对象`grec`，使用指定为 ActiveConnection URL 打开。 如果 URL 存在，它会打开;如果它尚不存在，则创建它。 请注意，应将为"<https://servername/foldername/>"与您的环境中有效的 URL。  
  
 记录集对象中， `grs`，在该记录的子级上打开`grec`。 然后`lstMain`填充用于发布到的 URL 的资源的文件名称。  
  
## <a name="see-also"></a>请参阅  
 [Internet 发布方案](../../../ado/guide/data/internet-publishing-scenario.md)   
 [步骤 1：设置 Visual Basic 项目](../../../ado/guide/data/step-1-set-up-the-visual-basic-project.md)   
 [步骤 3：填充字段列表框](../../../ado/guide/data/step-3-populate-the-fields-list-box.md)
