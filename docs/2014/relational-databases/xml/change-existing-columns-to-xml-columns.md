---
title: 将现有列更改为 XML 列 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: xml
ms.topic: conceptual
helpviewer_keywords:
- tables [XML]
ms.assetid: 0d951424-9862-41fe-bd46-127f1c059bcb
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 223f587b35a55b6f2df6d31ca64f48aac96fd6f1
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/26/2020
ms.locfileid: "63288338"
---
# <a name="change-existing-columns-to-xml-columns"></a>将现有列更改为 XML 列
  ALTER TABLE 语句支持 `xml` 数据类型。 例如，可以将任意字符串类型列更改为 `xml` 数据类型。 注意，在这些情况下，列中包含的文档必须格式正确。 此外，如果将列的类型从字符串更改为类型化的 xml，则列中的文档将根据指定的 XSD 架构进行验证。  
  
```  
CREATE TABLE T (Col1 int primary key, Col2 nvarchar(max))  
GO  
INSERT INTO T   
VALUES (1, '<Root><Product ProductID="1"/></Root>')  
GO  
ALTER TABLE T   
ALTER COLUMN Col2 xml  
GO  
```  
  
 可以将 `xml` 类型列从非类型化的 XML 更改为类型化的 XML。 例如：  
  
```  
CREATE TABLE T (Col1 int primary key, Col2 xml)  
GO  
INSERT INTO T   
values (1, '<p1:ProductDescription ProductModelID="1"   
xmlns:p1="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelDescription">  
            </p1:ProductDescription>')  
GO   
-- Make it a typed xml column by specifying a schema collection.  
ALTER TABLE T   
ALTER COLUMN Col2 xml (Production.ProductDescriptionSchemaCollection)  
GO  
```  
  
> [!NOTE]  
>  将对 [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] 数据库运行脚本，因为已将 XML 架构集合 `Production.ProductDescriptionSchemaCollection`创建为 [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] 数据库的一部分。  
  
 在上一个示例中，存储在列中的所有实例都将根据指定集合中的 XSD 架构来验证和类型化。 如果列包含对于指定架构无效的一个或多个 XML 实例，则 `ALTER TABLE` 语句将失败，并且您无法将非类型化的 XML 列更改为类型化的 XML。  
  
> [!NOTE]  
>  如果表非常庞大，则修改 `xml` 类型列的开销会很大。 这是因为必须检查每个文档格式是否正确，还必须验证每个文档是否为类型化的 XML。  
  
 有关类型化 XML 的详细信息，请参阅 [类型化的 XML 与非类型化的 XML 的比较](compare-typed-xml-to-untyped-xml.md)。  
  
  
