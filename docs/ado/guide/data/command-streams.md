---
title: 命令流 |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- command streams [ADO]
- streams [ADO], command
ms.assetid: 0ac09dbe-2665-411e-8fbb-d1efe6c777be
author: MightyPen
ms.author: genemi
ms.openlocfilehash: fd0c2273739a3651c7fdd4c424ce0cb47d39dd5b
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/15/2019
ms.locfileid: "67925847"
---
# <a name="command-streams"></a>命令流
ADO 始终支持命令输入中指定的字符串格式**CommandText**属性。 或者，使用 ADO 2.7 或更高版本，还可以使用信息的流的命令输入通过将分配到的流**CommandStream**属性。 可以将分配一个 ADO **Stream**对象或任何支持 COM 的对象**IStream**接口。  
  
 命令流的内容是只需从传递 ADO 到您的提供商，因此您的提供程序必须支持流即可使用此功能的命令输入。 例如，SQL Server 中的 XML 模板或 TRANSACT-SQL 扩展 OpenXML 窗体支持查询。  
  
 由于必须由访问接口解释的流的详细信息，因此必须通过设置指定将命令方言**方言**属性。 值**方言**是包含一个 GUID，由您的提供程序定义的字符串。 有关有效值的信息**方言**支持您的提供程序，请参阅提供程序文档。  
  
## <a name="xml-template-query-example"></a>XML 模板查询示例  
 下面的示例是用 VBScript 到 Northwind 数据库。  
  
 首先，初始化并打开**Stream**对象将用来包含查询流：  
  
```  
Dim adoStreamQuery  
Set adoStreamQuery = Server.CreateObject("ADODB.Stream")  
adoStreamQuery.Open  
```  
  
 流内容的查询将 XML 模板查询。  
  
 该模板查询需要对 sql 标识的 XML 命名空间的引用： 前缀\<sql:query > 标记。 SQL SELECT 语句是 XML 模板的内容包括，分配给字符串变量，如下所示：  
  
```  
sQuery = "<ROOT xmlns:sql='urn:schemas-microsoft-com:xml-sql'>  
<sql:query> SELECT * FROM PRODUCTS ORDER BY PRODUCTNAME </sql:query>  
</ROOT>"  
```  
  
 接下来，将字符串写入流：  
  
```  
adoStreamQuery.WriteText sQuery, adWriteChar  
adoStreamQuery.Position = 0  
```  
  
 将分配到 adoStreamQuery **CommandStream**属性的 ADO**命令**对象：  
  
```  
Dim adoCmd  
Set adoCmd  = Server.CreateObject("ADODB.Command"")  
adoCmd.CommandStream = adoStreamQuery  
```  
  
 指定的命令语言**方言**，指示 SQL Server OLE DB 提供程序应如何解释命令流。 特定于提供程序的 GUID 指定方言：  
  
```  
adoCmd.Dialect = "{5D531CB2-E6Ed-11D2-B252-00C04F681B71}"  
```  
  
 最后，执行查询并将结果返回到**记录集**对象：  
  
```  
Set objRS = adoCmd.Execute  
```
