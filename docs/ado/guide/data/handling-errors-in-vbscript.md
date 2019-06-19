---
title: 在 VBScript 中处理错误 |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
dev_langs:
- VB
helpviewer_keywords:
- VBScript error handling [ADO]
- errors [ADO], VBScript
ms.assetid: 31bc3743-32d3-4bc7-ac61-ee6ed0fdec70
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 13f769ae3d2b8ddcc720df33596093ff9562af99
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/15/2019
ms.locfileid: "66700643"
---
# <a name="handling-errors-in-vbscript"></a>处理 VBScript 中的错误
没有 Visual Basic 中使用的方法和那些与 VBScript 一起使用的一些区别。 主要区别在于，VBScript 不支持通过在一个标签位置继续执行处理的错误的概念。 换而言之，不能使用`On Error GoTo`在 VBScript 中。 请改用`On Error Resume Next`，然后检查这两**Err.Number**并且**计数**属性**错误**集合，如下面的示例中所示：  
  
```  
<!-- BeginErrorExampleVBS -->  
<HTML>  
<HEAD>  
<META NAME="GENERATOR" Content="Microsoft Visual Studio 6.0">  
<TITLE>Error Handling Example (VBScript)</TITLE>  
</HEAD>  
<BODY>  
  
<h1>Error Handling Example (VBScript)</h1>  
  
<%  
  
   Dim cnn1  
   Dim errLoop  
   Dim strError  
  
   On Error Resume Next  
  
   ' Intentionally trigger an error.  
   Set cnn1 = Server.CreateObject("ADODB.Connection")  
   cnn1.Open "nothing"  
  
   If cnn1.Errors.Count > 0 Then  
      ' Enumerate Errors collection and display  
      ' properties of each Error object.  
      For Each errLoop In cnn1.Errors  
         strError = "Error #" & errLoop.Number & "<br>" & _  
            "   " & errLoop.Description & "<br>" & _  
            "   (Source: " & errLoop.Source & ")" & "<br>" & _  
            "   (SQL State: " & errLoop.SQLState & ")" & "<br>" & _  
            "   (NativeError: " & errLoop.NativeError & ")" & "<br>"  
         If errLoop.HelpFile = "" Then  
            strError = strError & _  
               "   No Help file available" & _  
               "<br><br>"  
         Else  
            strError = strError & _  
               "   (HelpFile: " & errLoop.HelpFile & ")" & "<br>" & _  
               "   (HelpContext: " & errLoop.HelpContext & ")" & _  
               "<br><br>"  
         End If  
  
         Response.Write("<p>" & strError & "</p>")  
      Next  
   End If  
  
%>  
  
</BODY>  
</HTML>  
<!-- EndErrorExampleVBS -->  
```
