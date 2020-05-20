---
title: MSreplmonthresholdmetrics （Transact-sql） |Microsoft Docs
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
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 0a82ed4f1ec8c884105101920f41329a7314941d
ms.sourcegitcommit: 4d3896882c5930248a6e441937c50e8e027d29fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/05/2020
ms.locfileid: "82829822"
---
# <a name="msreplmonthresholdmetrics-transact-sql"></a>MSreplmonthresholdmetrics (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  **MSreplmonthresholdmetrics**表定义用于监视复制的指标。 该表存储在**msdb**数据库中。  
  
|列名称|数据类型|说明|  
|-----------------|---------------|-----------------|  
|**metric_id**|**int**|标识复制性能跃点，可以是下列值之一：<br /><br /> **1** = 过期<br /><br /> **2** = 滞后时间<br /><br /> **4** = mergeexpiration<br /><br /> **5** = mergeslowrunduration<br /><br /> **6** = mergefastrunduration<br /><br /> **7** = mergefastrunspeed<br /><br /> **8** = mergeslowrunspeed|  
|**title**|**sysname**|复制性能跃点的名称。|  
|**warningbitstatus**|**int**|用于为下列跃点之一提供阈值冲突警告的位标识符：<br /><br /> **1** = 过期-对事务发布的订阅已超出保持期超过允许的阈值（以保持期的百分比形式表示）。<br /><br /> **2** = 滞后时间-将数据从事务发布服务器复制到订阅服务器所用的时间超过了阈值（以秒为单位）。<br /><br /> **4** = mergeexpiration-针对合并发布的订阅已超出保持期超过允许的阈值（以保持期的百分比表示）。<br /><br /> **8** = mergefastrunduration-通过快速网络连接完成合并订阅同步所用的时间超过了阈值（以秒为单位）。<br /><br /> **16** = mergeslowrunduration-完成合并订阅同步所用的时间超过了慢速或拨号网络连接的阈值（以秒为单位）。<br /><br /> **32** = mergefastrunspeed-合并订阅的同步过程中的行传递速率未能维持快速网络连接上的阈值速率（以每秒行数为单位）。<br /><br /> **64** = mergeslowrunspeed-合并订阅的同步过程中的行传递速率未能维持慢速或拨号网络连接的阈值速率（以每秒行数为单位）。|  
|**alertmessageid**|**int**|出现阈值警告条件时显示的错误消息的 ID。|  
|**2008**|**nvarchar （3000）**|复制性能跃点的说明。|  
|**default_value**|**sql_variant**|复制性能跃点的默认值。|  
|**min_value**|**sql_variant**|绑定的复制性能跃点的最小值。|  
|**max_value**|**sql_variant**|绑定的复制性能跃点的最大值。|  
  
## <a name="see-also"></a>另请参阅  
 [Transact-sql&#41;&#40;复制表](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [复制视图 (Transact-SQL)](../../relational-databases/system-views/replication-views-transact-sql.md)  
  
  
