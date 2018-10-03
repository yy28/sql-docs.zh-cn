---
title: sys.database_mirroring_witnesses (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.database_mirroring_witnesses
- sys.database_mirroring_witnesses_TSQL
- database_mirroring_witnesses
- database_mirroring_witnesses_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- database mirroring [SQL Server], catalog views
- sys.database_mirroring_witnesses catalog view
- witness [SQL Server], sys.database_mirroring_witnesses catalog view
ms.assetid: 0dd5b794-733b-4a3c-b5a4-62f9f1f0f22d
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: e7542f7619a261a07349c5c55b01a10042ee16bc
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/01/2018
ms.locfileid: "47715645"
---
# <a name="database-mirroring-witness-catalog-views---sysdatabasemirroringwitnesses"></a>数据库镜像见证服务器目录视图-sys.database_mirroring_witnesses
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

  服务器在数据库镜像合作关系中充当的每个见证服务器角色在表中都占用一行。 
  
  在数据库镜像会话中，执行自动故障转移需要使用见证服务器。 理想状况是，见证服务器驻留在与主体服务器和镜像服务器分离的单独的计算机上。 见证服务器不为数据库提供服务。 相反，它会监视主体服务器和镜像服务器的状态。 如果主体服务器出现故障，见证服务器可能会启动自动故障转移到镜像服务器。 
  
|列名|数据类型|Description|  
|-----------------|---------------|-----------------|  
|**database_name**|**sysname**|数据库镜像会话中数据库的两个副本的名称。|  
|**principal_server_name**|**sysname**|伙伴服务器的名称，该服务器的数据库副本当前是主体数据库。|  
|**mirror_server_name**|**sysname**|伙伴服务器的名称，该服务器的数据库副本当前是镜像数据库。|  
|**safety_level**|**tinyint**|镜像数据库中更新的事务安全设置：<br /><br /> 0 = 未知状态<br /><br /> 1 = Off（异步）<br /><br /> 2 = Full（同步）<br /><br /> 使用自动故障转移的见证服务器要求具有完全事务安全性，这是默认设置。|  
|**safety_level_desc**|**nvarchar(60)**|对镜像数据库中更新的安全保证的说明：<br /><br /> UNKNOWN<br /><br /> OFF<br /><br /> FULL|  
|**safety_sequence_number**|**int**|更新对更改的序列号**safety_level**。|  
|**role_sequence_number**|**int**|镜像伙伴所充当的主体/镜像数据库角色的更改的更新序列号。|  
|**mirroring_guid**|**uniqueidentifier**|镜像合作关系的标识符。|  
|**family_guid**|**uniqueidentifier**|数据库备份系列的标识符。 用于检测匹配的还原状态。|  
|**is_suspended**|**bit**|数据库镜像挂起。|  
|**is_suspended_sequence_number**|**int**|设置的序列号**is_suspended**。|  
|**partner_sync_state**|**tinyint**|镜像会话的同步状态：<br /><br /> 5 = 伙伴已同步。 可以进行故障转移。 了解有关故障转移，请参阅要求[角色数据库镜像会话期间切换&#40;SQL Server&#41;](../../database-engine/database-mirroring/role-switching-during-a-database-mirroring-session-sql-server.md)。<br /><br /> 6 = 伙伴未同步。 现在无法进行故障转移。|  
|**partner_sync_state_desc**|**nvarchar(60)**|镜像会话同步状态的说明：<br /><br /> SYNCHRONIZED<br /><br /> UNSYNCHRONIZED|  
  
## <a name="permissions"></a>Permissions  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)] 有关详细信息，请参阅 [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md)。  
  
## <a name="see-also"></a>请参阅  
 [数据库镜像见证服务器](../../database-engine/database-mirroring/database-mirroring-witness.md)   
 [sys.database_mirroring &#40;TRANSACT-SQL&#41;](../../relational-databases/system-catalog-views/sys-database-mirroring-transact-sql.md)   
 [sys.database_mirroring_endpoints (Transact-SQL)](../../relational-databases/system-catalog-views/sys-database-mirroring-endpoints-transact-sql.md)   
 [查询 SQL Server 系统目录常见问题解答](../../relational-databases/system-catalog-views/querying-the-sql-server-system-catalog-faq.md)  
  
  
