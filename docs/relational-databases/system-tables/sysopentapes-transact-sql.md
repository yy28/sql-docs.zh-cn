---
title: sysopentapes (TRANSACT-SQL) |Microsoft Docs
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
author: stevestein
ms.author: sstein
ms.openlocfilehash: 813592ffa5b67a4926dff611c2ba0e0faf36d273
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/15/2019
ms.locfileid: "68029805"
---
# <a name="sysopentapes-transact-sql"></a>sysopentapes (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  当前打开的每个磁带设备在表中占一行。 此视图存储在**主**数据库。  
  
> [!IMPORTANT]  
>  包含此系统表作为一个视图是为了保持向后兼容性。 请改用[sys.dm_io_backup_tapes &#40;TRANSACT-SQL&#41; ](../../relational-databases/system-dynamic-management-views/sys-dm-io-backup-tapes-transact-sql.md)动态管理视图。  
  
> [!NOTE]  
>  您不能删除**sysopentapes**视图。  

  
|列名|数据类型|描述|  
|-----------------|---------------|-----------------|  
|**openTape**|**nvarchar(64)**|打开的磁带设备的物理文件名。 有关打开和释放磁带设备的详细信息，请参阅[备份&#40;TRANSACT-SQL&#41; ](../../t-sql/statements/backup-transact-sql.md)并[还原&#40;-&#41;](../../t-sql/statements/restore-statements-transact-sql.md)。|  
  
## <a name="permissions"></a>权限  
 用户需要对该服务器具有 VIEW SERVER STATE 权限。  
  
  
