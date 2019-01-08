---
title: MSreplication_queue (Transact SQL) |Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- MSreplication_queue
- MSreplication_queue_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- MSreplication_queue system table
ms.assetid: 664bf817-8021-4417-96d6-2bb1e4baabff
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: c2370bfc06f9fd939f5778ad52e6cb09aeae2806
ms.sourcegitcommit: ceb7e1b9e29e02bb0c6ca400a36e0fa9cf010fca
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/03/2018
ms.locfileid: "52819049"
---
# <a name="msreplicationqueue-transact-sql"></a>MSreplication_queue (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  **MSreplication_queue**复制过程使用表来存储所有发出使用的基于 SQL 的排队更新订阅排入队列的排队的命令。 此表存储在订阅数据库中。  
  
|列名|数据类型|Description|  
|-----------------|---------------|-----------------|  
|**publisher**|**sysname**|发布服务器的名称。|  
|**publisher_db**|**sysname**|发布数据库的名称。|  
|**发布**|**sysname**|发布的名称。|  
|**tranid**|**sysname**|执行排队命令时所使用的事务 ID。|  
|**data**|**varbinary(8000)**|存储有关排队命令信息的压缩字节流。|  
|**datalen**|**int**|数据的长度（字节）。|  
|**commandtype**|**int**|排队的命令类型包括：<br /><br /> 1 = 事务中的用户命令。<br /><br /> 2 = 订阅同步命令。|  
|**insertdate**|**datetime**|插入日期。|  
|**orderkey**|**bigint**|单调增加的标识列。|  
|**cmdstate**|**bit**|命令状态：<br /><br /> 0 = 完成。<br /><br /> 1 = 部分完成。|  
  
## <a name="see-also"></a>请参阅  
 [复制表&#40;Transact SQL&#41;](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [复制视图 (Transact-SQL)](../../relational-databases/system-views/replication-views-transact-sql.md)  
  
  
