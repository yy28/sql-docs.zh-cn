---
title: xml_schema_namespace (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 07/27/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- xml_schema_namespace_TSQL
- xml_schema_namespace
dev_langs:
- TSQL
helpviewer_keywords:
- XML schema collections [SQL Server], reconstructing schemas
- xml_schema_namespace function
- reconstructing schemas
- schemas [SQL Server], XML
- schema collections [SQL Server], reconstructing schemas
ms.assetid: ee9873d8-dd3a-4bff-a10c-68bbadbdf1a6
author: MightyPen
ms.author: genemi
ms.openlocfilehash: bb3b19e67a4a85ef3f7a26d7ad792e7e39459302
ms.sourcegitcommit: b2e81cb349eecacee91cd3766410ffb3677ad7e2
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/01/2020
ms.locfileid: "67948039"
---
# <a name="xml_schema_namespace"></a>xml_schema_namespace
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  重新构造指定 XML 架构集合中的所有架构或特定架构。 此函数返回 **xml** 数据类型实例。  
  
![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "“主题链接”图标") [Transact-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>语法  
  
```  
  
xml_schema_namespace( Relational_schema , XML_schema_collection_name , [ Namespace ] )  
```  
  
## <a name="arguments"></a>参数  
 *Relational_schema*  
 关系架构名称。 Relational_schema  是 **sysname**。  
  
 *XML_schema_collection_name*  
 要重新构造的 XML 架构集合的名称。 XML_schema_collection_name  是 **sysname**。  
  
 *Namespace*  
 要重新构造的 XML 架构的命名空间 URI。 它最多包含 1,000 个字符。 如果未提供命名空间 URI，则重新构造整个 XML 架构集合。 Namespace  是 **nvarchar(4000)** 。  
  
## <a name="return-types"></a>返回类型  
 **xml**  
  
## <a name="remarks"></a>备注  
 在使用 [CREATE XML SCHEMA COLLECTION](../../t-sql/statements/create-xml-schema-collection-transact-sql.md) 或 [ALTER XML SCHEMA COLLECTION](../../t-sql/statements/alter-xml-schema-collection-transact-sql.md) 在数据库中导入 XML 架构组件时，将保留架构用于验证的所有特征。 因此，重新构建的架构在用词上与原始架构文档可能有所不同。 特别是，注释、空格和批注将会丢失；并且隐式类型的信息将变成显式的。 例如，\<xs:element name="e1" /> 将变为 \<xs:element name="e1" type="xs:anyType"/>。 此外，不保留命名空间前缀。  
  
 如果指定了命名空间参数，则生成的架构文档将包含该命名空间中所有架构组件的定义，即使在不同的架构文档和/或 DDL 步骤中添加了这些组件也是如此。  
  
 此函数不能用于从 **sys.sys** XML 架构集合构建 XML 架构文档。  
  
## <a name="examples"></a>示例  
 以下示例从 `ProductDescriptionSchemaCollection` 数据库中的产品关系架构中检索 XML 架构集合 `AdventureWorks`。  
  
```  
USE AdventureWorks;  
GO  
SELECT xml_schema_namespace(N'production',N'ProductDescriptionSchemaCollection');  
GO  
```  
  
## <a name="see-also"></a>另请参阅  
 [查看存储 XML 架构集合](../../relational-databases/xml/view-a-stored-xml-schema-collection.md)   
 [XML 架构集合 (SQL Server)](../../relational-databases/xml/xml-schema-collections-sql-server.md)  
  
  
