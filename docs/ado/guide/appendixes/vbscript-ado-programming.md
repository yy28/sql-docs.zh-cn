---
title: VBScript ADO 编程 |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 11/08/2018
ms.reviewer: ''
ms.topic: conceptual
dev_langs:
- VB
helpviewer_keywords:
- ADO, VBScript
- VBScript [ADO]
ms.assetid: 6aaaf6d0-1376-4473-bea6-b81f2645a9ac
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: a9c13b532e1ac234c207fc70fe7578be341f72b4
ms.sourcegitcommit: 074d44994b6e84fe4552ad4843d2ce0882b92871
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/05/2019
ms.locfileid: "66701128"
---
# <a name="vbscript-ado-programming"></a>VBScript ADO 编程
## <a name="creating-an-ado-project"></a>创建 ADO 项目  
 Microsoft Visual Basic、 Scripting Edition 不支持类型库中，因此不需要在项目中引用 ADO。 因此，如命令行完成任何关联的功能是受不支持。 此外，默认情况下，ADO 枚举常量不在 VBScript 中定义。  
  
 但是，ADO 提供了两个包含文件包含以下定义可以与 VBScript 一起使用：  
  
-   用于服务器端脚本编写用途 Adovbs.inc，安装在 c:\Program Files\Common Files\System\ado\ 文件夹中默认情况下。  
  
-   供客户端侧脚本使用 Adcvbs.inc，安装在 c:\Program Files\Common Files\System\msdac\ 文件夹中默认情况下。  
  
 您可以复制，将从这些文件的常量定义粘贴到 ASP 页中，或者，如果你正在执行服务器端脚本，将 Adovbs.inc 文件复制到你的网站上的文件夹和引用从 ASP 页如下：  
  
```vb
<!--#include File="adovbs.inc"-->  
```  
  
## <a name="creating-ado-objects-in-vbscript"></a>在 VBScript 中创建 ADO 对象  
 不能使用**Dim**语句将分配给 VBScript 中的特定类型的对象。 此外，VBScript 不支持**新建**与一起使用的语法**Dim**在应用程序的 Visual Basic 中的语句。 必须改用**CreateObject**函数调用：  
  
```vb
Dim Rs1  
Set Rs1 = Server.CreateObject( "ADODB.Recordset" )  
```  
  
## <a name="vbscript-examples"></a>VBScript 示例  
 以下代码是 VBScript Active Server Page (ASP) 文件中的服务器端编程的一般示例：  
  
```vb
<%  @LANGUAGE="VBSCRIPT" %>  
<%  Option Explicit %>  
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
  
 使用 ADO 文档中包含更具体的 VBScript 示例。 有关详细信息，请参阅[Microsoft Visual Basic Scripting Edition 中的 ADO 代码示例](../../../ado/reference/ado-api/ado-code-examples-vbscript.md)。  
  
## <a name="differences-between-vbscript-and-visual-basic"></a>VBScript 和 Visual Basic 之间的差异  
 使用 ADO 与 VBScript 是类似于使用 ADO 与 Visual Basic 在许多方面，包括如何使用语法。 但是，存在一些重要差异：  
  
-   VBScript 的支持仅 Variant 数据类型，可以容纳不同类型的数据。 可以将所需的数据存储在 Variant 数据类型，以及数据将适当地发挥由于强制转换由 VBScript 执行。 它识别 ADO 中，所需的类型，并将相应地转换中将该变量的值。  
  
-   不能使用**上错误 goto\<标签 >** VBScript 中。  
  
-   VBScript 支持，一些内置的 Visual Basic 函数如**Msgbox**，**日期**，并**IsNumeric**。 但是，由于 VBScript 是 Visual Basic 的一个子集，并非所有的内置函数支持。 例如，不支持 VBScript**格式**函数和文件 I/O 功能。
