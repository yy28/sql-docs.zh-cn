---
title: sys.triggers (TRANSACT-SQL) |Microsoft 文档
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.component: system-catalog-views
ms.reviewer: ''
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- triggers
- triggers_TSQL
- sys.triggers
- sys.triggers_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.triggers catalog view
ms.assetid: cefa4fc4-b8b9-4cd7-b124-eed5283acbfc
caps.latest.revision: 22
author: edmacauley
ms.author: edmaca
manager: craigg
monikerRange: = azuresqldb-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: 7c176e5cdf68b5aa9516cd054a57f36c630b0c64
ms.sourcegitcommit: f1caaa156db2b16e817e0a3884394e7b30fb642f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/04/2018
ms.locfileid: "33221778"
---
# <a name="systriggers-transact-sql"></a>sys.triggers (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  每个类型为 TR 或 TA 的触发器对象对应一行。 DML 触发器名称的架构范围并且，因此，在中可见**sys.objects**。 DDL 触发器名称的作用域取决于父实体，只能在此视图中显示。  
  
 **Parent_class**和**名称**列唯一标识数据库中的触发器。  
  
|列名|数据类型|Description|  
|-----------------|---------------|-----------------|  
|**名称**|**sysname**|触发器名称。 DML 触发器名称的架构范围。 DDL 触发器名称的作用域取决于父实体。|  
|**object_id**|**int**|对象标识号。 是一个数据库中唯一的。|  
|**parent_class**|**tinyint**|触发器的父类。<br /><br /> 0 = DDL 触发器的数据库。<br /><br /> 1 = DML 触发器的对象或列。|  
|**parent_class_desc**|**nvarchar(60)**|触发器的父类的说明。<br /><br /> DATABASE<br /><br /> OBJECT_OR_COLUMN|  
|**parent_id**|**int**|触发器的父实体的 ID，如下所示：<br /><br /> 0 = 父实体为数据库的触发器。<br /><br /> 对于 DML 触发器，这是**object_id**的表或在其定义的 DML 触发器的视图。|  
|**类型**|**char(2)**|对象类型：<br /><br /> TA = 程序集 (CLR) 触发器<br /><br /> TR = SQL 触发器|  
|**type_desc**|**nvarchar(60)**|对象类型的描述。<br /><br /> CLR_TRIGGER<br /><br /> SQL_TRIGGER|  
|**create_date**|**datetime**|触发器的创建日期。|  
|**modify_date**|**datetime**|通过使用 ALTER 语句上次修改对象的日期。|  
|**is_ms_shipped**|**bit**|由内部 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 组件代表用户创建的触发器。|  
|**is_disabled**|**bit**|触发器被禁用。|  
|**is_not_for_replication**|**bit**|触发器是作为 NOT FOR REPLICATION 创建的。|  
|**is_instead_of_trigger**|**bit**|1 = INSTEAD OF 触发器。<br /><br /> 0 = AFTER 触发器。|  
  
## <a name="permissions"></a>权限  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)] 有关详细信息，请参阅 [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md)。  
  
## <a name="see-also"></a>另请参阅  
 [安全性目录视图 (Transact-SQL)](../../relational-databases/system-catalog-views/security-catalog-views-transact-sql.md)   
 [目录视图 (Transact-SQL)](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)  
  
  
