---
title: "MSarticles (Transact SQL) |Microsoft 文档"
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
- MSarticles
- MSarticles_TSQL
dev_langs: TSQL
helpviewer_keywords: MSarticles system table
ms.assetid: 1acd79a5-b3e2-4161-9592-7acc2a41ba38
caps.latest.revision: "25"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 458e353da5dd67489565948892b8a51025658fd8
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/21/2017
---
# <a name="msarticles-transact-sql"></a>MSarticles (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  **MSarticles**表包含每个项目正在发布服务器进行复制的一行。 此表存储在分发数据库中。  
  
|列名|数据类型|Description|  
|-----------------|---------------|-----------------|  
|**publisher_id**|**int**|发布服务器的 ID。|  
|**publisher_db**|**sysname**|发布服务器数据库的名称。|  
|**publication_id**|**int**|发布 ID。|  
|**文章**|**sysname**|项目的名称。|  
|**article_id**|**int**|文章的 ID。|  
|**destination_object**|**sysname**|在订阅服务器上创建的表的名称。|  
|**source_owner**|**sysname**|发布服务器上源表的架构的名称。|  
|**source_object**|**sysname**|添加项目时所在的源对象的名称。|  
|**说明**|**nvarchar(255)**|项目的说明。|  
|**destination_owner**|**sysname**|在订阅服务器上创建的表的架构的名称。|  
  
## <a name="see-also"></a>另请参阅  
 [复制表 &#40;Transact SQL &#41;](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [复制视图 (Transact-SQL)](../../relational-databases/system-views/replication-views-transact-sql.md)  
  
  
