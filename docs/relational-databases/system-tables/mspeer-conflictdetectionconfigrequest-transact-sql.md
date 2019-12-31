---
title: MSpeer_conflictdetectionconfigrequest （T-sql）
description: 描述用于跟踪对等发布的拓扑范围配置请求的 MSPeer_conflictdetectionconfigurerequest 存储过程。
ms.custom: seo-lt-2019
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- MSpeer_conflictdetectionconfigrequest_TSQL
- MSpeer_conflictdetectionconfigrequest
dev_langs:
- TSQL
helpviewer_keywords:
- MSpeer_conflictdetectionconfigurerequest
ms.assetid: 83afa0ca-707e-4468-a888-228268ed4e10
author: stevestein
ms.author: sstein
ms.openlocfilehash: 090236bd5e0bd0429985ff9c54039a576950ec84
ms.sourcegitcommit: 02d44167a1ee025ba925a6fefadeea966912954c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/20/2019
ms.locfileid: "75322090"
---
# <a name="mspeer_conflictdetectionconfigrequest-transact-sql"></a>MSpeer_conflictdetectionconfigrequest (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  用于在对等复制中跟踪拓扑范围内的发布配置请求。 该表存储在发布数据库中。  
  
|列名称|数据类型|说明|  
|-----------------|---------------|-----------------|  
|id|**整形**|标识冲突配置请求。 [MSpeer_conflictdetectionconfigresponse](../../relational-databases/system-tables/mspeer-conflictdetectionconfigresponse-transact-sql.md)中的 request_id 列使用此值。|  
|publication|**sysname**|发起冲突配置请求的发布的名称。|  
|sent_date|**型**|发起冲突配置请求的日期和时间。|  
|timeout|**整形**|过程应等待所有对等方返回冲突信息的时间。|  
|modified_date|**型**|阶段的完成日期和时间。|  
|progress_phase|**nvarchar （32）**|使用下列值之一标识当前处理阶段：<br /><br /> 已启动<br /><br /> 正在浏览拓扑<br /><br /> 正在收集状态<br /><br /> 已收集状态|  
|phase_timed_out|**小段**|指示当前阶段是否已超时。|  
  
## <a name="see-also"></a>另请参阅  
 [Transact-sql&#41;&#40;复制表](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [Transact-sql&#41;&#40;复制视图](../../relational-databases/system-views/replication-views-transact-sql.md)  
  
  
