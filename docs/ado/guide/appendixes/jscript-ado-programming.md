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
ms.openlocfilehash: 8d07759405dc337667cc8971ce7795af428a0cfa
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/27/2020
ms.locfileid: "67926804"
---
# <a name="jscript-ado-programming"></a>JScript ADO 编程
## <a name="creating-an-ado-project"></a>创建 ADO 项目  
 Microsoft JScript 不支持类型库，因此您不需要在项目中引用 ADO。 因此，不支持任何相关功能，如命令行完成。 另外，默认情况下，未在 JScript 中定义 ADO 枚举的常量。  
  
 但是，ADO 为你提供了包含以下定义的两个包含文件，以便与 JScript 一起使用：  
  
-   对于服务器端脚本编写，请使用安装在 ADO 库文件夹中的 Adojavas。  
  
-   对于客户端脚本编写，请使用安装在 ADO 库文件夹中的 Adcjavas。  
  
 您可以将这些文件中的常量定义复制并粘贴到您的 ASP 页面中，或者，如果您正在执行服务器端脚本编写，请将 Adojavas 文件复制到您的网站上的一个文件夹中，然后从您的 ASP 页引用它，如下所示：  
  
```javascript
<!--#include File="adojavas.inc"-->  
```  
  
## <a name="creating-ado-objects-in-jscript"></a>在 JScript 中创建 ADO 对象  
 您必须改用**CreateObject**函数调用：  
  
```javascript
var Rs1;  
Rs1 = Server.CreateObject("ADODB.Recordset");  
```  
  
## <a name="jscript-example"></a>JScript 示例  
 下面的代码是一个在 Active Server Page （ASP）文件中打开**Recordset**对象的 JScript 服务器端编程的一般示例：  
  
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
