---
title: "执行 SQL 查询 (SQLXMLOLEDB Provider) |Microsoft 文档"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: sqlxml
ms.reviewer: 
ms.suite: sql
ms.technology: dbe-xml
ms.tgt_pltfrm: 
ms.topic: reference
helpviewer_keywords:
- queries [SQLXML], SQLXMLOLEDB Provider
- xml root property [SQLXML]
- SQLXMLOLEDB Provider, executing SQL queries
- SQL queries [SQLXML]
ms.assetid: 50334cf5-9c87-4c00-9beb-e08577c4fa82
caps.latest.revision: "28"
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 2faab00c42a41468961ba34939cb9acb12fe67de
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/17/2017
---
# <a name="executing-sql-queries-sqlxmloledb-provider"></a>执行 SQL 查询（SQLXMLOLEDB 访问接口）
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]此示例演示了以下 SQLXMLOLEDB 提供程序特定属性的使用：  
  
-   ClientSideXML  
  
-   xml root  
  
 在该客户端 ADO 示例应用程序中，在客户端执行了一个简单 SQL 查询。 因为 ClientSideXML 属性设置为 True，则将不带 FOR XML 子句的 SELECT 语句发送到服务器。 服务器执行该查询并将一个行集返回给客户端。 然后客户端对行集应用 FOR XML 转换，并生成 XML 文档。  
  
 Xml 根属性生成的 XML 文档中提供的单个顶级根元素。  
  
> [!NOTE]  
>  在代码中，必须在连接字符串中提供 Microsoft [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 实例的名称。 此外，本示例还指定使用 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client (SQLNCLI11) 作为数据访问接口，该访问接口需要安装其他网络客户端软件。 有关详细信息，请参阅[SQL Server Native Client 的系统要求](../../../relational-databases/native-client/system-requirements-for-sql-server-native-client.md)。  
  
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
  
  
