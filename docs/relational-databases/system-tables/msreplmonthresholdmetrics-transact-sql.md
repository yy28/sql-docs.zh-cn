---
title: "MSreplmonthresholdmetrics (Transact SQL) |Microsoft 文档"
ms.custom: 
ms.date: 03/04/2017
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
- msreplmonthresholdmetrics_TSQL
- msreplmonthresholdmetrics
dev_langs:
- TSQL
helpviewer_keywords:
- MSreplmonthresholdmetrics system table
ms.assetid: 0cc9b40a-36ce-485b-9bc2-d4abd5aa6727
caps.latest.revision: 
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 7453274dee183a0222d6a0e6ae43f052a628c9aa
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/21/2017
---
# <a name="msreplmonthresholdmetrics-transact-sql"></a>MSreplmonthresholdmetrics (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  **MSreplmonthresholdmetrics**表定义了用于监视复制提供的度量值。 此表存储在**msdb**数据库。  
  
|列名|数据类型|Description|  
|-----------------|---------------|-----------------|  
|**metric_id**|**int**|标识复制性能跃点，可以是下列值之一：<br /><br /> **1** = 过期<br /><br /> **2** = 延迟<br /><br /> **4** = mergeexpiration<br /><br /> **5** = mergeslowrunduration<br /><br /> **6** = mergefastrunduration<br /><br /> **7** = mergefastrunspeed<br /><br /> **8** = mergeslowrunspeed|  
|**title**|**sysname**|复制性能跃点的名称。|  
|**warningbitstatus**|**int**|用于为下列跃点之一提供阈值冲突警告的位标识符：<br /><br /> **1** = 到期 – 对事务发布的订阅已保持期的百分比超过了允许的阈值，超出的保持期。<br /><br /> **2** = 延迟 – 将数据从事务发布服务器复制到订阅服务器上所花费的时间超过阈值，以秒为单位。<br /><br /> **4** = mergeexpiration – 对合并发布的订阅已保持期的百分比超过了允许的阈值，超出的保持期。<br /><br /> **8** = mergefastrunduration – 完成合并订阅的同步所花费的时间超过阈值，以秒为单位，通过快速网络连接。<br /><br /> **16** = mergeslowrunduration – 完成合并订阅的同步所花费的时间超过阈值，以秒为单位，通过慢速或拨号网络连接。<br /><br /> **32** = mergefastrunspeed – 传送速率的行在合并订阅的同步过程中失败的快速网络连接通过维护阈值速率，单位为秒，每个行。<br /><br /> **64** = mergeslowrunspeed – 传送速率的行在合并订阅的同步过程中无法通过慢速或拨号网络连接维护阈值速率，单位为秒，每个行。|  
|**alertmessageid**|**int**|出现阈值警告条件时显示的错误消息的 ID。|  
|**说明**|**nvarchar(3000)**|复制性能跃点的说明。|  
|**默认值**|**sql_variant**|复制性能跃点的默认值。|  
|**min_value**|**sql_variant**|绑定的复制性能跃点的最小值。|  
|**max_value**|**sql_variant**|绑定的复制性能跃点的最大值。|  
  
## <a name="see-also"></a>另请参阅  
 [复制表 &#40;Transact SQL &#41;](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [复制视图 (Transact-SQL)](../../relational-databases/system-views/replication-views-transact-sql.md)  
  
  
