---
title: sysschemaarticles (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sysschemaarticles_TSQL
- sysschemaarticles
dev_langs:
- TSQL
helpviewer_keywords:
- sysschemaarticles system table
ms.assetid: 67a1c039-c283-4a9c-bacc-b9b3973590c3
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 39444e0eaf9a44f48fc86b5d7f4595d63d1e9823
ms.sourcegitcommit: ceb7e1b9e29e02bb0c6ca400a36e0fa9cf010fca
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/03/2018
ms.locfileid: "52822701"
---
# <a name="sysschemaarticles-transact-sql"></a>sysschemaarticles (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  跟踪事务发布和快照发布的纯架构项目。 该表存储在发布数据库中。  
  
|列名|数据类型|Description|  
|-----------------|---------------|-----------------|  
|**artid**|**int**|文章 id。|  
|**creation_script**|**nvarchar(255)**|路径和用于创建目标表的项目架构脚本的名称。|  
|**description**|**nvarchar(255)**|本文说明项。|  
|**dest_object**|**sysname**|如果项目是纯架构项目（如存储过程、视图或 UDF），则为订阅数据库中的对象名称。|  
|**名称**|**sysname**|发布中的纯架构项目的名称。|  
|**objid**|**int**|项目基对象的对象标识符。 它可以是过程、视图、索引视图或 UDF 的对象标识符。|  
|**pubid**|**int**|发布的 ID。|  
|**pre_creation_cmd**|**tinyint**|指定当应用该项目的快照时，如果系统在订阅服务器上检测到同名的现有对象，系统应采取什么操作：<br /><br /> **0** = 执行任何操作。<br /><br /> **1** = 删除目标表。<br /><br /> **2** = 除去目标表。<br /><br /> **3** = 截断目标表。|  
|**status**|**int**|用于指示项目状态的位图。|  
|**类型**|**tinyint**|指示纯架构项目类型的值：<br /><br /> **32** = 存储过程。<br /><br /> **64** = 视图或索引视图。 <br /><br /> **96** = 聚合函数。<br /><br /> **128** = 函数。|  
|**schema_option**|**binary(8)**|给定项目的架构生成选项的位掩码。 它指定在目标数据库中为所有 CALL/MCALL/XCALL 语法自动创建存储过程，也可以是以下一个或多个值按位执行逻辑或运算的结果：<br /><br /> **0x00** = 禁用快照代理并使用通过脚本*creation_script*。<br /><br /> **0x01** = 生成对象创建 （CREATE TABLE、 CREATE PROCEDURE 等）。 该值是存储过程项目的默认值。<br /><br /> **0x02** = 生成项目，自定义存储的过程，如果已定义。<br /><br /> **0x10** = 生成相应的聚集索引。<br /><br /> **0x20** = 将用户定义数据类型转换为基本数据类型。<br /><br /> **0x40**= 生成相应的非聚集索引。<br /><br /> **0x80**= 包含在主键上声明的引用完整性。<br /><br /> **0x73** = 生成 CREATE TABLE 语句、 创建聚集索引和非聚集索引，将用户定义数据类型为基本数据类型转换和生成用于在订阅服务器上应用的自定义存储的过程脚本。 该值是除存储过程项目以外的所有项目的默认值。<br /><br /> **0x100**= 如果已定义的表项目，复制用户触发器。<br /><br /> **0x200**= 复制外键约束。 如果所引用的表不是发布的一部分，则不会复制已发布表的任何外键约束。<br /><br /> **0x400**= 复制检查约束。<br /><br /> **0x800**= 复制默认值。<br /><br /> **0x1000**= 复制列级排序规则。<br /><br /> **0x2000**= 复制与已发布的项目源对象关联的扩展属性。<br /><br /> **0x4000**= 复制唯一键，如果对表项目定义。<br /><br /> **0x8000**= 复制 primary key 和对表项目的唯一键作为约束使用 ALTER TABLE 语句。|  
|**dest_owner**|**sysname**|目标数据库中表的所有者。|  
  
## <a name="see-also"></a>请参阅  
 [复制表&#40;Transact SQL&#41;](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [复制视图 (Transact-SQL)](../../relational-databases/system-views/replication-views-transact-sql.md)  
  
  
