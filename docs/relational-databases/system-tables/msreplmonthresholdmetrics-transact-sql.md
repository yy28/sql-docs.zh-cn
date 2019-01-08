---
title: MSreplmonthresholdmetrics (Transact SQL) |Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- msreplmonthresholdmetrics_TSQL
- msreplmonthresholdmetrics
dev_langs:
- TSQL
helpviewer_keywords:
- MSreplmonthresholdmetrics system table
ms.assetid: 0cc9b40a-36ce-485b-9bc2-d4abd5aa6727
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 2ce0bca2913dc6b0fbc9c8deaa4e4dd28f32f747
ms.sourcegitcommit: ceb7e1b9e29e02bb0c6ca400a36e0fa9cf010fca
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/03/2018
ms.locfileid: "52796349"
---
# <a name="msreplmonthresholdmetrics-transact-sql"></a>MSreplmonthresholdmetrics (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  **MSreplmonthresholdmetrics**表定义了用于监视复制的度量值。 此表存储中**msdb**数据库。  
  
|列名|数据类型|Description|  
|-----------------|---------------|-----------------|  
|**metric_id**|**int**|标识复制性能跃点，可以是下列值之一：<br /><br /> **1** = 过期<br /><br /> **2** = 延迟<br /><br /> **4** = mergeexpiration<br /><br /> **5** = mergeslowrunduration<br /><br /> **6** = mergefastrunduration<br /><br /> **7** = mergefastrunspeed<br /><br /> **8** = mergeslowrunspeed|  
|**title**|**sysname**|复制性能跃点的名称。|  
|**warningbitstatus**|**int**|用于为下列跃点之一提供阈值冲突警告的位标识符：<br /><br /> **1** = 到期-对事务发布的订阅超出保留期允许的阈值，超过保留期的百分比。<br /><br /> **2** = latency-将数据从事务发布服务器复制到订阅服务器所用的时间超过阈值，以秒为单位。<br /><br /> **4** = mergeexpiration – 对合并发布的订阅超出保留期允许的阈值，超过保留期的百分比。<br /><br /> **8** = mergefastrunduration-完成的合并订阅同步所花费的时间超过阈值，以秒为单位，通过快速网络连接。<br /><br /> **16** = mergeslowrunduration-完成的合并订阅同步所花费的时间超过阈值，以秒为单位，通过慢速或拨号网络连接。<br /><br /> **32** = mergefastrunspeed-传送速率的行合并订阅的同步过程未能保持阈值速率，单位为每秒，行通过快速网络连接。<br /><br /> **64** = mergeslowrunspeed-传送速率的行合并订阅的同步过程未能保持阈值速率，单位为每秒，行通过慢速或拨号网络连接。|  
|**alertmessageid**|**int**|出现阈值警告条件时显示的错误消息的 ID。|  
|**description**|**nvarchar(3000)**|复制性能跃点的说明。|  
|**default_value**|**sql_variant**|复制性能跃点的默认值。|  
|**min_value**|**sql_variant**|绑定的复制性能跃点的最小值。|  
|**max_value**|**sql_variant**|绑定的复制性能跃点的最大值。|  
  
## <a name="see-also"></a>请参阅  
 [复制表&#40;Transact SQL&#41;](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [复制视图 (Transact-SQL)](../../relational-databases/system-views/replication-views-transact-sql.md)  
  
  
