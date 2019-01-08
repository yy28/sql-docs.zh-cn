---
title: sysmergeschemaarticles (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sysmergeschemaarticles_TSQL
- sysmergeschemaarticles
dev_langs:
- TSQL
helpviewer_keywords:
- sysmergeschemaarticles system table
ms.assetid: b5085979-2f76-48e1-bf3b-765a84003dd9
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 581a6be7472818f983bc82ef3a717be0c0edaa48
ms.sourcegitcommit: ceb7e1b9e29e02bb0c6ca400a36e0fa9cf010fca
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/03/2018
ms.locfileid: "52802809"
---
# <a name="sysmergeschemaarticles-transact-sql"></a>sysmergeschemaarticles (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  跟踪合并复制的仅限架构的项目。 此表存储在发布和订阅数据库中。  
  
|列名|数据类型|Description|  
|-----------------|---------------|-----------------|  
|**名称**|**sysname**|合并复制中仅限架构的项目的名称。|  
|**类型**|**tinyint**|指示仅限架构的项目的类型，可以是以下类型之一：<br /><br /> **0x20** = 存储过程仅限架构的项目。<br /><br /> **0x40** = 视图仅限架构的项目或索引的视图仅限架构的项目。|  
|**objid**|**int**|项目基对象的对象标识符。 可以是过程、视图、索引视图或用户定义函数的对象标识符。|  
|**artid**|**uniqueidentifier**|文章 id。|  
|**description**|**nvarchar(255)**|项目的说明。|  
|**pre_creation_command**|**tinyint**|在订阅数据库中创建项目时采取的默认操作：<br /><br /> **0 =** 无-如果表已存在于订阅服务器中，不执行任何操作。<br /><br /> **1** = 删除-删除该表，然后重新创建它。<br /><br /> **2** = 删除-发出基于子集筛选器中的 WHERE 子句的 delete 命令。<br /><br /> **3** = 截断-与相同**2**，但会删除页而非行。 不过，不要使用 WHERE 子句。|  
|**pubid**|**uniqueidentifier**|发布的唯一标识符。|  
|**status**|**tinyint**|指示仅限架构的项目的状态，可以是以下状态之一：<br /><br /> **1** = Unsynced-用于发布的表运行在下次运行快照代理时的初始处理脚本。<br /><br /> **2** = 活动-用于发布表的初始处理脚本已运行。<br /><br /> **5** = new_inactive-内容待定要添加。<br /><br /> **6** = new_active-内容待定要添加。|  
|**creation_script**|**nvarchar(255)**|用于创建目标表的可选项目架构预创建脚本的路径和名称。|  
|**schema_option**|**binary(8)**|给定的仅限架构的项目的架构生成选项的位图，它可以是以下一个或多个值的按位逻辑或结果：<br /><br /> **0x00** = 禁用快照代理编写脚本，并使用提供的 CreationScript。<br /><br /> **0x01** = 生成对象创建 （CREATE TABLE、 CREATE PROCEDURE 等）。<br /><br /> **0x10** = 生成相应的聚集索引。<br /><br /> **0x20** = convert 用户定义数据类型转换为基本数据类型。<br /><br /> **0x40** = 生成相应的非聚集索引。<br /><br /> **0x80** = 包括声明引用完整性在主键上。<br /><br /> **0x100** = 如果已定义的表项目，复制用户触发器。<br /><br /> **0x200** = 复制外键约束。 如果被所引用的表不是发布的一部分，则不会复制已发布表的任何外键约束。<br /><br /> **0x400** = 复制检查约束。<br /><br /> **0x800** = 复制默认值。<br /><br /> **0x1000** = 复制列级排序规则。<br /><br /> **0x2000** = 复制与已发布的项目源对象关联的扩展属性。<br /><br /> **0x4000** = 复制唯一键，如果对表项目定义。<br /><br /> **0x8000** = 的复制 primary key 和上一个表的唯一键作为约束使用 ALTER TABLE 语句的文章。<br /><br /> 有关详细信息的可能值为**schema_option**，请参阅[sp_addmergearticle](../../relational-databases/system-stored-procedures/sp-addmergearticle-transact-sql.md)。|  
|**destination_object**|**sysname**|订阅数据库中的目标对象名称。 该值仅应用于仅限架构的项目，例如，存储过程、视图和 UDF。|  
|**destination_owner**|**sysname**|如果不是订阅数据库中对象的所有者**dbo**。|  
  
## <a name="see-also"></a>请参阅  
 [复制表&#40;Transact SQL&#41;](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [复制视图 (Transact-SQL)](../../relational-databases/system-views/replication-views-transact-sql.md)  
  
  
