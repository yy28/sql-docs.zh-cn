---
title: "xml 数据类型方法 |Microsoft 文档"
ms.custom: 
ms.date: 03/16/2017
ms.prod: sql-non-specified
ms.prod_service: sql-database
ms.service: 
ms.component: t-sql|xml
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
dev_langs:
- TSQL
helpviewer_keywords:
- xml data type [SQL Server], methods
- methods [XML in SQL Server]
ms.assetid: d112b9c9-be9f-435c-a9e6-d21b65778fb7
caps.latest.revision: 32
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: fcf16bd9b71f27ab91fb02bbfd7bb7625185b44e
ms.contentlocale: zh-cn
ms.lasthandoff: 09/01/2017

---
# <a name="xml-data-type-methods"></a>XML 数据类型方法
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  你可以使用**xml**数据类型方法查询 XML 实例存储在变量或列**xml**类型。 本部分中的主题介绍如何使用**xml**数据类型方法。  
  
## <a name="in-this-section"></a>本节内容  
  
|主题|Description|  
|-----------|-----------------|  
|[查询 &#40; &#41;方法 &#40; xml 数据类型 &#41;](../../t-sql/xml/query-method-xml-data-type.md)|说明如何使用 query() 方法查询 XML 实例。|  
|[值 &#40; &#41;方法 &#40; xml 数据类型 &#41;](../../t-sql/xml/value-method-xml-data-type.md)|说明如何使用 value() 方法从 XML 实例中检索 SQL 类型的值。|  
|[存在 &#40; &#41;方法 &#40; xml 数据类型 &#41;](../../t-sql/xml/exist-method-xml-data-type.md)|说明如何使用 exist() 方法确定查询是否返回非空结果。|  
|[修改 &#40; &#41;方法 &#40; xml 数据类型 &#41;](../../t-sql/xml/modify-method-xml-data-type.md)|描述如何使用 modify （） 方法指定[XML 数据修改语言 &#40;XML DML &#41;](../../t-sql/xml/xml-data-modification-language-xml-dml.md)语句以执行更新。|  
|[节点 &#40; &#41;方法 &#40; xml 数据类型 &#41;](../../t-sql/xml/nodes-method-xml-data-type.md)|说明如何使用 nodes() 方法将 XML 拆分到多行中，从而将 XML 文档的组成部分传播到行集中。|  
|[在 XML 数据内部绑定关系数据](../../t-sql/xml/binding-relational-data-inside-xml-data.md)|说明如何在 XML 中绑定非 XML 数据。|  
|[xml 数据类型方法的使用准则](../../t-sql/xml/guidelines-for-using-xml-data-type-methods.md)|描述使用准则**xml**数据类型方法。|  
  
 您可以通过使用用户定义类型方法调用语法来调用这些方法。 例如：  
  
```  
SELECT XmlCol.query(' ... ')  
FROM   Table  
```  
  
> [!NOTE]  
>  **Xml**数据类型方法**query （)**， **value （)**，和**exist （)**返回 NULL，如果对 NULL XML 实例执行。 此外， **modify （)**不返回任何内容，但**nodes （)**与 NULL 输入返回行集和行集为空。  
  
## <a name="see-also"></a>另请参阅  
 [类型化的 XML 与非类型化的 XML 的比较](../../relational-databases/xml/compare-typed-xml-to-untyped-xml.md)   
 [创建 XML 数据的实例](../../relational-databases/xml/create-instances-of-xml-data.md)  
  
  

