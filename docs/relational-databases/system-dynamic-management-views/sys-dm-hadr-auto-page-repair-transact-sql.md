---
title: sys.dm_hadr_auto_page_repair (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 02/05/2019
ms.prod: sql
ms.reviewer: ''
ms.technology: system-objects
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
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: e817b17de8a8af93a13628334337686abbe66b5f
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/15/2019
ms.locfileid: "67900690"
---
# <a name="sysdmhadrautopagerepair-transact-sql"></a>sys.dm_hadr_auto_page_repair (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  为针对任何可用性数据库（位于服务器实例为任何可用性组承载的可用性副本上）的每一个自动页修复尝试都返回一行。 该视图包含对应于给定主/辅助数据库上最新自动页修复尝试的行，每个数据库最多可对应 100 行。 只要一个数据库对应的行达到最大值，则它的下个自动页修复尝试对应的行将替换现有的一个项。
  
  下表定义了各个列的含义：  
  
|列名|数据类型|描述|  
|-----------------|---------------|-----------------|  
|**database_id**|**int**|此行对应的数据库的 ID。|  
|**file_id**|**int**|页所在文件的 ID。|  
|**page_id**|**bigint**|文件中页的 ID。|  
|**error_type**|**int**|错误类型。 值可以是：<br /><br /> **-** 1 = 所有硬件 823 错误<br /><br /> 1 = 824 错误的校验和或页撕裂 （如错误的页 ID) 以外的错误<br /><br /> 2 = 错误的校验和<br /><br /> 3 = 页撕裂|  
|**page_status**|**int**|页修复尝试的状态：<br /><br /> 2 = 排队等候来自伙伴的请求。<br /><br /> 3 = 请求已发送到伙伴。<br /><br /> 4 = 已成功修复的页。<br /><br /> 5 = 最后一次尝试期间未能修复页 / 自动页修复将尝试重新修复此页。|  
|**modification_time**|**datetime**|页状态最后发生更改的时间。|  
  
## <a name="security"></a>安全性  
  
### <a name="permissions"></a>权限  
 要求具有服务器的 VIEW SERVER STATE 权限。  
  
## <a name="see-also"></a>请参阅  
 [自动页修复（可用性组：数据库镜像）](../../sql-server/failover-clusters/automatic-page-repair-availability-groups-database-mirroring.md)   
 [suspect_pages &#40;TRANSACT-SQL&#41;](../../relational-databases/system-tables/suspect-pages-transact-sql.md)   
 [管理 suspect_pages 表 (SQL Server)](../../relational-databases/backup-restore/manage-the-suspect-pages-table-sql-server.md)  
  
  

