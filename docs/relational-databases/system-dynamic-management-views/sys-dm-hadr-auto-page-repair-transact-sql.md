---
title: sys.dm_hadr_auto_page_repair (TRANSACT-SQL) |Microsoft 文档
ms.custom: ''
ms.date: 03/15/2017
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: dmv's
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- dm_hadr_auto_page_repair_TSQL
- sys.dm_hadr_auto_page_repair
- sys.dm_hadr_auto_page_repair_TSQL
- dm_hadr_auto_page_repair
dev_langs:
- TSQL
helpviewer_keywords:
- Availability Groups [SQL Server], monitoring
- automatic page repair
- sys.dm_hadr_auto_page_repair dynamic management view
ms.assetid: d7840adf-4a1b-41ac-bc94-102c07ad1c79
caps.latest.revision: 8
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 97aefe435d8c1db569aa10f4521b9af96f0c9899
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/16/2018
---
# <a name="sysdmhadrautopagerepair-transact-sql"></a>sys.dm_hadr_auto_page_repair (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  为针对任何可用性数据库（位于服务器实例为任何可用性组承载的可用性副本上）的每一个自动页修复尝试都返回一行。 该视图包含对应于给定主/辅助数据库上最新自动页修复尝试的行，每个数据库最多可对应 100 行。 只要一个数据库对应的行达到最大值，则它的下个自动页修复尝试对应的行将替换现有的一个项。
  
  下表定义了各个列的含义：  
  
|列名|数据类型|Description|  
|-----------------|---------------|-----------------|  
|**database_id**|**int**|此行对应的数据库的 ID。|  
|**file_id**|**int**|页所在文件的 ID。|  
|**page_id**|**bigint**|文件中页的 ID。|  
|**error_type**|**int**|错误类型。 值可以是：<br /><br /> **-**1 = 所有硬件 823 错误<br /><br /> 1 = 824 错误的校验和或残缺的页 （如错误的页 ID) 以外的错误<br /><br /> 2 = 错误的校验和<br /><br /> 3 = 页撕裂|  
|**page_status**|**int**|页修复尝试的状态：<br /><br /> 2 = 排队等候来自伙伴的请求。<br /><br /> 3 = 请求已发送到伙伴。<br /><br /> 4 = 排队等候自动页修复（已收到来自伙伴的响应）。<br /><br /> 5 = 自动页修复已成功，页应当可用。<br /><br /> 6 = 无法修复页。 这表示在页修复尝试期间发生了错误，例如，可能是由于伙伴上的页也已损坏、已经断开与伙伴的连接或网络发生故障。 此状态不是最终状态；如果在此页上再次发现损坏，则将再次请求伙伴上的该页。|  
|**modification_time**|**datetime**|页状态最后发生更改的时间。|  
  
## <a name="security"></a>Security  
  
### <a name="permissions"></a>权限  
 要求具有服务器的 VIEW SERVER STATE 权限。  
  
## <a name="see-also"></a>另请参阅  
 [自动页修复（可用性组：数据库镜像）](../../sql-server/failover-clusters/automatic-page-repair-availability-groups-database-mirroring.md)   
 [suspect_pages & #40;Transact SQL & #41;](../../relational-databases/system-tables/suspect-pages-transact-sql.md)   
 [管理 suspect_pages 表 (SQL Server)](../../relational-databases/backup-restore/manage-the-suspect-pages-table-sql-server.md)  
  
  

