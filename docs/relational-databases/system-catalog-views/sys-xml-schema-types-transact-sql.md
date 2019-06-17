---
title: sys.xml_schema_types (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.xml_schema_types_TSQL
- xml_schema_types_TSQL
- sys.xml_schema_types
- xml_schema_types
dev_langs:
- TSQL
helpviewer_keywords:
- sys.xml_schema_types catalog view
ms.assetid: 441ba49d-f778-4fa1-98c4-ced375a01a34
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 9ce5530e160fe6473ff84fca0978b5fc467fe688
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/15/2019
ms.locfileid: "64945863"
---
# <a name="sysxmlschematypes-transact-sql"></a>sys.xml_schema_types (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  返回每个 XML 架构组件，是一种类型，一行**symbol_space**的**T**。  
  
|列名|数据类型|Description|  
|-----------------|---------------|-----------------|  
|**\<继承列 >**||继承中的列[sys.xml_schema_components](../../relational-databases/system-catalog-views/sys-xml-schema-components-transact-sql.md)。|  
|**is_abstract**|**bit**|1 = 类型是抽象类型。 此类型的元素的所有实例必须都使用**xsi: type**以指示不是抽象的派生的类型。<br /><br /> 0 = 类型不是抽象的。 （默认值）|  
|**allows_mixed_content**|**bit**|1 = 允许混合内容<br /><br /> 0 = 不允许混合内容。 （默认值）|  
|**is_extension_blocked**|**bit**|1 = 的阻塞属性时，在实例中阻塞有类型的扩展的替换**complexType**定义或**blockDefault**属性的上级\<架构 >元素信息项设置为"extension"或"#all"。<br /><br /> 0 = 不阻塞有扩展名的替换项。|  
|**is_restriction_blocked**|**bit**|1 = 的阻塞属性时，在实例中阻塞有类型的限制的替换**complexType**定义或**blockDefault**属性的上级\<架构 >元素信息项设置为"restriction"或"#all"。<br /><br /> 0 = 不阻塞有限制的替换项。 （默认值）|  
|**is_final_extension**|**bit**|1 = 派生的类型的扩展时，阻塞上的 final 特性**complexType**定义或**finalDefault**属性的上级\<架构 > 元素的信息项设置为"extension"或"#all"。<br /><br /> 0 = 扩展允许。 （默认值）|  
|**is_final_restriction**|**bit**|1 = 派生的类型的限制时，阻塞简单的最终属性或**complexType**定义或**finalDefault**属性的上级\<架构 > 元素信息项设置为"restriction"或"#all"。<br /><br /> 0 = 允许限制。 （默认值）|  
|**is_final_list_member**|**bit**|1 = 此简单类型无法用作列表中的项类型。<br /><br /> 0 = 此类型是复杂类型，或者它可以用作列表项类型。 （默认值）|  
|**is_final_union_member**|**bit**|1 = 此简单类型无法用作联合类型的成员类型。<br /><br /> 0 = 此类型是复杂类型， 或者它可以用作联合成员类型。 （默认值）|  
  
## <a name="permissions"></a>权限  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)] 有关详细信息，请参阅 [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md)。  
  
## <a name="see-also"></a>请参阅  
 [目录视图 (Transact-SQL)](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)   
 [XML 架构&#40;XML 类型系统&#41;目录视图&#40;Transact SQL&#41;](../../relational-databases/system-catalog-views/xml-schemas-xml-type-system-catalog-views-transact-sql.md)  
  
  
