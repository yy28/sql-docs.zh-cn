---
title: "sys.all_objects (Transact SQL) |Microsoft 文档"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: system-catalog-views
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- sys.all_objects
- all_objects_TSQL
- all_objects
- sys.all_objects_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.all_objects catalog view
ms.assetid: 547e4be4-a8e4-48ce-9d8d-37b169985081
caps.latest.revision: 
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: fd8082ebb9b69aec413209096775d0d3c565f837
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/21/2017
---
# <a name="sysallobjects-transact-sql"></a>sys.all_objects (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  显示所有架构范围内的用户定义对象和系统对象的 UNION。  
  
|列名|数据类型|说明|  
|-----------------|---------------|-----------------|  
|name|**sysname**|对象名。|  
|object_id|**int**|对象标识号。 是一个数据库中唯一的。|  
|principal_id|**int**|如果不是架构所有者，则为特定所有者的 ID。 默认情况下，架构包含的对象由架构所有者拥有。 不过，通过使用 ALTER AUTHORIZATION 语句更改所有权可以指定其他所有者。<br /><br /> 如果没有可代替的单个所有者，则为 NULL。<br /><br /> 如果对象类型为下列类型之一，则为 NULL：<br /><br /> C = CHECK 约束<br /><br /> D = DEFAULT（约束或独立）<br /><br /> F = FOREIGN KEY 约束<br /><br /> PK = PRIMARY KEY 约束<br /><br /> R = 规则（旧式，独立）<br /><br /> TA = 程序集 (CLR) 触发器<br /><br /> TR = SQL 触发器<br /><br /> UQ = UNIQUE 约束|  
|schema_id|**int**|包含对象的架构的 ID。<br /><br /> 对于 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 所附带的所有以架构为作用域的系统对象，该值始终在 (schema_id('sys'), schema_id('INFORMATION_SCHEMA')) 中。|  
|parent_object_id|**int**|此对象所属对象的 ID。<br /><br /> 0 = 不是子对象。|  
|类型|**char(2)**|对象类型：<br /><br /> AF = 聚合函数 (CLR)<br /><br /> C = CHECK 约束<br /><br /> D = DEFAULT（约束或独立）<br /><br /> F = FOREIGN KEY 约束<br /><br /> FN = SQL 标量函数<br /><br /> FS = 程序集 (CLR) 标量函数<br /><br /> FT = 程序集 (CLR) 表值函数<br /><br /> IF = SQL 内联表值函数<br /><br /> IT = 内部表<br /><br /> P = SQL 存储过程<br /><br /> PC = 程序集 (CLR) 存储过程<br /><br /> PG = 计划指南<br /><br /> PK = PRIMARY KEY 约束<br /><br /> R = 规则（旧式，独立）<br /><br /> RF = 复制筛选过程<br /><br /> S = 系统基表<br /><br /> SN = 同义词<br /><br /> SQ = 服务队列<br /><br /> TA = 程序集 (CLR) DML 触发器<br /><br /> TF = SQL 表值函数<br /><br /> TR = SQL DML 触发器<br /><br /> TT = 表类型<br /><br /> U = 表（用户定义类型）<br /><br /> UQ = UNIQUE 约束<br /><br /> V = 视图<br /><br /> X = 扩展存储过程|  
|type_desc|**nvarchar(60)**|对象类型的说明。 AGGREGATE_FUNCTION<br /><br /> CHECK_CONSTRAINT<br /><br /> DEFAULT_CONSTRAINT<br /><br /> FOREIGN_KEY_CONSTRAINT<br /><br /> SQL_SCALAR_FUNCTION<br /><br /> CLR_SCALAR_FUNCTION<br /><br /> CLR_TABLE_VALUED_FUNCTION<br /><br /> SQL_INLINE_TABLE_VALUED_FUNCTION<br /><br /> INTERNAL_TABLE<br /><br /> SQL_STORED_PROCEDURE<br /><br /> CLR_STORED_PROCEDURE<br /><br /> PLAN_GUIDE<br /><br /> PRIMARY_KEY_CONSTRAINT<br /><br /> RULE<br /><br /> REPLICATION_FILTER_PROCEDURE<br /><br /> SYSTEM_TABLE<br /><br /> SYNONYM<br /><br /> SERVICE_QUEUE<br /><br /> CLR_TRIGGER<br /><br /> SQL_TABLE_VALUED_FUNCTION<br /><br /> SQL_TRIGGER<br /><br /> TABLE_TYPE<br /><br /> USER_TABLE<br /><br /> UNIQUE_CONSTRAINT<br /><br /> VIEW<br /><br /> EXTENDED_STORED_PROCEDURE|  
|create_date|**datetime**|对象的创建日期。|  
|modify_date|**datetime**|通过使用 ALTER 语句上次修改对象的日期。 如果对象是表或视图，则创建或修改表或视图的聚集索引时，modify_date 也会更改。|  
|is_ms_shipped|**bit**|内部 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 组件所创建的对象。|  
|is_published|**bit**|对象为发布对象。|  
|is_schema_published|**bit**|仅发布对象的架构。|  
  
## <a name="permissions"></a>Permissions  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)] 有关详细信息，请参阅 [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md)。  
  
## <a name="see-also"></a>另请参阅  
 [对象目录视图 &#40;Transact SQL &#41;](../../relational-databases/system-catalog-views/object-catalog-views-transact-sql.md)   
 [目录视图 (Transact-SQL)](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)   
 [sys.objects &#40;Transact SQL &#41;](../../relational-databases/system-catalog-views/sys-objects-transact-sql.md)   
 [sys.system_objects &#40;Transact SQL &#41;](../../relational-databases/system-catalog-views/sys-system-objects-transact-sql.md)  
  
  
