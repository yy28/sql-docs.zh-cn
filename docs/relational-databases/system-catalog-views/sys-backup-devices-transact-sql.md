---
title: sys.backup_devices (TRANSACT-SQL) |Microsoft 文档
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.component: system-catalog-views
ms.reviewer: ''
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- backup_devices_TSQL
- backup_devices
- sys.backup_devices
- sys.backup_devices_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- backup devices [SQL Server], viewing information
- sys.backup_devices catalog view
ms.assetid: 457edaa4-aca1-4bd3-bf8d-734490b80fcd
caps.latest.revision: 32
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: be1c29322063c33797ff56451b55c619fd07db82
ms.sourcegitcommit: 808d23a654ef03ea16db1aa23edab496b73e5072
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/04/2018
ms.locfileid: "33178243"
---
# <a name="sysbackupdevices-transact-sql"></a>sys.backup_devices (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  包含使用注册每个备份设备的行**sp_addumpdevice**或中创建[!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]。  
  
|列名|数据类型|Description|  
|-----------------|---------------|-----------------|  
|**名称**|**sysname**|备份设备的名称。 在集中是唯一的。|  
|**类型**|**tinyint**|备份设备的类型：<br /><br /> 2 = 磁盘<br /><br /> 3 = 软盘（已过时）<br /><br /> 5 = 磁带<br /><br /> 6 = 管道（已过时）<br /><br /> 7 = 虚拟设备（供第三方备份供应商选择使用）<br /><br /> 通常情况下，只使用磁盘 (2) 和磁带 (5)。|  
|**type_desc**|**nvarchar(60)**|备份设备类型的说明：<br /><br /> DISK<br /><br /> DISKETTE（已过时）<br /><br /> TAPE<br /><br /> PIPE（已过时）<br /><br /> VIRTUAL_DEVICE（供第三方备份供应商选择使用）<br /><br /> 通常情况下，只使用磁盘和磁带。|  
|**physical_name**|nvarchar(260)|备份设备的物理文件名或路径。|  
  
## <a name="permissions"></a>权限  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)] 有关详细信息，请参阅 [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md)。  
  
## <a name="see-also"></a>请参阅  
 [目录视图 (Transact-SQL)](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)   
 [BACKUP (Transact-SQL)](../../t-sql/statements/backup-transact-sql.md)   
 [备份设备 (SQL Server)](../../relational-databases/backup-restore/backup-devices-sql-server.md)   
 [sp_addumpdevice (Transact-SQL)](../../relational-databases/system-stored-procedures/sp-addumpdevice-transact-sql.md)   
 [数据库和文件目录视图 (Transact-SQL)](../../relational-databases/system-catalog-views/databases-and-files-catalog-views-transact-sql.md)   
 [查询 SQL Server 系统目录常见问题解答](../../relational-databases/system-catalog-views/querying-the-sql-server-system-catalog-faq.md)  
  
  
