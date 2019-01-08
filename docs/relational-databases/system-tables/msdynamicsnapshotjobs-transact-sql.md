---
title: MSdynamicsnapshotjobs (Transact SQL) |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- MSdynamicsnapshotjobs_TSQL
- MSdynamicsnapshotjobs
dev_langs:
- TSQL
helpviewer_keywords:
- MSdynamicsnapshotjobs system table
ms.assetid: 4f36a325-0e3c-46c4-aeeb-416346cce0bc
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 8b7934d914af50d61df554c2a82ae221a1d5490f
ms.sourcegitcommit: ceb7e1b9e29e02bb0c6ca400a36e0fa9cf010fca
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/03/2018
ms.locfileid: "52817279"
---
# <a name="msdynamicsnapshotjobs-transact-sql"></a>MSdynamicsnapshotjobs (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  **MSdynamicsnapshotjobs**表跟踪应用以生成已筛选的数据快照的参数化的行筛选器信息。 此表存储在发布和订阅数据库中。  
  
|列名|数据类型|Description|  
|-----------------|---------------|-----------------|  
|**id**|**int**|筛选数据快照作业的 ID。|  
|**名称**|**sysname**|筛选的数据快照作业的名称。|  
|**pubid**|**uniqueidentifier**|此发布的唯一标识号。|  
|**job_id**|**uniqueidentifier**|在分发服务器上的 SQL Server 代理作业的 ID。|  
|**agent_id**|**int**|SQL Server 代理的 ID。|  
|**dynamic_filter_login**|**sysname**|该值用于计算[SUSER_SNAME](../../t-sql/functions/suser-sname-transact-sql.md)中参数化的行筛选器为发布所定义的函数。|  
|**dynamic_filter_hostname**|**sysname**|该值用于计算[HOST_NAME](../../t-sql/functions/host-name-transact-sql.md)中参数化的行筛选器为发布所定义的函数。|  
|**dynamic_snapshot_location**|**nvarchar(255)**|如果使用筛选数据快照则从中读取快照文件的文件夹的路径。|  
|**partition_id**|**int**|作业所属数据分区的 ID。|  
  
## <a name="see-also"></a>请参阅  
 [复制表 (Transact-SQL)](../../relational-databases/system-tables/replication-tables-transact-sql.md)  
  
  
