---
title: "MSrepl_queuedtraninfo (Transact SQL) |Microsoft 文档"
ms.custom: 
ms.date: 03/04/2017
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
- MSrepl_queuedtraninfo_TSQL
- MSrepl_queuedtraninfo
dev_langs: TSQL
helpviewer_keywords: MSrepl_queuedtraninfo system table
ms.assetid: af7a5baf-32ea-475f-b6b9-68c557b4980c
caps.latest.revision: "25"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 5d7caf6825e7bcb3f17f4824b07ca931ee083998
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/21/2017
---
# <a name="msreplqueuedtraninfo-transact-sql"></a>MSrepl_queuedtraninfo (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  **MSreplication_queuedtraninfo**复制过程使用表存储发出的所有排队更新订阅正在使用基于 SQL 的排队更新的排队命令有关的信息。 该表存储在订阅数据库中。  
  
|列名|数据类型|Description|  
|-----------------|---------------|-----------------|  
|**发布服务器**|**sysname**|发布服务器的名称。|  
|**publisher_db**|**sysname**|发布数据库的名称。|  
|**发布**|**sysname**|发布的名称。|  
|**tranid**|**sysname**|执行排队命令时所使用的事务 ID。|  
|**maxorderkey**|**bigint**|仅供内部使用。|  
|**commandcount**|**bigint**|仅供内部使用。|  
  
## <a name="see-also"></a>另请参阅  
 [复制表 &#40;Transact SQL &#41;](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [复制视图 (Transact-SQL)](../../relational-databases/system-views/replication-views-transact-sql.md)  
  
  
