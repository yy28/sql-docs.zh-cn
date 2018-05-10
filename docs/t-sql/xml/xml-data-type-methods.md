---
title: xml 数据类型方法 | Microsoft Docs
ms.custom: ''
ms.date: 03/16/2017
ms.prod: sql
ms.prod_service: sql-database
ms.component: t-sql|xml
ms.reviewer: ''
ms.suite: sql
ms.technology: t-sql
ms.tgt_pltfrm: ''
ms.topic: language-reference
dev_langs:
- TSQL
helpviewer_keywords:
- xml data type [SQL Server], methods
- methods [XML in SQL Server]
ms.assetid: d112b9c9-be9f-435c-a9e6-d21b65778fb7
caps.latest.revision: 32
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: b788282072088b4c9ee98b27b6f4ce3fb2b923c6
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
---
# <a name="xml-data-type-methods"></a>XML 数据类型方法
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  可以使用 **xml** 数据类型方法查询存储在 **xml** 类型的变量或列中的 XML 实例。 本节中的主题介绍如何使用 **xml** 数据类型方法。  
  
## <a name="in-this-section"></a>本节内容  
  
|主题|Description|  
|-----------|-----------------|  
|[query() 方法（xml 数据类型）](../../t-sql/xml/query-method-xml-data-type.md)|说明如何使用 query() 方法查询 XML 实例。|  
|[value() 方法（xml 数据类型）](../../t-sql/xml/value-method-xml-data-type.md)|说明如何使用 value() 方法从 XML 实例中检索 SQL 类型的值。|  
|[exist() 方法（xml 数据类型）](../../t-sql/xml/exist-method-xml-data-type.md)|说明如何使用 exist() 方法确定查询是否返回非空结果。|  
|[modify() 方法（xml 数据类型）](../../t-sql/xml/modify-method-xml-data-type.md)|说明如何使用 modify() 方法指定 [XML 数据修改语言 (XML DML)](../../t-sql/xml/xml-data-modification-language-xml-dml.md) 语句以执行更新。|  
|[nodes() 方法（xml 数据类型）](../../t-sql/xml/nodes-method-xml-data-type.md)|说明如何使用 nodes() 方法将 XML 拆分到多行中，从而将 XML 文档的组成部分传播到行集中。|  
|[在 XML 数据内部绑定关系数据](../../t-sql/xml/binding-relational-data-inside-xml-data.md)|说明如何在 XML 中绑定非 XML 数据。|  
|[xml 数据类型方法的使用准则](../../t-sql/xml/guidelines-for-using-xml-data-type-methods.md)|说明使用 **xml** 数据类型方法的指导原则。|  
  
 您可以通过使用用户定义类型方法调用语法来调用这些方法。 例如：  
  
```  
SELECT XmlCol.query(' ... ')  
FROM   Table  
```  
  
> [!NOTE]  
>  如果对 NULL XML 实例执行 **xml** 数据类型方法 **query()**、**value()** 和 **exist()**，它们将返回 NULL。 此外，**modify()** 不返回任何值，而 **nodes()** 返回行集和一个输入为 NULL 的空行集。  
  
## <a name="see-also"></a>另请参阅  
 [类型化的 XML 与非类型化的 XML 的比较](../../relational-databases/xml/compare-typed-xml-to-untyped-xml.md)   
 [创建 XML 数据的实例](../../relational-databases/xml/create-instances-of-xml-data.md)  
  
  
