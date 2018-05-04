---
title: 在 JScript 中处理错误 |Microsoft 文档
ms.prod: sql
ms.prod_service: connectivity
ms.component: ado
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.tgt_pltfrm: ''
ms.topic: conceptual
dev_langs:
- JScript
helpviewer_keywords:
- errors [ADO], JScript
- JScript error handling [ADO]
ms.assetid: 3de527e5-2e65-4ab0-9b7f-6d317c4478de
caps.latest.revision: 4
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 8a1e965f08a9176da74724b549dd411065ca549c
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
---
# <a name="handling-errors-in-jscript"></a>在 JScript 中处理错误
你的 Microsoft® JScript® 代码必须检查**计数**属性**连接**对象的**错误**集合。 如果值大于 0，循环访问集合，并打印值，就像在任何其他语言。  
  
```  
<!-- BeginErrorExampleJS -->  
<%@ Language=JScript %>  
<HTML>  
<HEAD>  
<title>Error Handling Example (JScript)</title>  
</HEAD>  
<BODY>  
<h1>Error Handling Example (JScript)</h1>  
<%  
   var cnn1 = Server.CreateObject("ADODB.Connection");  
   var errLoop = Server.CreateObject("ADODB.Error");  
   var strError = new String;  
  
   // Intentionally trigger an error.  
   cnn1.Open("nothing");  
  
   if (cnn1.Errors.Count > 0) {  
      // Enumerate Errors collection and display  
      // properties of each Error object.  
      for (var i = 1; i < cnn1.Errors.Count; i++) {  
         errLoop = cnn1.Errors(i);  
         strError = "Error #" & errLoop.Number + "<br>" +  
            "   " + errLoop.Description + "<br>" +  
            "   (Source: " & errLoop.Source & ")" + "<br>" +  
            "   (SQL State: " & errLoop.SQLState + ")" + "<br>" +  
            "   (NativeError: " & errLoop.NativeError + ")" + "<br>";  
         if (errLoop.HelpFile == "")  
            strError = strError +  
               "   No Help file available" +  
               "<br><br>";  
         else  
            strError = strError +  
               "   (HelpFile: " & errLoop.HelpFile & ")" & "<br>" +  
               "   (HelpContext: " & errLoop.HelpContext & ")" +  
               "<br><br>";  
         Response.Write("<p>" & strError & "</p>");  
      }  
   }  
%>  
  
</BODY>  
</HTML>  
<!-- EndErrorExampleJS -->  
```
