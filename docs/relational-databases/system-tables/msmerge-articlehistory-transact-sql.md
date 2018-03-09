---
title: "MSmerge_articlehistory (Transact SQL) |Microsoft 文档"
ms.custom: 
ms.date: 03/06/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: system-tables
ms.reviewer: 
ms.suite: sql
ms.technology:
- replication
ms.tgt_pltfrm: 
ms.topic: language-reference
applies_to:
- SQL Server
f1_keywords:
- MSmerge_articlehistory
- MSmerge_articlehistory_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- MSmerge_articlehistory system table
ms.assetid: 2870e7ea-dbec-4636-9171-c2cee96018ac
caps.latest.revision: 
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: dbd2fef95a478eebc6526fc888fa621c1ec198ab
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/21/2017
---
# <a name="msmergearticlehistory-transact-sql"></a>MSmerge_articlehistory (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  **MSmerge_articlehistory**表跟踪与每个项目进行了更改的一个行的合并代理同步会话期间对项目所做的更改。 此表存储在分发数据库中。  
  
|列名|数据类型|Description|  
|-----------------|---------------|-----------------|  
|**session_id**|**int**|中的合并代理作业会话的 ID [MSmerge_sessions](../../relational-databases/system-tables/msmerge-sessions-transact-sql.md)系统表。|  
|**phase_id**|**int**|同步会话的阶段，可以是下列的一个值：<br /><br /> **1** = 上载。<br /><br /> **2** = 下载。<br /><br /> **4** = 清理。<br /><br /> **5** = 关闭。<br /><br /> **6** = 架构更改。<br /><br /> **7** = BCP。|  
|**article_name**|**sysname**|对其进行更改的项目的名称。|  
|**start_time**|**datetime**|代理开始处理项目的时间。|  
|**duration**|**int**|代理处理项目所用的时间（秒）。|  
|**插入**|**int**|在同步期间应用到特定项目的插入的数目。 在同步过程中此值将增大，结束值代表总数。|  
|**更新**|**int**|在同步期间应用到特定项目的更新的数目。 在同步过程中此值将增大，结束值代表总数。|  
|**删除**|**int**|在同步期间应用到特定项目的删除的数目。 在同步过程中此值将增大，结束值代表总数。|  
|**冲突**|**int**|同步期间发生的冲突的数目。 在同步过程中此值将增大，结束值代表总数。|  
|**conflicts_resolved**|**int**|同步期间发生并已经解决的冲突的数目。 在同步过程中此值将增大，结束值代表总数。|  
|**rows_retried**|**int**|在同步期间重试的错误行的数目。  在同步过程中此值将增大，结束值代表总数。|  
|**percent_complete**|**decimal**|在会话期间合并代理对项目进行同步所花费的时间占总同步时间的百分比。 在会话结束前，该值为 NULL。|  
|**estimated_changes**|**int**|必须应用到项目的一个估计的行更改数。|  
|**relative_cost**|**decimal**|将更改应用到项目所用的时间与整个会话的总时间的比值。|  
  
## <a name="see-also"></a>另请参阅  
 [复制表 (Transact-SQL)](../../relational-databases/system-tables/replication-tables-transact-sql.md)  
  
  
