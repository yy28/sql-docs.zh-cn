---
description: 'managed_backup fn_is_master_switch_on (Transact-sql) '
title: managed_backup fn_is_master_switch_on (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- fn_is_master_switch_on
- fn_is_master_switch_on_TSQL
- smart_admin.fn_is_master_switch_on
- smart_admin.fn_is_master_switch_on_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- smart_admin.fn_is_master_switch_on
- fn_is_master_switch_on
ms.assetid: e8c2108d-b104-46cb-9645-a15f46112c86
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: b73778128e18d2937e2866ba697ab297698f6574
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/17/2020
ms.locfileid: "88419471"
---
# <a name="managed_backupfn_is_master_switch_on-transact-sql"></a>managed_backup fn_is_master_switch_on (Transact-sql) 
[!INCLUDE [sqlserver2016](../../includes/applies-to-version/sqlserver2016.md)]

  返回 SQL Server 实例上 [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] 操作的状态。  
  
 使用此函数获取 [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] 的当前状态。  
  
 
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "“主题链接”图标") [Transact-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```sql  
managed_backup.fn_is_master_switch_on ()  
```  
  
##  <a name="arguments"></a><a name="Arguments"></a> 参数  
 无  
  
## <a name="return-type"></a>返回类型  
 **小段**  
  
 1 = [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] 处于活动状态，0 = [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] 暂停。  
  
## <a name="security"></a>安全性  
  
### <a name="permissions"></a>权限  
 需要针对此函数的 SELECT 权限。  
  
## <a name="see-also"></a>另请参阅  
 [目标为 Microsoft Azure 的 SQL Server 托管备份](../../relational-databases/backup-restore/sql-server-managed-backup-to-microsoft-azure.md)  
  
  
