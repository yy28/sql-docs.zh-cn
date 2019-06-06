---
title: Microsoft OLE DB 简单的提供程序 |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 11/08/2018
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- simple provider [ADO]
- providers [ADO], OLE DB simple provider
- OLE DB simple provider [ADO]
ms.assetid: 1e7dc6f0-482c-4103-8187-f890865e40fc
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: bc17df7bad00205803b33cb4af17cb3c6ddaac56
ms.sourcegitcommit: 074d44994b6e84fe4552ad4843d2ce0882b92871
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/05/2019
ms.locfileid: "66701283"
---
# <a name="microsoft-ole-db-simple-provider-overview"></a>Microsoft OLE DB 简单的提供程序概述
Microsoft OLE DB 简单提供程序 (OSP) 允许访问已为其提供程序已编写使用任何数据的 ADO [OLE DB 简单提供程序 (OSP) 工具包](https://msdn.microsoft.com/6e7b7931-9e4a-4151-ae51-672abd3f84a6)。 简单的提供程序用于访问需要唯一重要的 OLE DB 支持，如内存中数组或 XML 文档的数据源。

## <a name="connection-string-parameters"></a>连接字符串参数
 若要连接到 OLE DB 简单提供程序 DLL，请设置*提供程序*自变量[ConnectionString](../../../ado/reference/ado-api/connectionstring-property-ado.md)属性设置为：

```vb
MSDAOSP
```

 此值还可以设置或读取使用[提供程序](../../../ado/reference/ado-api/provider-property-ado.md)属性。

 你可以连接到已注册为完整的 OLE DB 访问接口使用已注册的提供程序名称，由提供程序编写器的简单提供程序。

## <a name="typical-connection-string"></a>典型的连接字符串
 此提供程序的典型的连接字符串是：

```vb
"Provider=MSDAOSP;Data Source=serverName"
```

 该字符串包含这些关键字：

|关键字|Description|
|-------------|-----------------|
|**提供程序**|指定 SQL Server 的 OLE DB 访问接口。|
|**数据源**|指定的服务器的名称。|

## <a name="xml-document-example"></a>XML 文档示例
 OLE DB 简单提供程序 (OSP) MDAC 2.7 或更高版本和 Windows 数据访问组件 (Windows DAC) 已经过增强，支持打开分层 ADO**记录集**通过任意 XML 文件。 这些 XML 文件可能包含的 ADO 持久化 xml，但不需要。 这实现了通过连接到 OSP **MSXML2.DLL**; 因此**MSXML2.DLL**或更高版本。

 **Portfolio.xml**在下面的示例中使用文件包含以下树：

```console
Portfolio
   Stock
      Shares
      Symbol
      Price
      Info
         Company Name
         WebSite
```

 XML DSO 使用内置的试探法来将 XML 树中的节点转换为分层结构中的各章**记录集**。

 使用这些内置的试探法，XML 树转换为两个级别分层**记录集**形式如下：

```console
Parent Recordset
Shares, Symbol, Price, $Text
   Child Recordset
      Company Name, WebSite, $Text
```

 请注意项目组合和信息标记不会出现在层次结构**记录集**。 有关 XML DSO 如何将 XML 树转换为层次结构的说明**记录集**，请参阅下面的规则。 下一节中讨论 $Text 列。

## <a name="rules-for-assigning-xml-elements-and-attributes-to-columns-and-rows"></a>分配 XML 元素和属性到列和行的规则
 XML DSO 遵循用于分配元素的过程和属性到列和数据绑定的应用程序中的行。 XML 建模为具有一个标记，包含整个层次结构的树。 例如，一书的 XML 说明可能包含一章标记、 图标记和部分标记。 最高级别将通讯簿标记，它包含的子元素的一章，图中和部分。 当 XML DSO 将 XML 元素映射到行和列时，将转换的子元素不是顶级元素。

 XML DSO 用于转换的子元素使用此过程：

-   每个子元素和属性的某些列对应**记录集**层次结构中。

-   列的名称是与同名的子元素或属性，除非父元素具有属性和子元素具有相同的名称，在这种情况下"！"预置到子元素的列名称。

-   每个列是*简单*列包含标量值 （通常为字符串） 或**记录集**包含子列**记录集**。

-   与属性相对应的列始终是简单的。

-   与子元素相对应的列均**记录集**列，如果子元素具有其自己的子元素或属性 （或两者），或子元素的父代具有子元素作为子级的多个实例。 否则，该列是简单的。

-   当有多个实例的子元素 （位于不同的父项） 时，其列并**记录集**列如果*任何*的实例表示**记录集**列; 它列是简单才*所有*实例表示简单列。

-   所有**记录集**具有名为 $Text 的其他列。

 构造所需的代码**记录集**如下所示：

```vb
Dim adoConn as ADODB.Connection
Dim adoRS as ADODB.Recordset

Set adoRS = New ADODB.Connection
Set adoRS = New ADODB.Recordset

adoConn.Open "Provider=MSDAOSP; Data Source=MSXML2.DSOControl.2.6;"
adoRS.Open "https://WebServer/VRoot/portfolio.xml, adoConn
```

> [!NOTE]
>  可以通过使用四个不同的命名约定指定数据文件的路径。

```vb
'HTTP://
adoRS.Open "https://WebServer/VRoot/portfolio.xml", adoConn
'FILE://
adoRS.Open "file:/// C:\\Directory\\portfolio.xml", adoConn
'UNC Path
adoRS.Open "\\ComputerName\ShareName\portfolio.xml", adoConn
'Full DOS Path
adoRS.Open "C:\Directory\portfolio.xml", adoConn
```

 只要**记录集**已打开，常用的 ADO**记录集**，可以使用导航命令。

 **记录集**生成 OSP 的具有一些限制：

-   客户端游标 (**adUseClient**) 不受支持。

-   分层**记录集**创建通过任意 XML 无法被持久化，使用**Recordset.Save**。

-   **记录集**使用 OSP 创建是只读的。

-   XMLDSO 将其他列的数据 ($Text) 添加到每**记录集**层次结构中。

 有关 OLE DB 简单的提供程序的详细信息，请参阅[构建一个简单的提供程序](https://msdn.microsoft.com/b31a6cba-58ae-4ee8-9039-700973d354d6)。

## <a name="code-example"></a>代码示例
 下面的 Visual Basic 代码演示了如何打开任意 XML 文件中，构造分层**记录集**，并以递归方式编写的每个每条记录**记录集**到调试窗口。

 下面是包含股市报价的简单 XML 文件。 下面的代码使用此文件来构造两个级别分层**记录集**。

```xml
<portfolio>
   <stock>
      <shares>100</shares>
      <symbol>MSFT</symbol>
      <price>$70.00</price>
      <info>
         <companyname>Microsoft Corporation</companyname>
         <website>https://www.microsoft.com</website>
      </info>
   </stock>
   <stock>
      <shares>100</shares>
      <symbol>AAPL</symbol>
      <price>$107.00</price>
      <info>
         <companyname>Apple Computer, Inc.</companyname>
         <website>https://www.apple.com</website>
      </info>
   </stock>
   <stock>
      <shares>100</shares>
      <symbol>DELL</symbol>
      <price>$50.00</price>
      <info>
         <companyname>Dell Corporation</companyname>
         <website>https://www.dell.com</website>
      </info>
    </stock>
    <stock>
       <shares>100</shares>
       <symbol>INTC</symbol>
       <price>$115.00</price>
       <info>
          <companyname>Intel Corporation</companyname>
          <website>https://www.intel.com</website>
       </info>
   </stock>
</portfolio>
```

 以下是两个 Visual Basic sub 过程。 创建第一个**记录集**并将其传递给*WalkHier* sub 的过程中，哪些以递归方式将沿层次结构，编写每个指导**字段**每个记录中每个**记录集**到调试窗口。

```vb
Private Sub BrowseHierRecordset()
' Add ADO 2.7 or later to Project/References
' No need to add MSXML2, ADO just passes the ProgID through to the OSP.

    Dim adoConn As ADODB.Connection
    Dim adoRS As ADODB.Recordset
    Dim adoChildRS As ADODB.Recordset

    Set adoConn = New ADODB.Connection
    Set adoRS = New ADODB.Recordset
    Set adoChildRS = ADODB.Recordset

    adoConn.Open "Provider=MSDAOSP; Data Source=MSXML2.DSOControl.2.6;"
    adoRS.Open "https://bwillett3/Kowalski/portfolio.xml", adoConn

    Dim iLevel As Integer
    iLevel = 0
    WalkHier iLevel, adoRS

End Sub

Sub WalkHier(ByVal iLevel As Integer, ByVal adoRS As ADODB.Recordset)
    iLevel = iLevel + 1
    PriorLevel = iLevel
    While Not adoRS.EOF
        For ndx = 0 To adoRS.Fields.Count - 1
            If adoRS.Fields(ndx).Name <> "$Text" Then
                If adoRS.Fields(ndx).Type = adChapter Then
                    Set adoChildRS = adoRS.Fields(ndx).Value
                    WalkHier iLevel, adoChildRS
                Else
                    Debug.Print iLevel & ": adoRS.Fields(" & ndx & _
                       ") = " & adoRS.Fields(ndx).Name & " = " & _
                       adoRS.Fields(ndx).Value
                End If
            End If
        Next ndx
        adoRS.MoveNext
    Wend
    iLevel = PriorLevel
End Sub
```
