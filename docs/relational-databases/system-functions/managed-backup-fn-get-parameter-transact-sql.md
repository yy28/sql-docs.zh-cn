---
description: 'managed_backup fn_get_parameter (Transact-sql) '
title: managed_backup fn_get_parameter (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 10/03/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- smart_admin.fn_get_parameter_TSQL
- smart_admin.fn_get_parameter
- fn_get_parameter_TSQL
- fn_get_parameter
dev_langs:
- TSQL
helpviewer_keywords:
- fn_get_parameter
- smart_admin.fn_get_parameter
ms.assetid: ed94e54d-4516-4806-a8ce-f013d3a04122
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: da8c646cca92a5ef25fd12322fd8a6bd222a1c9e
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/17/2020
ms.locfileid: "88419511"
---
# <a name="managed_backupfn_get_parameter-transact-sql"></a>managed_backup fn_get_parameter (Transact-sql) 
[!INCLUDE [sqlserver2016](../../includes/applies-to-version/sqlserver2016.md)]

  返回包含 0 行、1 行或多行参数和值对的表。  
  
 使用此存储过程可查看智能管理的所有或特定的配置设置。  
  
 如果从未配置参数，则此函数将返回 0 行。  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "“主题链接”图标") [Transact-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```sql  
managed_backup.fn_get_parameter ('parameter_name' | '' | NULL )  
```  
  
##  <a name="arguments"></a><a name="Arguments"></a> 参数  
 parameter_name  
 参数的名称。 parameter_name ** (128) 为 NVARCHAR **。 如果提供 NULL 或空字符串作为函数的参数，则该函数将返回所有已配置智能管理参数的名称/值对。  
  
## <a name="table-returned"></a>返回的表  
  
|列名|数据类型|说明|  
|-----------------|---------------|-----------------|  
|parameter_name|NVARCHAR(128)|参数的名称。 下面是返回的当前参数列表：<br/><br/>**FileRetentionDebugXevent**<br/><br/>**SSMBackup2WADebugXevent**<br/><br/>**SSMBackup2WANotificationEmailIds**<br/><br/>**SSMBackup2WAEnableUserDefinedPolicy**<br/><br/>**SSMBackup2WAEverConfigured**<br/><br/>**StorageOperationDebugXevent**|  
|parameter_value|NVARCHAR(128)|参数的当前设置值。|  
  
## <a name="security"></a>安全性  
  
### <a name="permissions"></a>权限  
 需要针对此函数的 SELECT 权限。  
  
## <a name="examples"></a>示例  
 以下示例返回至少配置了一次的所有参数及其当前值。  
  
```  
USE MSDB  
GO  
SELECT *   
FROM managed_backup.fn_get_parameter (NULL)  
  
```  
  
 以下示例返回指定为接收错误通知的电子邮件 ID。 如果未返回行，则说明未启用此电子邮件通知选项。  
  
```  
USE MSDB  
GO  
SELECT *  
FROM managed_backup.fn_get_parameter ('SSMBackup2WANotficationEmailIds')  
  
```  
  
## <a name="see-also"></a>另请参阅  
 [目标为 Microsoft Azure 的 SQL Server 托管备份](../../relational-databases/backup-restore/sql-server-managed-backup-to-microsoft-azure.md)  
  
  
