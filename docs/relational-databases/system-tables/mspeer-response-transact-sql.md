---
title: MSpeer_response (Transact SQL) |Microsoft Docs
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
author: stevestein
ms.author: sstein
ms.openlocfilehash: c930a5eeae8bfdb7d952610fadc0b7d779033435
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/15/2019
ms.locfileid: "68026674"
---
# <a name="mspeerresponse-transact-sql"></a>MSpeer_response (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  **MSpeer_response**表用于对等复制中存储对发布状态请求的每个节点的响应。 该表存储在发布数据库中。  
  
## <a name="definition"></a>定义  
  
|列名|数据类型|描述|  
|-----------------|---------------|-----------------|  
|**request_id**|**int**|标识中的状态请求项[MSpeer_request](../../relational-databases/system-tables/mspeer-request-transact-sql.md)表。|  
|**peer**|**sysname**|生成响应的对等方。|  
|**peer_db**|**sysname**|生成响应的对等方的订阅数据库。|  
|**received_date**|**datetime**|收到对等请求的日期和时间。|  
  
## <a name="see-also"></a>请参阅  
 [复制表 (Transact-SQL)](../../relational-databases/system-tables/replication-tables-transact-sql.md)  
  
  
