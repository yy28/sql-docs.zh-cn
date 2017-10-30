---
title: "JScript ADO 编程 |Microsoft 文档"
ms.prod: sql-non-specified
ms.technology:
- drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: 
ms.tgt_pltfrm: 
ms.topic: article
dev_langs:
- JScript
helpviewer_keywords:
- JScript programming in ADO
- ADO, JScript programming
ms.assetid: 62273658-0fe7-4aac-b4d8-f725e6baf043
caps.latest.revision: 10
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 6ae8137c2e5641594c3ddcf768c47b7fe844fafc
ms.contentlocale: zh-cn
ms.lasthandoff: 09/09/2017

---
# <a name="jscript-ado-programming"></a>JScript ADO 编程
## <a name="creating-an-ado-project"></a>创建 ADO 项目  
 Microsoft JScript 不支持类型库，因此不需要引用 ADO 项目中。 因此，没有关联的功能，如命令行完成是受支持。 此外，默认情况下，枚举的 ADO 常量不在 JScript 中定义。  
  
 但是，ADO 提供你使用两个包含文件包含用于 JScript 的以下定义：  
  
-   服务器端脚本使用 Adojavas.inc，安装在 ADO 库文件夹。  
  
-   脚本使用 Adcjavas.inc，ADO 库文件夹中安装的客户端。  
  
 您可以复制和粘贴到 ASP 页中，从这些文件的常量定义或时，如果你正在编写服务器端脚本，将 Adojavas.inc 文件复制到您的网站上的文件夹，并引用它的 ASP 页如下：  
  
```  
<!--#include File="adojavas.inc"-->  
```  
  
## <a name="creating-ado-objects-in-jscript"></a>在 JScript 中创建 ADO 对象  
 您必须改用**CreateObject**函数调用：  
  
```  
var Rs1;  
Rs1 = Server.CreateObject("ADODB.Recordset");  
```  
  
## <a name="jscript-example"></a>JScript 示例  
 下面的代码是打开的活动服务器页面 (ASP) 文件中的 JScript 服务器端编程的泛型示例**记录集**对象：  
  
```  
<%  @LANGUAGE="JScript" %>  
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

