---
title: MSmerge_metadataaction_request (Transact SQL) |Microsoft Docs
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.prod_service: database-engine
ms.component: system-tables
ms.reviewer: ''
ms.suite: sql
ms.technology:
- replication
ms.tgt_pltfrm: ''
ms.topic: language-reference
applies_to:
- SQL Server
f1_keywords:
- MSmerge_metadataaction_request
- MSmerge_metadataaction_request_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- MSmerge_metadataaction_request system table
ms.assetid: cd31a114-900a-4218-ab58-d959e547c647
caps.latest.revision: 14
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 951b42bb78d2b15d2d107e6a4de0291aa16c7693
ms.sourcegitcommit: a431ca21eac82117492d7b84c398ddb3fced53cc
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/17/2018
ms.locfileid: "39103225"
---
# <a name="msmergemetadataactionrequest-transact-sql"></a>MSmerge_metadataaction_request (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  **MSmerge_metadataaction_request**表存储每个补偿操作所需的一行。 如果发生错误，并且必须重试同步，请使用 Web 同步，到将一个条目**MSmerge_metadataaction_request**。 在后续合并的上载阶段，将从此表中检索对属于进行同步的发布的所有项目的请求，然后将其上载。 当同步成功完成后中的相应行**MSmerge_metadataaction_request**删除该表。 此表存储在发布服务器上的发布数据库中，并存储在订阅服务器上的订阅数据库中。  
  
|列名|数据类型|Description|  
|-----------------|---------------|-----------------|  
|**tablenick**|**int**|已发布表的别名。|  
|**rowguid**|**uniqueidentifier**|给定行的行标识符。|  
|**action**|**tinyint**|标识所需的补救措施。|  
|**生成**|**bigint**|需要补救措施的代的值。|  
|**已更改**|**int**|仅供内部使用。|  
  
## <a name="see-also"></a>请参阅  
 [复制表&#40;Transact SQL&#41;](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [复制视图&#40;Transact SQL&#41;](../../relational-databases/system-views/replication-views-transact-sql.md)   
 [合并复制的 Web 同步](../../relational-databases/replication/web-synchronization-for-merge-replication.md)  
  
  
