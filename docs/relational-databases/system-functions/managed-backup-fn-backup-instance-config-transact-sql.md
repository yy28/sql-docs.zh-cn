---
title: managed_backup.fn_backup_instance_config (TRANSACT-SQL) |Microsoft 文档
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.component: system-functions
ms.reviewer: ''
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- fn_backup_instance_config
- smart_admin.fn_backup_instance_config_TSQL
- fn_backup_instance_config_TSQL
- smart_admin.fn_backup_instance_config
dev_langs:
- TSQL
helpviewer_keywords:
- smart_admin.fn_backup_instance_config
- fn_backup_instance_config
ms.assetid: 2382a547-c0c9-4e1d-87c9-d8526192eb5a
caps.latest.revision: 16
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 4dae80911e6508a1a398cf208300bf4145faeecc
ms.sourcegitcommit: e77197ec6935e15e2260a7a44587e8054745d5c2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/11/2018
ms.locfileid: "37970499"
---
# <a name="managedbackupfnbackupinstanceconfig-transact-sql"></a>managed_backup.fn_backup_instance_config (Transact SQL)
[!INCLUDE[tsql-appliesto-ss2016-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-xxxx-xxxx-xxx-md.md)]

  返回 1 行，其中是 SQL Server 实例的 [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] 默认配置设置。  
  
 使用此存储过程检查或确定 SQL Server 实例的当前 [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] 默认配置设置。  
  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```sql  
managed_backup.fn_backup_db_config ()  
```  
  
##  <a name="Arguments"></a> 参数  
 InclusionThresholdSetting  
  
## <a name="table-returned"></a>返回的表  
  
|列名|数据类型|Description|  
|-----------------|---------------|-----------------|  
|is_smart_backup_enabled|INT|[!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] 启用时显示 1，[!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] 禁用时显示 0。|  
|credential_name|SYSNAME|用于向存储进行身份验证的默认 SQL 凭据。|  
|retention_days|INT|在实例级别设置的默认保持期。|  
|storage_url|NVARCHAR(1024)|在实例级别设置的默认存储帐户 URL。|  
|encryption_algorithm|SYSNAME|加密算法的名称。 如果未指定加密，则设置为 NULL。|  
|encryptor_type|NVARCHAR （32)|使用的加密程序的类型：证书或非对称密钥。 如果未指定加密程序，则设置为 NULL。|  
|encryptor_name|SYSNAME|证书或非对称密钥的名称。 如果未指定名称，则设置为 NULL|  
  
## <a name="security"></a>Security  
  
### <a name="permissions"></a>权限  
 要求的成员身份**db_backupoperator**拥有数据库角色**ALTER ANY CREDENTIAL**权限。 用户应被拒绝**VIEW ANY DEFINITION**权限。  
  
## <a name="examples"></a>示例  
 下例返回所在实例上的 [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] 的默认配置设置：  
  
```  
Use msdb;  
GO  
SELECT * FROM managed_backup.fn_backup_instance_config ();  
  
```  
  
  
