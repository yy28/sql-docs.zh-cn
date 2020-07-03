---
title: MSpeer_topologyrequest （Transact-sql） |Microsoft Docs
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- MSpeer_topologyrequest_TSQL
- MSpeer_topologyrequest
dev_langs:
- TSQL
helpviewer_keywords:
- MSpeer_topologyrequest
ms.assetid: c644814b-4e40-44d7-b6b4-5954b0d4db7c
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 5bc68682c968457d733e1b221b6983a95e46e204
ms.sourcegitcommit: f7ac1976d4bfa224332edd9ef2f4377a4d55a2c9
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/02/2020
ms.locfileid: "85889612"
---
# <a name="mspeer_topologyrequest-transact-sql"></a>MSpeer_topologyrequest (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  用于在对等复制中跟踪发布的拓扑状态请求。 该表存储在发布数据库中。  
  
|列名称|数据类型|说明|  
|-----------------|---------------|-----------------|  
|id|**int**|标识拓扑状态请求。 [MSpeer_topologyresponse](../../relational-databases/system-tables/mspeer-topologyresponse-transact-sql.md)中的 request_id 列使用此值。|  
|publication|**sysname**|发起拓扑状态请求的发布的名称。|  
|sent_date|**datetime**|发起拓扑状态请求的日期和时间。|  
  
## <a name="see-also"></a>另请参阅  
 [Transact-sql&#41;&#40;复制表](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [复制视图 (Transact-SQL)](../../relational-databases/system-views/replication-views-transact-sql.md)  
  
  
