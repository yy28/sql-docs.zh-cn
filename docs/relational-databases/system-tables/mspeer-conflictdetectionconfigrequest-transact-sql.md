---
title: MSpeer_conflictdetectionconfigrequest (Transact SQL) |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology:
- replication
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
manager: craigg
ms.openlocfilehash: 498d08e67e543e515fa137ff066418c303c4a049
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/01/2018
ms.locfileid: "47706985"
---
# <a name="mspeerconflictdetectionconfigrequest-transact-sql"></a>MSpeer_conflictdetectionconfigrequest (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  用于在对等复制中跟踪拓扑范围内的发布配置请求。 该表存储在发布数据库中。  
  
|列名|数据类型|Description|  
|-----------------|---------------|-----------------|  
|id|**int**|标识冲突配置请求。 中的 request_id 列[MSpeer_conflictdetectionconfigresponse](../../relational-databases/system-tables/mspeer-conflictdetectionconfigresponse-transact-sql.md)将使用此值。|  
|publication|**sysname**|发起冲突配置请求的发布的名称。|  
|sent_date|**datetime**|发起冲突配置请求的日期和时间。|  
|timeout|**int**|过程应等待所有对等方返回冲突信息的时间。|  
|modified_date|**datetime**|阶段的完成日期和时间。|  
|progress_phase|**nvarchar(32)**|使用下列值之一标识当前处理阶段：<br /><br /> Started<br /><br /> 正在浏览拓扑<br /><br /> 正在收集状态<br /><br /> 已收集状态|  
|phase_timed_out|**bit**|指示当前阶段是否已超时。|  
  
## <a name="see-also"></a>请参阅  
 [复制表&#40;Transact SQL&#41;](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [复制视图 (Transact-SQL)](../../relational-databases/system-views/replication-views-transact-sql.md)  
  
  
