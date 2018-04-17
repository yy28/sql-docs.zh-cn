---
title: sysmergeschemaarticles (Transact SQL) |Microsoft 文档
ms.custom: ''
ms.date: 03/04/2017
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
- sysmergeschemaarticles_TSQL
- sysmergeschemaarticles
dev_langs:
- TSQL
helpviewer_keywords:
- sysmergeschemaarticles system table
ms.assetid: b5085979-2f76-48e1-bf3b-765a84003dd9
caps.latest.revision: 27
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: be0e14898e488592e8c0dcdbf40b53b6e678a6a2
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/16/2018
---
# <a name="sysmergeschemaarticles-transact-sql"></a>sysmergeschemaarticles (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  跟踪合并复制的仅限架构的项目。 此表存储在发布和订阅数据库中。  
  
|列名|数据类型|Description|  
|-----------------|---------------|-----------------|  
|**名称**|**sysname**|合并复制中仅限架构的项目的名称。|  
|**类型**|**tinyint**|指示仅限架构的项目的类型，可以是以下类型之一：<br /><br /> **0x20** = 存储过程仅限于架构的项目。<br /><br /> **0x40** = 视图仅有架构的项目或索引的视图仅有架构的项目。|  
|**objid**|**int**|项目基对象的对象标识符。 可以是过程、视图、索引视图或用户定义函数的对象标识符。|  
|**artid**|**uniqueidentifier**|文章 id。|  
|**说明**|**nvarchar(255)**|项目的说明。|  
|**pre_creation_command**|**tinyint**|在订阅数据库中创建项目时采取的默认操作：<br /><br /> **0 =**无-如果该表已存在于订阅服务器，不执行任何操作。<br /><br /> **1** = drop-删除表，然后再重新创建它。<br /><br /> **2** = delete-发出删除基于子集筛选器中的 WHERE 子句。<br /><br /> **3** = Truncate-相同**2**，但删除了而不是行的页。 不过，不要使用 WHERE 子句。|  
|**pubid**|**uniqueidentifier**|发布唯一标识符。|  
|**status**|**tinyint**|指示仅限架构的项目的状态，可以是以下状态之一：<br /><br /> **1** = Unsynced-用于发布运行快照代理的下一步时间的表运行的初始处理脚本。<br /><br /> **2** = 活动-用于发布的表的初始处理脚本已运行。<br /><br /> **5** = New_inactive-要添加。<br /><br /> **6** = New_active-要添加。|  
|**creation_script**|**nvarchar(255)**|用于创建目标表的可选项目架构预创建脚本的路径和名称。|  
|**schema_option**|**binary(8)**|给定的仅限架构的项目的架构生成选项的位图，它可以是以下一个或多个值的按位逻辑或结果：<br /><br /> **0x00** = 禁用脚本由快照代理，并使用提供的创建脚本。<br /><br /> **0x01** = 生成对象创建 （CREATE TABLE 和 CREATE PROCEDURE 等）。<br /><br /> **0x10** = 生成相应的聚集索引。<br /><br /> **0x20** = 转换用户定义数据类型转换为基本数据类型。<br /><br /> **0x40** = 生成相应的非聚集索引。<br /><br /> **0x80** = 包括的主键上声明引用完整性。<br /><br /> **0x100** = 上表项目，复制用户触发器，如果定义。<br /><br /> **0x200** = 复制外键约束。 如果被所引用的表不是发布的一部分，则不会复制已发布表的任何外键约束。<br /><br /> **0x400** = 复制 check 约束。<br /><br /> **0x800** = 复制的默认值。<br /><br /> **0x1000** = 复制列级排序规则。<br /><br /> **0x2000** = 复制扩展与已发布的文章源对象相关联的属性。<br /><br /> **0x4000** = 复制的唯一键，如果在表项目上定义。<br /><br /> **0x8000** = 的复制主键和唯一键的表项目作为约束使用 ALTER TABLE 语句。<br /><br /> 有关详细信息的可能值**schema_option**，请参阅[sp_addmergearticle](../../relational-databases/system-stored-procedures/sp-addmergearticle-transact-sql.md)。|  
|**destination_object**|**sysname**|订阅数据库中的目标对象名称。 该值仅应用于仅限架构的项目，例如，存储过程、视图和 UDF。|  
|**destination_owner**|**sysname**|在订阅数据库中，如果不是对象的所有者**dbo**。|  
  
## <a name="see-also"></a>另请参阅  
 [复制表&#40;Transact SQL&#41;](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [复制视图 (Transact-SQL)](../../relational-databases/system-views/replication-views-transact-sql.md)  
  
  
