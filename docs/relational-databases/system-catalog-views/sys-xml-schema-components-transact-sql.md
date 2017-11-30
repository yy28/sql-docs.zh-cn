---
title: "sys.xml_schema_components (Transact SQL) |Microsoft 文档"
ms.custom: 
ms.date: 06/10/2016
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: system-catalog-views
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- xml_schema_components
- sys.xml_schema_components_TSQL
- sys.xml_schema_components
- xml_schema_components_TSQL
dev_langs: TSQL
helpviewer_keywords: sys.xml_schema_components catalog view
ms.assetid: 70142d3a-f8b5-4ee2-8287-3935f0f67aa2
caps.latest.revision: "35"
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 7a3e5b71a36df056dbba198a86af316d32fb9eaf
ms.sourcegitcommit: 9fbe5403e902eb996bab0b1285cdade281c1cb16
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/27/2017
---
# <a name="sysxmlschemacomponents-transact-sql"></a>sys.xml_schema_components (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  针对 XML 架构的每个组件返回一行。 对 (**collection_id**， **namespace_id**) 是包含的命名空间的复合外键。 对于名为组件，的值**symbol_space**，**名称**， **scoping_xml_component_id**， **is_qualified**， **xml_namespace_id**， **xml_collection_id**是唯一的。  
  
|列名|数据类型|Description|  
|-----------------|---------------|-----------------|  
|**xml_component_id**|**int**|在数据库中的 XML 架构组件的唯一 ID。|  
|**xml_collection_id**|**int**|包含此组件的命名空间的 XML 架构集合的 ID。|  
|**xml_namespace_id**|**int**|集合中的 XML 命名空间的 ID。|  
|**is_qualified**|**bit**|1 = 该组件具有显式命名空间限定符。<br /><br /> 0 = 这是一个本地范围的组件。 在此情况下，对， **namespace_id**， **collection_id**，指的是"没有命名空间" **targetNamespace**。<br /><br /> 对于通配符组成部分，该值将等于 1。|  
|**名称**|**nvarchar**<br /><br /> **(4000)**|XML 架构组件的唯一名称。 如果该组件未命名，则为 NULL。|  
|**symbol_space**|**char （1)**|此符号名称是唯一的在其中的空间基于**类型**:<br /><br /> N = 无<br /><br /> T = 类型<br /><br /> E = 元素<br /><br /> M = 模型–组<br /><br /> A = 属性<br /><br /> G = 属性–组|  
|**symbol_space_desc**|**nvarchar**<br /><br /> **(60)**|此符号名称是唯一的在其中的空间的说明基于**类型**:<br /><br /> 无<br /><br /> TYPE<br /><br /> ELEMENT<br /><br /> MODEL_GROUP<br /><br /> ATTRIBUTE<br /><br /> ATTRIBUTE_GROUP|  
|**类型**|**char （1)**|XML 架构组件的类型。<br /><br /> N = 任何类型（特殊的内部组件）<br /><br /> Z = 任意简单类型（特殊的内部组件）<br /><br /> P = Primitive 类型（内部类型）<br /><br /> S = 简单类型<br /><br /> L = 列表类型<br /><br /> U = 联合类型<br /><br /> C = 复杂的简单类型（派生自简单类型）<br /><br /> K = 复杂类型<br /><br /> E = 元素<br /><br /> M = 模型–组<br /><br /> W = 元素-通配符<br /><br /> A = 属性<br /><br /> G = 属性–组<br /><br /> V = 属性-通配符|  
|**kind_desc**|**nvarchar**<br /><br /> **(60)**|对 XML 架构组件类型的说明：<br /><br /> ANY_TYPE<br /><br /> ANY_SIMPLE_TYPE<br /><br /> PRIMITIVE_TYPE<br /><br /> SIMPLE_TYPE<br /><br /> LIST_TYPE<br /><br /> UNION_TYPE<br /><br /> COMPLEX_SIMPLE_TYPE<br /><br /> COMPLEX_TYPE<br /><br /> ELEMENT<br /><br /> MODEL_GROUP<br /><br /> ELEMENT_WILDCARD<br /><br /> ATTRIBUTE<br /><br /> ATTRIBUTE_GROUP<br /><br /> ATTRIBUTE_WILDCARD|  
|**派生**|**char （1)**|派生类型的派生方法：<br /><br /> N = 无（非派生）<br /><br /> X = 扩展<br /><br /> R = 限制<br /><br /> S = 替换|  
|**derivation_desc**|**nvarchar**<br /><br /> **(60)**|对派生类型的派生方法的说明：<br /><br /> 无<br /><br /> EXTENSION<br /><br /> RESTRICTION<br /><br /> SUBSTITUTION|  
|**base_xml_component_id**|**int**|该组件派生自的组件的 ID。 如果不存在，则为 NULL。|  
|**scoping_xml_component_id**|**int**|范围组件的唯一 ID。 如果不存在（全局范围），则为 NULL。|  
  
## <a name="permissions"></a>Permissions  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)] 有关详细信息，请参阅 [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md)。  
  
## <a name="see-also"></a>另请参阅  
 [目录视图 (Transact-SQL)](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)   
 [XML 架构 &#40;XML 类型系统 &#41;目录视图 &#40;Transact SQL &#41;](../../relational-databases/system-catalog-views/xml-schemas-xml-type-system-catalog-views-transact-sql.md)  
  
  
