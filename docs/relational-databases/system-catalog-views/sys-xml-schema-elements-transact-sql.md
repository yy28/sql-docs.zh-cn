---
title: sys. xml_schema_elements （Transact-sql） |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.xml_schema_elements
- sys.xml_schema_elements_TSQL
- xml_schema_elements
- xml_schema_elements_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.xml_schema_elements catalog view
ms.assetid: 190ed0cd-0c5e-4607-9db4-9e77cacf17d7
author: MightyPen
ms.author: genemi
ms.openlocfilehash: d43f30f15502a41882190dcdd19984d9ec042d4a
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/27/2020
ms.locfileid: "68037395"
---
# <a name="sysxml_schema_elements-transact-sql"></a>sys.xml_schema_elements (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  为每个 XML 架构组件返回一行， **symbol_space**为**E**类型。  
  
|列名称|数据类型|说明|  
|-----------------|---------------|-----------------|  
|**\<继承列>**|**--**|从 sys.databases 继承列[xml_schema_components](../../relational-databases/system-catalog-views/sys-xml-schema-components-transact-sql.md)。|  
|**is_default_fixed**|**bit**|1 = 默认值为固定值。 在 XML 实例中不能覆盖此值。<br /><br /> 0 = 默认值不是元素的固定值。 （默认值）。|  
|**is_abstract**|**bit**|1 = 元素是抽象元素，且不可用于实例文档中。 该元素的替换组成员必须出现在实例文档中。<br /><br /> 0 = 元素不是抽象元素。 （默认值）。|  
|**is_nillable**|**bit**|1 = 元素是 nillable 元素。<br /><br /> 0 = 元素不是 nillable 元素。 （默认值）|  
|**must_be_qualified**|**bit**|1 = 元素必须由命名空间显式限定。<br /><br /> 0 = 元素可由命名空间隐式限定。 （默认值）|  
|**is_extension_blocked**|**bit**|1 = 禁止使用扩展类型的实例进行替换。<br /><br /> 0 = 允许使用扩展类型进行替换。 （默认值）|  
|**is_restriction_blocked**|**bit**|1 = 禁止使用限制类型的实例进行替换。<br /><br /> 0 = 允许使用限制类型进行替换。 （默认值）|  
|**is_substitution_blocked**|**bit**|1 = 不能使用替换组的实例。<br /><br /> 0 = 允许使用替换组进行替换。 （默认值）|  
|**is_final_extension**|**bit**|1 = 不允许使用扩展类型的实例进行替换。<br /><br /> 0 = 允许使用扩展类型的实例进行替换。 （默认值）|  
|**is_final_restriction**|**bit**|1 = 不允许使用限制类型的实例进行替换。<br /><br /> 0 = 允许使用限制类型的实例进行替换。 （默认值）|  
|**default_value**|**nvarchar （4000）**|元素的默认值。 如果未提供默认值，则为 NULL。|  
  
## <a name="permissions"></a>权限  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)] 有关详细信息，请参阅 [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md)。  
  
## <a name="see-also"></a>另请参阅  
 [Transact-sql&#41;的目录视图 &#40;](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)   
 [XML 架构 &#40;XML 类型系统&#41; 目录视图 &#40;Transact-sql&#41;](../../relational-databases/system-catalog-views/xml-schemas-xml-type-system-catalog-views-transact-sql.md)  
  
  
