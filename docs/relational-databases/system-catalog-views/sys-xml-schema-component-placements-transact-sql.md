---
title: sys.xml_schema_component_placements （Transact-sql） |Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.xml_schema_component_placements
- xml_schema_component_placements_TSQL
- xml_schema_component_placements
- sys.xml_schema_component_placements_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.xml_schema_component_placements catalog view
ms.assetid: 2d3c8828-e4b3-423d-bf11-990464c1341b
author: pmasl
ms.author: pelopes
ms.reviewer: mikeray
ms.openlocfilehash: f63f2eee6898a3b20eeef21804f3ef3441ddc1c8
ms.sourcegitcommit: f7ac1976d4bfa224332edd9ef2f4377a4d55a2c9
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/02/2020
ms.locfileid: "85900612"
---
# <a name="sysxml_schema_component_placements-transact-sql"></a>sys.xml_schema_component_placements (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  对于每个 XML 架构组件位置，相应地返回一行。  
   
|列名称|数据类型|说明|  
|-----------------|---------------|-----------------|  
|**xml_component_id**|**int**|拥有此位置的 XML 架构组件的 ID。|  
|**placement_id**|**int**|位置的 ID。 在拥有它的 XML 架构组件中，位置 ID 是唯一的。|  
|**placed_xml_component_id**|**int**|所放置的 XML 架构组件的 ID。|  
|**is_default_fixed**|**bit**|1 = 默认值为固定值。 不能在 XML 实例中覆盖此值。<br /><br /> 0 = 可以覆盖该值。（默认）|  
|**min_occurrences**|**int**|所放置的组件的最小出现次数。|  
|**max_occurrences**|**int**|所放置的组件的最大出现次数。|  
|**default_value**|**nvarchar （4000）**|如果提供值，则该值为默认值。 如果未提供默认值，则为 NULL。|  
  
## <a name="permissions"></a>权限  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)] 有关详细信息，请参阅 [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md)。  
  
## <a name="see-also"></a>另请参阅  
 [Transact-sql&#41;的目录视图 &#40;](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)   
 [XML 架构 &#40;XML 类型系统&#41; 目录视图 &#40;Transact-sql&#41;](../../relational-databases/system-catalog-views/xml-schemas-xml-type-system-catalog-views-transact-sql.md)  
  
  
