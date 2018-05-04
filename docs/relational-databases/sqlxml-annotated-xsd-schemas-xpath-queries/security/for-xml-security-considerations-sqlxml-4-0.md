---
title: 有关 XML 安全注意事项 (SQLXML 4.0) |Microsoft 文档
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.service: ''
ms.component: sqlxml
ms.reviewer: ''
ms.suite: sql
ms.technology: xml
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- NESTED mode
- client-side XML formatting
- FOR XML clause, security
- server-side XML formatting
- AUTO mode
- security [SQLXML], FOR XML
ms.assetid: facba279-df93-475b-ad43-0043dc5bae03
caps.latest.revision: 23
author: douglaslMS
ms.author: douglasl
manager: craigg
monikerRange: = azuresqldb-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: 69626557e5e17e1e91c1b5f13af0f962f13f6483
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
---
# <a name="for-xml-security-considerations-sqlxml-40"></a>FOR XML 安全注意事项 (SQLXML 4.0)
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
  FOR XML AUTO 模式生成这样一种 XML 层次结构，其中的元素名称映射到表名，属性名称映射到列名。 这公开了数据库表和列的信息。 通过在查询中指定表和列的别名，可以在使用 AUTO 模式（服务器端格式）时隐藏数据库信息。 在生成的 XML 文档中，这些别名作为元素和属性名称返回。  
  
 例如，下面的查询指定 AUTO 模式；因此，在服务器上执行 XML 格式设置：  
  
```  
SELECT C.FirstName as F,C.LastName as L   
FROM Person.Contact C   
FOR XML AUTO  
```  
  
 在生成的 XML 文档中，这些别名用作元素和属性名称：  
  
```  
<?xml version="1.0" encoding="utf-8" ?>   
<root>  
  <C F="Nancy" L="Fuller" />   
  <CE F="Andrew" L="Peacock" />   
  <C F="Janet" L="Leverling" />   
  ...  
</root>  
```  
  
 使用 NESTED 模式（客户端格式）时，在生成的 XML 中仅为属性返回别名。 基表的名称始终作为元素名称返回。 例如，下面的查询指定 NESTED 模式。  
  
```  
SELECT C.FirstName as F,C.LastName as L   
FROM Person.Contact C   
FOR XML AUTO  
```  
  
 在生成的 XML 文档中，基表的名称作为元素名称返回，且未使用表别名：  
  
```  
<?xml version="1.0" encoding="utf-8" ?>   
<root>  
  <Person.Contact F="Nancy" L="Fuller" />   
  <Person.Contact F="Andrew" L="Peacock" />   
  <Person.Contact F="Janet" L="Leverling" />   
       ...  
</root>  
```  
  
  
