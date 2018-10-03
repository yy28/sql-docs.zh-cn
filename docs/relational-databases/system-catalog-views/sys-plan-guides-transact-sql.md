---
title: sys.plan_guides (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.planguides_TSQL
- plan_guides
- sys.planguides
- plan_guides_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.plan_guides catalog view
ms.assetid: 3dde0397-ef6f-4b3f-8250-3f25584eb62b
author: stevestein
ms.author: sstein
manager: craigg
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 75d95fbe9c289eab419360bef35263b41930c9f7
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/01/2018
ms.locfileid: "47696476"
---
# <a name="sysplanguides-transact-sql"></a>sys.plan_guides (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  数据库中的每个计划指南都在表中对应一行。  
  
|列名|数据类型|Description|  
|-----------------|---------------|-----------------|  
|**plan_guide_id**|**int**|数据库中计划指南的唯一标识符。|  
|**名称**|**sysname**|计划指南的名称。|  
|**create_date**|**datetime**|计划指南的创建日期和时间。|  
|**modify_date**|**日期时间**|上次修改计划指南的日期。|  
|**is_disabled**|**bit**|1 = 禁用计划指南。<br /><br /> 0 = 启用计划指南。|  
|**query_text**|**nvarchar(max)**|创建计划指南所依据的查询文本。|  
|**scope_type**|**tinyint**|标识计划指南的作用域。<br /><br /> 1 = OBJECT<br /><br /> 2 = SQL<br /><br /> 3 = TEMPLATE|  
|**scope_type_desc**|**nvarchar(60)**|计划指南作用域的说明。<br /><br /> OBJECT<br /><br /> SQL<br /><br /> TEMPLATE|  
|**scope_object_id**|**Int**|如果作用域为 OBJECT，则为定义计划指南作用域的对象的 object_id。<br /><br /> 如果计划指南的作用域不是 OBJECT，则其值为 NULL。|  
|**scope_batch**|**nvarchar(max)**|批处理文本，如果**scope_type**是 SQL。<br /><br /> 如果批处理类型不是 SQL，则其值为 NULL。<br /><br /> 如果为 NULL 并且**scope_type**是 SQL 的值**query_text**适用。|  
|**参数**|**nvarchar(max)**|定义与计划指南关联的参数列表的字符串。<br /><br /> NULL = 没有与计划指南关联的参数列表。|  
|**提示**|**nvarchar(max)**|与计划指南关联的 OPTION 子句提示。|  
  
## <a name="permissions"></a>Permissions  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)] 有关详细信息，请参阅 [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md)。  
  
## <a name="see-also"></a>请参阅  
 [目录视图 (Transact-SQL)](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)   
 [sp_create_plan_guide (Transact-SQL)](../../relational-databases/system-stored-procedures/sp-create-plan-guide-transact-sql.md)   
 [sp_create_plan_guide_from_handle (Transact-SQL)](../../relational-databases/system-stored-procedures/sp-create-plan-guide-from-handle-transact-sql.md)  
  
  
