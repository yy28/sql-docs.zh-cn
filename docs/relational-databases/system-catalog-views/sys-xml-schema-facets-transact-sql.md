---
title: sys. xml_schema_facets （Transact-sql） |Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.xml_schema_facets
- xml_schema_facets_TSQL
- sys.xml_schema_facets_TSQL
- xml_schema_facets
dev_langs:
- TSQL
helpviewer_keywords:
- sys.xml_schema_facets catalog view
ms.assetid: 4402dde9-1877-4872-8550-140dc2a177d2
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: fa9d06f18f1e5d401e730a8216d3bb43f4894e06
ms.sourcegitcommit: 4d3896882c5930248a6e441937c50e8e027d29fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/05/2020
ms.locfileid: "82833824"
---
# <a name="sysxml_schema_facets-transact-sql"></a>sys.xml_schema_facets (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  返回 xml 类型定义的每个方面（限制）的行（对应于**sys.databases. xml_types**）。  
  
|列名称|数据类型|说明|  
|-----------------|---------------|-----------------|  
|**xml_component_id**|**int**|此方面所属的 XML 组件（类型）的 ID。|  
|**facet_id**|**int**|方面的 ID（基于 1 的序号），在组件 ID 中是唯一的。|  
|**kind**|**char(2)**|方面的种类：<br /><br /> LG = 长度<br /><br /> LN = 最小长度<br /><br /> LX = 最大长度<br /><br /> PT = 模式（正则表达式）<br /><br /> EU = 枚举<br /><br /> IN = 最小包括值<br /><br /> IX = 最大包括值<br /><br /> EN = 最小排他值<br /><br /> EX = 最大排他值<br /><br /> DT = 总位数<br /><br /> DF = 小数位数<br /><br /> WS = 空格规范化|  
|**kind_desc**|**nvarchar （60）**|对方面种类的说明：<br /><br /> LENGTH<br /><br /> MINIMUM_LENGTH<br /><br /> MAXIMUM_LENGTH<br /><br /> PATTERN<br /><br /> ENUMERATION<br /><br /> MINIMUM_INCLUSIVE_VALUE<br /><br /> MAXIMUM_INCLUSIVE_VALUE<br /><br /> MINIMUM_EXCLUSIVE_VALUE<br /><br /> MAXIMUM_EXCLUSIVE_VALUE<br /><br /> TOTAL_DIGITS<br /><br /> FRACTION_DIGITS<br /><br /> WHITESPACE_NORMALIZATION|  
|**is_fixed**|**bit**|1 = 方面有预先指定的固定值。<br /><br /> 0 = 没有固定值。 （默认值）|  
|**value**|**nvarchar （4000）**|方面的预先指定的固定值。|  
  
## <a name="permissions"></a>权限  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)] 有关详细信息，请参阅 [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md)。  
  
## <a name="see-also"></a>另请参阅  
 [Transact-sql&#41;的目录视图 &#40;](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)   
 [XML 架构 &#40;XML 类型系统&#41; 目录视图 &#40;Transact-sql&#41;](../../relational-databases/system-catalog-views/xml-schemas-xml-type-system-catalog-views-transact-sql.md)  
  
  
