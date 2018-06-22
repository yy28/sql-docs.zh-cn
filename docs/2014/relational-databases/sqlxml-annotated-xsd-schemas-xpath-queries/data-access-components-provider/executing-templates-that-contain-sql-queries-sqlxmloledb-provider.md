---
title: 执行模板包含 SQL 查询 (SQLXMLOLEDB Provider) |Microsoft 文档
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- templates [SQLXML]
- SQLXMLOLEDB Provider, executing template files
- templates [SQLXML], SQL queries
- XML templates [SQLXML]
- SQL queries [SQLXML]
ms.assetid: ff2bc36f-e3fb-4d8f-8e3a-2680a39eda11
caps.latest.revision: 28
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: affea1983c83dbf3cd0a8f5ab82292f88f1cae65
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/19/2018
ms.locfileid: "36015856"
---
# <a name="executing-templates-that-contain-sql-queries-sqlxmloledb-provider"></a>执行包含 SQL 查询的模板（SQLXMLOLEDB 访问接口）
  此示例演示如何使用 SQLXMLOLEDB 提供程序特定属性 ClientSideXML。 在此客户端 ADO 示例应用程序中，在服务器上执行包含一个 SQL 查询的 XML 模板。  
  
 因为 ClientSideXML 属性设置为 True，则将不带 FOR XML 子句的 SELECT 语句发送到服务器。 服务器执行该查询并将一个行集返回给客户端。 然后客户端对行集应用 FOR XML 转换，并生成 XML 文档。  
  
 XML 模板提供一个顶级的根元素 (\<根 >)，生成的 XML 文档; 因此，未提供的 xml 根属性。  
  
 若要执行 XML 模板，必须指定方言 {5d531cb2-e6ed-11d2-b252-00c04f681b71}。  
  
> [!NOTE]  
>  在该代码中，必须在连接字符串中提供 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 实例的名称。 而且，该示例指定对于需要安装其他网络客户端软件的数据访问接口使用 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client (SQLNCLI11)。 有关详细信息，请参阅[SQL Server Native Client 的系统要求](../../native-client/system-requirements-for-sql-server-native-client.md)。  
  
```  
Option Explicit  
  
Sub Main()  
  Dim oTestStream As New ADODB.Stream  
  Dim oTestConnection As New ADODB.Connection  
  Dim oTestCommand As New ADODB.Command  
  oTestConnection.Open "Provider=SQLXMLOLEDB.4.0;Data Provider=SQLNCLI11;Data Source=SqlServerName;Initial Catalog=AdventureWorks;Integrated Security=SSPI;"  
  
  Set oTestCommand.ActiveConnection = oTestConnection  
  oTestCommand.Properties("ClientSideXML") = True  
  oTestCommand.CommandText = "<ROOT xmlns:sql='urn:schemas-microsoft-com:xml-sql'> " & _  
        " <sql:query> " & _  
        "   SELECT TOP 10 FirstName, LastName FROM Person.Contact FOR XML AUTO " & _  
        "   </sql:query> " & _  
        " </ROOT> "  
  oTestStream.Open  
  ' You need the dialect if you are executing   
  ' XML templates (not for SQL queries).  
  oTestCommand.Dialect = "{5d531cb2-e6ed-11d2-b252-00c04f681b71}"  
  oTestCommand.Properties("Output Stream").Value = oTestStream  
  oTestCommand.Execute , , adExecuteStream  
  
  oTestStream.Position = 0  
  oTestStream.Charset = "utf-8"  
  Debug.Print oTestStream.ReadText(adReadAll)  
End Sub  
  
Sub Form_Load()  
  Main  
End Sub  
```  
  
  