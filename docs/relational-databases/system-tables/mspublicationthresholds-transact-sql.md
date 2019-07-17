---
title: MSpublicationthresholds (Transact SQL) |Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- mspublicationthresholds
- mspublicationthresholds_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- MSpublicationthresholds system table
ms.assetid: 9da3879f-b1f4-4ab4-abd4-a9a8ac395eba
author: stevestein
ms.author: sstein
ms.openlocfilehash: 2bf5659dc8a5a440b764b3264556359205646d75
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/15/2019
ms.locfileid: "68088512"
---
# <a name="mspublicationthresholds-transact-sql"></a>MSpublicationthresholds (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  **MSpublicationthresholds**表用于跟踪复制性能度量值对于发布，对于每个受监视的阈值占一行。 此表存储在分发数据库中。  
  
|列名|数据类型|描述|  
|-----------------|---------------|-----------------|  
|**publication_id**|**int**|标识已为其设置阈值的发布。|  
|**metric_id**|**int**|标识复制性能跃点定义中受监视[MSreplmonthresholdmetrics](../../relational-databases/system-tables/msreplmonthresholdmetrics-transact-sql.md)系统表。|  
|**value**|**sql_variant**|受监视的跃点的阈值。|  
|**shouldalert**|**bit**|值为**1**指示该度量值超过定义的阈值时，应生成警报。|  
|**isenabled**|**bit**|值为**1**指示此复制性能指标启用监视。|  
  
## <a name="see-also"></a>请参阅  
 [复制表&#40;Transact SQL&#41;](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [复制视图 (Transact-SQL)](../../relational-databases/system-views/replication-views-transact-sql.md)  
  
  
