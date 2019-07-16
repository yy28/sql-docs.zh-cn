---
title: sys.xml_schema_wildcards (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.xml_schema_wildcards
- sys.xml_schema_wildcards_TSQL
- xml_schema_wildcards
- xml_schema_wildcards_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.xml_schema_wildcards catalog view
ms.assetid: 7cedfe9a-e99e-4777-8a28-98674b6e5cff
author: MightyPen
ms.author: genemi
ms.openlocfilehash: e725df2676084f74b51a8a68d74fbc32e0c32152
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/15/2019
ms.locfileid: "68060396"
---
# <a name="sysxmlschemawildcards-transact-sql"></a>sys.xml_schema_wildcards (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  返回行，每个 XML 架构组件，是属性通配符 (**种类**的**V**) 或元素通配符 (**种类**的**W**)，这两个与**symbol_space**的**N**。  
  
|列名|数据类型|描述|  
|-----------------|---------------|-----------------|  
|**\<继承列 >**||继承中的列[sys.xml_schema_components](../../relational-databases/system-catalog-views/sys-xml-schema-components-transact-sql.md)。|  
|**process_content**|**char(1)**|指示处理内容的方式。<br /><br /> S = 严格验证（必须验证）<br /><br /> L = 非严格验证（在可能的情况下进行验证）<br /><br /> P = 跳过验证|  
|**process_content_desc**|**nvarchar(60)**|有关处理内容的方式的说明：<br /><br /> **STRICT_VALIDATION**<br /><br /> **LAX_VALIDATION**<br /><br /> **SKIP_VALIDATION**|  
|**disallow_namespaces**|**bit**|0 = 枚举中的命名空间[sys.xml_schema_wildcard_namespaces](../../relational-databases/system-catalog-views/sys-xml-schema-wildcard-namespaces-transact-sql.md)是唯一允许的。<br /><br /> 1 = 只禁止命名空间。|  
  
## <a name="permissions"></a>权限  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)] 有关详细信息，请参阅 [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md)。  
  
## <a name="see-also"></a>请参阅  
 [目录视图 (Transact-SQL)](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)   
 [XML 架构&#40;XML 类型系统&#41;目录视图&#40;Transact SQL&#41;](../../relational-databases/system-catalog-views/xml-schemas-xml-type-system-catalog-views-transact-sql.md)  
  
  
