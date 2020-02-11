---
title: MSarticles （Transact-sql） |Microsoft Docs
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- MSarticles
- MSarticles_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- MSarticles system table
ms.assetid: 1acd79a5-b3e2-4161-9592-7acc2a41ba38
author: stevestein
ms.author: sstein
ms.openlocfilehash: 81598b65daf5fa7370004c890ab775e5b29b518f
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/08/2020
ms.locfileid: "68132100"
---
# <a name="msarticles-transact-sql"></a>MSarticles (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  发布服务器正在复制的每个项目在**MSarticles**表中各占一行。 此表存储在分发数据库中。  
  
|列名称|数据类型|说明|  
|-----------------|---------------|-----------------|  
|**publisher_id**|**smallint**|发布服务器的 ID。|  
|**publisher_db**|**sysname**|发布服务器数据库的名称。|  
|**publication_id**|**int**|发布 ID。|  
|**下文**|**sysname**|项目的名称。|  
|**article_id**|**int**|项目的 ID。|  
|**destination_object**|**sysname**|在订阅服务器上创建的表的名称。|  
|**source_owner**|**sysname**|发布服务器上源表的架构的名称。|  
|**source_object**|**sysname**|添加项目时所在的源对象的名称。|  
|**2008**|**nvarchar(255)**|项目的说明。|  
|**destination_owner**|**sysname**|在订阅服务器上创建的表的架构的名称。|  
  
## <a name="see-also"></a>另请参阅  
 [Transact-sql&#41;&#40;复制表](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [复制视图 (Transact-SQL)](../../relational-databases/system-views/replication-views-transact-sql.md)  
  
  
