---
title: IHarticles (Transact SQL) |Microsoft Docs
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- IHarticles
- IHarticles_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- IHarticles system table
ms.assetid: 773ef9b7-c993-4629-9516-70c47b9dcf65
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: cc1a800ff61bde8e4d446462143bf0d333a16fe7
ms.sourcegitcommit: ceb7e1b9e29e02bb0c6ca400a36e0fa9cf010fca
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/03/2018
ms.locfileid: "52802609"
---
# <a name="iharticles-transact-sql"></a>IHarticles (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  **IHarticles**系统表中占一行的每个项目正在复制从非 SQL Server 发布服务器使用当前分发服务器。 此表存储在分发数据库中。  
  
## <a name="definition"></a>定义  
  
|列名|数据类型|Description|  
|-----------------|---------------|-----------------|  
|**article_id**|**int**|为项目提供唯一 ID 号的标识列。|  
|**名称**|**sysname**|与项目关联的名称，在发布内是唯一的。|  
|**publication_id**|**smallint**|项目所属发布的 ID。|  
|**table_id**|**int**|从发布的表的 ID [IHpublishertables](../../relational-databases/system-tables/ihpublishertables-transact-sql.md)。|  
|**publisher_id**|**smallint**|非 SQL Server 发布服务器的 ID。|  
|**creation_script**|**nvarchar(255)**|项目的架构脚本。|  
|**del_cmd**|**nvarchar(255)**|复制对表项目的删除操作时所使用的复制命令类型。 有关详细信息，请参阅[指定如何传播事务项目的更改](../../relational-databases/replication/transactional/transactional-articles-specify-how-changes-are-propagated.md)。|  
|**filter**|**int**|此列未使用，包括只是为了[sysarticles](../../relational-databases/system-views/sysarticles-system-view-transact-sql.md)视图**IHarticles**表与兼容[sysarticles](../../relational-databases/system-views/sysarticles-system-view-transact-sql.md)用于 SQL Server 的文章 （视图[sysarticles](../../relational-databases/system-tables/sysarticles-transact-sql.md))。|  
|**filter_clause**|**ntext**|项目的 WHERE 子句，用于水平筛选并以非 SQL 发布服务器可以解释的标准 Transact-SQL 编写。|  
|**ins_cmd**|**nvarchar(255)**|复制对表项目的插入操作时所使用的复制命令类型。 有关详细信息，请参阅[指定如何传播事务项目的更改](../../relational-databases/replication/transactional/transactional-articles-specify-how-changes-are-propagated.md)。|  
|**pre_creation_cmd**|**tinyint**|当订阅服务器中已经存在同名对象时，将应用在初始快照之前执行的命令。<br /><br /> **0** = 无-不执行命令。<br /><br /> **1** = 除去-除去目标表。<br /><br /> **2** = 删除-删除目标表中的数据。<br /><br /> **3** = 截断-截断目标表。|  
|**status**|**tinyint**|项目选项和状态的位掩码，可以是对以下一个或多个值执行逻辑位或运算的结果：<br /><br /> **0** = 没有附加属性。<br /><br /> **1** = 活动。<br /><br /> **8** = 包括 INSERT 语句中的列名称。<br /><br /> **16** = 使用参数化语句。<br /><br /> 例如，使用参数化语句的活动项目在此列中的值为 17。 如果值为 0，则表示项目处于非活动状态，而且未定义其他属性。|  
|**类型**|**tinyint**|项目的类型：<br /><br /> **1** = 基于日志的项目。|  
|**upd_cmd**|**nvarchar(255)**|复制对表项目的更新操作时所使用的复制命令类型。 有关详细信息，请参阅[指定如何传播事务项目的更改](../../relational-databases/replication/transactional/transactional-articles-specify-how-changes-are-propagated.md)。|  
|**schema_option**|**binary(8)**|给定项目的架构生成选项的位图，它可以是下面的一个或多个值的位逻辑或结果：<br /><br /> **0x00** = 禁用快照代理编写脚本，并使用提供的 CreationScript。<br /><br /> **0x01** = 生成对象创建 （CREATE TABLE、 CREATE PROCEDURE 等）。<br /><br /> **0x10** = 生成相应的聚集索引。<br /><br /> **0x40** = 生成相应的非聚集索引。<br /><br /> **0x80** = 包括声明引用完整性在主键上。<br /><br /> **0x1000** = 复制列级排序规则。 注意：默认情况下，将为 Oracle 发布服务器设置该选项，以启用区分大小写的比较。<br /><br /> **0x4000** = 复制唯一键，如果对表项目定义。<br /><br /> **0x8000** = 的复制 primary key 和上一个表的唯一键作为约束使用 ALTER TABLE 语句的文章。|  
|**dest_owner**|**sysname**|目标数据库中表的所有者。|  
|**dest_table**|**sysname**|目标表的名称。|  
|**tablespace_name**|**nvarchar(255)**|标识项目的日志记录表使用的表空间。|  
|**objid**|**int**|此列未使用，包括只是为了[sysarticles](../../relational-databases/system-views/sysarticles-system-view-transact-sql.md)视图**IHarticles**表与兼容[sysarticles](../../relational-databases/system-views/sysarticles-system-view-transact-sql.md)用于 SQL Server 的文章 （视图[sysarticles](../../relational-databases/system-tables/sysarticles-transact-sql.md))。|  
|**sync_objid**|**int**|此列未使用，包括只是为了[sysarticles](../../relational-databases/system-views/sysarticles-system-view-transact-sql.md)视图**IHarticles**表与兼容[sysarticles](../../relational-databases/system-views/sysarticles-system-view-transact-sql.md)用于 SQL Server 的文章 （视图[sysarticles](../../relational-databases/system-tables/sysarticles-transact-sql.md))。|  
|**description**|**nvarchar(255)**|本文说明项。|  
|**publisher_status**|**int**|用于指示是否已通过调用定义用于定义已发布的项目的视图[sp_articleview](../../relational-databases/system-stored-procedures/sp-articleview-transact-sql.md)。<br /><br /> **0** = [sp_articleview](../../relational-databases/system-stored-procedures/sp-articleview-transact-sql.md)已调用。<br /><br /> **1** = [sp_articleview](../../relational-databases/system-stored-procedures/sp-articleview-transact-sql.md)尚未调用。|  
|**article_view_owner**|**nvarchar(255)**|发布服务器上由日志读取器代理使用的同步对象的所有者。|  
|**article_view**|**nvarchar(255)**|发布服务器上由日志读取器代理使用的同步对象。|  
|**ins_scripting_proc**|**int**|此列未使用，包括只是为了[sysarticles](../../relational-databases/system-views/sysarticles-system-view-transact-sql.md)视图**IHarticles**表与兼容[sysarticles](../../relational-databases/system-views/sysarticles-system-view-transact-sql.md)用于 SQL Server 的文章 （视图[sysarticles](../../relational-databases/system-tables/sysarticles-transact-sql.md))。|  
|**del_scripting_proc**|**int**|此列未使用，包括只是为了[sysarticles](../../relational-databases/system-views/sysarticles-system-view-transact-sql.md)视图**IHarticles**表与兼容[sysarticles](../../relational-databases/system-views/sysarticles-system-view-transact-sql.md)用于 SQL Server 的文章 （视图[sysarticles](../../relational-databases/system-tables/sysarticles-transact-sql.md))。|  
|**upd_scripting_proc**|**int**|此列未使用，包括只是为了[sysarticles](../../relational-databases/system-views/sysarticles-system-view-transact-sql.md)视图**IHarticles**表与兼容[sysarticles](../../relational-databases/system-views/sysarticles-system-view-transact-sql.md)用于 SQL Server 的文章 （视图[sysarticles](../../relational-databases/system-tables/sysarticles-transact-sql.md))。|  
|**custom_script**|**int**|此列未使用，包括只是为了[sysarticles](../../relational-databases/system-views/sysarticles-system-view-transact-sql.md)视图**IHarticles**表与兼容[sysarticles](../../relational-databases/system-views/sysarticles-system-view-transact-sql.md)用于 SQL Server 的文章 （视图[sysarticles](../../relational-databases/system-tables/sysarticles-transact-sql.md))。|  
|**fire_triggers_on_snapshot**|**bit**|此列未使用，包括只是为了[sysarticles](../../relational-databases/system-views/sysarticles-system-view-transact-sql.md)视图**IHarticles**表与兼容[sysarticles](../../relational-databases/system-views/sysarticles-system-view-transact-sql.md)用于 SQL Server 的文章 （视图[sysarticles](../../relational-databases/system-tables/sysarticles-transact-sql.md))。|  
|**instance_id**|**int**|标识已发布表的项目日志的当前实例。|  
|**use_default_datatypes**|**bit**|指示项目是否使用默认数据类型映射;值为**1**表示使用默认数据类型映射。|  
  
## <a name="see-also"></a>请参阅  
 [异类数据库复制](../../relational-databases/replication/non-sql/heterogeneous-database-replication.md)   
 [复制表&#40;Transact SQL&#41;](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [复制视图&#40;Transact SQL&#41;](../../relational-databases/system-views/replication-views-transact-sql.md)   
 [sp_addarticle &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addarticle-transact-sql.md)   
 [sp_changearticle &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-changearticle-transact-sql.md)  
  
  
