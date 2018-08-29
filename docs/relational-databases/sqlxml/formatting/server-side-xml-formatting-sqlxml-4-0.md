---
title: 服务器端 XML 格式化 (SQLXML 4.0) |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.component: sqlxml
ms.reviewer: ''
ms.suite: sql
ms.technology: xml
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- FOR XML clause, formatting
- server-side XML formatting
ms.assetid: ae9ea068-0857-4505-a3b2-f53d256b644c
caps.latest.revision: 12
author: douglaslMS
ms.author: douglasl
manager: craigg
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 85cb344627ccf006ccde6f6becb80713b046b3e4
ms.sourcegitcommit: 4183dc18999ad243c40c907ce736f0b7b7f98235
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/27/2018
ms.locfileid: "43064629"
---
# <a name="server-side-xml-formatting-sqlxml-40"></a>服务器端 XML 格式 (SQLXML 4.0)
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
  本主题提供有关在服务器端从对 Microsoft [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 中数据库执行的查询生成的行集设置 XML 文档格式的信息。  
  
 在 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 中，可以将 XML 文档存储到数据库表中，或者从数据库表中检索 XML 文档。 若要检索某一 XML 文档，请在 SELECT 查询中使用 FOR XML 查询扩展插件。  
  
 例如，假定客户端应用程序执行对执行命令[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]，它包含以下[!INCLUDE[tsql](../../../includes/tsql-md.md)]查询：  
  
```  
SELECT FirstName, LastName  
FROM   Person.Contact  
FOR XML AUTO  
```  
  
 服务器分两步执行该查询。 首先，服务器执行此 SELECT 语句：  
  
```  
SELECT FirstName, LastName  
FROM   Person.Contact  
```  
  
 然后，服务器将 FOR XML 转换应用到生成的行集中。 生成的 XML 然后作为单列行集发送到客户端。 在本文档中，此过程称作服务器端 XML 格式。  
  
 在服务器端，可以使用 FOR XML 子句指定以下模式：  
  
-   RAW  
  
-   AUTO  
  
-   EXPLICIT  
  
 有关 FOR XML 子句的详细信息，请参阅[使用 FOR XML 构造 XML](../../../relational-databases/xml/for-xml-sql-server.md)。  
  
## <a name="see-also"></a>请参阅  
 [客户端和服务器端 XML 格式的体系结构&#40;SQLXML 4.0&#41;](../../../relational-databases/sqlxml/formatting/architecture-of-client-side-and-server-side-xml-formatting-sqlxml-4-0.md)   
 [客户端 XML 格式设置&#40;SQLXML 4.0&#41;](../../../relational-databases/sqlxml/formatting/client-side-xml-formatting-sqlxml-4-0.md)   
 [FOR XML (SQL Server)](../../../relational-databases/xml/for-xml-sql-server.md)  
  
  
