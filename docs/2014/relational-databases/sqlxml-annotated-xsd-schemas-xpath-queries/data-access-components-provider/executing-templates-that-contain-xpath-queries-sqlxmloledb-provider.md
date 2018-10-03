---
title: 执行包含 XPath 查询 （sqlxmloledb 访问接口） 的模板 |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- database-engine
- docset-sql-devref
ms.topic: reference
helpviewer_keywords:
- SQLXMLOLEDB Provider, executing template files
- Base Path property
- templates [SQLXML], XPath queries
- XPath queries [SQLXML], templates
- XPath queries [SQLXML], SQLXMLOLEDB Provider
- Mapping Schema property
- XML templates [SQLXML]
ms.assetid: 7368c188-607e-459e-8254-8f23352dfa01
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 8e50e819fd2a0cca62ebaabd32a351422f393d6a
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/02/2018
ms.locfileid: "48083977"
---
# <a name="executing-templates-that-contain-xpath-queries-sqlxmloledb-provider"></a>执行包含 XPath 查询的模板（SQLXMLOLEDB 访问接口）
  此示例显示如何使用以下 SQLXMLOLEDB 访问接口特定的属性：  
  
-   ClientSideXML  
  
-   基路径  
  
-   映射架构  
  
 在此示例 ADO 应用程序中，由 XPath 查询 （根） 组成的 XML 模板指定针对 XSD 映射架构 (MySchema.xml) 所述[执行 XPath 查询&#40;sqlxmloledb 访问接口&#41;](executing-xpath-queries-sqlxmloledb-provider.md).  
  
 映射架构属性提供对其执行 XPath 查询的 XSD 映射架构。 基路径属性提供映射架构的文件路径。  
  
 ClientSideXML 属性设置为 True。 因此，在客户端上生成 XML 文档。  
  
 在应用程序中，可直接指定 XPath 查询。 因此，必须包括方言 {5d531cb2-e6ed-11d2-b252-00c04f681b71}。  
  
> [!NOTE]  
>  在代码中，必须在连接字符串中提供 Microsoft [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 实例的名称。 而且，该示例指定对于需要安装其他网络客户端软件的数据访问接口使用 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client (SQLNCLI11)。 有关详细信息，请参阅[SQL Server Native Client 的系统要求](../../native-client/system-requirements-for-sql-server-native-client.md)。  
  
```  
Option Explicit  
Sub Main()  
  
   Dim oTestStream As New ADODB.Stream  
   Dim oTestConnection As New ADODB.Connection  
   Dim oTestCommand As New ADODB.Command  
  
   oTestConnection.Open "provider=SQLXMLOLEDB.4.0;data provider=SQLNCLI11;data source=SqlServerName;initial catalog=AdventureWorks;Integrated Security=SSPI;"  
  
   oTestCommand.ActiveConnection = oTestConnection  
   oTestCommand.Properties("ClientSideXML") = "False"  
  
   oTestCommand.CommandText = "<ROOT xmlns:sql='urn:schemas-microsoft-com:xml-sql'> " & _  
        " <sql:xpath-query mapping-schema='mySchema.xml' > " & _  
        "   root " & _  
        "   </sql:xpath-query> " & _  
        " </ROOT> "  
   oTestStream.Open  
   ' You need the dialect if you are executing a template.  
   oTestCommand.Dialect = "{5d531cb2-e6ed-11d2-b252-00c04f681b71}"  
   oTestCommand.Properties("Output Stream").Value = oTestStream  
   oTestCommand.Properties("Base Path").Value = "c:\Schemas\SQLXML4\TemplateWithXPath\"  
   oTestCommand.Properties("Mapping Schema").Value = "mySchema.xml"  
   oTestCommand.Properties("Output Encoding") = "utf-8"  
   oTestCommand.Execute , , adExecuteStream  
   oTestStream.Position = 0  
   oTestStream.Charset = "utf-8"  
   Debug.Print oTestStream.ReadText(adReadAll)  
  
End Sub  
  
Sub Form_Load()  
   Main  
End Sub  
```  
  
 以下是架构：  
  
```  
<xsd:schema xmlns:xsd='http://www.w3.org/2001/XMLSchema'  
   xmlns:sql='urn:schemas-microsoft-com:mapping-schema'>  
 <xsd:element name= 'root' sql:is-constant='1'>   
    <xsd:complexType>  
       <xsd:sequence>  
         <xsd:element ref = 'Contact'/>  
       </xsd:sequence>  
    </xsd:complexType>  
  </xsd:element>  
  
  <xsd:element name='Contact' sql:relation='Person.Contact'>  
     <xsd:complexType>  
          <xsd:attribute name='ContactID' type='xsd:integer' />  
          <xsd:attribute name='FirstName' type='xsd:string'/>   
          <xsd:attribute name='LastName' type='xsd:string' />   
     </xsd:complexType>  
   </xsd:element>  
</xsd:schema>  
```  
  
  
