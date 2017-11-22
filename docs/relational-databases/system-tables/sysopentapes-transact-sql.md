---
title: "sysopentapes (Transact SQL) |Microsoft 文档"
ms.custom: 
ms.date: 06/10/2016
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: system-tables
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- sysopentapes
- sysopentapes_TSQL
dev_langs: TSQL
helpviewer_keywords:
- backup media [SQL Server], sysopentapes system table
- sysopentapes system table
ms.assetid: c066ca9b-9cfd-46b1-90a3-5c8dc9e7b6ae
caps.latest.revision: "37"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: bb39670ced045b6ae5f14b9225d1b46d35aef792
ms.sourcegitcommit: 66bef6981f613b454db465e190b489031c4fb8d3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/17/2017
---
# <a name="sysopentapes-transact-sql"></a>sysopentapes (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  当前打开的每个磁带设备在表中占一行。 此视图存储在**master**数据库。  
  
> [!IMPORTANT]  
>  包含此系统表作为一个视图是为了保持向后兼容性。 请改用[sys.dm_io_backup_tapes &#40;Transact SQL &#41;](../../relational-databases/system-dynamic-management-views/sys-dm-io-backup-tapes-transact-sql.md)动态管理视图。  
  
> [!NOTE]  
>  无法删除**sysopentapes**视图。  

  
|列名|数据类型|Description|  
|-----------------|---------------|-----------------|  
|**openTape**|**nvarchar(64)**|打开的磁带设备的物理文件名。 有关打开和释放磁带设备的详细信息，请参阅[备份 &#40;Transact SQL &#41;](../../t-sql/statements/backup-transact-sql.md)和[还原 &#40;Transact SQL &#41;](../../t-sql/statements/restore-statements-transact-sql.md).|  
  
## <a name="permissions"></a>Permissions  
 用户需要对该服务器具有 VIEW SERVER STATE 权限。  
  
  
