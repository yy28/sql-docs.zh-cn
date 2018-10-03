---
title: sys.xml_schema_elements (TRANSACT-SQL) |Microsoft Docs
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
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: ed5c7efe1c5adacba99b74ab40e2978a51ba7517
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/01/2018
ms.locfileid: "47716685"
---
# <a name="sysxmlschemaelements-transact-sql"></a>sys.xml_schema_elements (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  返回每个 XML 架构组件，是一种类型，一行**symbol_space**的**E**。  
  
|列名|数据类型|Description|  
|-----------------|---------------|-----------------|  
|**\<继承列 >**|**--**|继承中的列[sys.xml_schema_components](../../relational-databases/system-catalog-views/sys-xml-schema-components-transact-sql.md)。|  
|**is_default_fixed**|**bit**|1 = 默认值为固定值。 在 XML 实例中不能覆盖此值。<br /><br /> 0 = 默认值不是元素的固定值。 （默认值）。|  
|**is_abstract**|**bit**|1 = 元素是抽象元素，且不可用于实例文档中。 该元素的替换组成员必须出现在实例文档中。<br /><br /> 0 = 元素不是抽象元素。 （默认值）。|  
|**is_nillable**|**bit**|1 = 元素是 nillable 元素。<br /><br /> 0 = 元素不是 nillable 元素。 （默认值）|  
|**must_be_qualified**|**bit**|1 = 元素必须由命名空间显式限定。<br /><br /> 0 = 元素可由命名空间隐式限定。 （默认值）|  
|**is_extension_blocked**|**bit**|1 = 禁止使用扩展类型的实例进行替换。<br /><br /> 0 = 允许使用扩展类型进行替换。 （默认值）|  
|**is_restriction_blocked**|**bit**|1 = 禁止使用限制类型的实例进行替换。<br /><br /> 0 = 允许使用限制类型进行替换。 （默认值）|  
|**is_substitution_blocked**|**bit**|1 = 不能使用替换组的实例。<br /><br /> 0 = 允许使用替换组进行替换。 （默认值）|  
|**is_final_extension**|**bit**|1 = 不允许使用扩展类型的实例进行替换。<br /><br /> 0 = 允许使用扩展类型的实例进行替换。 （默认值）|  
|**is_final_restriction**|**bit**|1 = 不允许使用限制类型的实例进行替换。<br /><br /> 0 = 允许使用限制类型的实例进行替换。 （默认值）|  
|**default_value**|**nvarchar (4000)**|元素的默认值。 如果未提供默认值为 NULL。|  
  
## <a name="permissions"></a>Permissions  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)] 有关详细信息，请参阅 [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md)。  
  
## <a name="see-also"></a>请参阅  
 [目录视图 (Transact-SQL)](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)   
 [XML 架构&#40;XML 类型系统&#41;目录视图&#40;Transact SQL&#41;](../../relational-databases/system-catalog-views/xml-schemas-xml-type-system-catalog-views-transact-sql.md)  
  
  
