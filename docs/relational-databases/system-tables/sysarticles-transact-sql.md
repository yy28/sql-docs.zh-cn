---
title: "sysarticles (Transact SQL) |Microsoft 文档"
ms.custom: 
ms.date: 03/03/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: system-tables
ms.reviewer: 
ms.suite: sql
ms.technology: replication
ms.tgt_pltfrm: 
ms.topic: language-reference
applies_to: SQL Server
f1_keywords:
- sysarticles
- sysarticles_TSQL
dev_langs: TSQL
helpviewer_keywords: sysarticles system table
ms.assetid: 9d9d5d51-6d8f-4e42-84a9-82e58eb0301e
caps.latest.revision: "30"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 2ce368158e29c1ba76442e38d374a5ddd615f75f
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/21/2017
---
# <a name="sysarticles-transact-sql"></a>sysarticles (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  本地数据库中定义的每个项目在表中各占一行。 该表存储在已发布的数据库中。  
  
|列名|数据类型|Description|  
|-----------------|---------------|-----------------|  
|**artid**|**int**|为项目提供唯一 ID 号的标识列。|  
|**creation_script**|**nvarchar(255)**|项目的架构脚本。|  
|**del_cmd**|**nvarchar(255)**|复制对表项目的删除操作时所使用的复制命令类型。 有关详细信息，请参阅[指定如何传播事务项目的更改](../../relational-databases/replication/transactional/transactional-articles-specify-how-changes-are-propagated.md)。|  
|**说明**|**nvarchar(255)**|本文描述项。|  
|**dest_table**|**sysname**|目标表的名称。|  
|**filter**|**int**|存储过程 ID，用于水平分区。|  
|**filter_clause**|**ntext**|项目的 WHERE 子句，用于水平筛选。|  
|**ins_cmd**|**nvarchar(255)**|复制对表项目的插入操作时所使用的复制命令类型。 有关详细信息，请参阅[指定如何传播事务项目的更改](../../relational-databases/replication/transactional/transactional-articles-specify-how-changes-are-propagated.md)。|  
|**名称**|**sysname**|与项目关联的名称，在发布内是唯一的。|  
|**objid**|**int**|已发布的表对象 ID。|  
|**pubid**|**int**|项目所属发布的 ID。|  
|**pre_creation_cmd**|**tinyint**|DROP TABLE、DELETE TABLE 或 TRUNCATE 的预创建命令：<br /><br /> **0** = none。<br /><br /> **1** = DROP。<br /><br /> **2** = DELETE。<br /><br /> **3** = TRUNCATE。|  
|**status**|**tinyint**|项目选项和状态的位掩码，可以是对以下一个或多个值执行逻辑位或运算的结果：<br /><br /> **1** = 文章处于活动状态。<br /><br /> **8** = 包括 INSERT 语句中的列名称。<br /><br /> **16** = 使用参数化语句。<br /><br /> **24** = 这两在 INSERT 语句中包括的列名称并使用参数化的语句。<br /><br /> **64** = [!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]<br /><br /> 例如，使用参数化的语句的活动项目将具有值为**17**此列中。 值为**0**意味着文章处于非活动状态并且未定义任何其他属性。|  
|**sync_objid**|**int**|表示项目定义的表或视图的 ID。|  
|**type**|**tinyint**|项目的类型：<br /><br /> **1** = 基于日志的文章。<br /><br /> **3**带手工筛选 = 基于日志的文章。<br /><br /> **5** = 与手动视图基于日志的文章。<br /><br /> **7** = 具有手工筛选和手动视图基于日志的项目。<br /><br /> **8** = 存储过程执行。<br /><br /> **24** = 可序列化的存储的过程执行。<br /><br /> **32** = 存储过程 （仅限架构）。<br /><br /> **64** = 视图 （仅限架构）。<br /><br /> **128** = 函数 （仅限架构）。|  
|**upd_cmd**|**nvarchar(255)**|复制对表项目的更新操作时所使用的复制命令类型。 有关详细信息，请参阅[指定如何传播事务项目的更改](../../relational-databases/replication/transactional/transactional-articles-specify-how-changes-are-propagated.md)。|  
|**schema_option**|**binary （8)**|项目的架构生成选项的位掩码，这些选项用于控制项目架构的哪些部分可以进行脚本处理，以便传递给订阅服务器。 有关架构选项的详细信息，请参阅 [sp_addarticle (Transact-SQL)](../../relational-databases/system-stored-procedures/sp-addarticle-transact-sql.md)。|  
|**dest_owner**|**sysname**|目标数据库中表的所有者。|  
|**ins_scripting_proc**|**int**|复制 INSERT 语句时执行的已注册自定义存储过程或脚本。|  
|**del_scripting_proc**|**int**|复制 DELETE 语句时执行的已注册自定义存储过程或脚本。|  
|**upd_scripting_proc**|**int**|复制 UPDATE 语句时执行的已注册自定义存储过程或脚本。|  
|**custom_script**|**nvarchar(2048)**|在 DDL 触发器的末尾执行的已注册自定义存储过程或脚本。|  
|**fire_triggers_on_snapshot**|**bit**|指示在应用快照时是否执行已复制的触发器，可以是以下值之一：<br /><br /> **0** = 触发器不会执行。<br /><br /> **1** = 触发器将执行。|  
  
## <a name="see-also"></a>另请参阅  
 [复制表 &#40;Transact SQL &#41;](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [复制视图 &#40;Transact SQL &#41;](../../relational-databases/system-views/replication-views-transact-sql.md)   
 [sp_addarticle &#40;Transact SQL &#41;](../../relational-databases/system-stored-procedures/sp-addarticle-transact-sql.md)   
 [sp_changearticle (Transact-SQL)](../../relational-databases/system-stored-procedures/sp-changearticle-transact-sql.md)   
 [sp_helparticle &#40;Transact SQL &#41;](../../relational-databases/system-stored-procedures/sp-helparticle-transact-sql.md)  
  
  
