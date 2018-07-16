---
title: 执行 SQL 查询 （SQLXMLOLEDB 提供程序） |Microsoft Docs
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
- queries [SQLXML], SQLXMLOLEDB Provider
- xml root property [SQLXML]
- SQLXMLOLEDB Provider, executing SQL queries
- SQL queries [SQLXML]
ms.assetid: 50334cf5-9c87-4c00-9beb-e08577c4fa82
caps.latest.revision: 28
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 1173e11fb6a5b1ed6dd61af23491cc8146a36d7f
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/02/2018
ms.locfileid: "37225209"
---
# <a name="executing-sql-queries-sqlxmloledb-provider"></a>执行 SQL 查询（SQLXMLOLEDB 访问接口）
  该示例说明以下特定于 SQLXMLOLEDB 访问接口的属性的用法：  
  
-   ClientSideXML  
  
-   xml root  
  
 在该客户端 ADO 示例应用程序中，在客户端执行了一个简单 SQL 查询。 因为 ClientSideXML 属性设置为 True，则将不带 FOR XML 子句的 SELECT 语句发送到服务器。 服务器执行该查询并将一个行集返回给客户端。 然后客户端对行集应用 FOR XML 转换，并生成 XML 文档。  
  
 Xml 根属性生成的 XML 文档提供一个顶级根元素。  
  
> [!NOTE]  
>  在代码中，必须在连接字符串中提供 Microsoft [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 实例的名称。 此外，本示例还指定使用 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client (SQLNCLI11) 作为数据访问接口，该访问接口需要安装其他网络客户端软件。 有关详细信息，请参阅[SQL Server Native Client 的系统要求](../../native-client/system-requirements-for-sql-server-native-client.md)。  
  
```  
Option Explicit  
Sub main()  
Dim oTestStream As New ADODB.Stream  
Dim oTestConnection As New ADODB.Connection  
Dim oTestCommand As New ADODB.Command  
  
oTestConnection.Open "provider=SQLXMLOLEDB.4.0;data provider=SQLNCLI11;data source=SqlServerName;initial catalog=AdventureWorks;Integrated Security=SSPI ;"  
oTestCommand.ActiveConnection = oTestConnection  
oTestCommand.Properties("ClientSideXML") = True  
oTestCommand.CommandText = "SELECT TOP 10 FirstName, LastName FROM Person.Contact FOR XML AUTO"  
oTestStream.Open  
oTestCommand.Properties("Output Stream").Value = oTestStream  
oTestCommand.Properties("xml root") = "root"  
oTestCommand.Execute , , adExecuteStream  
  
oTestStream.Position = 0  
oTestStream.Charset = "utf-8"  
Debug.Print oTestStream.ReadText(adReadAll)  
End Sub  
Sub Form_Load()  
 main  
End Sub  
```  
  
  
