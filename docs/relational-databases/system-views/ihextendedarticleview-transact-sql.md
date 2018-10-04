---
title: IHextendedArticleView (Transact SQL) |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology:
- replication
ms.topic: language-reference
f1_keywords:
- IHextendedArticleView_TSQL
- IHextendedArticleView
dev_langs:
- TSQL
helpviewer_keywords:
- IHextendedArticleView view
ms.assetid: 19ef0a12-3214-4bb0-9c25-a665897e65a2
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 9ed3cb8ca49a22d9358941554cdef2030d584fb2
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/01/2018
ms.locfileid: "47848955"
---
# <a name="ihextendedarticleview-transact-sql"></a>IHextendedArticleView (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  **IHextendedArticleView**视图显示有关非 SQL Server 发布中的项目信息。 此视图存储在**分发**数据库。  
  
|列名|数据类型|Description|  
|-----------------|---------------|-----------------|  
|**publisher_id**|**smallint**|发布服务器的唯一标识符。|  
|**publication_id**|**int**|发布的唯一标识符。|  
|**article**|**sysname**|项目的名称。|  
|**destination_object**|**sysname**|在订阅服务器上已发布对象的名称。|  
|**source_owner**|**sysname**|在发布服务器上已发布对象的所有者。|  
|**source_object**|**sysname**|在发布服务器上发布的对象的名称。|  
|**description**|**nvarchar(255)**|项目的说明。|  
|**creation_script**|**nvarchar(255)**|项目的架构创建脚本。|  
|**del_cmd**|**nvarchar(255)**|执行 DELETE 的命令。|  
|**filter**|**int**|用于定义水平分区的存储过程的标识符。|  
|**filter_clause**|**ntext**|用于水平筛选项目的 WHERE 子句。|  
|**ins_cmd**|**nvarchar(255)**|执行 INSERT 的命令。|  
|**pre_creation_cmd**|**tinyint**|DROP TABLE、DELETE TABLE 或 TRUNCATE 的预创建命令：<br /><br /> **0** = none。<br /><br /> **1** = DROP。<br /><br /> **2** = DELETE。<br /><br /> **3** = 截断。|  
|**status**|**tinyint**|项目选项和状态的位掩码，可以是对以下一个或多个值执行逻辑位或运算的结果：<br /><br /> **1** = 项目处于活动状态。<br /><br /> **8** = 包括 INSERT 语句中的列名称。<br /><br /> **16** = 使用参数化语句。<br /><br /> **24** = 同时在 INSERT 语句中包括的列名称并使用参数化的语句。<br /><br /> 例如，使用参数化的语句的活动项目将具有值**17**此列中。 值为**0**意味着项目处于非活动状态并且未定义任何其他属性。|  
|**类型**|**tinyint**|项目的类型：<br /><br /> **1** = 基于日志的项目。<br /><br /> **3** = 具有手动筛选器基于日志的项目。<br /><br /> **5** = 具有手动视图并且基于日志的项目。<br /><br /> **7** = 具有手动筛选器和手动视图并且基于日志的项目。|  
|**upd_cmd**|**nvarchar(255)**|执行 UPDATE 的命令。|  
|**schema_option**|**binary**|指示将写入脚本的内容。请参阅[sp_addarticle &#40;TRANSACT-SQL&#41; ](../../relational-databases/system-stored-procedures/sp-addarticle-transact-sql.md)有关支持的架构选项的列表。|  
|**dest_owner**|**sysname**|在目标数据库中已发布对象的所有者。|  
  
## <a name="see-also"></a>请参阅  
 [异类数据库复制](../../relational-databases/replication/non-sql/heterogeneous-database-replication.md)   
 [复制表&#40;Transact SQL&#41;](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [复制视图 (Transact-SQL)](../../relational-databases/system-views/replication-views-transact-sql.md)  
  
  
