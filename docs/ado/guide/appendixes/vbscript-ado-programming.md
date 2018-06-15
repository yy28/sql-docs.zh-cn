---
title: VBScript ADO 编程 |Microsoft 文档
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.tgt_pltfrm: ''
ms.topic: conceptual
dev_langs:
- VB
helpviewer_keywords:
- ADO, VBScript
- VBScript [ADO]
ms.assetid: 6aaaf6d0-1376-4473-bea6-b81f2645a9ac
caps.latest.revision: 10
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: a3f565f610e5f98adae7160d61acf01ab7e41c46
ms.sourcegitcommit: 62826c291db93c9017ae219f75c3cfeb8140bf06
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/11/2018
ms.locfileid: "35270466"
---
# <a name="vbscript-ado-programming"></a>VBScript ADO 编程
## <a name="creating-an-ado-project"></a>创建 ADO 项目  
 Microsoft Visual Basic、 Scripting Edition 不支持类型库，因此不需要在你的项目中引用 ADO。 因此，没有关联的功能，如命令行完成是受支持。 此外，默认情况下，枚举的 ADO 常量不在 VBScript 中定义。  
  
 但是，ADO 提供你使用两个包含文件包含与 VBScript 一起使用的以下定义：  
  
-   对于服务器端脚本使用 Adovbs.inc，这是默认安装在 c:\Program Files\Common Files\System\ado\ 文件夹。  
  
-   对于客户端脚本使用 Adcvbs.inc，这是默认安装在 c:\Program Files\Common Files\System\msdac\ 文件夹。  
  
 您可以复制和粘贴到 ASP 页中，从这些文件的常量定义或时，如果你正在编写服务器端脚本，将 Adovbs.inc 文件复制到您的网站上的文件夹，并引用它的 ASP 页如下：  
  
```  
<!--#include File="adovbs.inc"-->  
```  
  
## <a name="creating-ado-objects-in-vbscript"></a>在 VBScript 中创建 ADO 对象  
 不能使用**Dim**语句将对象分配给在 VBScript 中特定类型。 此外，VBScript 不支持**新建**语法用于**Dim**在应用程序的 Visual Basic 中的语句。 您必须改用**CreateObject**函数调用：  
  
```  
Dim Rs1  
Set Rs1 = Server.CreateObject( "ADODB.Recordset" )  
```  
  
## <a name="vbscript-examples"></a>VBScript 示例  
 下面的代码是在活动服务器页面 (ASP) 文件中的 VBScript 服务器端编程的泛型示例：  
  
```  
<%  @LANGUAGE="VBSCRIPT" %>  
<%  Option Explicit %>  
<!--#include File="adovbs.inc"-->  
<HTML>  
    <BODY BGCOLOR="White" topmargin="10" leftmargin="10">  
  
    <!-- Your ASP Code goes here -->  
<%  
Dim Source  
Dim Connect  
Dim Rs1  
  
Source = "SELECT * FROM Authors"  
Connect = "Provider=sqloledb;Data Source=srv;" & _  
    "Initial Catalog=Pubs;Integrated Security=SSPI;"  
  
Set Rs1 = Server.CreateObject( "ADODB.Recordset" )  
Rs1.Open Source, Connect, adOpenForwardOnly  
Response.Write("Success!")  
%>  
    </BODY>  
</HTML>  
```  
  
 更具体的 VBScript 示例包括包含的 ADO 文档。 有关详细信息，请参阅[ADO 代码示例在 Microsoft Visual Basic Scripting Edition](../../../ado/reference/ado-api/ado-code-examples-vbscript.md)。  
  
## <a name="differences-between-vbscript-and-visual-basic"></a>VBScript 和 Visual Basic 之间的差异  
 使用 ADO 的 VBScript 是类似于使用 Visual Basic 中使用 ADO，在许多方面，包括如何使用语法。 但是，存在一些重要差异：  
  
-   VBScript 支持仅 Variant 数据类型，可以容纳不同类型的数据。 你可以在 Variant 数据类型，存储所需的数据和数据将适当地发挥由于强制转换由 VBScript。 它识别 ADO，所需的类型，并相应地将转换该变体中的值。  
  
-   不能使用**上错误 goto\<标签 >** VBScript 中。  
  
-   VBScript 支持某些内置的 Visual Basic 函数如**Msgbox**，**日期**，和**IsNumeric**。 但是，由于 VBScript 是 Visual Basic 的一个子集，并非所有内置函数支持。 例如，VBScript 不支持**格式**函数和文件 I/O 函数。
