---
title: 应用 XSL 转换 （SQLXMLOLEDB 提供程序） |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: xml
ms.topic: reference
helpviewer_keywords:
- SQLXMLOLEDB Provider, applying XSL transformations
- applying XSL transformations [SQLXML]
- xsl property
- Base Path property
- XSL Transformations [SQLXML]
ms.assetid: cb5e41ab-dd20-4873-af20-f417bd1bbf6d
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 74f8834ef29e4b5a1cf2b3988585f771cb9d1f1f
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63016293"
---
# <a name="applying-an-xsl-transformation-sqlxmloledb-provider"></a>应用 XSL 转换（SQLXMLOLEDB 访问接口）
  在此示例 ADO 应用程序中，将执行 SQL 查询并将 XSL 转换应用到结果。 ClientSideXML 属性设置为 True，则强制实施客户端上的行集的处理。 将命令方言设置为 {5d531cb2-e6ed-11d2-b252-00c04f681b71}，因为在模板中指定 SQL 查询且在执行模板时必须指定此方言。 Xsl 属性指定要使用应用转换的 XSL 文件。 基路径属性的值用于搜索 XSL 文件。 如果 xsl 属性的值中指定的路径，路径是相对于基路径属性中指定的路径。  
  
 此示例显示如何使用以下 SQLXMLOLEDB 访问接口特定的属性：  
  
-   ClientSideXML  
  
-   xsl  
  
 在此客户端 ADO 示例应用程序中，在服务器上执行包含一个 SQL 查询的 XML 模板。  
  
 因为 ClientSideXML 属性设置为 True，则将不带 FOR XML 子句的 SELECT 语句发送到服务器。 服务器执行该查询并将一个行集返回给客户端。 客户端然后将 FOR XML 转换应用到该行集并生成 XML 文档。  
  
 在应用程序; 中指定的 xsl 属性因此，对在客户端生成的 XML 文档应用 XSL 转换，并且结果是两个列的表。  
  
 若要执行模板命令，必须指定 XML 模板方言-{5d531cb2-e6ed-11d2-b252-00c04f681b71}。  
  
> [!NOTE]  
>  在代码中，必须在连接字符串中提供 Microsoft [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 实例的名称。 此示例还指定使用数据访问接口的 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client，这要求安装其他网络客户端软件。 有关详细信息，请参阅[SQL Server Native Client 的系统要求](../../native-client/system-requirements-for-sql-server-native-client.md)。  
  
```  
Option Explicit  
Sub main()  
Dim oTestStream As New ADODB.Stream  
Dim oTestConnection As New ADODB.Connection  
Dim oTestCommand As New ADODB.Command  
oTestConnection.Open "provider=SQLXMLOLEDB.4.0;data provider=SQLNCLI11;data source=SqlServerName;initial catalog=AdventureWorks;Integrated Security=SSPI;"  
Set oTestCommand.ActiveConnection = oTestConnection  
oTestCommand.Properties("ClientSideXML") = True  
oTestCommand.CommandText = _  
        "<ROOT xmlns:sql='urn:schemas-microsoft-com:xml-sql' >" & _  
       " <sql:query> " & _  
        "   SELECT TOP 25 FirstName, LastName FROM Person.Contact FOR XML AUTO " & _  
        "   </sql:query> " & _  
        " </ROOT> "  
oTestStream.Open  
' You need the dialect if you are executing a template.  
oTestCommand.Dialect = "{5d531cb2-e6ed-11d2-b252-00c04f681b71}"  
oTestCommand.Properties("Output Stream").Value = oTestStream  
oTestCommand.Properties("Base Path").Value = "c:\Schemas\SQLXML4\ExecuteTemplateWithXSL\"  
oTestCommand.Properties("xsl").Value = "myxsl.xsl"  
oTestCommand.Execute , , adExecuteStream  
  
oTestStream.Position = 0  
oTestStream.Charset = "utf-8"  
Debug.Print oTestStream.ReadText(adReadAll)  
End Sub  
Sub Form_Load()  
 main  
End Sub  
```  
  
 紧接着是 XSL 模板。 应用此 XSL 模板后得到一个包含两列的表。  
  
```  
<?xml version='1.0' encoding='UTF-8'?>            
 <xsl:stylesheet xmlns:xsl="http://www.w3.org/1999/XSL/Transform" version="1.0">   
  
    <xsl:template match = 'Person.Contact'>  
       <TR>  
         <TD><xsl:value-of select = '@FirstName' /></TD>  
         <TD><B><xsl:value-of select = '@LastName' /></B></TD>  
       </TR>  
    </xsl:template>  
    <xsl:template match = '/'>  
      <HTML>  
        <HEAD>  
           <STYLE>th { background-color: #CCCCCC }</STYLE>  
        </HEAD>  
        <BODY>  
         <TABLE border='1' style='width:300;'>  
           <TR><TH colspan='2'>Contacts</TH></TR>  
           <TR>  
              <TH >First name</TH>  
              <TH>Last name</TH>  
           </TR>  
           <xsl:apply-templates select = 'ROOT' />  
         </TABLE>  
        </BODY>  
      </HTML>  
    </xsl:template>  
</xsl:stylesheet>  
```  
  
  
