---
title: "命令流 |Microsoft 文档"
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: guide
ms.technology:
- drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- command streams [ADO]
- streams [ADO], command
ms.assetid: 0ac09dbe-2665-411e-8fbb-d1efe6c777be
caps.latest.revision: 11
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 1be2cc9528e62e548feb242b06686ad50a1753c8
ms.contentlocale: zh-cn
ms.lasthandoff: 09/09/2017

---
# <a name="command-streams"></a>命令流
ADO 已始终支持指定的字符串格式的命令输入**CommandText**属性。 作为替代方法，用 ADO 2.7 或更高版本，你还可以使用信息的流用于命令输入通过分配到流**CommandStream**属性。 你可以分配 ADO**流**对象或任何支持 COM 的对象**IStream**接口。  
  
 命令流的内容只需从传递 ADO 至你提供程序，因此你的提供程序必须支持由使用此功能的流的命令输入。 例如，SQL Server 支持的 XML 模板或为 TRANSACT-SQL 的 OpenXML 扩展的形式进行查询。  
  
 因为提供程序，则必须解释流的详细信息，你必须通过设置中指定的命令方言**方言**属性。 值**方言**是包含 GUID，它由你提供程序定义的字符串。 有关有效值的有关信息**方言**支持你的提供程序，请参阅提供程序文档。  
  
## <a name="xml-template-query-example"></a>XML 模板查询示例  
 下面的示例将写入在 VBScript 中 Northwind 数据库。  
  
 首先，初始化并打开**流**将用于包含查询流对象：  
  
```  
Dim adoStreamQuery  
Set adoStreamQuery = Server.CreateObject("ADODB.Stream")  
adoStreamQuery.Open  
```  
  
 查询流的内容将是 XML 模板查询。  
  
 模板查询需要对由 sql 识别的 XML 命名空间的引用： 前缀\<sql:query > 标记。 SQL SELECT 语句是包括在作为 XML 模板的内容，并分配给字符串变量，如下所示：  
  
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
  
 分配到 adoStreamQuery **CommandStream** ADO 属性**命令**对象：  
  
```  
Dim adoCmd  
Set adoCmd  = Server.CreateObject("ADODB.Command"")  
adoCmd.CommandStream = adoStreamQuery  
```  
  
 指定的命令语言**方言**，指示 SQL Server OLE DB 提供程序应如何解释命令流。 特定于提供程序 GUID 指定的方言：  
  
```  
adoCmd.Dialect = "{5D531CB2-E6Ed-11D2-B252-00C04F681B71}"  
```  
  
 最后，执行查询并将结果返回到**记录集**对象：  
  
```  
Set objRS = adoCmd.Execute  
```

