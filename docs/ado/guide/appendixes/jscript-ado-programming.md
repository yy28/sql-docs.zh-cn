---
title: JScript ADO 编程 |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 11/08/2018
ms.reviewer: ''
ms.topic: conceptual
dev_langs:
- JScript
helpviewer_keywords:
- JScript programming in ADO
- ADO, JScript programming
ms.assetid: 62273658-0fe7-4aac-b4d8-f725e6baf043
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: da87199347052189e5af8b881154b37723408d1f
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62720346"
---
# <a name="jscript-ado-programming"></a>JScript ADO 编程
## <a name="creating-an-ado-project"></a>创建 ADO 项目  
 Microsoft JScript 不支持类型库，因此不需要引用 ADO 在项目中。 因此，如命令行完成任何关联的功能是受不支持。 此外，默认情况下，ADO 枚举常量未在 JScript 中定义。  
  
 但是，ADO 提供了具有两个包含文件包含要与 JScript 一起使用的以下定义：  
  
-   用于服务器端脚本使用 Adojavas.inc，ADO 库文件夹中安装。  
  
-   用于客户端侧脚本使用 Adcjavas.inc，ADO 库文件夹中安装。  
  
 您可以复制，将从这些文件的常量定义粘贴到 ASP 页中，或者，如果你正在执行服务器端脚本，将 Adojavas.inc 文件复制到你的网站上的文件夹和引用从 ASP 页如下：  
  
```javascript
<!--#include File="adojavas.inc"-->  
```  
  
## <a name="creating-ado-objects-in-jscript"></a>在 JScript 中创建 ADO 对象  
 必须改用**CreateObject**函数调用：  
  
```javascript
var Rs1;  
Rs1 = Server.CreateObject("ADODB.Recordset");  
```  
  
## <a name="jscript-example"></a>JScript 示例  
 下面的代码是打开的 Active Server Page (ASP) 文件中的 JScript 服务器端编程的一般示例**记录集**对象：  
  
```javascript
<%  @LANGUAGE="JScript" %>  
<!--#include File="adojavas.inc"-->  
<HTML>  
<BODY BGCOLOR="White" topmargin="10" leftmargin="10">  
<%  
var Source = "SELECT * FROM Authors";  
var Connect =  "Provider=sqloledb;Data Source=srv;" +  
    "Initial Catalog=Pubs;Integrated Security=SSPI;"  
var Rs1 = Server.CreateObject( "ADODB.Recordset.2.5" );  
Rs1.Open(Source,Connect,adOpenForwardOnly);  
Response.Write("Success!");  
%>  
</BODY>  
</HTML>  
```
