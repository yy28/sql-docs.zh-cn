---
description: sysopentapes (Transact-SQL)
title: sysopentapes (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sysopentapes
- sysopentapes_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- backup media [SQL Server], sysopentapes system table
- sysopentapes system table
ms.assetid: c066ca9b-9cfd-46b1-90a3-5c8dc9e7b6ae
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: d97f19143a2d1128f6164543847cfbc27b275877
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/17/2020
ms.locfileid: "88473128"
---
# <a name="sysopentapes-transact-sql"></a>sysopentapes (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  当前打开的每个磁带设备在表中占一行。 此视图存储在 **master** 数据库中。  
  
> [!IMPORTANT]  
>  包含此系统表作为一个视图是为了保持向后兼容性。 请改用 [transact-sql&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-io-backup-tapes-transact-sql.md) 动态管理视图 &#40;的 dm_io_backup_tapes。  
  
> [!NOTE]  
>  不能删除 **sysopentapes** 视图。  

  
|列名称|数据类型|说明|  
|-----------------|---------------|-----------------|  
|**openTape**|**nvarchar (64) **|打开的磁带设备的物理文件名。 有关打开和释放磁带设备的详细信息，请参阅 [BACKUP &#40;transact-sql&#41;](../../t-sql/statements/backup-transact-sql.md) 和 [RESTORE &#40;transact-sql&#41;](../../t-sql/statements/restore-statements-transact-sql.md)。|  
  
## <a name="permissions"></a>权限  
 用户需要对该服务器具有 VIEW SERVER STATE 权限。  
  
  
