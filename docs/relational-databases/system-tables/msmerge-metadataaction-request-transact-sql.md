---
title: "MSmerge_metadataaction_request (Transact SQL) |Microsoft 文档"
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
- MSmerge_metadataaction_request
- MSmerge_metadataaction_request_TSQL
dev_langs: TSQL
helpviewer_keywords: MSmerge_metadataaction_request system table
ms.assetid: cd31a114-900a-4218-ab58-d959e547c647
caps.latest.revision: "14"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 7cdb53489f18f2936a418e9a4a1d29145fcdb4ae
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/21/2017
---
# <a name="msmergemetadataactionrequest-transact-sql"></a>MSmerge_metadataaction_request (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  **MSmerge_metadataaction_request**表存储每个补偿操作所需的一行。 如果出现错误并且必须重试同步，请使用 Web 同步，一个条目将变成**MSmerge_metadataaction_request**。 在后续合并的上载阶段，将从此表中检索对属于进行同步的发布的所有项目的请求，然后将其上载。 在成功完成同步后中的相应行**MSmerge_metadataaction_request**删除表。 此表存储在发布服务器上的发布数据库中，并存储在订阅服务器上的订阅数据库中。  
  
|列名|数据类型|Description|  
|-----------------|---------------|-----------------|  
|**tablenick**|**int**|已发布表的别名。|  
|**rowguid**|**uniqueidentifier**|给定行的行标识符。|  
|**操作**|**tinyint**|标识所需的补救措施。|  
|**生成**|**bigint**|需要补救措施的代的值。|  
|**更改**|**int**|仅供内部使用。|  
  
## <a name="see-also"></a>另请参阅  
 [复制表 &#40;Transact SQL &#41;](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [复制视图 &#40;Transact SQL &#41;](../../relational-databases/system-views/replication-views-transact-sql.md)   
 [合并复制的 Web 同步](../../relational-databases/replication/web-synchronization-for-merge-replication.md)  
  
  
