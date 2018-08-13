---
title: 使用 Updategram 修改 SQLXML 4.0 中的数据 |Microsoft Docs
ms.custom: ''
ms.date: 03/17/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.component: sqlxml
ms.reviewer: ''
ms.suite: sql
ms.technology: xml
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- SQLXML, updategrams
- data insertions [SQLXML]
- data deletions [SQLXML]
- updating data [SQLXML]
- modifying data [SQLXML]
- OPENXML function
- updategrams [SQLXML]
- database modifications [SQLXML]
- data updates [SQLXML]
- modifying databases
- data modifications [SQLXML]
- deleting data
- inserting data
ms.assetid: b8b3b892-cb73-41d0-b945-bce148d81d9b
caps.latest.revision: 26
author: douglaslMS
ms.author: douglasl
manager: craigg
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017
ms.openlocfilehash: 7a6e29fdb90e0e0eee35d6b072e25b1ffc6451e1
ms.sourcegitcommit: 4cd008a77f456b35204989bbdd31db352716bbe6
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/06/2018
ms.locfileid: "39545547"
---
# <a name="using-updategrams-to-modify-data-in-sqlxml-40"></a>使用 Updategram 修改 SQLXML 4.0 中的数据
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
  您可以修改 （插入、 更新或删除） 中的数据库[!INCLUDE[msCoName](../../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]从现有 XML 文档通过使用 updategram 或 OPENXML[!INCLUDE[tsql](../../../includes/tsql-md.md)]函数。  
  
 本节提供有关 updategram 的信息及其使用示例。  
  
## <a name="in-this-section"></a>本节内容  
 [Updategram 简介&#40;SQLXML 4.0&#41;](../../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/updategrams/introduction-to-updategrams-sqlxml-4-0.md)  
 提供 updategram 的基本信息和示例。  
  
 [在 Updategram 中指定带批注的映射架构&#40;SQLXML 4.0&#41;](../../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/updategrams/specifying-an-annotated-mapping-schema-in-an-updategram-sqlxml-4-0.md)  
 说明 updategram 中带批注的映射架构并提供有关示例。  
  
 [NULL 处理&#40;SQLXML 4.0&#41;](../../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/updategrams/null-handling-sqlxml-4-0.md)  
 说明如何为元素和属性值指定 NULL。  
  
 [使用 XML Updategram 插入数据&#40;SQLXML 4.0&#41;](../../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/updategrams/inserting-data-using-xml-updategrams-sqlxml-4-0.md)  
 说明如何使用 updategram 插入数据并提供有关示例。  
  
 [使用 XML Updategram 删除数据&#40;SQLXML 4.0&#41;](../../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/updategrams/deleting-data-using-xml-updategrams-sqlxml-4-0.md)  
 说明如何使用 updategram 删除数据并提供有关示例。  
  
 [使用 XML Updategram 更新数据&#40;SQLXML 4.0&#41;](../../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/updategrams/updating-data-using-xml-updategrams-sqlxml-4-0.md)  
 说明如何使用 updategram 修改现有数据并提供有关示例。  
  
 [将参数传递到 Updategram &#40;SQLXML 4.0&#41;](../../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/updategrams/passing-parameters-to-updategrams-sqlxml-4-0.md)  
 说明如何将参数传递到 updategram 并提供有关示例。  
  
 [处理数据库并发问题在 Updategram 中的&#40;SQLXML 4.0&#41;](../../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/updategrams/handling-database-concurrency-issues-in-updategrams-sqlxml-4-0.md)  
 说明为处理 updategram 中的并发问题可能采取的不同层级的保护并且提供有关示例。  
  
 [Updategram 示例应用程序&#40;SQLXML 4.0&#41;](http://msdn.microsoft.com/library/d2287e10-4007-4ba4-ad84-4e2b6adfede5)  
 提供使用 updategram 的示例应用程序。  
  
 [XML Updategram 的准则和限制&#40;SQLXML 4.0&#41;](../../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/updategrams/guidelines-and-limitations-of-xml-updategrams-sqlxml-4-0.md)  
 列出使用 updategram 时应注意的一些事项。  
  
  
