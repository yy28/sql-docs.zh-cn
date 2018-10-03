---
title: sysextendedarticlesview (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology:
- replication
ms.topic: language-reference
f1_keywords:
- sysextendedarticlesview_TSQL
- sysextendedarticlesview
dev_langs:
- TSQL
helpviewer_keywords:
- sysextendedarticlesview view
ms.assetid: 8bdd22f7-c268-49b6-820c-3fe603feb128
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: fe6c88ac0dc8b131323282478a2330525d0fcf9b
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/01/2018
ms.locfileid: "47648185"
---
# <a name="sysextendedarticlesview-transact-sql"></a>sysextendedarticlesview (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  **Sysextendedarticlesview**视图提供已发布项目的相关信息。 此视图存储在分发数据库中。  
  
|列名|数据类型|Description|  
|-----------------|---------------|-----------------|  
|**artid**|**int**|为项目提供唯一 ID 号的标识列。|  
|**creation_script**|**nvarchar(255)**|项目的架构创建脚本。|  
|**del_cmd**|**nvarchar(255)**|在 DELETE 时所执行的命令；否则根据日志构造。|  
|**description**|**nvarchar(255)**|本文说明项。|  
|**dest_table**|**nvarchar(128)**|目标表的名称。|  
|**filter**|**int**|用于水平分区的存储过程的对象标识符。|  
|**filter_clause**|**ntext**|项目的 WHERE 子句，用于水平筛选。|  
|**ins_cmd**|**nvarchar(255)**|要对 INSERT 执行的命令。|  
|**名称**|**nvarchar(128)**|与项目关联的名称，在发布内是唯一的。|  
|**objid**|**int**|已发布的表对象 ID。|  
|**pubid**|**int**|项目所属发布的 ID。|  
|**pre_creation_cmd**|**tinyint**|DROP TABLE、DELETE TABLE 或 TRUNCATE 的预创建命令：<br /><br /> **0** = none。<br /><br /> **1** = DROP。<br /><br /> **2** = DELETE。<br /><br /> **3** = 截断。|  
|**status**|**int**|项目选项和状态的位掩码，可以是对以下一个或多个值执行逻辑位或运算的结果：<br /><br /> **1** = 项目处于活动状态。<br /><br /> **8** = 包括 INSERT 语句中的列名称。<br /><br /> **16** = 使用参数化语句。<br /><br /> **24** = 同时在 INSERT 语句中包括的列名称并使用参数化的语句。<br /><br /> 例如，使用参数化语句的活动项目在此列中的值为 17。 如果值为 0，则表示项目处于非活动状态，而且未定义其他属性。|  
|**sync_objid**|**int**|表示项目定义的表或视图的 ID。|  
|**类型**|**tinyint**|项目的类型：<br /><br /> **1** = 基于日志的项目。<br /><br /> **3** = 具有手动筛选器基于日志的项目。<br /><br /> **5** = 具有手动视图并且基于日志的项目。<br /><br /> **7** = 具有手动筛选器和手动视图并且基于日志的项目。|  
|**upd_cmd**|**nvarchar(255)**|在 UPDATE 时执行的命令；否则根据日志构造。|  
|**schema_option**|**binary**|指示在快照中编写已发布对象的哪些属性的脚本。 有关支持的架构选项的列表，请参阅[sp_addarticle](../../relational-databases/system-stored-procedures/sp-addarticle-transact-sql.md)。|  
|**dest_owner**|**nvarchar(128)**|目标数据库中表的所有者。|  
|**ins_scripting_proc**|**int**|复制 INSERT 语句时执行的自定义存储过程或脚本的对象标识符。|  
|**del_scripting_proc**|**int**|复制 DELETE 语句时执行的自定义存储过程或脚本的对象标识符。|  
|**upd_scripting_proc**|**int**|复制 UPDATE 语句时执行的自定义存储过程或脚本的对象标识符。|  
|**custom_script**|**int**|DDL 触发器完成时执行的自定义脚本或过程的对象标识符。|  
|**fire_triggers_on_snapshot**|**int**|指示在应用快照时是否执行所复制的触发器，可以为下列值之一：<br /><br /> **0** = 不执行触发器。<br /><br /> **1** = 执行触发器。|  
  
## <a name="see-also"></a>请参阅  
 [复制表&#40;Transact SQL&#41;](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [复制视图&#40;Transact SQL&#41;](../../relational-databases/system-views/replication-views-transact-sql.md)   
 [sp_addarticle &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addarticle-transact-sql.md)   
 [sp_changearticle (Transact-SQL)](../../relational-databases/system-stored-procedures/sp-changearticle-transact-sql.md)   
 [sp_helparticle (Transact-SQL)](../../relational-databases/system-stored-procedures/sp-helparticle-transact-sql.md)   
 [sysarticles &#40;TRANSACT-SQL&#41;](../../relational-databases/system-tables/sysarticles-transact-sql.md)  
  
  
