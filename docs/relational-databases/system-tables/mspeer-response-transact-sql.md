---
title: MSpeer_response （Transact-sql） |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- MSpeer_response
- MSpeer_response_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- MSpeer_response system table
ms.assetid: 510e24cf-0292-47a9-b1d9-71a30fef030f
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: a1be9d2d5420e3a105249b43195eba63eb273f81
ms.sourcegitcommit: 4d3896882c5930248a6e441937c50e8e027d29fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/05/2020
ms.locfileid: "82821015"
---
# <a name="mspeer_response-transact-sql"></a>MSpeer_response (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  **MSpeer_response**表用于对等复制，以存储每个节点对发布状态请求的响应。 该表存储在发布数据库中。  
  
## <a name="definition"></a>定义  
  
|列名称|数据类型|说明|  
|-----------------|---------------|-----------------|  
|**request_id**|**int**|标识[MSpeer_request](../../relational-databases/system-tables/mspeer-request-transact-sql.md)表中的状态请求条目。|  
|**对等**|**sysname**|生成响应的对等方。|  
|**peer_db**|**sysname**|生成响应的对等方的订阅数据库。|  
|**received_date**|**datetime**|收到对等请求的日期和时间。|  
  
## <a name="see-also"></a>另请参阅  
 [复制表 (Transact-SQL)](../../relational-databases/system-tables/replication-tables-transact-sql.md)  
  
  
