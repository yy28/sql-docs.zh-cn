---
title: IHarticles (Transact SQL) |Microsoft 文档
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: system-tables
ms.reviewer: ''
ms.suite: sql
ms.technology:
- replication
ms.tgt_pltfrm: ''
ms.topic: language-reference
applies_to:
- SQL Server
f1_keywords:
- IHarticles
- IHarticles_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- IHarticles system table
ms.assetid: 773ef9b7-c993-4629-9516-70c47b9dcf65
caps.latest.revision: 27
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 2f6d2f9b3bba59f44246d60cd35cdea8d8706989
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/16/2018
---
# <a name="iharticles-transact-sql"></a>IHarticles (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  **IHarticles**系统表包含每个项目正在复制从非 SQL Server 发布服务器使用当前分发服务器的一行。 此表存储在分发数据库中。  
  
## <a name="definition"></a>定义  
  
|列名|数据类型|Description|  
|-----------------|---------------|-----------------|  
|**article_id**|**int**|为项目提供唯一 ID 号的标识列。|  
|**名称**|**sysname**|与项目关联的名称，在发布内是唯一的。|  
|**publication_id**|**int**|项目所属发布的 ID。|  
|**table_id**|**int**|正在从发布表的 ID [IHpublishertables](../../relational-databases/system-tables/ihpublishertables-transact-sql.md)。|  
|**publisher_id**|**int**|非 SQL Server 发布服务器的 ID。|  
|**creation_script**|**nvarchar(255)**|项目的架构脚本。|  
|**del_cmd**|**nvarchar(255)**|复制对表项目的删除操作时所使用的复制命令类型。 有关详细信息，请参阅[指定如何传播事务项目的更改](../../relational-databases/replication/transactional/transactional-articles-specify-how-changes-are-propagated.md)。|  
|**filter**|**int**|此列未使用，包括只是为了使[sysarticles](../../relational-databases/system-views/sysarticles-system-view-transact-sql.md)视图**IHarticles**表与兼容[sysarticles](../../relational-databases/system-views/sysarticles-system-view-transact-sql.md)用于 SQL Server 文章 （视图[sysarticles](../../relational-databases/system-tables/sysarticles-transact-sql.md))。|  
|**filter_clause**|**ntext**|项目的 WHERE 子句，用于水平筛选并以非 SQL 发布服务器可以解释的标准 Transact-SQL 编写。|  
|**ins_cmd**|**nvarchar(255)**|复制对表项目的插入操作时所使用的复制命令类型。 有关详细信息，请参阅[指定如何传播事务项目的更改](../../relational-databases/replication/transactional/transactional-articles-specify-how-changes-are-propagated.md)。|  
|**pre_creation_cmd**|**tinyint**|当订阅服务器中已经存在同名对象时，将应用在初始快照之前执行的命令。<br /><br /> **0** = none-不执行命令。<br /><br /> **1** = DROP-删除目标表。<br /><br /> **2** = DELETE-删除表中数据的目标。<br /><br /> **3** = TRUNCATE-截断目标表。|  
|**status**|**tinyint**|项目选项和状态的位掩码，可以是对以下一个或多个值执行逻辑位或运算的结果：<br /><br /> **0** = 任何其他属性。<br /><br /> **1** = 活动。<br /><br /> **8** = 包括 INSERT 语句中的列名称。<br /><br /> **16** = 使用参数化语句。<br /><br /> 例如，使用参数化语句的活动项目在此列中的值为 17。 如果值为 0，则表示项目处于非活动状态，而且未定义其他属性。|  
|**类型**|**tinyint**|项目的类型：<br /><br /> **1** = 基于日志的文章。|  
|**upd_cmd**|**nvarchar(255)**|复制对表项目的更新操作时所使用的复制命令类型。 有关详细信息，请参阅[指定如何传播事务项目的更改](../../relational-databases/replication/transactional/transactional-articles-specify-how-changes-are-propagated.md)。|  
|**schema_option**|**binary(8)**|给定项目的架构生成选项的位图，它可以是下面的一个或多个值的位逻辑或结果：<br /><br /> **0x00** = 禁用脚本由快照代理，并使用提供的创建脚本。<br /><br /> **0x01** = 生成对象创建 （CREATE TABLE 和 CREATE PROCEDURE 等）。<br /><br /> **0x10** = 生成相应的聚集索引。<br /><br /> **0x40** = 生成相应的非聚集索引。<br /><br /> **0x80** = 包括的主键上声明引用完整性。<br /><br /> **0x1000** = 均会复制列级排序规则。 注意： 此选项是默认情况下，Oracle 发布服务器启用区分大小写的比较的设置。<br /><br /> **0x4000** = 复制的唯一键，如果在表项目上定义。<br /><br /> **0x8000** = 的复制主键和唯一键的表项目作为约束使用 ALTER TABLE 语句。|  
|**dest_owner**|**sysname**|目标数据库中表的所有者。|  
|**dest_table**|**sysname**|目标表的名称。|  
|**tablespace_name**|**nvarchar(255)**|标识项目的日志记录表使用的表空间。|  
|**objid**|**int**|此列未使用，包括只是为了使[sysarticles](../../relational-databases/system-views/sysarticles-system-view-transact-sql.md)视图**IHarticles**表与兼容[sysarticles](../../relational-databases/system-views/sysarticles-system-view-transact-sql.md)用于 SQL Server 文章 （视图[sysarticles](../../relational-databases/system-tables/sysarticles-transact-sql.md))。|  
|**sync_objid**|**int**|此列未使用，包括只是为了使[sysarticles](../../relational-databases/system-views/sysarticles-system-view-transact-sql.md)视图**IHarticles**表与兼容[sysarticles](../../relational-databases/system-views/sysarticles-system-view-transact-sql.md)用于 SQL Server 文章 （视图[sysarticles](../../relational-databases/system-tables/sysarticles-transact-sql.md))。|  
|**说明**|**nvarchar(255)**|本文描述项。|  
|**publisher_status**|**int**|用于指示是否已通过调用定义的视图的定义已发布的文章[sp_articleview](../../relational-databases/system-stored-procedures/sp-articleview-transact-sql.md)。<br /><br /> **0** = [sp_articleview](../../relational-databases/system-stored-procedures/sp-articleview-transact-sql.md)已调用。<br /><br /> **1** = [sp_articleview](../../relational-databases/system-stored-procedures/sp-articleview-transact-sql.md)尚未调用。|  
|**article_view_owner**|**nvarchar(255)**|发布服务器上由日志读取器代理使用的同步对象的所有者。|  
|**article_view**|**nvarchar(255)**|发布服务器上由日志读取器代理使用的同步对象。|  
|**ins_scripting_proc**|**int**|此列未使用，包括只是为了使[sysarticles](../../relational-databases/system-views/sysarticles-system-view-transact-sql.md)视图**IHarticles**表与兼容[sysarticles](../../relational-databases/system-views/sysarticles-system-view-transact-sql.md)用于 SQL Server 文章 （视图[sysarticles](../../relational-databases/system-tables/sysarticles-transact-sql.md))。|  
|**del_scripting_proc**|**int**|此列未使用，包括只是为了使[sysarticles](../../relational-databases/system-views/sysarticles-system-view-transact-sql.md)视图**IHarticles**表与兼容[sysarticles](../../relational-databases/system-views/sysarticles-system-view-transact-sql.md)用于 SQL Server 文章 （视图[sysarticles](../../relational-databases/system-tables/sysarticles-transact-sql.md))。|  
|**upd_scripting_proc**|**int**|此列未使用，包括只是为了使[sysarticles](../../relational-databases/system-views/sysarticles-system-view-transact-sql.md)视图**IHarticles**表与兼容[sysarticles](../../relational-databases/system-views/sysarticles-system-view-transact-sql.md)用于 SQL Server 文章 （视图[sysarticles](../../relational-databases/system-tables/sysarticles-transact-sql.md))。|  
|**custom_script**|**int**|此列未使用，包括只是为了使[sysarticles](../../relational-databases/system-views/sysarticles-system-view-transact-sql.md)视图**IHarticles**表与兼容[sysarticles](../../relational-databases/system-views/sysarticles-system-view-transact-sql.md)用于 SQL Server 文章 （视图[sysarticles](../../relational-databases/system-tables/sysarticles-transact-sql.md))。|  
|**fire_triggers_on_snapshot**|**bit**|此列未使用，包括只是为了使[sysarticles](../../relational-databases/system-views/sysarticles-system-view-transact-sql.md)视图**IHarticles**表与兼容[sysarticles](../../relational-databases/system-views/sysarticles-system-view-transact-sql.md)用于 SQL Server 文章 （视图[sysarticles](../../relational-databases/system-tables/sysarticles-transact-sql.md))。|  
|**instance_id**|**int**|标识已发布表的项目日志的当前实例。|  
|**use_default_datatypes**|**bit**|指示是否文章将使用默认数据类型映射;值为**1**表示使用默认数据类型映射。|  
  
## <a name="see-also"></a>另请参阅  
 [异类数据库复制](../../relational-databases/replication/non-sql/heterogeneous-database-replication.md)   
 [复制表&#40;Transact SQL&#41;](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [复制视图&#40;Transact SQL&#41;](../../relational-databases/system-views/replication-views-transact-sql.md)   
 [sp_addarticle &#40;Transact SQL&#41;](../../relational-databases/system-stored-procedures/sp-addarticle-transact-sql.md)   
 [sp_changearticle &#40;Transact SQL&#41;](../../relational-databases/system-stored-procedures/sp-changearticle-transact-sql.md)  
  
  
