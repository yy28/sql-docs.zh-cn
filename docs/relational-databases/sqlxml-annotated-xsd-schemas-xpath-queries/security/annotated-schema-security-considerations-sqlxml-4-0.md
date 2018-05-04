---
title: 批注架构安全注意事项 (SQLXML 4.0) |Microsoft 文档
ms.custom: ''
ms.date: 03/17/2017
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
- mapping schema [SQLXML], security
- annotated XDR schemas, security
- XDR schemas [SQLXML], security
- annotations [SQLXML]
- annotated XSD schemas, security
- SQLXML, annotated XSD schemas
- SQLXML, annotated XDR schemas
- security [SQLXML], annotated schemas
- XSD schemas [SQLXML], security
ms.assetid: 7d7e44dc-b6d3-4e0f-95c7-8f99930c94f2
caps.latest.revision: 22
author: douglaslMS
ms.author: douglasl
manager: craigg
monikerRange: = azuresqldb-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: 0766c1b8f4a043f1e1fbec96350e4bfb1c26a5c4
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
---
# <a name="annotated-schema-security-considerations-sqlxml-40"></a>带批注的架构的安全注意事项 (SQLXML 4.0)
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
  以下是在使用带批注的架构时应遵循的安全准则：  
  
-   避免在映射架构中使用默认映射。 默认映射会在生成的 XML 文档中公开数据库信息（表和列名），因为在默认情况下元素名映射为表名而属性名则映射为列名。 因此，能够查看该 XML 文档的任何用户都可以获得数据库中表和列的相关信息，从而带来潜在的安全风险。 若要避免此风险，请在架构中指定随意的元素名和属性名并使用批注将它们显式映射到表和列。 有关使用默认的映射，在创建 XSD 架构的详细信息，请参阅[默认映射的 XSD 元素和特性移动到表和列&#40;SQLXML 4.0&#41;](../../../relational-databases/sqlxml-annotated-xsd-schemas-using/default-mapping-of-xsd-elements-and-attributes-to-tables-and-columns-sqlxml-4-0.md)。  
  
-   使用批注指定的显式映射公开数据库信息（如表名和列名）。 因此，最好不要让这些架构能够公开使用。  
  
-   如指定针对具有递归的映射架构的某些查询 (使用指定**最大深度**批注设置为较高的值) 可能需要更长时间才能执行。 通过将命令超时属性设置 （以秒为单位），可以选择指定的超时限制。 例如：  
  
    ```  
    cn.Open "Provider=SQLOLEDB;Server=localhost;Database=tempdb;Integrated Security=SSPI;Command Properties='Command Time Out=50';"  
    ```  
  
## <a name="see-also"></a>另请参阅  
 [SQLXML 4.0 中的带批注的 XSD 架构](../../../relational-databases/sqlxml/annotated-xsd-schemas/annotated-xsd-schemas-in-sqlxml-4-0.md)  
  
  
