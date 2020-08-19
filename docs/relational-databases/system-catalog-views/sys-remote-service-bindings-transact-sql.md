---
description: sys.remote_service_bindings (Transact-SQL)
title: sys. remote_service_bindings (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.remote_service_bindings_TSQL
- remote_service_bindings_TSQL
- remote_service_bindings
- sys.remote_service_bindings
dev_langs:
- TSQL
helpviewer_keywords:
- sys.remote_service_bindings catalog view
ms.assetid: 4e1a885d-eed1-4993-9c87-e6fd781f437d
author: VanMSFT
ms.author: vanto
ms.openlocfilehash: 3688159328e073deaf3e815826ee861d9cf27d14
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/17/2020
ms.locfileid: "88490180"
---
# <a name="sysremote_service_bindings-transact-sql"></a>sys.remote_service_bindings (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  每个远程服务绑定都在该目录视图中占一行。 
  
|列名称|数据类型|说明|  
|-----------------|---------------|-----------------|  
|name|**sysname**|该远程服务绑定的名称。 不可为 NULL。|  
|**remote_service_binding_id**|**int**|该远程服务绑定的 ID。 不可为 NULL。|  
|principal_id|**int**|拥有该远程服务绑定的数据库主体的 ID。 可以为 null.|  
|**remote_service_name**|**nvarchar(256)**|应用该绑定的远程服务的名称。 可以为 null.|  
|**service_contract_id**|**int**|应用该绑定的约定的 ID。 值 0 为通配符，表示该绑定应用于服务的所有约定。 不可为 NULL。|  
|**remote_principal_id**|**int**|远程服务绑定中指定的用户的 ID。 Service Broker 使用该用户拥有的证书与指定约定中的指定服务进行通信。 可以为 null.|  
|**is_anonymous_on**|**bit**|该远程服务绑定使用 ANONYMOUS 安全性。 未向目标服务提供开始会话的用户的标识。 不可为 NULL。|  
  
## <a name="permissions"></a>权限  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)] 有关详细信息，请参阅 [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md)。  
  
  
